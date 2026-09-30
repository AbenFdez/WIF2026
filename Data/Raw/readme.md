# Raw · Datos de origen

## Public · Datos públicos

| Carpeta | Fuente | Contenido | Archivos |
|---|---|---|---|
| `Public/MITECO` | Ministerio para la Transición Ecológica y el Reto Demográfico · Registro administrativo de instalaciones de producción de energía eléctrica | Maestro de instalaciones de Galicia (extracción del 04/09/2026) y clasificación de categorías, grupos y subtipos normativos | `Galicia_InformeInstalaciones_04092026.xlsx`, `Clasificación Instalaciones.xlsx` |
| `Public/INEGA` | Instituto Enerxético de Galicia · Centrales eólicas operativas en Galicia (junio 2026) | Parques eólicos con propietario, potencia neta, municipio y fecha de puesta en marcha | `INEGA_Centrales_Eolicas_Galicia_202606.xlsx`, `centrales_eolicas-galicia-202606.pdf` (documento original) |
| `Public/INE` | Instituto Nacional de Estadística | Códigos y nombres de comunidades autónomas y provincias | `D_ccaa_ine_prev.xlsx`, `D_provincias_ine_prev.xlsx` |

Datos reutilizados citando la fuente, según las condiciones de reutilización de cada organismo. Todos los propietarios del fichero de INEGA son personas jurídicas.

## Dummy · Datos sintéticos para la demo

| Carpeta | Contenido | Archivos |
|---|---|---|
| `Dummy/Generacion_y_Ventas` | Dataset mensual por instalación y fase: energía generada y vendida (GWh), potencia instalada (MW), precio de mercado (€/MWh) e ingresos estimados (€). Años 2023, 2024 y 2025. | `Ingresos_parques_eolicos_Galicia_2023.xlsx`, `…_2024.xlsx`, `…_2025.xlsx` |
| `Dummy/Generadores_y_Tecnologos` | Maestro MITECO de Galicia enriquecido con número de aerogeneradores, fabricante, modelo, potencia unitaria, altura de buje y diámetro de rotor. | `MaestroInstalacionesGalicia_InfoAdicional.xlsx` |

> ⚠️ **Importante:**
> - **Generación y Ventas:** la clave, el nombre y la potencia de la instalación son reales (MITECO). El precio de mercado es el precio medio mensual del mercado diario de [OMIE](https://www.omie.es). La energía generada, la energía vendida y los ingresos son **sintéticos o estimados**. Cada fichero tiene una hoja `Supuestos_y_fuentes` con el detalle.
> - **Generadores y Tecnólogos:** 58 instalaciones tienen datos de fuentes públicas (DOG/Xunta, BOE, operadores, The Wind Power). Otras **146 se han completado con IA** y están marcadas como *"Información generada por IA"* en la columna `Fuente`. El detalle está en la hoja `Resumen_enriquecimiento`.

## Otros datasets

| Archivo | Contenido |
|---|---|
| `Ember Data.zip` | Datos mensuales de electricidad de [Ember](https://ember-energy.org) (generación europea, capacidad eólica y solar, interconexiones) con su metodología. |
| `Kaggle Datasets.zip` | Datasets de Kaggle sobre renovables y mercados eléctricos europeos. Los enlaces están en `Renovables - Kaggle Datasets Links.txt`. |

## Relación entre fuentes

- `Clave Registro` (MITECO) = `Clave_Registro` (Dummy, con sufijo de fase, p. ej. `RE-000845-1`)
- `Número de Registro Autonómico` (MITECO) ≈ `Registro_inega` (INEGA)
- `Provincia` (MITECO / INEGA) → `nombre_provincia` (INE)
- `Grupo Normativo` (MITECO) → `CódigoSubtipo` (Clasificación Instalaciones)
