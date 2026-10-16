# Artefacto 06: Prototipos y Pruebas de Concepto (PoC)
## Proyecto: Sistema de Gestión de Inventario y Punto de Venta para Papelería Liz-Leo ("StockPapel Liz-Leo")
**Metodología:** Proceso Unificado (UP) - Fase de Inicio

---

## 1. Introducción y Propósito
En la Fase de Inicio del Proceso Unificado, los prototipos y pruebas de concepto se utilizan para:
1. Validar la viabilidad de las tecnologías clave y resolver las incógnitas arquitectónicas de mayor riesgo en la estación de trabajo de **Papelería Liz-Leo**.
2. Aclarar y consensuar la visión con los usuarios finales de la papelería (cajeros de mostrador, encargados de almacén y dueño).
3. Evaluar la ergonomía de las pantallas de alta interacción operativa (Punto de Venta y Gestión de Stock) con precios y costos en Pesos Mexicanos ($ MXN).

---

## 2. Pruebas de Concepto Técnicas (PoC)

### 2.1. PoC 1: Integración de Lector de Código de Barras e Impresora ESC/POS
- **Objetivo:** Comprobar que la captura por escáner USB no cause retardos ni interfiera con el foco de la interfaz gráfica, y que la impresora térmica de 58mm/80mm corte el papel y abra el cajón en menos de 1 segundo.
- **Arquitectura de Prueba:**
  - Lector óptico láser USB configurado en emulación de teclado HID con sufijo `[ENTER]` automático.
  - Listener global de eventos de teclado en el frontend que detecta secuencias rápidas de caracteres (< 30ms entre teclas) para redirigir la entrada directamente a la grilla de venta, sin importar qué elemento tenga el foco.
  - Módulo de comunicación directa con impresora térmica enviando secuencias de escape estándar:
    - Inicialización: `0x1B 0x40`
    - Apertura de cajón de dinero: `0x1B 0x70 0x00 0x19 0xFA`
    - Corte parcial de papel: `0x1D 0x56 0x01`
- **Resultado:** La prueba demostró tiempos de respuesta de escaneo de 45 ms y emisión de ticket completa en 0.8 segundos en el hardware de mostrador. Se validó la viabilidad total.

---

### 2.2. PoC 2: Algoritmo de Despiece y Transacciones Atómicas de Stock
- **Objetivo:** Validar que la conversión de productos mayoristas a piezas individuales no genere inconsistencias contables ni duplicidades en el inventario de Liz-Leo.
- **Regla de Negocio Probada:**
  - Al abrir 1 "Caja Bolígrafo BIC Cristal Negro x 50 pzas" (Costo de adquisición: $150.00 MXN):
    - Se descuenta 1 unidad del producto mayorista (Saldo anterior: 5 cajas $\rightarrow$ Saldo posterior: 4 cajas).
    - Se incrementan 50 unidades al producto hijo "Bolígrafo BIC Cristal Negro Suelto" (Saldo anterior: 8 pzas $\rightarrow$ Saldo posterior: 58 pzas).
    - El costo unitario de la pieza suelta se hereda automáticamente: $\frac{\$150.00 \text{ MXN}}{50} = \$3.00 \text{ MXN}$ por pieza.
- **Resultado:** La simulación en base de datos relacional con transacción `BEGIN TRANSACTION ... COMMIT` garantizó cero inconsistencias aún en casos de corte abrupto de conexión.

---

## 3. Wireframes y Prototipos de Interfaz de Usuario (UI)

### 3.1. Prototipo UI 01: Pantalla Principal de Punto de Venta (POS)
Diseñada para máxima velocidad de atención en mostrador de Papelería Liz-Leo, navegación 100% por teclado y accesos directos para productos sin código de barras y servicios.

```
+----------------------------------------------------------------------------------------------------+
| Papelería Liz-Leo POS | Turno: Matutino | Cajero: Ana Gómez | F1: Ayuda | F2: Buscar | F12: Cobrar |
+----------------------------------------------------------------------------------------------------+
|  [ ESCANEAR CÓDIGO DE BARRAS O BUSCAR PRODUCTO... (F2)                              ] [ + AGREGAR ]|
+-------------------------------------------------------------------------+--------------------------+
|  CANT | DESCRIPCIÓN DEL ARTÍCULO          | P. UNIT   | DESC. | SUBTOTAL| BOTONERA RÁPIDA (Sin CB) |
+-------+-----------------------------------+-----------+-------+---------+--------------------------+
|   2   | Cuaderno Profesional Raya Scribe  | $   34.50 |  $0.00| $  69.00| [F3] Fotocopia B/N $1.00 |
|   5   | Bolígrafo BIC Cristal Negro       | $    6.50 |  $0.00| $  32.50| [F4] Fotocopia Color $4  |
|   1   | Pegamento en Barra Pritt 22g      | $   28.00 |  $0.00| $  28.00| [F5] Cartulina Blanca $6 |
|   3   | Cartulina Iris Varios Colores     | $    7.50 |  $0.00| $  22.50| [F6] Papel Crepé $7.50   |
|  10   | Fotocopias B/N Carta              | $    1.00 |  $0.00| $  10.00| [F7] Enmicado Carta $15  |
|   1   | Papel Contac Adhesivo (Metro)     | $   18.00 |  $0.00| $  18.00| [F8] Hojas Blancas x100  |
+-------+-----------------------------------+-----------+-------+---------+--------------------------+
|  Total de Artículos: 22                   | Subtotal:         | $ 180.00| RESUMEN DE COBRO (MXN)   |
|  [DEL]: Eliminar fila | [+/-]: Modif. Cant| IVA (16% inc.):   | $  28.80| TOTAL:    $ 180.00 MXN   |
|  [F9]: Aplicar Descuento Especial Mayorista                   |         | Recibido: [ $ 200.00 MXN]|
|                                                                         | CAMBIO:   $  20.00 MXN   |
|                                                                         | [   F12: COBRAR E IMPR  ]|
+-------------------------------------------------------------------------+--------------------------+
```

---

### 3.2. Prototipo UI 02: Módulo de Control de Inventario y Alertas de Stock Mínimo
Permite supervisar existencias en Papelería Liz-Leo, ver el estatus de stock de un vistazo (semáforo) y reordenar con un clic.

```
+----------------------------------------------------------------------------------------------------+
| Papelería Liz-Leo | INVENTARIO Y EXISTENCIAS | Total SKUs: 3,420 | Valor Inventario: $ 145,280.00 MXN |
+----------------------------------------------------------------------------------------------------+
| Filtros: [ Categoría: Todos v ] [ Estado: Alerta Stock Mínimo v ] [ Buscar por SKU / Nombre...   ]|
+----------------------------------------------------------------------------------------------------+
| SKU       | PRODUCTO                        | CATEGORÍA   | STOCK ACT | STOCK MÍN | ESTATUS | ACCIONES |
+-----------+---------------------------------+-------------+-----------+-----------+---------+----------+
| PAP-00102 | Cuaderno Forma Francesa Cuadro  | Cuadernos   |     3 pza |    20 pza | [CRÍTICO| [Reorden]|
| ESC-00455 | Lápiz Adhesivo Pritt 42g        | Pegamentos  |     5 pza |    15 pza | [ALERTA]| [Reorden]|
| ESC-00012 | Bolígrafo BIC Negro Mediano     | Escritura   |   120 pza |    50 pza | [ÓPTIMO]| [Editar] |
| SER-00001 | Resma Papel Bond Carta 500h     | Papel       |     2 paq |    10 paq | [CRÍTICO| [Reorden]|
| ESC-00890 | Tijera Escolar Punta Roma       | Geometría   |    18 pza |    12 pza | [ÓPTIMO]| [Editar] |
+-----------+---------------------------------+-------------+-----------+-----------+---------+----------+
| Mostrando 5 de 42 productos en alerta crítica                                                      |
| [ GENERAR ORDEN DE COMPRA SUGERIDA AUTOMÁTICA ]   [ EXPORTAR REPORTE EXCEL ]   [ AUDITAR FÍSICO ]  |
+----------------------------------------------------------------------------------------------------+
```

---

## 4. Conclusiones y Validación de la Prueba de Concepto
1. **Factibilidad Comprobada:** Se verificó que los periféricos estándar del mostrador de Papelería Liz-Leo funcionan sin problemas técnicos con la arquitectura seleccionada.
2. **Aprobación de la Interfaz:** Los usuarios de mostrador validaron que la botonera de accesos directos (teclas `F3` a `F8`) para cartulinas, servicios y fotocopias elimina el 80% de los retrasos habituales en la atención al cliente.
3. **Paso a la Fase de Elaboración:** Con los riesgos técnicos de hardware y despiece despejados, el equipo cuenta con bases sólidas para arrancar la construcción de la primera iteración ejecutable.
