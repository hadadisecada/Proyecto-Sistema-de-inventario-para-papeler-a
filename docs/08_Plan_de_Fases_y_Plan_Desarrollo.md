# Artefacto 08: Plan de Fases y Plan de Desarrollo de Software (SDP)
## Proyecto: Sistema de Gestión de Inventario y Punto de Venta para Papelería Liz-Leo ("StockPapel Liz-Leo")
**Metodología:** Proceso Unificado (UP) - Fase de Inicio

---

## 1. Introducción
El Plan de Desarrollo de Software (Software Development Plan - SDP) establece la estimación global de fases, iteraciones, asignación de recursos humanos, presupuesto en pesos mexicanos ($ MXN), herramientas tecnológicas e infraestructura necesarias para llevar el proyecto desde su concepción hasta su despliegue operativo en la tienda física de la **Papelería Liz-Leo**.

Siguiendo el Proceso Unificado, durante la Fase de Inicio las estimaciones para las fases posteriores son de **precisión preliminar/baja (orden de magnitud)** y se refinarán de forma adaptativa al concluir la fase de Elaboración.

---

## 2. Cronograma de Fases e Iteraciones

El ciclo de vida del proyecto contempla una duración total estimada de **14 a 15 semanas**, distribuidas a lo largo de las 4 fases fundamentales del Proceso Unificado:

```mermaid
gantt
    title Cronograma Global de Fases - Proceso Unificado
    dateFormat  YYYY-MM-DD
    section Inicio (Inception)
    I1: Definición de visión y arquitectura preliminar :done, i1, 2026-10-01, 2w
    section Elaboración (Elaboration)
    E1: Línea base de arquitectura y POS básico         :active, e1, after i1, 2w
    E2: Módulo de Compras, Despiece e Impresión POS     :e2, after e1, 2w
    section Construcción (Construction)
    C1: Módulos de Ajustes, Kardex y Auditoría Física   :c1, after e2, 2w
    C2: Alertas de Stock Mínimo y Reportes de Utilidad :c2, after c1, 2w
    C3: Gestión de Roles, Permisos y Respaldos          :c3, after c2, 2w
    section Transición (Transition)
    T1: Pruebas beta en tienda y carga de catálogo real :t1, after c3, 2w
    T2: Capacitación, Go-Live y puesta en marcha        :t2, after t1, 1w
```

### Tabla Resumen de Fases y Esfuerzo

| Fase UP | Iteraciones | Duración | Porcentaje Esfuerzo | Hito de Cierre de Fase (Milestone) |
|---|---|---|---|---|
| **Inicio (Inception)** | 1 (I1) | 2 semanas | ~10% | **LCS (Lifecycle Objectives):** Visión, alcance y viabilidad de negocio aprobados. |
| **Elaboración (Elaboration)** | 2 (E1, E2) | 4 semanas | ~30% | **LCA (Lifecycle Architecture):** Arquitectura ejecutable estabilizada; riesgos mayores retirados. |
| **Construcción (Construction)** | 3 (C1, C2, C3)| 6 semanas | ~45% | **IOC (Initial Operational Capability):** Sistema completo probado en entorno de desarrollo. |
| **Transición (Transition)** | 2 (T1, T2) | 3 semanas | ~15% | **PR (Product Release):** Sistema operando en vivo en Papelería Liz-Leo con datos reales y personal capacitado. |
| **TOTAL** | **8 iteraciones** | **15 semanas** | **100%** | **Entrega final y soporte inicial** |

---

## 3. Presupuesto Global Estimado del Proyecto (en MXN)

| Concepto de Inversión | Monto Estimado ($ MXN) | Justificación |
|---|:---:|---|
| **Desarrollo de Software a la Medida** | $70,000.00 MXN | Análisis, diseño arquitectónico, construcción de 8 iteraciones UP y QA. |
| **Hardware Periférico de Mostrador** | $4,500.00 MXN | 1 lector de código de barras 2D USB + 1 impresora térmica de tickets 58/80 mm. |
| **Carga y Migración Inicial de Catálogo** | $5,500.00 MXN | Digitalización y depuración de más de 3,500 SKUs de Papelería Liz-Leo. |
| **Capacitación y Puesta en Marcha en Tienda** | $4,000.00 MXN | Talleres prácticos a cajeros, encargados y dueño, más acompañamiento in-situ (72h). |
| **TOTAL DE INVERSIÓN INICIAL** | **$84,000.00 MXN** | **Retorno de inversión (ROI) proyectado: 28.6% en 9 a 10 meses.** |

---

## 4. Equipo de Trabajo y Asignación de Roles

| Rol en el Proyecto | Responsabilidades Principales | Dedicación |
|---|---|---|
| **Líder de Proyecto / Analista de Negocio** | Gestión del cronograma, comunicación directa con el dueño de Papelería Liz-Leo, refinamiento de casos de uso y facilitación de entregas. | Medio tiempo (50%) |
| **Arquitecto de Software / Desarrollador Backend** | Diseño del modelo de datos en MXN, arquitectura modular de servicios, concurrencia, integración con base de datos y lógica de kardex. | Tiempo completo (100%) |
| **Desarrollador Frontend / UI Designer** | Desarrollo de interfaces de usuario (POS de mostrador, gestión de catálogo), ergonomía del teclado, diseño reactivo y prototipos. | Tiempo completo (100%) |
| **Ingeniero de Pruebas / QA & Periféricos** | Pruebas de integración con hardware real en la tienda (impresoras térmicas, lectores USB), pruebas de carga y escenarios de merma. | Medio tiempo (50%) |

---

## 5. Recursos Tecnológicos y Herramientas

### 5.1. Entorno de Desarrollo y Lenguajes
- **Control de Versiones:** Git con repositorio alojado en GitHub / GitLab.
- **Backend / Lógica:** Node.js (TypeScript) o Python (FastAPI) / C# (.NET) por su excelente rendimiento en aplicaciones de escritorio/locales y soporte nativo de periféricos de comunicación COM/USB.
- **Frontend:** Framework moderno de componentes web (HTML5, CSS modular moderno, JavaScript/TypeScript reactivo) empaquetado para escritorio ligero (Electron o Tauri para mínimo consumo de memoria RAM) o aplicación web SPA servida localmente en la red de Papelería Liz-Leo.
- **Base de Datos:** PostgreSQL o SQLite con WAL (Write-Ahead Logging) habilitado para consistencia y cero mantenimiento de administración.
- **Herramientas de Modelado y Diseño:** Mermaid.js, draw.io, Figma para prototipos visuales.

### 5.2. Infraestructura y Hardware Requerido para Pruebas
- 1 PC de desarrollo con Windows 10/11.
- 1 Lector de códigos de barras USB láser 1D/2D (emulación de teclado).
- 1 Impresora térmica de recibos de 58 mm o 80 mm con cable USB y puerto RJ11.
- 1 Cajón portamonedas con apertura automática vía solenoide RJ11.
- Muestras físicas de productos de Papelería Liz-Leo para pruebas de escaneo (cuadernos, cartulinas, bolígrafos, gomas, hojas).

---

## 6. Plan de Capacitación y Gestión del Cambio (Transición en Liz-Leo)

1. **Capacitación a Cajeros de Liz-Leo (2 sesiones de 1.5 horas):**
   - Manejo del punto de venta con atajos de teclado.
   - Cobro rápido de artículos con y sin código de barras en pesos ($ MXN).
   - Manejo de devoluciones, cancelaciones y arqueo de caja.
2. **Capacitación a Encargados de Almacén (2 sesiones de 2 horas):**
   - Alta y edición de productos en el catálogo de Liz-Leo.
   - Recepción de facturas de proveedores con costos en MXN.
   - Realización de despieces y registro de mermas.
3. **Capacitación al Dueño / Administrador de Liz-Leo (1 sesión de 3 horas):**
   - Interpretación de reportes de utilidades y rotación de stock en $ MXN.
   - Generación de órdenes de compra automáticas basadas en stock mínimo.
   - Ejecución de auditorías físicas periódicas y respaldos de base de datos.
