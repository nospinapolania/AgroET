# Inventario de datasets — evaluación inicial

Fecha: 2026-10-25. Prioridad acordada: examinar datasets antes de seleccionar zona y pregunta. Se obtuvieron muestras pequeñas de dos servicios y metadatos de un tercero. No se ha seleccionado zona.

## Datasets concretos

| Dataset / proveedor | Tipo y contenido | Cobertura y resolución documentadas | Acceso comprobado | Utilidad inicial y límites |
|---|---|---|---|---|
| [NASA POWER](https://power.larc.nasa.gov/docs/services/api/temporal/daily/) / NASA | Meteorología de reanálisis/modelos y radiación derivada de satélites. | Global; meteorología diaria desde 1981. MERRA-2: 0,5° × 0,625°; radiación CERES: 1°. Periodos de radiación según producto. | API HTTP 200; siete días × ocho variables guardados. | Entradas para métodos de ET y comparación de fuentes; evaluar representatividad de mallas gruesas. La muestra no incluye ET medida. |
| [Open-Meteo Historical, ERA5 explícito](https://open-meteo.com/en/docs/historical-weather-api) / Open-Meteo, datos ECMWF | Reanálisis y variables derivadas, incluida ET₀ FAO-56. | Global; ERA5: 0,25°, horario, desde 1940. Otras opciones del servicio tienen otros periodos y resoluciones. | API HTTP 200; siete filas diarias y 168 horarias guardadas. | Inspección meteorológica y comparación con ET₀ calculada. Se fijó ERA5 para evitar selección automática de modelos. |
| [PISCOeo_pm v3](https://figshare.com/articles/dataset/Reference_crop_evapotranspiration_PISCOeo_pm_/15215106) / Huerta y colaboradores | ET₀ calculada con meteorología preparada e interpolada. | Perú continental; 1981–2016, diario, 0,01° (~1 km). | API Figshare HTTP 200: licencia y catálogo de 37 archivos comprobados; datos ZIP/NetCDF no descargados. | Comparación de ET₀ espacial y temporal, con revisión de dependencias. Elegir extracción limitada antes de descargar archivos grandes. |
| [Estaciones SENAMHI](https://www.senamhi.gob.pe/index.php?p=descarga-datos-hidrometeorologicos) / SENAMHI | Observaciones por estación; variables y procesamiento por verificar. | Perú; periodo, frecuencia y variables dependen de estación. | Portal localizado; mapa respondió HTTP 403. No se obtuvo serie de estación. | Meteorología local. Faltan disponibilidad por variable, cobertura, calidad y condiciones de uso. |
| [MOD16A2GF.061](https://developers.google.com/earth-engine/datasets/catalog/MODIS_061_MOD16A2GF) / NASA LP DAAC | ET y ET potencial modeladas con teledetección y meteorología; incluye ET_QC. | Global; 500 m, compuestos de ocho días desde 2000. Último compuesto anual: cinco o seis días. | Catálogo/documentación comprobados; no se descargó raster. | Candidato para ET de superficie; requiere escalado y control de calidad. No es ET₀ ni medición de campo. |

Fuentes de resolución y procedencia: [NASA POWER](https://power.larc.nasa.gov/docs/methodology/data/sources/), [Open-Meteo](https://open-meteo.com/en/docs/historical-weather-api), [artículo PISCOeo_pm](https://www.nature.com/articles/s41597-022-01373-8). El acceso puntual no acredita idoneidad científica del dataset completo.

## Variables, unidades y condiciones comprobadas

- **NASA POWER:** `T2M`, `T2M_MAX`, `T2M_MIN` (°C); `RH2M` (%); `WS2M` (m/s a 2 m); `ALLSKY_SFC_SW_DWN` (MJ/m²/día); `PRECTOTCORR` (mm/día); `PS` (kPa). Respuesta declara MERRA2/SYN1DEG/POWER, faltante -999. [Servicio gratuito](https://power.larc.nasa.gov/), consulta sin cuenta ni clave. La respuesta no incorpora licencia explícita; conservar atribución y revisar requisitos de publicación. Automatización puntual comprobada.
- **Open-Meteo/ERA5:** muestra diaria con Tmax/Tmin (°C), precipitación y ET₀ (mm acumulados por día), radiación (MJ/m² acumulados por día); muestra horaria con humedad relativa (%) y viento a 10 m (m/s). [Términos](https://open-meteo.com/en/terms): CC BY 4.0, API gratuita para uso no comercial y límites de llamadas. Sin clave en la prueba educativa. No mezclar alturas de viento o agregaciones temporales sin tratamiento explícito.
- **SENAMHI:** [catálogo nacional](https://www.datosabiertos.gob.pe/dataset/datos-hidrometeorol%C3%B3gicos-de-libre-acceso) declara acceso público y licencia no especificada. Verificar redistribución antes de publicar series. HTTP 403 en este entorno no demuestra ausencia de datos.
- **MOD16A2GF:** bandas ET/PET en kg/m² por compuesto, escala 0,1; conservar ET_QC y revisar valores especiales. El catálogo informa ausencia de restricciones de uso de productos MODIS adquiridos por LP DAAC. Descarga y automatización de recorte no probadas; Earth Engine requiere registro y no se creó cuenta.

## Familia PISCO: productos diferentes

El HTML del [portal oficial PISCO](https://www.senamhi.gob.pe/observatorio-dev/investigadores/descarga-pisco) respondió HTTP 200. Anuncia precipitación, temperaturas máxima/mínima y evapotranspiración potencial, 0,1°, 1981–2025; la pestaña de ET potencial indica v1.1. Falta verificar periodo efectivo por variable, método, licencia y exportación.

No equiparar automáticamente esa ET potencial con PISCOeo_pm a 0,01°. Registrar nombre, versión y método de cada producto.

## Muestras obtenidas

Ver [archivos y diccionario](../data/access_samples_2026-10-25/README.md).

- Punto técnico: latitud -10°, longitud -75°; 2010-01-01 a 2010-01-07, UTC. No constituye elección de zona.
- NASA: siete filas × ocho variables. Open-Meteo: siete filas × cinco variables diarias y 168 filas × dos horarias.
- Sin nulos o -999 en estas muestras; no prueba calidad ni continuidad multianual.
- Se conservaron JSON originales, CSV de lectura y manifiesto de URLs, parámetros, fecha y SHA-256.
- No se han combinado fuentes ni entrenado modelos. Sus mallas, elevaciones representadas y alturas de viento difieren.

## Pistas anteriores de medición, sin prioridad territorial

| Zona / organismo | Evidencia primaria | Variable y procedimiento informado | Cobertura temporal y espacial | Acceso, licencia y coste | Función potencial y condición pendiente |
|---|---|---|---|---|---|
| La Molina, Lima / UNALM | [Artículo de 2020 en Idesia](https://www.scielo.cl/scielo.php?script=sci_arttext&pid=S0718-34292020000200049), DOI 10.4067/S0718-34292020000200049 | ET del arroz, denominada ETc en el artículo, mediante lisímetro de drenaje; meteorología automática y ET₀ calculada. | Diciembre de 2017 a abril de 2018; área experimental. Resumen informa lecturas diarias; unidades y datos completos por comprobar en método y tablas. | Artículo accesible. Serie instrumental, formato, licencia de datos, coste y automatización: no verificados. | Posible evaluación en arroz; verificar supuestos, calidad, datos originales y correspondencia de superficie. Una campaña puede limitar generalización y entrenamiento. |
| Huancayo, valle del Mantaro / IGP | [Ficha institucional del estudio de 2021](https://repositorio.igp.gob.pe/items/ddac7c19-729e-4e36-98b8-bf3bbe00b835/full), DOI 10.1016/j.atmosres.2021.105760 | ET y flujos de energía por covarianza de remolinos. | Julio de 2016 a junio de 2017; observatorio a 3330 m. Resumen describe escalas horaria, diaria y mensual. Unidades, cobertura vegetal y huella por comprobar. | Metadatos y resumen accesibles; disponibilidad efectiva y licencia de series: no verificadas. | Posible referencia experimental; revisar correcciones, cierre energético y representatividad antes de comparar. No asumir condiciones de superficie de referencia. |
| Majes, Arequipa / AUTODEMA | [Comunicación institucional de 2022](https://www.autodema.gob.pe/autodema-realiza-investigacion-para-mejorar-el-riego-en-la-pampa-de-majes/) | Estudios de coeficientes de cultivo con lisímetros de drenaje; estaciones meteorológicas. | Centro de Reconversión Agroganadera. Fechas de campañas, frecuencia y duración por cultivo: no verificadas. La fecha de la noticia no define el periodo de las series. | No se verificaron archivos públicos, licencia, coste o API. | Pista para localizar publicaciones, anexos y series; la noticia no basta para calibrar o validar. |

Estos antecedentes surgieron de ejemplos sobre medición. El investigador no eligió estas zonas como prioritarias; se conservan como pistas sin restringir la búsqueda de datasets en Perú.

## Producto modelado candidato

**PISCOeo_pm — Huerta y colaboradores / SENAMHI y colaboradores.**

- Fuente: [artículo de Scientific Data de 2022](https://www.nature.com/articles/s41597-022-01373-8), DOI 10.1038/s41597-022-01373-8.
- ET₀ calculada mediante FAO Penman–Monteith; Perú continental, 1981–2016, resolución 0,01° (aproximadamente 1 km), paso diario. Se describen archivos NetCDF de ET₀ y subvariables meteorológicas.
- Método: preparación e interpolación de meteorología, con dependencias de otros productos. No es ETa observada.
- Acceso actualizado: página web dio HTTP 403, pero la API pública `https://api.figshare.com/v2/articles/15215106` respondió HTTP 200. DOI del dataset: `10.6084/m9.figshare.15215106.v3`; licencia CC BY 4.0 verificada. Solo se guardaron metadatos (~16 kB).
- El catálogo enumera 37 archivos y 52.562.414.618 bytes (~52,56 GB decimales). Ejemplos: `eo_mean_1981-2010.nc`, 67.092.969 bytes; `eo_daily_1981.zip`, 1.457.274.332 bytes. Son tamaños anunciados, no datos descargados.
- Papel posible: comparación de estimaciones o estudio de ET₀, con revisión de dependencias. No usarlo como verdad independiente para demostrar mejora física de ETa.
- Pendiente: completar ficha por variable, unidades, cobertura efectiva, datos faltantes, incertidumbre y validación del producto.

## Próxima decisión

Revisar estructura y procedencia de las muestras y completar el acceso a datos peruanos. Comparar cobertura, calidad, escala, acceso y posibles preguntas antes de elegir ubicación y objetivo. La búsqueda de mediciones sigue abierta. No sustituir una medición faltante por un producto modelado y mantener la misma afirmación de validación física.

## Importancia agrícola

Una diferencia de 0,1 mm equivale geométricamente a 1 m³/ha. Esto no es por sí solo ahorro de riego demostrado. La interpretación requiere signo y persistencia de errores, incertidumbre, cultivo, suelo, lluvia y manejo. El umbral de mejora relevante se definirá antes de la evaluación final.

## Fichas en revisión

### NASA POWER — Datos meteorológicos

- **Origen:** MERRA-2 para el periodo histórico y GEOS-IT
  para extender la información reciente.
- **Tipo de información:** datos meteorológicos en una malla,
  generados mediante sistemas que combinan observaciones
  y modelos físicos.
- **Resolución espacial:** 0,5° de latitud × 0,625° de longitud
  para MERRA-2.
- **Resolución temporal de la consulta prevista:** diaria,
  mediante la API diaria.
- **Limitación:** los valores no corresponden necesariamente
  a mediciones de una estación situada en las coordenadas
  consultadas, ya que son parte de una malla de datos metereológicos