# Plan de Desarrollo de Software - Sistema de Gestión de Inventario para Papelería Liz-Leo ("StockPapel Liz-Leo")
## Metodología: Proceso Unificado (UP / RUP) - Fase de Inicio

Este repositorio contiene la documentación completa de la **Fase de Inicio (Inception)** para el desarrollo a la medida del software de gestión de inventario y punto de venta para la **Papelería Liz-Leo**, siguiendo las directrices del **Proceso Unificado (Unified Process - UP)** basadas en las mejores prácticas de ingeniería de software (Craig Larman). Todos los presupuestos, análisis financieros y operaciones de caja se encuentran expresados en **Pesos Mexicanos ($ MXN)**.

---

## Estructura de Artefactos de la Fase de Inicio

| # | Artefacto UP | Descripción Resumida | Archivo Detallado |
|---|---|---|---|
| 1 | **Visión y Caso de Negocio** | Objetivos, declaración del problema en Liz-Leo, alcance, stakeholders y viabilidad económica/ROI en MXN ($84,000 MXN de inversión). | [`docs/01_Vision_y_Caso_de_Negocio.md`](docs/01_Vision_y_Caso_de_Negocio.md) |
| 2 | **Modelo de Casos de Uso** | Requisitos funcionales de la tienda, actores (cajero, almacén, dueño de Liz-Leo), diagrama y casos núcleo "fully dressed". | [`docs/02_Modelo_de_Casos_de_Uso.md`](docs/02_Modelo_de_Casos_de_Uso.md) |
| 3 | **Especificación Suplementaria** | Requisitos no funcionales FURPS+, periféricos POS, confiabilidad ante cortes eléctricos y moneda localizada en $ MXN. | [`docs/03_Especificacion_Suplementaria.md`](docs/03_Especificacion_Suplementaria.md) |
| 4 | **Glosario y Diccionario de Datos** | Vocabulario técnico y papelero (despiece, merma, temporadas) y entidades base con precios y costos en pesos mexicanos. | [`docs/04_Glosario.md`](docs/04_Glosario.md) |
| 5 | **Lista de Riesgos y Gestión de Riesgos** | Matriz de riesgos de negocio, técnicos, de periféricos y temporada escolar para Liz-Leo con mitigaciones. | [`docs/05_Gestion_de_Riesgos.md`](docs/05_Gestion_de_Riesgos.md) |
| 6 | **Prototipos y Pruebas de Concepto (PoC)** | Validación de lector de barras, despiece de bolígrafos y wireframes de UI de cobro e inventario en MXN. | [`docs/06_Prototipos_y_PoC.md`](docs/06_Prototipos_y_PoC.md) |
| 7 | **Plan de Iteración (Elaboración 1)** | Objetivos, WBS de 80 horas-hombre, tareas y criterios de aceptación para la primera iteración ejecutable en Liz-Leo. | [`docs/07_Plan_de_Iteracion.md`](docs/07_Plan_de_Iteracion.md) |
| 8 | **Plan de Fases y Plan de Desarrollo** | Cronograma de 15 semanas (Inicio, Elaboración, Construcción, Transición), presupuesto total en MXN y equipo. | [`docs/08_Plan_de_Fases_y_Plan_Desarrollo.md`](docs/08_Plan_de_Fases_y_Plan_Desarrollo.md) |
| 9 | **Caso de Desarrollo** | Personalización ágil (Agile UP) adaptada específicamente a las necesidades operativas de Papelería Liz-Leo. | [`docs/09_Caso_de_Desarrollo.md`](docs/09_Caso_de_Desarrollo.md) |

---

## Resumen del Proyecto

- **Nombre del Sistema:** *StockPapel Liz-Leo* (Sistema a la Medida de Gestión de Inventario y Ventas para Papelería Liz-Leo).
- **Entorno y Dominio:** Comercio minorista (Retail) de artículos escolares, papelería de oficina, mercería y servicios (fotocopiado/impresión/enmicado).
- **Moneda Base:** Pesos Mexicanos (**MXN** / `$ MXN`).
- **Objetivo Principal:** Eliminar el descontrol de existencias en mostrador y almacén, automatizar la detección de mermas y desabasto, agilizar las ventas mediante lectores ópticos de código de barras y optimizar las compras anticipadas para temporadas críticas ("Regreso a Clases").
- **Documento Consolidado Maestro:** [`Plan_de_Desarrollo_Software_Papeleria.md`](Plan_de_Desarrollo_Software_Papeleria.md).
