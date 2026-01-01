# Post-Incident Improvements – CAP

## Detection

* No se generan alertas por acceso no autorizado a archivos de captura de tráfico (`.pcap`).
* Ausencia de detección sobre exposición de recursos sensibles vía HTTP.
* Falta de correlación entre:

  * Accesos al servicio web
  * Descarga de archivos PCAP
  * Autenticaciones SSH posteriores
* Los accesos a información crítica no se diferencian de tráfico web legítimo.

---

## Prevention

* Implementar controles estrictos de **autenticación y autorización** para cualquier archivo de captura.
* Evitar el almacenamiento persistente de tráfico que contenga credenciales o sesiones.
* Sanitizar o anonimizar datos sensibles antes de cualquier almacenamiento.
* Separar completamente los servicios de captura de red del entorno accesible al usuario.
* Forzar cifrado en servicios internos para evitar exposición de credenciales en texto claro.

---

## Automation

* Scripts automáticos para detectar:

  * Archivos `.pcap` accesibles desde rutas públicas.
  * Descargas repetitivas de capturas de red desde una misma fuente.
* Alertas por:

  * Acceso a recursos sensibles sin autenticación válida.
  * Correlación temporal entre descarga de PCAP y autenticaciones exitosas.
* Integración con SIEM para análisis de secuencia: **exposición → análisis → acceso**.

---

## SOC Process

* Definir playbook específico para:

  * Exposición de información sensible.
  * Fuga pasiva de credenciales.
* Escalamiento automático a Tier 2 cuando:

  * Se detecte acceso a archivos PCAP sin autorización.
  * Existan autenticaciones posteriores usando credenciales recién expuestas.
* Incorporar revisión de controles de acceso como parte del triage inicial.
* Documentar el incidente como **fallo de control de acceso**, no como error de usuario.

---

## Key Takeaway

> No todo compromiso requiere explotación activa.
> A veces, el sistema entrega las credenciales por sí solo.

---
