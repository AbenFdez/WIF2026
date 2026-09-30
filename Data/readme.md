# Data

Los datos siguen una **arquitectura medallion**:

| Capa | Contenido |
|---|---|
| [`Raw`](Raw/) | Datos de origen sin transformar: públicos (INE, INEGA, MITECO) y sintéticos (Dummy). |
| [`Silver`](Silver/) | Datos limpios, tipados y normalizados. |
| [`Gold`](Gold/) | Tablas dimensión (`Dim`) y de hechos (`Fact`) que forman el modelo semántico. |
