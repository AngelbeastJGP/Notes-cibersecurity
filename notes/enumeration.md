# Enumeración en Pentesting
Autor: [Angelbeast]
Perfil: ASIR → Ciberseguridad

---

## 1. Principio fundamental
La enumeración es un proceso **metódico**, no una colección de comandos.
El objetivo es **entender el sistema**, no solo encontrar vulnerabilidades.

> IP → Puertos → Servicios → Versiones → Configuración → Credenciales → Acceso

Si no hay acceso, la enumeración **no ha terminado**.

---

## 2. Reconocimiento inicial

### 2.1 Comprobación básica
```bash
ping IP

TTL aproximado → Linux / Windows

Latencia → VM local / red real

---

### 2.2 Descubrimiento de puertos
```bash
nmap -p- --min-rate 1000 IP

---

### 2.2 enumeración servicios
```bash
nmap -sC -sV -p PUERTOS IP -oN nmap.txt

---

## 3. Enumeración por servicio

3.1 SSH (22)

Qué pienso:

¿Permite login de root?

¿Usuarios válidos?

¿Autenticación por contraseña o clave?

Pruebas:

ssh usuario@IP


Errores comunes:

Contraseñas débiles

Reutilización de credenciales

Claves privadas mal protegidas

3.2 FTP (21)

Qué busco:

Acceso anónimo

Archivos sensibles

Backups o credenciales

ftp IP


Configuraciones inseguras típicas:

anonymous enabled

write permissions

directorios expuestos

3.3 HTTP / HTTPS (80 / 443)

Orden correcto:

Navegador

Código fuente

Rutas comunes

Tecnologías

Enumeración automática

Herramientas:

whatweb http://IP
gobuster dir -u http://IP -w wordlist.txt


Busco:

Formularios

Paneles de login

Versiones vulnerables

Archivos de configuración

Comentarios en HTML/JS

3.4 SMB (445)

Mentalidad sysadmin (clave):

Shares

Permisos

Usuarios

Información interna

smbclient -L //IP


Configuraciones inseguras:

Shares públicos

Acceso sin autenticación

Permisos excesivos

3.5 Otros servicios (según aparezcan)

MySQL (3306)

PostgreSQL (5432)

LDAP (389)

RDP (3389)

Regla:

Si no conozco el servicio, lo investigo antes de atacarlo.
## 4. Búsqueda de credenciales

Las credenciales son el objetivo principal, más importantes que los exploits.

Fuentes habituales:

Archivos de configuración

Backups

Shares SMB

Variables de entorno

Reutilización de contraseñas

## 5. Enumeración post-acceso
5.1 Linux

Usuarios y grupos

Sudo (sudo -l)

Cron jobs

Servicios activos

Permisos de archivos

Binarios SUID

5.2 Windows

Usuarios y grupos

Privilegios

Servicios

Scheduled Tasks

ACLs

Movimiento lateral

## 6. Errores que evito

Ejecutar herramientas sin entenderlas

No analizar los outputs

Enumerar solo una vez

Pensar solo como atacante

No documentar el proceso

## 7. Documentación profesional

Siempre documento:

Qué encontré

Por qué es relevante

Cómo se explota

Cómo se detecta

Cómo se mitiga

Un buen pentester explota.
Un excelente profesional explica cómo corregir el problema.

## 8. Checklist mental rápido

¿He enumerado todos los puertos?

¿He analizado cada servicio?

¿He buscado credenciales?

¿He pensado como sysadmin?

¿He documentado correctamente?

Si alguna respuesta es “no”, continúo enumerando.

