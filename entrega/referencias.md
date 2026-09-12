# 📚 Referencias Bibliográficas del Taller

Este archivo contiene las fuentes consultadas para el desarrollo del taller, tanto para el componente técnico como para la investigación complementaria.

## 🔖 Taller
Taller_5_Seguridad


**Microsoft. (s.f.). *The STRIDE Threat Model*. Microsoft Learn.**
URL: https://learn.microsoft.com/en-us/previous-versions/commerce-server/ee823878(v=cs.20)
Descripción: documentación oficial del marco STRIDE, origen de las 6 categorías (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege) utilizadas como base metodológica del taller.
 
**OWASP Foundation. (2023). *API1:2023 — Broken Object Level Authorization*. OWASP API Security Top 10.**
URL: https://owasp.org/API-Security/editions/2023/en/0xa1-broken-object-level-authorization/
Descripción: describe la falla de autorización a nivel de objeto (BOLA/IDOR), ocupa el primer lugar del OWASP API Security Top 10 y respalda directamente la amenaza de Information Disclosure identificada en la BD de Transacciones (T4), así como el reto práctico resuelto en OWASP Juice Shop.
 
**OWASP Foundation. (2023). *OWASP API Security Top 10 — 2023*.**
URL: https://owasp.org/API-Security/editions/2023/en/0x11-t10
Descripción: listado completo de los diez riesgos más críticos en APIs (autorización rota, autenticación rota, consumo irrestricto de recursos, entre otros), usado como referencia complementaria para contextualizar las amenazas de Spoofing y Denial of Service del flujo de pagos.
 
**PCI Security Standards Council. (s.f.). *PCI DSS — Payment Card Industry Data Security Standard*.**
URL: https://www.pcisecuritystandards.org/standards/pci-dss/
Descripción: estándar de la industria de pagos con tarjeta; establece requisitos técnicos y operativos (cifrado en tránsito con TLS 1.2+, minimización de datos de tarjeta en el servidor propio, segmentación de red) directamente aplicables a la mitigación de las amenazas de Tampering (T2) y Spoofing (T1) sobre el flujo de pagos con terceros.
 
**OWASP Foundation. (s.f.). *OWASP Juice Shop Project*.**
URL: https://owasp.org/www-project-juice-shop/
Descripción: aplicación web deliberadamente vulnerable utilizada para la práctica guiada de explotación real; sustenta la validación práctica del reto 3 (acceso al carrito de otro usuario) relacionado con la amenaza T4 de la tabla STRIDE.
 
**NIST. (2018). *Framework for Improving Critical Infrastructure Cybersecurity (Cybersecurity Framework), versión 1.1*. National Institute of Standards and Technology.**
URL: https://www.nist.gov/cyberframework
Descripción: marco de referencia para la gestión de riesgos de ciberseguridad; utilizado como respaldo conceptual para la clasificación de impacto, probabilidad y nivel de riesgo aplicada en la priorización de hallazgos (Paso 5 de la metodología).
_Este archivo forma parte de la entrega académica del curso AREM - Universidad de La Sabana._
