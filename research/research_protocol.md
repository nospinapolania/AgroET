# Protocolo preliminar — borrador 0.1

Fecha: 2026-10-25. Documento de formulación; no es un protocolo experimental cerrado.

## Objetivo actual

Determinar qué pregunta sobre evapotranspiración en Perú puede responderse con datos verificables y una validación defendible. La idea de combinar física y aprendizaje automático es una candidata metodológica, no un resultado ni una hipótesis de superioridad ya aceptada.

Actualización acordada: priorizar inspección de datasets y sus contenidos, con ubicación abierta. La Molina, Majes y Huancayo se conservan como antecedentes, sin constituir una selección del investigador. Ver data_inventory.md y las muestras de acceso en data/.

## Hipótesis preliminar y pregunta problema

**Pregunta:** ¿Qué tanto se ve afectado el cálculo de la evapotranspiración a través del método Penman-Monteith al agregar nuevas variables meteorológicas?

**Hipótesis:** La incorporación de variables seleccionadas por su fundamento físico y respaldo bibliográfico reducirá el error de estimación al momento de calcular la evapotranspiración de referencia en comparación con la formulación original de FAO-56 Penman–Monteith.

El "grado de pertinencia" de cada una de las variables se va a evaluar teniendo en cuenta el desempeño en los cálculos de la evapotranspiración en sí.

La selección de variables y la forma de incorporarlas se justificarán
mediante fundamentos físicos, bibliografía y disponibilidad de datos.



## Etapas y criterios de avance

| Etapa | Entregable verificable | Criterio para finalizar |
|---|---|---|
| A. Reconocimiento | starting_point.md y decision_log.md | Estado local y conocimientos reutilizables identificados; límites de la revisión explícitos. Cumplida en su alcance breve. |
| B. Preguntas científicas | Comparación razonada de preguntas sobre ET₀, ETc y ETa | Investigador y asesor distinguen variable, referencia y medición independiente; registran prioridades y restricciones. En curso. |
| C. Literatura | Estrategia reproducible y matriz de referencias | Registrar consultas, fechas, criterios de inclusión, metadatos verificados y diseño de validación de cada estudio incluido. Búsqueda exploratoria iniciada; ver search_log.md. |
| D. Zonas peruanas | Matriz de selección | Al menos tres candidatas si la evidencia lo permite, con criterios explícitos, limitaciones y recomendación condicionada a datos. Tres pistas iniciales identificadas; comparación completa pendiente. |
| E. Datos | Inventario de fuentes | Confirmar procedencia, variables, unidades, escala, periodo, acceso, licencia y función experimental de cada fuente priorizada. Inventario preliminar iniciado; series por verificar. |
| F. Diseño preliminar | Pregunta e hipótesis falsables y protocolo de comparación | Definir objetivo, referencias, particiones, métricas, incertidumbre, resultados refutadores y requisitos mínimos de datos. Pendiente. |
| G. Plan técnico | Etapas de implementación y primera tarea del investigador | Entregables y criterios para datos, análisis exploratorio, código, pruebas, evaluación, documentación y GitHub; Power BI después de resultados fiables. Pendiente. |

## Distinciones iniciales para la etapa B

La referencia conceptual inicial es FAO-56, capítulo 1. ET₀ representa la demanda de una superficie de referencia; ETc corresponde a un cultivo en condiciones estándar. En AgroET usaremos ETa para la ET efectivamente ocurrida, especificando superficie, disponibilidad de agua y manejo. Las comparaciones requieren escalas compatibles.

| Variable | Pregunta candidata, todavía sin selección | Información necesaria | Alcance posible de la evaluación |
|---|---|---|---|
| ET₀ | ¿Cómo cambia la reproducción de FAO-56 Penman–Monteith cuando faltan entradas meteorológicas y se evalúa en periodos o estaciones no usados en el ajuste? | Meteorología de calidad con entradas suficientes para calcular la referencia y diseñar escenarios de disponibilidad reducida; metadatos y cobertura. | Concordancia con la referencia calculada. Por sí sola no demuestra mayor exactitud frente a la ET medida. |
| ETc | ¿Qué validez local tienen coeficientes de cultivo candidatos durante etapas fenológicas definidas? | Meteorología, cultivo, fenología, manejo y datos independientes de ET del cultivo bajo condiciones acordes con los supuestos; incertidumbre de las mediciones. | Evaluación de la estimación del cultivo bajo esas condiciones. Multiplicar ET₀ por un coeficiente tabulado no constituye validación independiente. |
| ETa | ¿Un método físico o híbrido reduce el error frente a mediciones independientes bajo condiciones de agua y cobertura definidas? | Datos del método elegido y mediciones de campo compatibles en superficie y tiempo, con control de calidad y descripción de su incertidumbre. | Evaluación física dentro del dominio observado. Comparar solo productos modelados permite estudiar discrepancias, pero no establecer cuál representa mejor la realidad. |

Se propone explorar primero una resolución diaria en mm/día para ordenar las preguntas. No está adoptada: la disponibilidad y la representatividad de los datos pueden exigir otra resolución. Las preguntas de la tabla son propuestas; no se ha comprobado su novedad.

## Condiciones previas a los experimentos

- Precisar variable objetivo, superficie, unidades, periodo y resolución.
- Distinguir estimación retrospectiva de uso operativo y definir qué entradas estarían disponibles.
- Documentar las dependencias entre entradas, objetivo y productos de comparación.
- Exigir acceso verificable a datos y condiciones de uso compatibles con la investigación.
- Definir particiones y ajustar transformaciones aprendidas sin usar la prueba final.
- Establecer hipótesis, referencias, métricas y criterios de mejora antes de ver resultados finales.
- Si no se consigue validación independiente, reformular explícitamente el alcance y las afirmaciones.

Ninguna de estas condiciones se considera satisfecha por tener un dataset meteorológico o una API accesible.

## Comparación futura de zonas

Antes de asignar puntajes se definirán criterios y su importancia según la pregunta: observaciones de la variable objetivo, cobertura y calidad meteorológica, coincidencia espacial y temporal, acceso/licencia, contexto agrícola, antecedentes y esfuerzo viable para un investigador individual. El acceso a datos esenciales será una condición de viabilidad; una suma alta en otros criterios no compensará su falta. Se registrará «no verificado» cuando corresponda.

## Participación inicial del investigador

Ejercicio de razonamiento, sin programar: explicar la diferencia entre un día con 0 mm de lluvia y un día sin medición; proponer cómo conservar ambos estados; identificar por qué contar fechas después de completar un calendario no acredita cobertura observacional. Se revisará la respuesta y se usarán sus criterios en el futuro inventario de calidad.

Restricción confirmada por el investigador: se trabajará con datos públicos y no existe acceso de campo confirmado. La revisión buscará también mediciones de campo publicadas con datos accesibles. Un artículo que menciona mediciones no garantiza que su serie pueda obtenerse. Si no se consigue evidencia independiente suficiente, se reformulará el alcance sin asumir automáticamente ET₀ como objetivo.

## Fuente conceptual consultada

Allen, R. G.; Pereira, L. S.; Raes, D.; Smith, M. (1998). *Crop evapotranspiration — Guidelines for computing crop water requirements*. FAO Irrigation and Drainage Paper 56.

- [Portada y metadatos oficiales](https://www.fao.org/4/X0490E/X0490E00.htm).
- [Capítulo 1: conceptos y determinación de ET](https://www.fao.org/4/X0490E/x0490e04.htm).
- Consulta: 2026-10-25. Verificados título, autores, año y contenido conceptual del capítulo; no se declara revisado el manual completo.

Esta consulta inicial no equivale a una revisión de literatura ni respalda todavía una brecha de investigación en Perú.
