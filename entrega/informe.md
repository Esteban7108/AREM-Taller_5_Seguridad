# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
Taller_5_Seguridad


## 📆 Fecha de la sesión
11/09/2026
## 👥 Integrantes presentes
- Esteban Díaz
- Juliana Moreno

## 🧠 Descripción general del trabajo
 
El objetivo del taller es analizar los riesgos de seguridad de una parte crítica del sistema EdukIT (plataforma de educación virtual) usando el marco STRIDE (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege). La actividad se desarrolló siguiendo la metodología de 5 pasos de la guía del taller: elegir un flujo crítico y dibujar su diagrama de flujo de datos (DFD), identificar los elementos a analizar, aplicar las 6 categorías STRIDE, evaluar impacto y proponer mitigación, y priorizar los hallazgos por nivel de riesgo. Como complemento práctico, se resolvió uno de los retos guiados en OWASP Juice Shop y se relacionó con una fila de la tabla de amenazas.
 
## 🔧 Proceso de desarrollo
 
De los elementos sensibles listados para EdukIT en el enunciado del taller (acceso de estudiantes a cursos, publicación de contenidos por docentes, procesamiento de pagos con terceros, almacenamiento de datos personales y notas académicas), se decidió trabajar el flujo de **procesamiento de pagos con terceros**, distinto al flujo de acceso a cursos ya desarrollado como ejemplo guiado en la guía del taller. Esta decisión se tomó porque el flujo de pagos introduce un actor externo adicional —la pasarela de pago— fuera del control directo del sistema, y maneja información financiera cuya exposición o manipulación tiene un impacto de negocio más severo.
 
Se modeló primero el DFD, ubicando el límite de confianza entre el estudiante y la pasarela de pago (ambos externos) frente al backend de EdukIT (Módulo de Pagos, Módulo de Suscripciones y BD de Transacciones). Sobre este diagrama se aplicaron sistemáticamente las 6 categorías STRIDE, formulando una amenaza concreta por categoría y ajustando la redacción para que cada una apuntara a un elemento específico del diagrama en lugar de una amenaza genérica. Como herramientas se usó un editor de diagramas para el DFD y una hoja de cálculo basada en la plantilla oficial de 12 columnas para consolidar la tabla de amenazas. Finalmente, se validó una de las amenazas identificadas (Information Disclosure sobre la BD de Transacciones) con un reto práctico de explotación real en OWASP Juice Shop, ajustando la descripción de la amenaza para reflejar la causa raíz observada (falta de validación de propiedad del recurso, patrón IDOR).
 
## 🧩 Análisis del modelo propuesto
 
- **Estructura del modelo:** el DFD se compone de un actor externo (estudiante), un segundo actor externo fuera del control del sistema (pasarela de pago), dos procesos internos (Módulo de Pagos y Módulo de Suscripciones) y un almacén de datos (BD de Transacciones), conectados por seis flujos de datos. Esta estructura es deliberadamente compacta para mantener el análisis enfocado en el flujo crítico, sin diluirlo en elementos secundarios del sistema.
- **Representación de las necesidades del cliente:** el modelo refleja la necesidad de EdukIT de procesar suscripciones pagadas de forma segura, delegando el cobro en un proveedor externo pero manteniendo el control interno sobre cuándo se activa el acceso del estudiante — precisamente el punto donde se concentran las amenazas de mayor riesgo (Elevation of Privilege e Information Disclosure).
- **Supuestos tomados:** se asumió que la comunicación entre el backend de EdukIT y la pasarela de pago ya usa HTTPS como transporte base, y que el sistema cuenta hoy con autenticación de sesión y control de acceso a nivel de aplicación, pero sin mecanismos adicionales (MFA, validación server-to-server, logs firmados) — estos supuestos se reflejan en la columna "Controles de Seguridad Existentes" de la tabla STRIDE.
## 📈 Diagrama final entregado
> DFD del flujo de procesamiento de pagos con terceros (ver diagrama y tabla `tabla-stride-clase.xlsx` entregados junto con este informe).
 
## 📋 Tabla de actores, entidades o componentes
 
| Nombre del elemento | Tipo | Descripción | Responsable |
|---------------------|------|-------------|-------------|
| Estudiante | Actor externo | Inicia el pago de la suscripción | Cliente (fuera del sistema) |
| Pasarela de pago | Actor externo | Procesa el cobro con el medio de pago del estudiante | Proveedor de terceros |
| Módulo de Pagos (P1) | Proceso | Orquesta la solicitud de cobro hacia la pasarela | EdukIT |
| Módulo de Suscripciones (P2) | Proceso | Activa el acceso pagado del estudiante | EdukIT |
| BD de Transacciones (D1) | Almacén de datos | Registra el historial de pagos y suscripciones | EdukIT |
 
## 🔍 Investigación complementaria
 
### Tema investigado:
Principios de seguridad STRIDE aplicados a flujos de pago, y buenas prácticas de autorización a nivel de API (OWASP) y de protección de datos de tarjeta (PCI DSS).
 
### Resumen:
El marco STRIDE, definido originalmente por Microsoft, clasifica las amenazas en seis categorías que cubren de forma sistemática la autenticación, integridad, trazabilidad, confidencialidad, disponibilidad y control de acceso de un sistema. Aplicado al flujo de pagos con terceros de EdukIT, permitió identificar que la amenaza de mayor riesgo (Elevation of Privilege) surge de confiar en una confirmación de pago reportada por el cliente en lugar de validarla directamente con la pasarela, un antipatrón de diseño conocido en sistemas de pago.
 
La investigación en el OWASP API Security Top 10 confirmó que la falla de autorización a nivel de objeto (Broken Object Level Authorization, también conocida como IDOR) ocupa el primer lugar entre los riesgos más críticos en APIs, lo cual respalda directamente la amenaza de Information Disclosure identificada sobre la BD de Transacciones y su validación práctica en el reto de OWASP Juice Shop. Por su parte, el estándar PCI DSS aporta los controles concretos recomendados para mitigar las amenazas de Spoofing y Tampering sobre datos de pago: cifrado en tránsito con TLS 1.2 o superior, minimización de datos de tarjeta almacenados en el servidor propio y verificación adicional del titular del medio de pago.