# Inventario de fuentes de datos

Estado: en elaboración.

Este documento reúne las fuentes revisadas para evaluar
su posible uso en AgroET. Las fichas pueden estar incompletas
y no implican la selección definitiva de un dataset.

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
- **Limitación:** son datos meteorológicos de una malla;
  consultar unas coordenadas no equivale a obtener una serie
  observada por una estación situada exactamente allí.
- **Fuente oficial:** NASA POWER — Data Sources.
  https://power.larc.nasa.gov/docs/methodology/data/sources/
- **Fecha de revisión:** 2026-10-28.
- **Pendiente:** revisar variables, unidades, cobertura temporal
  y condiciones de acceso y uso.