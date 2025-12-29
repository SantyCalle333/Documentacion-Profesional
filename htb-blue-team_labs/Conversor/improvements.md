# Post-Incident Improvements – Conversor

## Detección
- Falta de alertas por ejecución de comandos desde servicios web.
- No existe correlación entre logs web y de sistema.

## Prevención
- Endurecimiento de permisos del servicio web.
- Validación estricta de inputs.
- WAF con reglas personalizadas.

## Automatización
- Script para detectar patrones sospechosos en parámetros HTTP.
- Alertas por frecuencia de requests anómalos.

## Proceso SOC
- Definir playbook específico para abuso de aplicaciones web.
- Escalamiento automático a Tier 2 en casos repetitivos.
