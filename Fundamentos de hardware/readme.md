# Eficafix: Diseño de Infraestructura de Hardware para Consultoría IT

Este repositorio contiene la documentación técnica y el análisis de costes para el diseño de la infraestructura física de **Eficafix S.L.**, una consultoría especializada en soporte IT, redes y ciberseguridad con sede en Madrid.

## 1. Contexto del Proyecto
El objetivo principal es establecer una base material robusta, redundante y escalable que soporte las operaciones de tres técnicos especializados. La infraestructura ha sido diseñada para integrarse perfectamente con arquitecturas de Redes y Cloud (AWS), siguiendo el lema de la empresa: *"Infraestructura IT que simplemente funciona"*.

## 2. Análisis de Necesidades
Para garantizar la operatividad de Eficafix, se han identificado los siguientes requerimientos de hardware:

* 💻 **Equipos Técnicos (Alto Rendimiento):** 3 estaciones de trabajo fijas para tareas de virtualización de redes y auditorías de seguridad, acompañadas de 3 portátiles para intervenciones presenciales.
* 📊 **Equipos de Administración:** 1 equipo dedicado exclusivamente a tareas administrativas y contabilidad.
* 🖥️ **Infraestructura de Servidores:**
    * **Servidor Web (DMZ):** Para alojamiento de la web corporativa y servicios externos.
    * **Servidor de Producción:** Orientado a la virtualización de entornos de prueba para clientes.
    * **Servidor de Backups (NAS):** Almacenamiento local aislado en una VLAN específica (VLAN 50).
* 🌐 **Hardware Crítico de Red:** Firewall perimetral Cisco ASA y electrónica de red gestionable (Cisco Catalyst) para segmentación mediante VLANs.

## 3. Descripción de Componentes Principales
La selección de componentes se basa en el equilibrio entre rendimiento profesional y fiabilidad de grado empresarial:

| Componente | Selección Estratégica | Función en el Sistema |
| :--- | :--- | :--- |
| **CPU** | Intel Core i7-13700 / Xeon E-2336 | Ejecución de procesos pesados, VMs y servicios críticos 24/7. |
| **Placa Base** | ASUS Prime Z790-P / Supermicro X12STH-F | Interconexión con soporte PCIe 5.0 y gestión remota IPMI en servidores. |
| **RAM** | DDR5 5200MHz / DDR4 ECC | Alta velocidad para multitarea y corrección de errores (ECC) en el servidor. |
| **Almacenamiento** | NVMe Gen4 / HDD SATA | Velocidad de acceso ultra rápida (7000 MB/s) y capacidad masiva para backups. |
| **Fuente Alim.** | Corsair 80 Plus Gold / Redundante (1+1) | Eficiencia energética superior y continuidad del servicio ante fallos eléctricos. |

## 4. Configuración Propuesta: Estación de Trabajo IT
Se detalla a continuación la configuración estándar para los técnicos especialistas, diseñada para maximizar la productividad en entornos de virtualización.

### Especificaciones Técnicas
| Ítem | Detalle del Componente |
| :--- | :--- |
| **Procesador** | Intel Core i7-13700 (16 núcleos) |
| **Memoria RAM** | 32 GB DDR5 5200MHz (2x16GB) |
| **Gráfica** | NVIDIA RTX 3060 12GB (Arquitectura CUDA para auditorías) |
| **Almacenamiento** | 1 TB SSD NVMe M.2 (Gen4) |
| **Placa Base** | ASUS Prime Z790-P ATX |

### Justificación Técnica
* 🚀 **Capacidad de Virtualización:** Permite ejecutar de 3 a 4 servidores virtuales simultáneamente (Kali Linux, Windows Client) sin pérdida de rendimiento.
* ⚡ **Agilidad de Respuesta:** El almacenamiento NVMe Gen4 reduce los tiempos de arranque y despliegue de aplicaciones pesadas como GNS3 o VS Code.
* 🛡️ **Estabilidad:** La certificación 80 Plus Gold de la fuente asegura un aprovechamiento del 90% de la energía, reduciendo el calor generado en jornadas intensivas.

## 5. Sistema de Almacenamiento
Eficafix emplea una estrategia de almacenamiento híbrido para optimizar el rendimiento y la seguridad de los datos.

1.  **Capa de Rendimiento (SSD NVMe):** Instalada en estaciones de trabajo y servidores de aplicaciones para minimizar la latencia en procesos de E/S y virtualización.
2.  **Capa de Capacidad (HDD SATA):** Discos mecánicos de 4TB en el NAS para copias de seguridad históricas e imágenes ISO, priorizando el bajo coste por GB.
3.  **Redundancia Física (RAID 1):** El servidor central implementa *Mirroring* (espejo), permitiendo que el sistema siga operando si un disco falla y facilitando su sustitución en caliente (*Hot Swap*).

## 6. Reflexión y Mejora
La infraestructura ha sido diseñada pensando en el crecimiento orgánico de la empresa:

* **Escalabilidad Vertical:** Las estaciones de trabajo cuentan con ranuras libres para duplicar la RAM hasta 64GB si aumenta el volumen de máquinas virtuales.
* **Centralización (VDI):** Si la plantilla crece, se propone evolucionar hacia la Virtualización de Escritorios utilizando servidores de alta densidad y Thin Clients.
* **Infraestructura de Datos:** Migración hacia una red SAN (Storage Area Network) conectada por Fibra Óptica para garantizar la alta disponibilidad.
* **Networking:** Actualización del backbone de la red local de 1Gbps a 10GbE para soportar el tráfico de backups masivos concurrentes.

---
