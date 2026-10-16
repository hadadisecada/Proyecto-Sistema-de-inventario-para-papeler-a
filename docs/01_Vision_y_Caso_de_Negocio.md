# Artefacto 01: Visión y Caso de Negocio
## Proyecto: Sistema de Gestión de Inventario y Punto de Venta para Papelería Liz-Leo ("StockPapel Liz-Leo")
**Metodología:** Proceso Unificado (UP) - Fase de Inicio

---

## 1. Resumen Ejecutivo
El presente documento describe la visión, justificación económica y estratégica para el desarrollo del software de gestión de inventario, control de existencias, compras a proveedores y ventas de mostrador diseñado exclusivamente a la medida de la **Papelería Liz-Leo**, un establecimiento comercial dedicado a la venta al por menor de artículos escolares, papelería de oficina, mercería, manualidades y servicios (fotocopiado, enmicado e impresiones).

Actualmente, la Papelería Liz-Leo opera mediante registros manuales en libretas o herramientas genéricas de hoja de cálculo, lo que genera discrepancias frecuentes entre el inventario físico en estanterías y el teórico, pérdidas económicas por merma no cuantificada (roturas de cartulinas y pliegos de papel, secado de pegamentos/adhesivos, robo hormiga de bolígrafos y útiles pequeños), desabasto crítico durante el "Regreso a Clases" (temporada alta), y demoras en la atención al cliente en mostrador por desconocimiento de existencias y precios actualizados.

El sistema **StockPapel Liz-Leo** resolverá estas problemáticas centralizando el catálogo de productos con soporte para códigos de barras, gestión de despiece (caja cerrada vs. venta por pieza suelta), niveles de stock de seguridad con alertas automáticas de reorden, registro ágil de ventas en mostrador y auditorías físicas de inventario.

---

## 2. Declaración del Problema

| Elemento | Descripción |
|---|---|
| **El problema de...** | Descontrol de existencias, lentitud en mostrador, falta de visibilidad del inventario real y compras ineficientes a proveedores. |
| **Afecta a...** | Dueño/Administrador de Papelería Liz-Leo, personal de mostrador/caja, encargado de almacén y clientes de la tienda. |
| **Cuyo impacto es...** | Pérdida de ventas por falta de stock imprevista, sobre-inventario de productos de baja rotación que inmovilizan capital de trabajo, pérdidas de hasta un 7-12% por merma y robo hormiga no detectado, y filas en mostrador durante horas de alta afluencia. |
| **Una solución exitosa sería...** | Implementar un sistema informático especializado en el flujo operativo de Papelería Liz-Leo, capaz de rastrear existencias en tiempo real, agilizar ventas con lectores de código de barras, calcular necesidades de compra por estacionalidad escolar y auditar desviaciones de stock con precisión. |

---

## 3. Posicionamiento del Producto

Para la **Papelería Liz-Leo**, que **necesita controlar miles de artículos de papelería, mercería y servicios con alta rotación**, el sistema **StockPapel Liz-Leo** es una **solución integral de inventario y punto de venta** que **automatiza el control de existencias por unidad/paquete, alerta sobre niveles críticos de stock y agiliza las transacciones de cobro en mostrador**.

A diferencia de **sistemas POS genéricos rígidos o plantillas de Excel propensas a errores de captura**, nuestro producto **ofrece un modelo especializado en el comportamiento operativo de Papelería Liz-Leo (despiece de artículos mayoristas, venta rápida de productos sin código de barras mediante botonera de atajos y servicios integrados de copiado, enmicado e impresiones)**.

---

## 4. Partes Interesadas (Stakeholders) y Usuarios

| Rol / Stakeholder | Interés Principal | Nivel de Influencia | Perfil Tecnológico |
|---|---|---|---|
| **Dueño / Administrador de Liz-Leo** | Control financiero del negocio, reducción de mermas, maximización del margen de ganancia en cada línea y reportes ejecutivos confiables en pesos ($ MXN). | Alto (Decisor final) | Intermedio. Requiere paneles gráficos claros, métricas de caja y resúmenes de rentabilidad. |
| **Encargado de Compras e Inventario** | Detección oportuna de stock mínimo, gestión de proveedores papeleros, recepción de mercancías con cotejo de notas/facturas y auditorías físicas periódicas. | Alto (Usuario clave) | Intermedio. Familiarizado con hojas de cálculo y lectores de códigos de barras. |
| **Cajero / Vendedor de Mostrador** | Velocidad de búsqueda y cobro, confirmación visual inmediata de existencias, cálculo rápido de cambio e impresión ágil de tickets. | Medio (Operador diario) | Básico. Requiere interfaz intuitiva con navegación por teclado y mínimos clics. |
| **Clientes de Papelería Liz-Leo** | Atención rápida, surtido garantizado de sus listas de útiles escolares u oficina, y tickets de compra claros y transparentes. | Externo | N/A (Beneficiario directo del buen servicio). |
| **Proveedores de Artículos Escolares** | Claridad en las órdenes de compra emitidas y confirmación oportuna de recepciones de mercancía. | Externo | N/A. |

---

## 5. Objetivos de Negocio de Alto Nivel

1. **Reducción de Mermas y Desajustes:** Disminuir en al menos un **70%** las discrepancias entre el inventario físico y el inventario registrado durante los primeros 4 meses de operación en Papelería Liz-Leo.
2. **Eliminación de Quiebres de Stock en Temporada Escolar:** Asegurar un **98%** de disponibilidad en los 100 productos clave ("Top 100") durante la temporada alta de Regreso a Clases mediante alertas preventivas de punto de reorden.
3. **Agilidad en la Atención al Cliente:** Reducir el tiempo promedio de atención y cobro en mostrador por cliente de 3.5 minutos a menos de **50 segundos**.
4. **Optimización del Capital de Trabajo:** Disminuir compras excesivas de artículos de baja rotación en un **30%**, liberando liquidez para surtir productos de mayor demanda.
5. **Trazabilidad Total:** Registrar el 100% de los movimientos de almacén y mostrador (altas por compra, bajas por venta, ajustes por rotura/vencimiento de pegamentos y devoluciones) con usuario responsable, fecha y motivo auditado.

---

## 6. Limitaciones y Restricciones del Proyecto

- **Restricciones Presupuestarias:** La inversión debe mantenerse contenida y maximizar la rentabilidad del negocio; el software debe ejecutarse en el equipo de cómputo actual de Papelería Liz-Leo (PCs con procesadores de gama de entrada, Windows 10/11, 4 GB a 8 GB de RAM).
- **Restricciones de Hardware Periférico:** Debe ser 100% compatible con los periféricos existentes o a instalar en la estación de mostrador: lectores de código de barras USB estándar (emulación de teclado HID), impresoras térmicas de tickets (58 mm y 80 mm vía protocolo ESC/POS) y cajón de dinero con apertura automática por puerto RJ11.
- **Conectividad:** Debe operar con alta fiabilidad en la red de área local (LAN) de la papelería sin depender de una conexión constante a internet para las operaciones críticas de venta y consulta de stock.
- **Curva de Aprendizaje:** El personal de mostrador rota periódicamente y cuenta con habilidades digitales básicas; la capacitación del cajero no debe tomar más de 2 horas.

---

## 7. Caso de Negocio y Viabilidad Económica

### 7.1. Estimación de Costos de Desarrollo e Implementación (en MXN)
- **Desarrollo de Software (Iteraciones UP a la medida de Liz-Leo):** $65,000 - $75,000 MXN (esfuerzo de análisis, arquitectura, construcción iterativa y afinación).
- **Hardware Periférico (1 lector de código de barras 2D + 1 impresora térmica de tickets 58/80 mm):** $4,500 MXN.
- **Migración y Carga Inicial de Catálogo e Inventario de Liz-Leo:** $5,500 MXN.
- **Capacitación del Personal y Puesta en Marcha en Tienda:** $4,000 MXN.
- **Costo Total Estimado de Inversión Inicial:** **$84,000 MXN**.

### 7.2. Beneficios Económicos Anuales Proyectados (en MXN)
- **Recuperación de ventas perdidas por falta de stock:** Estimado en **$48,000 MXN/año**.
- **Reducción de mermas, robo hormiga y caducidades:** Estimado en **$36,000 MXN/año**.
- **Ahorro de horas-hombre en inventarios manuales y conteos:** Estimado en **$24,000 MXN/año**.
- **Beneficio Total Anual:** **~$108,000 MXN/año**.

### 7.3. Periodo de Retorno de Inversión (ROI)
$$\text{ROI} = \frac{\text{Beneficio Neto Año 1}}{\text{Inversión Inicial}} \times 100 = \frac{108,000 - 84,000}{84,000} \times 100 = \frac{24,000}{84,000} \times 100 \approx 28.6\%$$

El periodo estimado de recuperación de la inversión es de **9 a 10 meses** (generando un flujo positivo neto a partir del décimo mes), lo que confirma una excelente viabilidad financiera para Papelería Liz-Leo.

---

## 8. Alcance del Sistema

### 8.1. Dentro del Alcance (Fase 1 y Fase 2)
- Gestión del catálogo de productos de Papelería Liz-Leo (SKUs, códigos de barras EAN/UPC, categorías, marcas, unidades de medida y precios en pesos mexicanos MXN).
- Manejo de productos compuestos y despiece (ej. apertura de caja de 50 bolígrafos vs. venta individual por pieza suelta).
- Registro de compras y recepción de mercancías con actualización automática de existencias y costo promedio ponderado en MXN.
- Módulo de Punto de Venta (POS) en mostrador con actualización atómica de existencias.
- Módulo de Ajustes de Inventario (mermas, roturas, secado de pegamentos, muestras, autoconsumo y pérdidas).
- Alertas visuales y reportes de stock mínimo y sugerencia de compra por punto de reorden.
- Control de perfiles de usuario y permisos (Administrador, Almacenero, Cajero).
- Auditoría física de inventario (conteo ciego por pasillo o estante con cálculo de diferencias en unidades y en pesos MXN).

### 8.2. Fuera del Alcance (Versiones Futuras)
- Tienda de comercio electrónico (E-commerce B2C) con pasarela de pagos en línea (evaluable para fases posteriores).
- Facturación electrónica masiva con timbrado CFDI directo al momento de venta (se mantendrá ticket de compra simplificado y exportación a Excel para gestión contable).
- Múltiples sucursales interconectadas a nivel regional (el alcance está 100% concentrado en optimizar la sucursal física de Papelería Liz-Leo).
