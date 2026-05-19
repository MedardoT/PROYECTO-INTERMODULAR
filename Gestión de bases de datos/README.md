# Proyecto Intermodular – Prometeo  
## Base de Datos para EficaFix S.L.

### Autores
- Ismael Medardo Torres Becerra
- Noa Maximilian Tóth-Égetö

---

# Descripción del proyecto

Este proyecto consiste en el diseño, implementación y administración de una base de datos para la empresa ficticia **EficaFix S.L.**, dedicada al soporte técnico y servicios informáticos.

El objetivo principal es centralizar la información de:
- Clientes
- Técnicos
- Servicios
- Tickets de soporte
- Facturación
- Solicitudes web

La base de datos ha sido desarrollada utilizando **PostgreSQL**, aplicando principios de normalización, integridad referencial y seguridad.

---

# Objetivos del proyecto

- Diseñar un modelo de datos funcional y escalable
- Aplicar normalización hasta 3FN
- Implementar relaciones complejas N:M
- Gestionar tickets e incidencias
- Administrar clientes y servicios
- Automatizar la facturación
- Aplicar buenas prácticas de administración y seguridad

---

# Tecnologías utilizadas

| Tecnología | Función |
|---|---|
| PostgreSQL | Sistema gestor de base de datos |
| SQL (DDL/DML) | Creación y manipulación de datos |
| pg_dump | Backups |
| CSV Export | Exportación de datos |
| Modelo E/R | Diseño conceptual |

---

# Estructura del sistema

La base de datos gestiona las siguientes áreas principales:

- Empresas clientes
- Catálogo de servicios
- Técnicos y especialidades
- Solicitudes de contacto
- Tickets de soporte
- Facturación
- Etiquetado de incidencias

---

# Modelo Entidad-Relación

## Entidades principales

| Entidad | Descripción |
|---|---|
| EMPRESA | Clientes de EficaFix |
| TECNICO | Personal técnico |
| ESPECIALIDAD | Áreas técnicas de cada técnico |
| TICKET | Incidencias y soporte |
| TAG | Etiquetas de clasificación |
| FACTURA | Facturación |
| CATALOGO_SERVICIO | Servicios ofrecidos |
| SOLICITUD_CONTACTO | Leads del formulario web |

---

# Relaciones principales

| Relación | Cardinalidad |
|---|---|
| EMPRESA → TICKET | 1:N |
| TECNICO → TICKET | 1:N |
| TECNICO → ESPECIALIDAD | 1:N |
| EMPRESA → FACTURA | 1:N |
| FACTURA ↔ SERVICIO | N:M |
| TICKET ↔ TAG | N:M |

---

# Motor de base de datos

## PostgreSQL

Se ha elegido PostgreSQL por:
- Robustez
- Compatibilidad SQL avanzada
- Integridad referencial
- Seguridad
- Escalabilidad
- Soporte para restricciones CHECK
- Gestión avanzada de usuarios y permisos

---

# Diseño lógico

## Tablas principales

### EMPRESA
Almacena información de clientes:
- Nombre comercial
- CIF/NIF
- Correo
- Teléfono
- Dirección

### TECNICO
Gestiona el personal técnico:
- Nombre
- Correo interno
- Estado activo

### TICKET
Gestiona incidencias:
- Asunto
- Prioridad
- Estado
- Técnico asignado
- Empresa asociada

### FACTURA
Control económico:
- Número de factura
- Base imponible
- IVA
- Estado de cobro

---

# Relaciones N:M

## TICKET_TAG
Relaciona tickets con etiquetas:
- Urgente
- Redes
- Hardware
- Software

## FACTURA_SERVICIO
Relaciona:
- Facturas
- Servicios facturados
- Precio unitario
- Cantidad de meses

---

# Normalización

La base de datos cumple:

- Primera Forma Normal (1FN)
- Segunda Forma Normal (2FN)
- Tercera Forma Normal (3FN)

## Objetivos alcanzados
- Eliminación de redundancia
- Integridad de datos
- Escalabilidad
- Coherencia relacional

---

# Creación de la base de datos

## Características implementadas

- Claves primarias SERIAL
- Claves foráneas
- Restricciones CHECK
- ON DELETE RESTRICT
- ON UPDATE CASCADE
- Borrado lógico mediante campo `activo`

---

# Ejemplo de creación de tablas

sql
CREATE TABLE EMPRESA (
    id_empresa SERIAL PRIMARY KEY,
    nombre_comercial VARCHAR(100) NOT NULL,
    cif_nif VARCHAR(15) NOT NULL UNIQUE,
    correo VARCHAR(100),
    telefono VARCHAR(20),
    direccion TEXT,
    fecha_alta DATE DEFAULT CURRENT_DATE,
    activo BOOLEAN DEFAULT TRUE
);


---

# Inserción de datos

Se han creado datos de prueba para:
- Empresas
- Técnicos
- Especialidades
- Servicios
- Tickets
- Facturas
- Etiquetas

---

# Ejemplo de inserción

sql
INSERT INTO TECNICO (nombre, correo_interno) VALUES
('Ismael', 'ismael@eficafix.es'),
('Noa', 'noa@eficafix.es');


---

# Consultas implementadas

## Gestión de tickets prioritarios
Filtrado de incidencias:
- Alta prioridad
- Críticas
- Abiertas

## JOINs complejos
Consultas combinando:
- Tickets
- Empresas
- Técnicos

## Facturación
Listado de:
- Facturas pendientes
- Facturas vencidas
- Clientes asociados

## Buscador de incidencias
Uso de:
- ILIKE
- Búsqueda parcial
- Filtros por texto

---

# Administración de la base de datos

## Copias de seguridad

Se utiliza:

bash
pg_dump -U postgres -d eficafix_db -f /backups/eficafix_backup.sql


---

# Exportación de datos

Exportación CSV:

sql
COPY FACTURA TO '/tmp/listado_facturas.csv'
DELIMITER ','
CSV HEADER;


---

# Seguridad y permisos

## Principio de menor privilegio

Se han creado usuarios específicos para:
- Aplicación web
- Contabilidad
- Administración

## Ejemplo

sql
CREATE USER app_eficafix WITH PASSWORD 'AppS3cur3P@ss';

GRANT SELECT, INSERT, UPDATE
ON ALL TABLES IN SCHEMA public
TO app_eficafix;


---

# Funcionalidades del sistema

- Gestión de clientes
- Gestión de incidencias
- Clasificación mediante tags
- Facturación
- Gestión de técnicos
- Control de servicios
- Captación de leads
- Seguridad y backups

---

# Estructura del repositorio

text
/
├── README.md
├── docs/
│   ├── memoria.pdf
│   ├── modelo_er.png
│   └── capturas/
├── sql/
│   ├── ddl.sql
│   ├── dml.sql
│   └── consultas.sql
└── backups/


---

# Requisitos

## Software necesario
- PostgreSQL 14+
- pgAdmin (opcional)
- Cliente SQL compatible

---

# Ejecución del proyecto

## 1. Crear la base de datos

sql
CREATE DATABASE eficafix_db;


## 2. Ejecutar script DDL

bash
psql -U postgres -d eficafix_db -f ddl.sql


## 3. Ejecutar script DML

bash
psql -U postgres -d eficafix_db -f dml.sql


---

# Conclusión

Este proyecto ha permitido desarrollar una solución de base de datos completa para una empresa de soporte técnico realista.

La implementación en PostgreSQL demuestra:
- Diseño relacional correcto
- Aplicación de integridad referencial
- Gestión eficiente de incidencias
- Seguridad mediante roles y permisos
- Automatización de administración y backups

La base de datos se encuentra preparada para crecer y adaptarse a futuras necesidades empresariales.