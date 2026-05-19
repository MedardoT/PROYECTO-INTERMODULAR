# Eficafix S.L.: Infraestructura de Red Empresarial Segura y Escalable

Este repositorio contiene la documentación técnica y lógica del diseño de red para **Eficafix S.L.**, una consultoría tecnológica. El proyecto se centra en la implementación de una arquitectura robusta, segmentada mediante VLANs y protegida por un firewall perimetral, garantizando la alta disponibilidad y la seguridad de los activos de información.

## 1. Topología de Red
La arquitectura se basa en un **Modelo Jerárquico** simplificado, diseñado para optimizar el rendimiento y facilitar la administración:

* **Capa de Core/Distribución:** Centralizada en un switch gestionable multicapa (Cisco Catalyst 3560) que interconecta la red interna con el firewall.
* **Capa de Acceso:** Compuesta por switches Cisco 2960 que proporcionan conectividad final a los puestos de trabajo y servidores.
* **Zona Desmilitarizada (DMZ):** Segmento aislado para el servidor web, accesible desde el exterior pero restringido hacia la red interna.
* **Segmentación Funcional:** Se utiliza una topología en estrella extendida con segmentación lógica mediante VLANs para reducir los dominios de colisión y difusión.

## 2. Diseño Lógico y Direccionamiento

### Esquema de Direccionamiento IP
Se ha implementado un esquema de direccionamiento privado bajo el estándar RFC 1918, dimensionado para soportar el crecimiento de la plantilla.

| Subred (VLAN) | Rango IP | Máscara | Puerta de Enlace | Propósito |
| :--- | :--- | :--- | :--- | :--- |
| VLAN 10 (Management) | 192.168.10.0/24 | 255.255.255.0 | 192.168.10.1 | Gestión de equipos de red |
| VLAN 20 (Staff) | 192.168.20.0/24 | 255.255.255.0 | 192.168.20.1 | Usuarios técnicos y portátiles |
| VLAN 30 (DMZ) | 192.168.30.0/24 | 255.255.255.0 | 192.168.30.1 | Servidor Web y servicios externos |
| VLAN 50 (Backup) | 192.168.50.0/24 | 255.255.255.0 | 192.168.50.1 | Almacenamiento NAS y backups |

### Configuración de VLANs
| ID | Nombre | Descripción Técnica |
| :--- | :--- | :--- |
| 10 | ADMIN_MGMT | Tráfico de administración (SSH, SNMP). Aislada de usuarios. |
| 20 | CORP_DATA | Datos corporativos de empleados y técnicos. |
| 30 | DMZ_EXT | Servidores con exposición pública. |
| 50 | BKUP_ISOLATED | Tráfico de backup. Acceso restringido solo a servidores origen. |

## 3. Equipamiento de Red
El hardware seleccionado garantiza estabilidad y soporte para funciones avanzadas de capa 2 y capa 3:

* **Firewall Cisco ASA 5506-X:** Inspección de estado de paquetes (SPI), terminación de VPNs y control perimetral.
* **Switch Core Cisco Catalyst 3560:** Enrutamiento inter-VLAN y gestión de la troncalidad.
* **Switches de Acceso Cisco 2960:** Conectividad de nodos finales con soporte para port-security.
* **Servidor NAS:** Almacenamiento dedicado en VLAN 50 para backups automatizados.

## 4. Servicios y Protocolos
Se han configurado los siguientes servicios esenciales para la operatividad de la red:

### Checklist de Implementación
- [x] **STP (Spanning Tree Protocol):** Prevención de bucles de capa 2 (PVST+).
- [x] **EtherChannel (LACP):** Agregación de enlaces para aumentar el ancho de banda y proporcionar redundancia.
- [x] **DHCP:** Asignación dinámica de IPs en la VLAN de usuarios.
- [x] **NAT/PAT:** Traducción de direcciones para acceso a Internet desde la red privada.
- [x] **Inter-VLAN Routing:** Configuración de interfaces virtuales (SVIs) en el switch core.
- [x] **Regla de Backup 3-2-1:** Implementada mediante el servidor aislado en VLAN 50.

## 5. Seguridad de Red
La seguridad se articula en múltiples capas (Defensa en Profundidad):

* **Niveles de Seguridad ASA:** Uso de `security-level` (Inside 100, Outside 0, DMZ 50) para control de flujo de tráfico por defecto.
* **Listas de Control de Acceso (ACLs):** Restricción de tráfico entre VLANs, permitiendo únicamente el tráfico estrictamente necesario (ej. SSH solo desde VLAN 10).
* **Seguridad de Puertos (Port-Security):** Limitación de direcciones MAC por puerto en los switches de acceso para prevenir ataques de suplantación o inundación.

### Ejemplo de Configuración de ACL (Concepto)
```bash
# Denegar acceso de la red de invitados a la red de Backup
access-list 101 deny ip 192.168.20.0 0.0.0.255 192.168.50.0 0.0.0.255
access-list 101 permit ip any any
# Aplicar a la interfaz correspondiente
interface Vlan20
 ip access-group 101 in