+++
title = "Auditoría Web: Análisis de Superficie de Ataque"
image = "/images/auditoria.png"
date = 2026-02-08
description = "Identificación de vulnerabilidades, servicios obsoletos y paneles expuestos en infraestructura web."
tags = ["Cybersecurity", "Pentesting", "Nmap", "Fuzzing"]
categories = ["Proyectos"]
featured = true
+++
## 🛡️ Resumen del Proyecto
Realice un análisis de seguridad sobre un dominio perteneciente al estado para identificar puntos débiles que comprometan datos o disponibilidad del servicio. Fue realizado con un enfoque ético y preventivo, usando técnicas de reconocimiento pasivo y validaciones manuales.
Una vez recopilada toda la información se procedió a hacer un reporte técnico y entregado a dos funcionarios públicos para poder presentarlo ante quien corresponda.

## 🔍 Hallazgos Principales

### 1. Exposición de Paneles Administrativos
Mediante la lectura del archivo `robots.txt` y técnicas de **fuzzing de directorios**, localicé interfaces de gestión accesibles desde el internet público:
* **CMS Sisfox:** Panel de gestión de contenido con una falta de actualización de casi 3 años.
* **cPanel & Webmail:** Puertos administrativos (`2083`, `2096`) abiertos, permitiendo intentos de acceso directo al backend del servidor.

### 2. Análisis de Servicios (Escaneo de Puertos)
El servidor cuenta con una superficie de ataque excesiva con múltiples servicios expuestos:
* **Base de Datos (MySQL):** Puerto `3306` visible, lo que facilita ataques de reconocimiento y posibles DoS.
* **Gestión de Correo:** Puertos `21` (FTP), `25/587` (SMTP) y `110/143` (POP3/IMAP) abiertos, aumentando los vectores de entrada.
* **DNS (ISC BIND):** Servicio abierto que podría revelar la estructura interna o facilitar un ataque DoS.

### 3. Infraestructura Obsoleta
* **Sistema Operativo:** Uso de **Red Hat Enterprise Linux 7**, versión que requiere soporte extendido para parches de seguridad, elevando el riesgo ante vulnerabilidades no corregidas.

## 🛠️ Stack Tecnológico
* **Reconocimiento:** `Nmap` (mapeo de puertos) y `WhatWeb`.
* **Enumeración Web:** `ffuf` (fuzzing de directorios).
* **Análisis Ético:** Pruebas manuales de credenciales y análisis de vulnerabilidades conocidas (CVE).

## 🚀 Recomendaciones Propuestas
1.  **Hardening de Red:** Restringir el acceso a paneles administrativos mediante VPN o filtrado por IP.
2.  **Cierre de Puertos:** Bloquear el acceso externo a los puertos de MySQL y DNS.
3.  **Actualización:** Migrar el sistema operativo a una versión con soporte activo y actualizar el CMS de forma urgente.

> **Nota:** Este reporte se realizó con fines educativos y de colaboración ciudadana, garantizando en todo momento la estabilidad de los servicios analizados.
