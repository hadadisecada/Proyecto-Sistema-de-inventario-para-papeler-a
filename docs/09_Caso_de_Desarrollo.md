# Artefacto 09: Caso de Desarrollo (Development Case)
## Proyecto: Sistema de Gestión de Inventario y Punto de Venta para Papelería Liz-Leo ("StockPapel Liz-Leo")
**Metodología:** Proceso Unificado (UP) - Fase de Inicio

---

## 1. Introducción y Justificación de la Personalización
En el Proceso Unificado (UP), el proceso nunca se aplica de forma dogmática ni rígida; **siempre se personaliza ("tailoring")** de acuerdo con la escala del proyecto, el tamaño del equipo, los riesgos técnicos y el dominio del negocio.

Para el desarrollo del sistema de la **Papelería Liz-Leo** (software integral de inventario y punto de venta para su local comercial):
- Se adopta un enfoque **Ágil-UP (Agile Unified Process)**: se preserva la rigurosidad en la identificación de riesgos, modelado de dominio y diseño arquitectónico temprano, pero se minimiza la burocracia documental innecesaria.
- Los artefactos se mantienen en formatos claros, pragmáticos y directamente aprovechables por el equipo de desarrollo y el dueño del negocio.

---

## 2. Matriz de Artefactos Personalizados para el Proyecto

La siguiente tabla resume los artefactos de UP seleccionados para el ciclo de vida de este proyecto, indicando en qué fases se crean, refinan o mantienen, y su nivel de formalidad:
- **s (start):** Se inicia su elaboración.
- **r (refine):** Se refina y actualiza sustancialmente.
- **m (maintain):** Se mantiene o consulta sin cambios mayores.

| Disciplina UP | Artefacto Personalizado | Inicio (Incep.) | Elaboración (Elab.) | Construcción (Const.) | Transición (Trans.) | Nivel de Formalidad | Justificación en Papelería Liz-Leo |
|---|---|:---:|:---:|:---:|:---:|---|---|
| **Gestión de Proyecto** | Visión y Caso de Negocio | **s** | **r** | m | m | Medio | Define el alcance financiero en pesos ($ MXN) y límites del software en tienda. |
| **Requisitos** | Modelo de Casos de Uso | **s** (10-15%) | **r** (80%) | m | m | Alto (para CU núcleo) | Crucial para asegurar que el flujo de cobro y descarga de inventario sea exacto. |
| **Requisitos** | Especificación Suplementaria | **s** | **r** | m | m | Alto | Define requisitos críticos de usabilidad (teclado rápido) y periféricos POS. |
| **Requisitos** | Glosario y Diccionario de Datos | **s** | **r** | m | m | Medio | Estandariza conceptos como "despiece", "merma", productos en MXN y temporadas. |
| **Gestión de Proyecto** | Lista de Riesgos | **s** | **r** | **r** | m | Alto | Control continuo de riesgos de captura de inventario y periféricos de Liz-Leo. |
| **Análisis y Diseño** | Prototipos y PoC | **s** | **r** | - | - | Práctico / Código | Valida la compatibilidad del escáner y la UI con los cajeros reales de Liz-Leo. |
| **Gestión de Proyecto** | Plan de Iteración | **s** | **r** | **r** | **r** | Medio | Planifica cada iteración de 2 semanas con entregables ejecutables. |
| **Gestión de Proyecto** | Plan de Desarrollo (SDP) | **s** | **r** | m | m | Medio | Guía global de recursos, calendario de 15 semanas y presupuesto en $ MXN. |
| **Gestión de Proyecto** | Caso de Desarrollo | **s** | m | - | - | Bajo | Documenta las decisiones metodológicas adoptadas. |
| **Análisis y Diseño** | Modelo de Dominio (UML) | - | **s** | **r** | m | Medio | Diagrama de clases conceptual del modelo de existencias y kardex. |
| **Análisis y Diseño** | Documento de Arquitectura (SAD)| - | **s** | m | m | Medio | Documenta el patrón de capas, seguridad y modelo relacional. |
| **Pruebas** | Plan y Casos de Prueba (QA) | - | **s** | **r** | **r** | Alto | Valida que ninguna venta ni ajuste descuadre el balance contable de stock. |
| **Despliegue** | Manual de Usuario y Operación | - | - | **s** | **r** | Alto | Guía visual con capturas de pantalla para la capacitación de cajeros y dueños. |

---

## 3. Artefactos de UP Omitidos o Simplificados y su Justificación

1. **Modelo de Negocio Extenso (Business Modeling con BPMN complejo):**
   - *Decisión:* Omitido como artefacto independiente; se sintetiza en la *Visión* y en las descripciones de los *Casos de Uso*.
   - *Justificación:* El funcionamiento de Papelería Liz-Leo es un flujo minorista directo bien delimitado (compra, exhibición, venta en mostrador y cobro); no se justifica un modelado de procesos corporativos formal.
2. **Modelo de Análisis Formal (Analysis Model con clases frontera, control y entidad abstractas):**
   - *Decisión:* Se transita directamente del *Modelo de Dominio* y los *Casos de Uso* al diseño de la solución en la arquitectura de software.
   - *Justificación:* En un proyecto ágil enfocado a un comercio específico, un modelo intermedio genera duplicidad y retrasos innecesarios.
3. **Planes de Gestión de Configuración Corporativos:**
   - *Decisión:* Se reemplaza por el uso de estándares ágiles basados en Git (ramas tipo *GitHub Flow* y versionado semántico `MAJOR.MINOR.PATCH`).

---

## 4. Ritmo y Reglas de Iteración

- **Duración fija de las iteraciones (Timeboxing):** Cada iteración dura exactamente **2 semanas**. Si una funcionalidad secundaria no se concluye a tiempo, se traslada a la siguiente iteración en lugar de retrasar la fecha del hito.
- **Entregables verificables:** Toda iteración concluye obligatoriamente con un incremento de software ejecutable y probado, no únicamente con documentos teóricos.
- **Demostración al cliente:** Al finalizar cada iteración, se realiza una sesión de 30 minutos con el dueño de la **Papelería Liz-Leo** para validar el avance y ajustar prioridades operativas.
