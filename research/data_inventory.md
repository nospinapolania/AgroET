# Inventario de fuentes de datos

Estado: en elaboración.

Este documento reúne las fuentes revisadas para evaluar
su posible uso en AgroET. Las fichas pueden estar incompletas
y no implican la selección definitiva de un dataset.

## Fichas en revisión

### NASA POWER — Meteorología y radiación

- **Origen meteorológico:** MERRA-2 para el periodo histórico y GEOS-IT
  para extender la información reciente.
- **Origen de la radiación en la muestra de 2010:** CERES SYN1deg.
- **Tipo de información:** productos en malla; meteorología generada
  mediante sistemas que combinan observaciones y modelos físicos,
  y radiación derivada de observaciones satelitales y modelación.
- **Resolución espacial de meteorología MERRA-2:**
  0,5° de latitud × 0,625° de longitud.
- **Resolución espacial de radiación CERES SYN1deg:** 1° × 1°.
- **Resolución temporal de la consulta prevista:** diaria,
  mediante la API diaria.
- **Limitación:** son datos meteorológicos de una malla;
  consultar unas coordenadas no equivale a obtener una serie
  observada por una estación situada exactamente allí.
- **Fuente oficial:** NASA POWER — Data Sources.
  https://power.larc.nasa.gov/docs/methodology/data/sources/
- **Fecha de revisión:** 2026-10-28.
- **Pendiente:** revisar la cobertura histórica por variable y producto,
  y las condiciones de acceso y uso.

#### Variables inspeccionadas en la muestra diaria

| Código | Descripción | Unidad |
|---|---|---|
| T2M | Temperatura media del aire a 2 m | °C |
| T2M_MAX | Temperatura máxima del aire a 2 m | °C |
| T2M_MIN | Temperatura mínima del aire a 2 m | °C |
| RH2M | Humedad relativa del aire a 2 m | % |
| WS2M | Velocidad del viento a 2 m | m/s |
| ALLSKY_SFC_SW_DWN | Radiación incidente de onda corta, acumulada diaria | MJ/m²/día |
| PRECTOTCORR | Precipitación corregida del producto | mm/día |
| PS | Presión atmosférica superficial | kPa |

Fuente: metadatos de la respuesta guardada en `nasa_power.json`.

Estas variables corresponden a la consulta de prueba realizada;
no constituyen una selección definitiva para los modelos.

#### Características de la consulta de prueba

- **Periodo solicitado:** 2010-01-01 a 2010-01-07.
- **Referencia horaria:** UTC.
- **Versión de la API:** v2.10.1.
- **Fuentes declaradas por la respuesta:** MERRA2, SYN1DEG y POWER.
- **Código de dato faltante:** -999; no representa una medición
  ni debe sustituirse automáticamente por cero.
- **Alcance:** estas fechas describen la muestra descargada,
  no la cobertura histórica completa del servicio.

Fuente: cabecera de la respuesta guardada en `nasa_power.json`.
La correspondencia de CERES SYN1deg con la radiación se revisó
en la documentación oficial de fuentes; la cabecera por sí sola
no asigna cada variable a una fuente.
