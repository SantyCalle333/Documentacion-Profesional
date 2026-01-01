# Post-Incident Improvements – WhiteRabbit

## Detection

* No se generan alertas ante patrones de autenticación derivados de credenciales regeneradas.
* Ausencia de detección sobre uso anómalo de librerías estándar (`rand()` / `srand()`) en contextos sensibles.
* Falta de correlación entre:

  * Timestamps del sistema
  * Procesos de generación de secretos
  * Eventos de autenticación SSH
* Los accesos se registran como legítimos, evadiendo controles tradicionales.

---

## Prevention

* Reemplazar PRNG no criptográficos por fuentes seguras (`/dev/urandom`, `getrandom()`, libs criptográficas).
* Eliminar dependencias de tiempo como semilla para generación de credenciales.
* Separar completamente la lógica de generación de secretos del flujo de autenticación.
* Implementar expiración estricta y rotación automática de credenciales.
* Limitar intentos de autenticación incluso con credenciales válidas recién creadas.

---

## Automation

* Scripts de monitoreo para detectar:

  * Generación repetitiva de secretos en ventanas temporales cortas.
  * Accesos SSH inmediatamente posteriores a procesos de generación.
* Alertas por:

  * Patrones de autenticación sincronizados con eventos de sistema.
  * Uso anómalo de funciones pseudoaleatorias en binarios críticos.
* Integración con SIEM para análisis temporal y correlación avanzada.

---

## SOC Process

* Definir playbook específico para:

  * Compromiso lógico por debilidad criptográfica.
  * Abuso de PRNG predecibles.
* Escalamiento automático a Tier 2 cuando:

  * Se detecten accesos válidos con patrones no humanos.
  * Exista dependencia crítica de timestamps para autenticación.
* Incorporar análisis de diseño lógico como parte del triage inicial.
* Documentar el incidente como **failure of secure design**, no como misconfiguration.

---

## Key Takeaway

> Un sistema puede fallar sin exploits, sin malware y sin alertas…
> si la lógica de seguridad es predecible.

