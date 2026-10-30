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
- **Documentación de meteorología:**
  https://power.larc.nasa.gov/docs/methodology/data/sources_meteorology/
- **Documentación de radiación:**
  https://power.larc.nasa.gov/docs/methodology/data/sources_fluxes/
- **Fecha de revisión:** 2026-10-28.
- **Pendiente:** comprobar disponibilidad efectiva, continuidad
  y calidad para las variables, zona y periodo que se seleccionen.

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

#### Periodo candidato para la exploración

- **Inicio provisional:** 1985-01-01.
- **Fecha final:** 2025-12-31
- **Justificación:** Teniendo en cuenta que no todos los datos tenian cobertura de datos desde el mismo año, arbitrariamente se tomó la decisión de fijar el inicio provisional en el año 1985 para contar con al menos 40 años en información.
- **Condición de revisión:** comprobar disponibilidad, continuidad
  y coincidencia temporal con las demás fuentes seleccionadas.

#### Acceso y condiciones de uso

- **Acceso:** público y gratuito.
- **Licencia indicada en el catálogo:** Creative Commons BY 4.0.
- **Atribución:** citar NASA POWER, conservar la referencia
  a la fuente y enlazar la licencia.
- **Modificaciones:** indicar las transformaciones realizadas
  cuando se comparta material adaptado.
- **Fecha de revisión:** 2026-10-30.

#### Cobertura temporal documentada

- **Meteorología diaria:** disponible desde 1981-01-01.
- **Radiación solar diaria:** disponible desde 1984-01-01.
- **Cambios de fuente:** la radiación histórica utiliza SRB
  durante 1984–2000 y CERES SYN1deg desde 2001.
  El tramo más reciente se complementa con FLASHFlux.
- **Fecha final disponible:** debe comprobarse por variable
  al realizar la descarga.
- **Limitación:** la cobertura anunciada no demuestra por sí sola
  ausencia de faltantes ni homogeneidad de toda la serie.

Fuente: cabecera de la respuesta guardada en `nasa_power.json`.
La correspondencia de CERES SYN1deg con la radiación se revisó
en la documentación oficial de fuentes; la cabecera por sí sola
no asigna cada variable a una fuente.
