# Ontología · Eólicas en Galicia

Capa ontológica creada en **Microsoft Fabric (Fabric IQ)** sobre las tablas de [`Data/Gold`](../Data/Gold), cargadas en el Lakehouse `dlh_eolicas_galicia`.

- **Ontología:** `Ontology_Eolicas_Galicia`
- **Modelo semántico de origen:** *Modelo Eolicas Galicia* (ver [`/Demo`](../Demo))

## Entidades

| Entidad | Clave | Tabla del Lakehouse (esquema `gold`) | Tabla en este repo |
|---|---|---|---|
| **Instalaciones** | `Id_Instalacion` | `D_Instalaciones` | `Data/Gold/Dim/MaestroInstalacionesGalicia.xlsx` |
| **Propietarios** | `Id_Propietario` | `D_Propietarios_Instalaciones` | Propietarios únicos del Maestro |
| **Provincias** | `cod-prv` | `D_Provincias` | `Data/Gold/Dim/D_Geografia.xlsx` |
| **Generacion** | `Id_Generacion` (instalación · año · mes) | `F_Generacion_Eolicas` | `Data/Gold/Fact/Generacion_parques_eolicos_Galicia.xlsx` |
| **Ventas** | `Id_Venta` (instalación · año · mes) | `F_Ventas_Eolicas` | `Data/Gold/Fact/Ventas_parques_eolicos_Galicia.xlsx` |
| **Contratistas** | `Id` | `D_Contratistas` | `Data/Gold/Dim/EmpresasContratistas.xlsx` |

Cada entidad tiene descripción, sinónimos (p. ej. *Propietarios*: Empresa, Titular, Responsable…) y un enlace al informe **Modelo Eolicas Galicia**, para que usuarios y agentes de IA entiendan el significado de los datos.

## Relaciones

```mermaid
graph LR
    I["Instalaciones"] -- "Instalacion_Makes_Generacion" --> G["Generacion"]
    I -- "Instalacion_Makes_Ventas" --> V["Ventas"]
    I -- "D_Instalaciones_has_D_Propietarios" --> P["Propietarios"]
    I -- "D_Instalaciones_has_D_Provincia" --> PR["Provincias"]
    C["Contratistas"]
```

`Contratistas` está definida como entidad pero, por ahora, **no tiene relaciones** con el resto.

## Guía: crear y mantener una ontología en Fabric

Paso a paso con capturas, también disponible en Word: [`Ontologias_en_Fabric.docx`](Ontologias_en_Fabric.docx).

### Creación de ontologías en Fabric

¿Cómo dar de alta ontologías en Fabric? Hay dos formas:

- Desde un nuevo elemento / Item de Fabric, llamado “Ontology”

- Desde un modelo semántico ya existente.

**Opción 1: Alta de un nuevo elemento de Fabric tipo “Ontology”**:

<img src="img/image1.png" width="700">

<img src="img/image2.png" width="700">

Resultado final:

<img src="img/image3.png" width="700">

**Opción 2: Generación de una ontología desde un modelo semántico ya existente**:

<img src="img/image4.png" width="700">

<img src="img/image5.png" width="700">

Resultado final:

<img src="img/image6.png" width="700">

### Mantenimiento de ontologías en Fabric

#### Configuración de una Entidad

### Cambio de nombre y propiedades de una entidad

Para cambiar el nombre de una Entidad en Fabric, es necesario seleccionar la entidad a modificar y pinchar “Ver detalles del tipo de entidad”:

<img src="img/image7.png" width="700">

A continuación, seleccionamos los 3 puntos de la derecha y pinchamos en “Cambiar nombre”:

<img src="img/image8.png" width="700">

Resultado final:

<img src="img/image9.png" width="700">

Nota: Esto es interesante cuando creamos ontologías y relaciones partiendo de un modelo semántico ya existente, donde suele incluir el nombre de las tablas a las entidades que genera desde cero.

### Incluir enlaces a origen de datos que forman las Entidades

Para asociar un campo de una entidad a u su origen de datos, preferiblemente campos de tablas de un Data Lakehouse, es necesario realizar los siguientes pasos.

Primero, seleccionamos la opción “Agregar enlace y propiedades” dentro del desplegable de “Administrar enlaces de propiedad”:

<img src="img/image10.png" width="700">

A continuación, seleccionamos el tipo de enlace: o bien una tabla de Lakehouse, o tabla de centro de eventos o vista materializada:

<img src="img/image11.png" width="700">

Seleccionamos el origen del Lakehouse (en OneLake):

<img src="img/image12.png" width="700">

Navegamos hasta encontrar la tabla que queremos usar como enlace a los campos de las entidades:

<img src="img/image13.png" width="700">

Resultado final:

<img src="img/image14.png" width="700">

Otro ejemplo de enlace de datos para la entidad *Provincias*:

<img src="img/image15.png" width="700">

Seleccionamos también la opción “Tabla de Lakehouse” como tipo de enlace de datos:

<img src="img/image16.png" width="700">

<img src="img/image17.png" width="700">

En la siguiente imagen se visualiza el mapeo entre los campos de la tabla de origen de Lakehouse con las propiedades de la entidad *Provincias*:

<img src="img/image18.png" width="700">

Una vez que se han incluido los enlaces del origen de los datos en las propiedades de la Entidad, se puede incluir una descripción a cada propiedad para enriquecer el contexto y entendimiento de cada propiedad:

<img src="img/image19.png" width="700">

### Enriquecimiento de metadatos de Entidades

Dentro de la configuración de una Entidad, se puede incluir información sobre los metadatos de la entidad, para aportar contexto y significado a los datos, mediante descripciones, sinónimos y otra información relevante. Esto facilita su interpretación, descubrimiento y uso por parte de usuarios y agentes de IA.

<img src="img/image20.png" width="700">

Además, se pueden enlazar informes de Power BI o otros recursos relacionados con el contexto de la Ontología para enriquecer la información disponible y facilitar el acceso a contenido relevante desde un mismo punto, tal como se observa en la siguiente imagen:

<img src="img/image21.png" width="700">

Ejemplo para la entidad *Provincia*:

<img src="img/image22.png" width="700">

Ejemplo para la entidad *Propietarios*:

<img src="img/image23.png" width="700">

Ejemplo para la entidad *Instalaciones*:

<img src="img/image24.png" width="700">

#### Exploración de las Instancias de una entidad

Dentro del panel de Instancias, podemos ver una primera vista de registros de los campos de la tabla del Lakehouse que alimentan a las entidades de la ontologia:

<img src="img/image25.png" width="700">

<img src="img/image26.png" width="700">

<img src="img/image27.png" width="700">

#### Relaciones entre entidades

Relaciones entre entidades:
<img src="img/image28.png" width="700">

<img src="img/image29.png" width="700">

<img src="img/image30.png" width="700">

### Consumo de ontologías en Fabric

Hay diferentes tipos:

<https://learn.microsoft.com/es-es/fabric/iq/ontology/tutorial-4-create-data-agent>

Se va a crear con un agente de datos en Fabric:

<img src="img/image31.png" width="700">

<img src="img/image32.png" width="700">

<img src="img/image33.png" width="700">

<img src="img/image34.png" width="700">

<img src="img/image35.png" width="700">

<img src="img/image36.png" width="700">

### Tablas finales

#### Tabla final de generación

Tabla final de generación:

<img src="img/image37.png" width="700">

Detalles de la entidad Generación:

<img src="img/image38.png" width="700">

<img src="img/image39.png" width="700">

<img src="img/image40.png" width="700">

#### Tabla final de ventas

<img src="img/image41.png" width="700">

<img src="img/image42.png" width="700">

<img src="img/image43.png" width="700">

<img src="img/image44.png" width="700">

### Otras imágenes

<img src="img/image45.png" width="700">

<img src="img/image46.png" width="700">

<img src="img/image47.png" width="700">
