# WhiteRabbit – Notas de Análisis de Incidente

**Dificultad:** Insane
**SO:** Linux
**Plataforma:** Hack The Box

## Visión General

Este documento resume el análisis de un incidente de seguridad realizado sobre la máquina **WhiteRabbit**.
El enfoque está orientado a la identificación de comportamientos anómalos, la correlación de eventos y la evaluación de riesgos arquitectónicos y operativos desde una perspectiva defensiva.

---

## Observaciones Iniciales

* Se detectaron intentos repetitivos de autenticación SSH siguiendo un patrón estructurado y no aleatorio.
* La actividad no corresponde a ataques de fuerza bruta tradicionales ni a accesos impulsados por interacción humana.
* Varios intentos involucran archivos presentados como claves privadas que fallan durante la validación criptográfica.
* El comportamiento sugiere conocimiento previo de la lógica interna del sistema de autenticación.

---

## Correlación de Eventos

* Los intentos de autenticación SSH se correlacionan directamente con procesos locales responsables de la generación de credenciales.
* Los timestamps del sistema coinciden estrechamente con la creación del material de autenticación.
* La ventana de tiempo reducida entre la generación y el uso indica dependencia de valores temporales predecibles.
* El patrón de acceso sugiere fuertemente reconstrucción de credenciales en lugar de simples intentos por adivinanza.

---

## Hipótesis

* El sistema depende de un **generador de números pseudoaleatorios (PRNG) débil** (`rand()` / `srand()`).
* La semilla del PRNG se deriva de **timestamps predecibles**, lo que permite la reconstrucción de credenciales.
* Los mecanismos de autenticación aparentan ser criptográficamente correctos a nivel superficial, pero presentan fallas lógicas.
* No existe una mitigación efectiva contra la reutilización o regeneración de credenciales.

---

## Acciones Tomadas

* Se clasificó la actividad como un **incidente de seguridad real**, y no como una simple mala configuración.
* Se priorizó la investigación de:

  * Lógica de generación de credenciales y claves
  * Uso de librerías estándar inseguras en operaciones críticas de seguridad
* Se recomendó una auditoría completa del código relacionado con autenticación.
* Se sugirió la rotación inmediata de credenciales y revisión de accesos.

---

## Riesgos Identificados

* Compromiso total del sistema mediante credenciales válidas
* Persistencia sin generación de ruido de explotación
* Evasión de sistemas de detección al tratarse de accesos “legítimos”
* Reutilización de lógica insegura en otros sistemas o entornos

---

## Aprendizajes Defensivos

* La criptografía es tan fuerte como la lógica que la implementa.
* Las semillas basadas en tiempo son predecibles y no son adecuadas para operaciones sensibles.
* Las estrategias de detección deben incluir análisis de comportamiento, no solo alertas basadas en firmas.
* La generación de credenciales debe apoyarse en fuentes de aleatoriedad criptográficamente seguras.

---

## Etiquetas

`#CyberSecurity` `#BlueTeam` `#SOC` `#IncidentResponse` `#HTB` `#LinuxSecurity`

---


