# Notebooks · ETL

Notebooks en Python (pandas) que transforman los datos de `Data/Raw` en las tablas de `Data/Silver` y `Data/Gold`.

## Orden de ejecución

Hay que ejecutarlos **en este orden**, porque cada uno usa la salida del anterior:

| # | Notebook | Entradas | Salidas |
|---|---|---|---|
| 1 | [`01_ETL_Geografia_INE.ipynb`](01_ETL_Geografia_INE.ipynb) | `Raw/Public/INE` | `Silver/D_provincias_ine.xlsx`, `Silver/D_ccaa_ine.xlsx`, **`Gold/Dim/D_Geografia.xlsx`** |
| 2 | [`02_ETL_Maestro_Instalaciones_Galicia.ipynb`](02_ETL_Maestro_Instalaciones_Galicia.ipynb) | `Raw/Public/MITECO`, `Raw/Public/INEGA`, `Raw/Dummy/Generadores_y_Tecnologos`, `Silver/D_provincias_ine.xlsx` | `Silver/MaestroInstalacionesGalicia_prev.xlsx`, **`Gold/Dim/MaestroInstalacionesGalicia.xlsx`** |
| 3 | [`03_ETL_Ingresos_Eolicas_Galicia.ipynb`](03_ETL_Ingresos_Eolicas_Galicia.ipynb) | `Raw/Dummy/Generacion_y_Ventas`, `Gold/Dim/MaestroInstalacionesGalicia.xlsx` | `Silver/Ingresos_parques_eolicos_Galicia.xlsx`, **`Gold/Fact/Generacion_…xlsx`**, **`Gold/Fact/Ventas_…xlsx`** |

`Clasificación Instalaciones.xlsx` y `EmpresasContratistas.xlsx` no pasan por ningún notebook: se usan tal cual en Gold.

## Qué hace cada uno

1. **Geografía INE**: quita las tildes de los nombres de provincia (`Nombre_provincia_st`), normaliza los nombres de columna y une provincias con comunidades autónomas.
2. **Maestro de instalaciones**:
   - Filtra las instalaciones **eólicas** del registro del MITECO (grupos `b.2.1` y `b.2.2`).
   - Corrige los nombres de provincia (`La Coruña` → `A Coruña`, `Orense` → `Ourense`) y los números de registro que no coinciden con los de INEGA.
   - Añade el propietario (INEGA) y el código de provincia (INE), y descarta las instalaciones sin propietario identificado.
   - Añade la tecnología de los aerogeneradores.
   - Crea la clave `Id_Instalacion` = `Clave_Registro` + fase.
3. **Ingresos eólicos**: une los tres años (2023–2025), añade `Codigo_Mes`, `Fecha` y la clave `Id_…` = `Id_Instalacion_Año_Mes`, incorpora propietario y provincia, y separa los datos en dos tablas de hechos: **Generación** y **Ventas**.

## Cómo ejecutarlos

Desde la carpeta `Notebooks/` (las rutas son relativas a ella):

```bash
pip install pandas openpyxl
jupyter nbconvert --to notebook --execute --inplace 01_ETL_Geografia_INE.ipynb
jupyter nbconvert --to notebook --execute --inplace 02_ETL_Maestro_Instalaciones_Galicia.ipynb
jupyter nbconvert --to notebook --execute --inplace 03_ETL_Ingresos_Eolicas_Galicia.ipynb
```

También se pueden abrir y ejecutar celda a celda en VS Code, Jupyter o un notebook de Microsoft Fabric. En Fabric, las rutas hay que cambiarlas por las del Lakehouse.
