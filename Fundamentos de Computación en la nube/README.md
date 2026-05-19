# Eficafix Cloud: Infraestructura Escalable y Alta Disponibilidad en AWS

Este repositorio detalla la fase de migración y despliegue en la nube de **Eficafix S.L.**, realizada para el módulo de Fundamentos de Computación en la Nube. El objetivo es evolucionar la infraestructura física tradicional hacia un entorno gestionado, elástico y seguro utilizando Amazon Web Services (AWS).

## 1. Elección del Proveedor Cloud: Amazon Web Services (AWS)

Para este proyecto se ha seleccionado **AWS** como proveedor estratégico tras una comparativa técnica frente a Azure y Google Cloud. Las razones clave de esta elección incluyen:

* **Madurez y Liderazgo:** AWS es el líder del mercado con la infraestructura global más robusta y una mayor variedad de servicios certificados.
* **AWS Free Tier (Capa Gratuita):** Permite el despliegue de una arquitectura de pruebas funcional durante 12 meses sin incurrir en costes elevados, ideal para la fase de desarrollo de Eficafix.
* **Elasticidad:** Capacidad de escalar recursos de cómputo de forma automática según la demanda de los clientes de la consultoría.
* **Ecosistema de Herramientas:** Integración nativa con herramientas de despliegue y gestión (AWS CLI, SDKs) que facilitan la administración técnica.

## 2. Arquitectura Cloud Propuesta

La arquitectura se ha diseñado bajo un modelo de **VPC (Virtual Private Cloud)** para garantizar el aislamiento de los recursos. El flujo de operación se define de la siguiente manera:

1.  **Segmentación de Red:** La infraestructura se divide en subredes públicas (para el servidor web) y subredes privadas (para la base de datos), aumentando la seguridad perimetral.
2.  **Cómputo:** La aplicación y los servicios de la consultoría se ejecutan en instancias elásticas que permiten una disponibilidad del 99.9%.
3.  **Persistencia de Datos:** Se delega la gestión de la base de datos a un servicio gestionado para eliminar las tareas de mantenimiento de hardware y parches del SO.
4.  **Acceso de Usuario:** Los usuarios acceden a través de un nombre de dominio gestionado que resuelve las peticiones hacia la IP de la instancia de cómputo de forma transparente.

## 3. Servicios Cloud Utilizados

A continuación se detallan los servicios específicos de AWS que integran la solución:

| Servicio AWS | Categoría | Función en la Infraestructura |
| :--- | :--- | :--- |
| **Amazon VPC** | Redes | Creación del entorno de red virtual aislado y segmentado por subredes. |
| **Amazon EC2** | Cómputo | Servidores virtuales (instancias) que alojan la web corporativa y aplicaciones. |
| **Amazon RDS** | Bases de Datos | Servicio gestionado para bases de datos relacionales con backups automáticos. |
| **Amazon S3** | Almacenamiento | Almacenamiento de objetos para archivos estáticos y copias de seguridad externas. |
| **Amazon Route 53** | DNS | Sistema de nombres de dominio para dirigir el tráfico de los usuarios. |
| **Internet Gateway** | Conectividad | Permite la comunicación entre la VPC e Internet. |

## 4. Estimación de Costes

La estrategia de costes de Eficafix se centra en el aprovechamiento de la **Capa Gratuita de AWS** para minimizar la inversión inicial durante los primeros 12 meses.

| Recurso / Servicio | Configuración Estimada | Coste Mensual (Free Tier) | Coste Mensual (Estimado Producción) |
| :--- | :--- | :--- | :--- |
| **Instancia EC2** | t2.micro / t3.micro | 0.00 € (750h gratis) | ~10.00 € - 15.00 € |
| **Amazon RDS** | db.t3.micro (Single-AZ) | 0.00 € (750h gratis) | ~15.00 € - 20.00 € |
| **Amazon S3** | 5 GB Standard Storage | 0.00 € (5GB gratis) | ~1.00 € |
| **Tráfico de Red** | Data Transfer Out | 0.00 € (Hasta 100GB) | Según demanda |
| **TOTAL ESTIMADO** | **Fase de Desarrollo** | **~0.00 € - 1.00 €** | **~30.00 € - 45.00 €** |

*Nota: Los costes de producción son estimaciones basadas en la calculadora de AWS y dependen del uso real de recursos y tráfico.*

## 5. Diagrama de Arquitectura (Lógico)

Para la representación visual del sistema, se sigue el flujo de datos descrito a continuación:

**[Flujo de Acceso y Datos]**
`Usuario Final` --> `Internet` --> `Internet Gateway` --> `VPC de Eficafix` --> `Subred Pública (Amazon EC2 / Servidor Web)` --> `Subred Privada (Amazon RDS / Base de Datos)` <--> `Almacenamiento (Amazon S3 / Backups)`

---
*Documentación técnica generada para el Proyecto Prometeo - Módulo Fundamentos de Computación en la Nube (1º ASIR).*