# Incident Analysis Notes – Conversor

## Observaciones iniciales
- El servicio web presenta comportamiento no esperado ante entradas manipuladas.
- Se detectan accesos repetitivos desde una misma fuente.
- El patrón sugiere automatización más que uso humano.

## Correlación de eventos
- Requests HTTP anómalos coinciden con ejecución de procesos en el sistema.
- Los timestamps muestran relación directa entre petición y ejecución.

## Hipótesis
- La aplicación no valida correctamente entradas del usuario.
- El servicio web ejecuta comandos con privilegios innecesarios.

## Decisiones tomadas
- Clasificar el evento como incidente real.
- Priorizar análisis de procesos y accesos recientes.
- Recomendar aislamiento del sistema.

## Riesgos identificados
- Escalada de privilegios
- Persistencia
- Exfiltración de información
