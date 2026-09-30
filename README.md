# WIF2026 · Capa Ontológica en Fabric

Todos los datos, notebooks y la demo de la charla **"Capa Ontológica en Fabric"** (WIF 2026).

El caso de uso son los **parques eólicos de Galicia**: instalaciones, propietarios, tecnología de los aerogeneradores, generación, ventas e ingresos.

## Estructura del repositorio

```
WIF2026/
├── Data/
│   ├── Raw/        Datos de origen, tal como se obtienen (bronze)
│   │   ├── Dummy/      Datos sintéticos generados para la demo
│   │   └── Public/     Datos públicos: INE, INEGA, MITECO
│   ├── Silver/     Datos limpios y normalizados
│   └── Gold/       Tablas del modelo semántico
│       ├── Dim/        Dimensiones
│       └── Fact/       Hechos
├── Notebooks/      Transformaciones Raw → Silver → Gold
├── Ontologia/      Definición de la capa ontológica
├── Demo/           Modelo semántico e informe (Power BI Project, .pbip)
└── Slides/         Presentación de la charla
```

## Cómo reproducir la demo

1. Clona el repositorio o descárgalo como ZIP (**Code → Download ZIP**).
2. Los datos de partida están en `Data/Raw`. Los notebooks de `Notebooks/` generan las capas Silver y Gold.
3. Si solo quieres ver el modelo, usa directamente las tablas de `Data/Gold`.
4. Abre el proyecto de `Demo/` con Power BI Desktop.

## Fuentes de datos

El detalle de cada fuente, con su licencia, está en [`Data/Raw/readme.md`](Data/Raw/readme.md).

> ⚠️ Los datos de `Data/Raw/Dummy` son **sintéticos o estimados** y solo sirven para la demo. No reflejan la producción ni los ingresos reales de ninguna instalación.

## Autoras

- Alejandra Ben ([@AbenFdez](https://github.com/AbenFdez))
- Lorena Méndez ([@lmendezotero](https://github.com/lmendezotero))
