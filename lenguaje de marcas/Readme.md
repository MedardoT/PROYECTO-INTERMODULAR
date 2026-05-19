# Sistema de Gestión de Activos e Inventario - Eficafix

Este proyecto constituye el núcleo de información de Eficafix S.L., integrando en una estructura XML tanto la oferta comercial y el capital humano como el inventario técnico de hardware detallado en el proyecto intermodular de Prometeo.

## 📋 Descripción de los Datos

El sistema organiza la información en dos grandes bloques lógicos validados por sus respectivos esquemas XSD:

### 1. Gestión Corporativa (`info.xml`)
Almacena la estructura operativa y organizativa de la empresa:
* **Empresa**: Nivel principal que identifica a la entidad legal.
* **Servicios**: Catálogo de soluciones técnicas (Mantenimiento, Soporte, Outsourcing). Cada servicio posee un **ID único** obligatorio, un título y una descripción detallada.
* **Empleados**: Listado del personal activo, vinculando nombres con sus funciones específicas dentro de la organización (ej. Técnico de Sistemas, Auditoría de Redes).

### 2. Inventario de Hardware (`hardware.xml`)
Detalla la base física sobre la que se asientan los servicios de la consultoría:
* **Equipos**: Clasificados por categorías funcionales (Usuario Técnico, Servidor, Red Crítica).
* **Especificaciones Técnicas**: Desglose pormenorizado de componentes internos:
    * **CPU y RAM**: Modelos y capacidades específicas (ej. i7-13700, Xeon E-2336, DDR5/ECC).
    * **Almacenamiento**: Gestión de múltiples unidades (SSD, HDD, Flash) utilizando atributos para definir la tecnología de disco.
    * **Otros**: Componentes adicionales críticos como GPUs NVIDIA RTX o fuentes de alimentación redundantes.
* **Estado**: Control del ciclo de vida del activo (Compra propuesta, Operativo, En Rack).

## 🛠 Estructura Técnica

El proyecto utiliza **XSD (XML Schema Definition)** para garantizar una validación robusta y superior al DTD tradicional:

* **Control de Tipos**: Asegura que las especificaciones técnicas y nombres sean cadenas de texto válidas (`xs:string`).
* **Cardinalidad**: Uso de `maxOccurs="unbounded"` para permitir el crecimiento ilimitado de la lista de empresas, servicios o equipos según las necesidades de Eficafix.
* **Integridad**: Uso de `xs:ID` para garantizar que no existan identificadores duplicados, facilitando el rastreo de activos.

## ✅ Cómo Validar los Documentos

Para asegurar que los archivos XML cumplen con la normativa técnica de Eficafix, utiliza uno de los siguientes métodos:

### Método A: Visual Studio Code (Recomendado)
1. Instala la extensión **"XML"** de Red Hat.
2. El editor detectará automáticamente los archivos `.xsd` referenciados en las cabeceras (`info.xsd` o `hardware.xsd`) y marcará cualquier error de estructura en tiempo real.

### Método B: Validación Online
1. Sube tu archivo XML a un validador como [CodeBeautify XML Validator](https://codebeautify.org/xmlvalidator).
2. Proporciona el archivo XSD correspondiente cuando el sitio lo solicite.

### Método C: Línea de Comandos (xmllint)
Si utilizas Linux o macOS, puedes ejecutar los siguientes comandos:

```bash
# Validar estructura corporativa
xmllint --noout --schema info.xsd info.xml

# Validar inventario de hardware
xmllint --noout --schema hardware.xsd hardware.xml