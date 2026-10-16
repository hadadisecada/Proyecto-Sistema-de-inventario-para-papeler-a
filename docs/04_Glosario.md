# Artefacto 04: Glosario y Diccionario de Datos
## Proyecto: Sistema de Gestión de Inventario y Punto de Venta para Papelería Liz-Leo ("StockPapel Liz-Leo")
**Metodología:** Proceso Unificado (UP) - Fase de Inicio

---

## 1. Introducción
El Glosario define la terminología específica del dominio de negocio adaptada a la operación comercial de la **Papelería Liz-Leo** (inventarios, mostrador, artículos escolares, oficina y servicios). Establece un lenguaje ubicuo compartido entre los desarrolladores, el dueño de la papelería y el personal operativo. Asimismo, incluye el Diccionario de Datos conceptual con sus atributos fundamentales expresados en moneda nacional mexicana ($ MXN).

---

## 2. Terminología Clave del Dominio

| Término | Definición y Contexto Operativo en Papelería Liz-Leo |
|---|---|
| **SKU (Stock Keeping Unit)** | Código alfanumérico único asignado a cada producto en el catálogo de Papelería Liz-Leo para su identificación y control en anaqueles (ej. `PAP-CUAD-001`). |
| **Código de Barras (EAN-13 / UPC)** | Código numérico estándar impreso en el empaque de productos comerciales (ej. marcas como Scribe, BIC, Pritt, Pelikan, Mae). Es leído ópticamente por el escáner del mostrador. |
| **Despiece / Fraccionamiento** | Operación mediante la cual un producto empaquetado en lote mayorista (ej. caja de 50 bolígrafos BIC o paquete de 500 hojas) se abre y se convierte en unidades sueltas para venta individual en Liz-Leo, descontando la caja mayorista y sumando las piezas sueltas con costo proporcional en pesos ($ MXN). |
| **Merma** | Pérdida no recuperable de inventario ocasionada por daños físicos (cartulinas dobladas, hojas manchadas), secado de solventes (pegamentos, correctores líquidos, tintas), caducidad o defecto de fábrica en la tienda. |
| **Robo Hormiga** | Pérdida oculta de artículos pequeños de mostrador de fácil ocultación (gomas, sacapuntas, lápices, plumones) que causa descuadres entre el conteo físico y el sistema. |
| **Stock de Seguridad (Stock Mínimo)** | Nivel de existencias mínimo que Liz-Leo debe mantener en anaquel o bodega para evitar desabasto ante demoras de distribuidores mayoristas. |
| **Punto de Reorden** | Cantidad umbral calculada por el sistema en la cual se sugiere una nueva orden de compra al proveedor antes de agotar el stock de seguridad. |
| **Costo Promedio Ponderado (CPP)** | Método de valuación de inventario en pesos mexicanos ($ MXN) que promedia el costo unitario de las existencias actuales con el costo de las nuevas compras ingresadas. |
| **Margen de Ganancia / Utilidad** | Porcentaje de incremento sobre el costo de adquisición para fijar el precio de venta final en mostrador en pesos ($ MXN): $\text{Precio Venta} = \text{Costo} \times (1 + \text{Margen})$. |
| **Temporada Alta ("Regreso a Clases")** | Periodo de máxima demanda comercial para Papelería Liz-Leo (julio a septiembre), donde el volumen de venta de cuadernos, lápices y papel se multiplica sustancialmente. |
| **Producto de Servicio** | Ítem intangible comercializado en el mostrador de Liz-Leo que no requiere control de stock físico unitario pero genera ingresos en MXN (ej. fotocopia B/N, fotocopia color, enmicado térmico, engargolados, impresiones). |
| **Producto por Medida / Granel** | Ítem comercializado fraccionadamente por metros, centímetros o pliegos (ej. papel autoadherible contac, papel crepé, cartulina, foami, listón). |
| **Kardex** | Registro cronológico inmutable de entradas (compras), salidas (ventas) y ajustes (mermas, despiece), valuado en pesos mexicanos ($ MXN). |
| **Conteo Físico Ciego** | Procedimiento de auditoría en el cual el personal de Liz-Leo cuenta la mercancía física sin conocer el stock teórico del sistema, evitando sesgos. |

---

## 3. Diccionario de Datos Conceptual

Todas las variables monetarias se encuentran normalizadas en **Pesos Mexicanos ($ MXN)** con precisión decimal a 2 posiciones.

### 3.1. Entidad: `Producto`
Representa cualquier artículo comercializado o servicio brindado en Papelería Liz-Leo.

| Atributo | Tipo de Dato | Requerido | Descripción / Regla de Negocio (Moneda: $ MXN) |
|---|---|---|---|
| `id_producto` | Entero / UUID | Sí (PK) | Identificador único interno del producto. |
| `sku` | Texto(30) | Sí (Único) | Código interno de referencia asignado en el catálogo de Liz-Leo. |
| `codigo_barras` | Texto(50) | No (Indexado) | Código de barras estándar (EAN-13, UPC). Puede ser nulo para servicios o granel. |
| `nombre` | Texto(150) | Sí | Nombre descriptivo del artículo (ej. "Cuaderno Profesional Raya 100h Scribe"). |
| `id_categoria` | Entero | Sí (FK) | Categoría (ej. Cuadernos, Pegamentos, Escritura, Servicios). |
| `es_servicio` | Booleano | Sí | Verdadero si es servicio (ej. fotocopia) que no descuenta stock unitario. |
| `precio_costo` | Decimal(10,2) | Sí | Costo promedio de compra unitario expresado en pesos mexicanos ($ MXN). |
| `precio_venta` | Decimal(10,2) | Sí | Precio de venta al público en mostrador en pesos mexicanos ($ MXN). |
| `precio_mayoreo` | Decimal(10,2) | No | Precio con descuento por volumen en pesos mexicanos ($ MXN). |
| `stock_actual` | Decimal(10,2) | Sí | Cantidad física disponible actualmente en la papelería. |
| `stock_minimo` | Decimal(10,2) | Sí | Umbral de stock de seguridad para emitir alerta de compra. |
| `unidad_medida` | Texto(15) | Sí | Unidad de venta: `PZA` (pieza), `CJA` (caja), `PAQ` (paquete), `MTR` (metro), `PLG` (pliego). |
| `es_compuesto` | Booleano | Sí | Indica si es un producto padre que puede despiezarse. |
| `id_producto_hijo` | Entero (FK) | No | Producto unitario resultante al abrir este empaque (si aplica). |
| `factor_conversion` | Entero | No | Cantidad de piezas individuales que contiene el empaque (ej. 12, 24, 50). |

---

## 3.2. Entidad: `MovimientoKardex`
Registro de auditoría inmutable de entradas y salidas de inventario en Papelería Liz-Leo.

| Atributo | Tipo de Dato | Requerido | Descripción |
|---|---|---|---|
| `id_movimiento` | Entero / UUID | Sí (PK) | Folio único del movimiento de inventario. |
| `id_producto` | Entero | Sí (FK) | Producto afectado en el catálogo. |
| `tipo_movimiento` | Enumerado | Sí | `ENTRADA_COMPRA`, `SALIDA_VENTA`, `AJUSTE_MERMA`, `AJUSTE_DESPIECE`, `AUDITORIA_AJUSTE`. |
| `cantidad` | Decimal(10,2) | Sí | Cantidad de unidades involucradas (positiva o negativa). |
| `stock_anterior` | Decimal(10,2) | Sí | Existencia previa a la transacción. |
| `stock_posterior` | Decimal(10,2) | Sí | Existencia resultante tras la transacción. |
| `costo_unitario_mov`| Decimal(10,2) | Sí | Costo unitario registrado al momento del movimiento ($ MXN). |
| `id_referencia` | Entero | No | Folio de la venta, compra o auditoría asociada. |
| `motivo` | Texto(255) | No | Justificación documentada del movimiento. |
| `id_usuario` | Entero | Sí (FK) | Usuario responsable que ejecutó la acción. |
| `fecha_hora` | Timestamp | Sí | Fecha y hora exacta en tiempo real. |

---

## 3.3. Entidad: `Venta` y `DetalleVenta`
Registro de las operaciones comerciales de mostrador en Papelería Liz-Leo (todas las cifras monetarias en $ MXN).

- **Venta:** `id_venta` (PK), `folio_ticket`, `fecha_hora`, `total_venta` ($ MXN), `subtotal` ($ MXN), `iva` ($ MXN), `monto_recibido` ($ MXN), `cambio` ($ MXN), `metodo_pago` (Efectivo/Tarjeta/Transferencia), `id_cajero` (FK), `estado` (Cobrada/Cancelada).
- **DetalleVenta:** `id_detalle` (PK), `id_venta` (FK), `id_producto` (FK), `cantidad`, `precio_unitario` ($ MXN), `precio_costo_momento` ($ MXN, para cálculo de utilidad bruta), `subtotal_linea` ($ MXN).

---

## 3.4. Entidad: `Proveedor`
Distribuidores mayoristas de artículos escolares, de oficina y papelería que surten a Papelería Liz-Leo.

- `id_proveedor` (PK), `razon_social`, `rfc`, `contacto_nombre`, `telefono`, `correo`, `dias_credito`, `direccion`.eedor` (PK), `razon_social`, `rfc`, `contacto_nombre`, `telefono`, `correo`, `dias_credito`, `direccion`.
