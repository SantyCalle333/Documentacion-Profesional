# 📘 SOC Analyst Lab Report – Conversor (Hack The Box)

1. Información general

Plataforma: Hack The Box

Nombre del lab: Conversor

Sistema operativo: Linux

Dificultad: Easy

Tipo de análisis: Defensive / Blue Team perspective

Rol asumido: SOC Analyst Tier 1


2. Objetivo del laboratorio

Analizar un entorno Linux vulnerable desde la perspectiva de un Centro de Operaciones de Seguridad (SOC) con el fin de:

Identificar vectores de ataque comunes en aplicaciones web

Analizar evidencias de abuso de servicios

Reconocer indicadores de compromiso (IOC)

Evaluar controles de detección y respuesta


3. Contexto del incidente

Durante el monitoreo del sistema se observa:

Un servicio web accesible públicamente

Procesamiento de entradas del usuario

Comportamiento anómalo asociado a ejecución de comandos

Sistema afectado:

Servidor Linux expuesto a Internet

Servicio web vulnerable a abuso de input

Vector de ataque sospechado:

Web Application Abuse / Command Injection


4. Evidencias recolectadas
   
4.1 Indicadores observados

Accesos repetitivos a endpoints web

Parámetros manipulados en peticiones HTTP

Respuestas del servidor indicando ejecución no esperada

Procesos hijos iniciados desde el servicio web


4.2 Logs analizados

Web server logs

Requests anómalos

Parámetros con caracteres especiales

System logs

Ejecución de procesos no habituales

Comandos lanzados por el usuario del servicio web

No se documentan payloads ni comandos específicos para cumplir con ToS.


5. Análisis técnico

5.1 Evaluación del comportamiento

El patrón de peticiones no corresponde a uso legítimo

Se identifican intentos sistemáticos de manipulación

Existe impacto potencial en:

Confidencialidad

Integridad del sistema


5.2 Clasificación del evento

Tipo: Incidente de seguridad

Categoría: Compromiso de aplicación web

Severidad estimada: Medium


6. Mapeo MITRE ATT&CK

Técnicas asociadas:

T1190 – Exploit Public-Facing Application

T1059 – Command and Scripting Interpreter

Justificación: El servicio web permite ejecución de comandos mediante manipulación de entradas, comprometiendo el sistema subyacente.


7. Respuesta y acciones recomendadas

7.1 Acciones inmediatas

Aislar el servidor afectado

Revisar integridad del sistema

Rotar credenciales potencialmente expuestas

Revisar accesos recientes


7.2 Medidas preventivas

Validación estricta de entradas

Principio de mínimo privilegio

WAF para detección de patrones maliciosos

Alertas sobre ejecución anómala de procesos


8. Automatización / mejora propuesta

Script para detectar:

Caracteres sospechosos en parámetros HTTP

Ejecución de procesos desde servicios web

Alertas automáticas por:

Creación de shells

Uso anómalo del intérprete de comandos


9. Lecciones aprendidas

Las aplicaciones web mal protegidas son un vector crítico

Logs de aplicaciones y sistema deben correlacionarse

La detección temprana reduce impacto

La automatización es clave para SOC Tier 1


10. Conclusión

Este laboratorio permitió aplicar conceptos fundamentales de un SOC Analyst Junior, reforzando habilidades en:

Análisis de actividad sospechosa

Evaluación de incidentes web

Uso de MITRE ATT&CK

Propuesta de controles defensivos


11. Disclaimer

Este repositorio documenta el laboratorio exclusivamente desde una perspectiva defensiva y educativa.
No se incluyen flags, payloads ni pasos de explotación.
