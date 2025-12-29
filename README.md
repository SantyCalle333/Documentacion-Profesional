# 🛡️ SOC Analyst Lab Report – Conversor (Hack The Box)

## 📌 Información general

| Campo | Detalle |
|------|--------|
| Plataforma | Hack The Box |
| Laboratorio | Conversor |
| Sistema Operativo | Linux |
| Dificultad | Easy |
| Enfoque | Blue Team / Defensive Analysis |
| Rol | SOC Analyst Tier 1 |

---

## 🎯 Objetivo del laboratorio

Analizar un entorno Linux vulnerable desde una **perspectiva defensiva**, con el fin de identificar actividad anómala, evaluar el impacto de un posible compromiso y proponer acciones de detección y respuesta alineadas a un **SOC Analyst Junior**.

---

## 🧩 Contexto del incidente

Durante el monitoreo del sistema se identificó:

- Un **servicio web expuesto públicamente**
- Procesamiento de entradas controladas por el usuario
- Comportamientos compatibles con **abuso de aplicación web**

**Sistema afectado:**  
Servidor Linux con servicio web accesible desde Internet.

**Vector de ataque sospechado:**  
Web Application Abuse / Command Injection.

---

## 🔍 Evidencias recolectadas

### Indicadores observados
- Accesos repetitivos a endpoints web
- Manipulación anómala de parámetros HTTP
- Respuestas del servidor inconsistentes con uso legítimo
- Ejecución de procesos no habituales desde el servicio web

### Logs analizados
- **Web server logs**
  - Requests con patrones anómalos
- **System logs**
  - Procesos ejecutados por el usuario del servicio web

> No se incluyen payloads, comandos ni flags para cumplir con los términos de uso de Hack The Box.

---

## 🧠 Análisis técnico

### Evaluación del comportamiento
- La actividad observada **no corresponde a uso normal**
- Se detectan patrones automatizados
- Existe impacto potencial sobre:
  - Confidencialidad
  - Integridad del sistema

### Clasificación del evento

| Criterio | Resultado |
|--------|-----------|
| Tipo de evento | Incidente de seguridad |
| Categoría | Compromiso de aplicación web |
| Severidad | Media |

---

## 🧭 Mapeo MITRE ATT&CK

Técnicas identificadas:

- **T1190 – Exploit Public-Facing Application**
- **T1059 – Command and Scripting Interpreter**

**Justificación:**  
La aplicación web permite la ejecución de comandos mediante manipulación de entradas, afectando el sistema subyacente.

---

## 🚨 Respuesta y acciones recomendadas

### Acciones inmediatas
- Aislar el servidor afectado
- Revisar integridad del sistema
- Analizar accesos recientes
- Evaluar rotación de credenciales

### Medidas preventivas
- Validación estricta de entradas
- Principio de mínimo privilegio
- Implementación de WAF
- Alertas por ejecución anómala de procesos

---

## ⚙️ Automatización y mejora propuesta

- Detección automática de:
  - Caracteres sospechosos en parámetros HTTP
  - Procesos iniciados por servicios web
- Alertas por:
  - Uso del intérprete de comandos
  - Creación de shells no esperadas

---

## 📚 Lecciones aprendidas

- Las aplicaciones web expuestas son un vector crítico
- La correlación entre logs web y de sistema es clave
- La detección temprana reduce impacto
- La automatización es fundamental en SOC Tier 1

---

## ✅ Conclusión

Este laboratorio permitió reforzar habilidades esenciales de un **SOC Analyst Junior**, incluyendo:

- Análisis de actividad anómala
- Clasificación de incidentes
- Uso del marco MITRE ATT&CK
- Propuesta de controles defensivos

---

## ⚠️ Disclaimer

Este repositorio contiene **documentación defensiva y educativa**.  
No se incluyen walkthroughs, flags ni detalles de explotación que violen los términos de Hack The Box.


11. Disclaimer

Este repositorio documenta el laboratorio exclusivamente desde una perspectiva defensiva y educativa.
No se incluyen flags, payloads ni pasos de explotación.
