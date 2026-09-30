# Demo · Informe Power BI

Informe **Instalaciones Eólicas Galicia**, construido sobre las tablas de [`Data/Gold`](../Data/Gold).

## Archivos

| Archivo | Origen de datos | Cuándo usarlo |
|---|---|---|
| `Instalaciones_Eolicas_Galicia_Excel.pbix` | Ficheros Excel en local | Para abrir la demo desde este repositorio. Al abrirlo hay que apuntar el origen a la carpeta `Data/Gold` (ver abajo). |
| `Instalaciones_Eolicas_Galicia_SharePoint.pbix` | Ficheros Excel en SharePoint | Versión usada en la charla, con actualización programada en el servicio. Requiere acceso al SharePoint original. |

Los dos informes son idénticos salvo por el origen de datos.

## Páginas

1. **Inicio**: portada y navegación.
2. **Instalaciones**: nº de instalaciones, propietarios y fabricantes, potencia instalada, media de aerogeneradores; desglose por provincia, propietario, fabricante y modelo.
3. **Generación y Ventas**: energía generada y vendida, precio de mercado e ingresos estimados, con filtros por año, mes, provincia, propietario e instalación.

## Modelo semántico

| Tabla | Tipo | Procede de |
|---|---|---|
| `D_Instalaciones` | Dimensión | `Gold/Dim/MaestroInstalacionesGalicia.xlsx` |
| `D_Propietarios_Instalaciones` | Dimensión | Derivada de `D_Instalaciones` en Power Query (propietarios únicos) |
| `D_Clasificacion_Instalaciones` | Dimensión | `Gold/Dim/Clasificación Instalaciones.xlsx` |
| `D_Geografia` | Dimensión | `Gold/Dim/D_Geografia.xlsx` |
| `D_Contratistas` | Dimensión | `Gold/Dim/EmpresasContratistas.xlsx` |
| `D_Calendario` | Dimensión | Generada en el modelo |
| `F_Generacion_Eolicas` | Hechos | `Gold/Fact/Generacion_parques_eolicos_Galicia.xlsx` |
| `F_Ventas_Eolicas` | Hechos | `Gold/Fact/Ventas_parques_eolicos_Galicia.xlsx` |
| `DAX Measures` | Medidas | — |
| `aux_refresco_datos` | Auxiliar | Fecha de la última actualización |

**Medidas principales:** Nº Instalaciones, Nº Propietarios, Nº Fabricantes, Potencia Instalada (MW), Avg Generadores, Energía Generada Instalaciones, Energía Vendida Instalaciones, Precio Mercado Venta, Ingresos Instalaciones, Date Last Refreshed.

## Cómo abrir la demo

1. Clona el repositorio.
2. Abre `Instalaciones_Eolicas_Galicia_Excel.pbix` con **Power BI Desktop**.
3. Ve a **Transformar datos → Configuración de origen de datos**, selecciona cada origen y pulsa **Cambiar origen** para apuntarlo al fichero correspondiente de tu copia de `Data/Gold`.
4. Pulsa **Actualizar**.

> 💡 Si el modelo usa un parámetro de ruta, basta con cambiarlo en **Transformar datos → Administrar parámetros**.

## Pendiente

Guardar el informe como **Proyecto de Power BI (.pbip)** con formato TMDL (**Archivo → Guardar como → .pbip**). Así el modelo, las relaciones y las medidas DAX quedan como texto legible y versionable en GitHub, en lugar de dentro de un binario.
