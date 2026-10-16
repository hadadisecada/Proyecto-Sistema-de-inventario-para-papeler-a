# Artefacto 03: Especificación Suplementaria (FURPS+)
## Proyecto: Sistema de Gestión de Inventario y Punto de Venta para Papelería Liz-Leo ("StockPapel Liz-Leo")
**Metodología:** Proceso Unificado (UP) - Fase de Inicio

---

## 1. Introducción
La Especificación Suplementaria captura los requisitos del sistema para la **Papelería Liz-Leo** que no son modelados naturalmente en los casos de uso, enfocándose principalmente en requisitos no funcionales, restricciones técnicas del establecimiento y requerimientos arquitectónicos globales utilizando el modelo **FURPS+** (Functionality, Usability, Reliability, Performance, Supportability, más restricciones de implementación, interfaz y normativas comerciales mexicanas).

---

## 2. Requisitos FURPS+

### 2.1. Funcionalidad (Functionality - Requisitos Transversales)

1. **Seguridad y Control de Acceso (RBAC):**
   - El sistema debe contar con autenticación de usuarios mediante identificador/usuario y contraseña encriptada (algoritmo bcrypt o Argon2).
   - Control de roles estricto:
     - `Cajero`: Acceso restringido al módulo de Punto de Venta, búsqueda rápida de productos y apertura/cierre de su propio turno de caja. No puede alterar precios, modificar existencias de almacén ni anular tickets sin clave de supervisor.
     - `Almacenero`: Acceso a catálogo de productos, registro de compras, ajustes de inventario y auditorías físicas.
     - `Administrador`: Acceso ilimitado a configuraciones, reportes de utilidades, márgenes, eliminación de registros y gestión de usuarios.
2. **Pista de Auditoría (Audit Log):**
   - Toda modificación manual de existencias (ajuste por merma, corrección de inventario, entrada extraordinaria) debe registrar automáticamente: fecha y hora exacta (timestamp ISO 8601), ID de usuario, valor anterior, nuevo valor y motivo documentado.
3. **Respaldo y Recuperación (Backup & Restore):**
   - El sistema debe programar copias de seguridad automáticas diarias de la base de datos al finalizar la jornada comercial.
   - Posibilidad de exportar respaldos cifrados a un dispositivo de almacenamiento externo USB o a un servicio en la nube (Google Drive/Dropbox/OneDrive).
4. **Alertas de Reorden Proactivas:**
   - Detección automática en segundo plano de artículos que alcanzan o caen por debajo de su umbral de *Stock de Seguridad*, generando un badge/indicador visual en el dashboard principal.

---

### 2.2. Usabilidad (Usability)

1. **Ergonomía en Punto de Venta (Operación "Mouse-less"):**
   - El 100% de las operaciones de venta en mostrador (escaneo, cambio de cantidad, búsqueda manual, cobro, cambio de método de pago y confirmación de ticket) deben poder realizarse exclusivamente mediante el teclado (teclas de función `F1` a `F12`, `Tab`, flechas y teclado numérico).
2. **Retroalimentación Acústica y Visual en Escaneo:**
   - Al escanear un código de barras válido: pitido agudo y resaltado verde suave en la fila agregada.
   - Al escanear un código no registrado o error: sonido grave de alerta y modal emergente con foco directo para solución.
3. **Legibilidad y Contraste:**
   - La tipografía en la interfaz de mostrador debe tener un tamaño mínimo de 16px para nombres de productos y 28px con alto contraste para el "Total a Pagar" y "Cambio a Devolver", facilitando la lectura a distancia prudente y en condiciones variables de iluminación de la tienda.
4. **Tiempo de Capacitación:**
   - Un operador nuevo con conocimientos elementales de computación debe ser capaz de cobrar artículos con fluidez tras un entrenamiento guiado no superior a **60 minutos**.

---

### 2.3. Confiabilidad (Reliability)

1. **Disponibilidad Operativa:**
   - Disponibilidad del 99.5% durante el horario de atención al público de la **Papelería Liz-Leo** (ej. 7:00 AM a 9:00 PM, de lunes a domingo).
2. **Consistencia Transaccional (ACID):**
   - Toda transacción de venta, recepción o despiece debe garantizar las propiedades de Atomicidad, Consistencia, Aislamiento y Durabilidad. Si la impresora de tickets se traba o la máquina se apaga abruptamente, la base de datos no debe quedar en un estado inconsistente ni corrupto.
3. **Tolerancia a Cortes Eléctricos:**
   - En caso de apagón repentino en la zona comercial de Papelería Liz-Leo, el sistema debe registrar en disco todas las transacciones confirmadas hasta el último milisegundo mediante WAL (Write-Ahead Logging). Se recomienda la incorporación de una unidad UPS (No-Break) para la estación de cobro.
4. **Tiempo Medio Entre Fallos (MTBF):**
   - MTBF superior a 720 horas de operación continua sin requerir reinicio del software o de la base de datos.

---

### 2.4. Rendimiento (Performance)

1. **Tiempo de Búsqueda de Productos:**
   - La búsqueda reactiva por texto predictivo (autocompletado por nombre o marca) sobre el catálogo de hasta **15,000 SKUs** de Papelería Liz-Leo debe devolver resultados en menos de **250 milisegundos**.
2. **Tiempo de Escaneo y Procesamiento de Código de Barras:**
   - La inserción del producto en la grilla de venta tras la lectura del código de barras no debe demorar más de **150 milisegundos**.
3. **Cierre de Venta e Impresión:**
   - Desde que el cajero pulsa "Confirmar Venta" hasta que la impresora térmica expulsa la primera línea del ticket no deben transcurrir más de **1.2 segundos**.
4. **Capacidad de Concurrencia:**
   - Diseñado para soportar la estación principal de mostrador y terminales auxiliares (almacén/administración) operando simultáneamente sobre una base de datos local compartida en red LAN sin bloqueos ni retrasos perceptibles.

---

### 2.5. Soportabilidad y Mantenibilidad (Supportability)

1. **Arquitectura Modular:**
   - Separación estricta entre capa de presentación (UI), capa de lógica de negocio (Servicios de Dominio) y capa de persistencia/datos (Repositorios / ORM o query builder).
2. **Facilidad de Instalación y Portabilidad:**
   - Instalador empaquetado o contenedor ligero que permita desplegar el sistema en los equipos de cómputo de Papelería Liz-Leo en menos de 15 minutos.
3. **Localización e Internacionalización:**
   - Interfaz de usuario en Español (México).
   - **Formato monetario estricto en Pesos Mexicanos (`$ MXN`):** Todos los valores, precios unitarios, costos de adquisición, subtotales, IVA y totales se expresan exclusivamente en Pesos Mexicanos (ej. `$ 1,250.50 MXN`).
   - Formato de fecha estándar local (`DD/MM/AAAA hh:mm A/P`).
4. **Exportación e Intercambio de Datos:**
   - Capacidad de exportar todos los catálogos, reportes de ventas, compras y kardex a formatos estándar abiertos: **Excel (.xlsx)** y **CSV (.csv)** para análisis contable y fiscal en moneda nacional.

---

## 3. Restricciones Adicionales (+)

### 3.1. Restricciones de Hardware y Periféricos
- **Lector de Códigos de Barras:** Compatibilidad universal con lectores USB de emulación de teclado (HID Keyboard Emulation), capaces de decodificar simbologías 1D (EAN-13, EAN-8, UPC-A, Code 128) y 2D (códigos QR para pagos CoDi/SPEI si aplica).
- **Impresoras Térmicas de Tickets:** Soporte nativo para impresoras térmicas de 58 mm y 80 mm mediante el estándar de comandos **ESC/POS** a través de conexión USB, puerto COM virtual o red ethernet.
- **Cajón de Dinero Portamonedas:** Conexión estándar RJ11/RJ12 conectado a la impresora de tickets, abriéndose automáticamente mediante el comando ESC/POS `ESC p` al finalizar una venta en efectivo.

### 3.2. Restricciones de Sistema Operativo y Software Base
- **Sistema Operativo:** Windows 10 (versión 1903 o superior) y Windows 11 de 64 bits instalados en la papelería.
- **Motor de Base de Datos:** Base de datos relacional ligera y confiable (PostgreSQL 14+ o SQLite con WAL mode para versión monousuario, MySQL/MariaDB compatible).
- **Consumo de Memoria RAM:** La aplicación en ejecución no debe superar los 350 MB de memoria RAM en reposo.

### 3.3. Restricciones Legales y Normativas
- Cumplimiento de normativas de emisión de comprobantes simplificados de venta (tickets de compra con razón social comercial de **Papelería Liz-Leo**, RFC genérico o fiscal del negocio, fecha, hora, desglose de impuestos en MXN e información de garantía/devolución).
- Protección de datos personales de clientes y empleados conforme a la legislación mexicana vigente.
