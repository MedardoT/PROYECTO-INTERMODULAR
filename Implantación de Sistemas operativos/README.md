# Proyecto Intermodular – Prometeo  
## Implantación y documentación de sistemas operativos en Efica Fix S.L.

### Autores
- Ismael Medardo Torres Becerra  
- Noa Maximilian Tóth-Égetö  

### Fecha
20 de abril de 2026

---

# Descripción del proyecto

Este proyecto consiste en el diseño, implantación y configuración de una infraestructura informática híbrida para la empresa ficticia **Efica Fix S.L.**.  

La infraestructura combina:
- Servidores físicos
- Virtualización mediante VMware ESXi
- Servicios Windows y Linux
- Gestión centralizada de usuarios mediante Active Directory
- Servicios web y DNS
- Sistema de copias de seguridad

El objetivo principal es implementar un entorno empresarial funcional y seguro, documentando cada paso del proceso.

---

# Infraestructura utilizada

## Servidores físicos
- 1 servidor físico con **Windows Server 2019**
- 1 servidor físico con **VMware ESXi**

## Máquinas virtuales
- Ubuntu Server (alojado en ESXi)

## Equipos cliente
- Windows 11
- Portátiles de usuarios

---

# Tecnologías utilizadas

| Tecnología | Función |
|---|---|
| Windows Server 2019 | Controlador de dominio |
| Active Directory | Gestión de usuarios y permisos |
| Windows 11 | Equipos cliente |
| Ubuntu Server | Servidor web y DNS |
| Apache2 | Hosting web |
| Bind9 | Servidor DNS |
| VMware ESXi | Virtualización |
| SSH | Administración remota |
| Unraid | NAS y backups |
| Rufus | Creación de USB booteable |

---

# Arquitectura del sistema


                    INTERNET
                        |
                  [ Firewall ]
                        |
                 ----------------
                 |              |
         Windows Server      VMware ESXi
         (Active Directory)       |
                                  |
                           Ubuntu Server
                          (Apache + DNS)


---

# Sistemas operativos implementados

## Windows Server 2019
Utilizado como:
- Controlador de dominio
- Gestión de usuarios
- Políticas de grupo
- Administración de permisos

### Servicios configurados
- Active Directory
- DNS interno
- Gestión de grupos y usuarios
- Backups programados

---

## Ubuntu Server
Implementado como:
- Servidor web
- Servidor DNS
- Servidor SSH
- Servidor de almacenamiento interno

### Servicios configurados
- Apache2
- Bind9
- SSH
- DNS local

---

## Windows 11
Instalado en los equipos cliente de la empresa.

### Funciones
- Unión al dominio
- Acceso remoto y autenticación centralizada
- Uso de software ofimático y desarrollo

---

## VMware ESXi
Hipervisor de tipo 1 utilizado para:
- Virtualización
- Gestión de máquinas virtuales
- Optimización de recursos

---

# Instalación de los sistemas operativos

## Instalación manual

Todos los sistemas operativos fueron instalados manualmente mediante memorias USB booteables creadas con Rufus.

### Sistemas instalados
- Windows 11
- Windows Server 2019
- VMware ESXi

Ubuntu Server fue instalado como máquina virtual dentro de ESXi.

---

# Configuración de Active Directory

## Funcionalidades implementadas
- Creación de dominio
- Gestión de usuarios
- Gestión de grupos
- Restricción de permisos
- Integración de equipos cliente

## Grupos creados

| Grupo | Función |
|---|---|
| Administradores | Gestión total del sistema |
| Asistentes de sistemas | Usuarios limitados |

## Usuarios creados

| Usuario | Grupo | Permisos |
|---|---|---|
| Noa | Administradores | Privilegiado |
| Ismael | Administradores | Privilegiado |
| Asistente1 | Asistentes de sistemas | No privilegiado |

---

# Configuración del servidor web

## Apache2

Instalación:

bash
sudo apt update && sudo apt upgrade -y
sudo apt install apache2


### Funciones implementadas
- Hosting de la web corporativa
- Configuración de Virtual Hosts
- Acceso desde la red interna

---

# Configuración DNS

## Bind9

Instalación:

bash
sudo apt install bind9


### Funciones implementadas
- Resolución DNS local
- Dominio interno
- Configuración de registros:
  - SOA
  - NS
  - A
  - CNAME

---

# Conectividad y pruebas

Se realizaron pruebas de:
- Ping entre equipos
- Resolución DNS
- Acceso a la web
- Inicio de sesión en dominio
- Restricción de permisos

---

# Backups

Se configuraron copias de seguridad del:
- Active Directory
- Usuarios
- Configuración crítica del sistema

Los backups se almacenan en un servidor NAS interno basado en Ubuntu/Unraid.

---

# Seguridad

## Medidas aplicadas
- Instalación limpia de sistemas operativos
- Usuarios limitados mediante Active Directory
- Segmentación lógica de servicios
- DNS interno
- SSH para administración remota

---

# Servicios implementados

| Servicio | Sistema |
|---|---|
| Active Directory | Windows Server |
| Apache2 | Ubuntu Server |
| Bind9 | Ubuntu Server |
| SSH | Ubuntu Server |
| Backups | NAS interno |

---