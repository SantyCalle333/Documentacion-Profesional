# CAP – Notas de Análisis de Incidente

**Dificultad:** Easy
**SO:** Linux
**Plataforma:** Hack The Box

## Visión General

Este documento resume el análisis de un incidente de seguridad realizado sobre la máquina **CAP**.
El enfoque está orientado a la identificación de comportamientos anómalos, la correlación de eventos y la evaluación de riesgos técnicos desde una perspectiva defensiva.

---

## Observaciones Iniciales

* El servicio web expone tráfico capturado accesible sin controles de autorización adecuados.
* Se detecta acceso directo a archivos PCAP desde el navegador.
* La información expuesta permite identificar credenciales y sesiones activas.
* El comportamiento observado indica una falla de control de acceso, no un error operativo.

---

## Correlación de Eventos

* Accesos HTTP a archivos PCAP preceden intentos de autenticación SSH exitosos.
* Las credenciales capturadas en tráfico de red coinciden con accesos posteriores al sistema.
* No existe separación entre datos sensibles y contenido público.
* Los eventos siguen una secuencia lógica de recolección → análisis → acceso.

---

## Hipótesis

* La aplicación no implementa controles de autorización adecuados sobre recursos sensibles.
* Los archivos de captura contienen información confidencial en texto claro.
* El sistema asume confianza implícita en el usuario que accede al servicio web.
* No existen mecanismos de sanitización o expiración del material capturado.

---

## Acciones Tomadas

* Clasificar el evento como **incidente de seguridad real** por exposición de información sensible.
* Priorizar revisión de:

  * Controles de acceso en la aplicación web
  * Manejo y almacenamiento de capturas de red
* Recomendar eliminación o restricción inmediata de acceso a archivos PCAP.
* Sugerir rotación de credenciales comprometidas.

---

## Riesgos Identificados

* Compromiso del sistema mediante credenciales válidas.
* Exposición pasiva de información sensible sin interacción activa.
* Reutilización de credenciales capturadas.
* Movimiento lateral en entornos reales.

---

## Aprendizajes Defensivos

* La captura de tráfico debe considerarse información altamente sensible.
* Todo recurso debe validar autenticación y autorización.
* El cifrado es inútil si los datos se exponen antes o después de su uso.
* Los sistemas de monitoreo deben alertar por accesos a datos sensibles.

---

## Etiquetas

`#CyberSecurity` `#BlueTeam` `#SOC` `#IncidentResponse` `#HTB` `#LinuxSecurity`

---

---

# CAP – Mejoras Post-Incidente

## Detección

* No existen alertas por acceso no autorizado a archivos PCAP.
* Falta correlación entre accesos web y autenticaciones SSH.
* Ausencia de monitoreo sobre exposición de datos sensibles.

---

## Prevención

* Implementar controles de acceso estrictos sobre archivos de captura.
* Eliminar almacenamiento innecesario de tráfico sensible.
* Forzar cifrado extremo a extremo en servicios internos.
* Aislar servicios de captura del entorno productivo.

---

## Automatización

* Scripts para detectar exposición de archivos `.pcap` vía HTTP.
* Alertas automáticas por accesos a recursos sensibles.
* Integración con SIEM para correlación de eventos web y sistema.

---

## Proceso SOC

* Definir playbook para exposición de información sensible.
* Escalamiento automático a Tier 2 ante detección de fuga de datos.
* Documentar el incidente como **fallo de control de acceso**.

---

## Conclusión

> Un sistema no necesita ser explotado para estar comprometido.
> Basta con exponer información crítica sin control.

---
