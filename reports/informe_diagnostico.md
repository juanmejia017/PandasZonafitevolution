# Informe técnico: diagnóstico inicial de calidad de datos

**Evidencia:** GA1-220501094-01-AA1-EV06 – Diagnosticar la calidad de datos: preparación, exploración y documentación
**Aprendiz:** Juan Diego Mejía Llano
**Programa:** Análisis y Desarrollo de Software (ADSO) – SENA Regional Antioquia, ficha 3223873
**Fecha:** noviembre de 2026

Todas las cifras de este informe salen del notebook [`notebooks/diagnostico_calidad.ipynb`](../notebooks/diagnostico_calidad.ipynb).

---

## 1. Nombre del proyecto y pregunta analítica

**Proyecto:** Análisis de deserción de miembros en Zona Fit Evolution.

**Pregunta analítica:** ¿Qué factores (tipo de plan, frecuencia de asistencia, horario de entrenamiento y antigüedad) influyen en que un miembro de Zona Fit Evolution cancele o no renueve su membresía durante sus primeros seis meses?

El objetivo de este diagnóstico es determinar si los datos seleccionados están en condiciones de responder esa pregunta y qué hay que corregir antes de analizarlos.

## 2. Descripción de los datasets utilizados

Se usan ocho datasets de tres fuentes. Cada uno se cargó en un DataFrame independiente.

| DataFrame | Fuente | Contenido | Uso en el proyecto |
|---|---|---|---|
| `zf_planes` | Zona Fit (simulado) | Catálogo de 6 planes: tipo, duración, ingresos y precio | Factor *tipo de plan* |
| `zf_miembros` | Zona Fit (simulado) | 908 personas inscritas: género, nacimiento, comuna, canal, registro | Antigüedad y perfil del miembro |
| `zf_membresias` | Zona Fit (simulado) | 3.425 compras o renovaciones con fechas y estado | Variable de deserción |
| `zf_pagos` | Zona Fit (simulado) | 3.572 pagos con valor, método y estado | Morosidad y valor del cliente |
| `zf_accesos` | Lector de huella de Zona Fit (simulado) | 57.003 intentos de ingreso con fecha, hora y resultado | Frecuencia y horario de asistencia |
| `kg_churn` | Kaggle | 4.000 clientes de gimnasio con la variable `Churn` | Referencia externa de deserción |
| `kg_actividad` | Kaggle | 2.600 visitas con tipo de entrenamiento y asistencia | Referencia de patrones de asistencia |
| `gov_escenarios` | datos.gov.co (INDER Medellín) | 1.071 escenarios deportivos públicos con barrio y coordenadas | Contexto geográfico |

Zona Fit Evolution todavía no tiene datos reales de operación. Las cinco tablas `zf_` son una exportación simulada de su base de datos MySQL, descrita en [`data/raw/zonafit/DICCIONARIO.md`](../data/raw/zonafit/DICCIONARIO.md). La fecha de corte de esa exportación es el 15 de octubre de 2026.

## 3. Resultados de la inspección estructural

Para cada DataFrame se ejecutaron `head()`, `tail()`, `shape`, `columns`, `dtypes`, `info()`, `describe()` y `describe(include='object')`.

| Dataset | Filas | Columnas | Tipos de datos | Observaciones |
|---|---:|---:|---|---|
| zf_planes | 6 | 6 | int64 (3), str (2), float64 (1) | Catálogo pequeño. Vacíos esperados en `ingresos_incluidos` (planes ilimitados). |
| zf_miembros | 908 | 7 | str (6), int64 (1) | Fechas como texto; vacíos en género, nacimiento y comuna; categorías inconsistentes; documentos repetidos. |
| zf_membresias | 3.425 | 7 | int64 (3), str (3), float64 (1) | Fechas como texto; 51 precios vacíos; estados que no coinciden con las fechas. |
| zf_pagos | 3.572 | 6 | str (4), int64 (2) | Monto (`valor`) cargado como texto; IDs repetidos; método de pago vacío; fechas en dos formatos. |
| zf_accesos | 57.003 | 5 | str (3), int64 (2) | Tabla más grande; `fecha_hora` como texto; dispositivo vacío; accesos de miembros inexistentes. |
| kg_churn | 4.000 | 14 | int64 (10), float64 (4) | Todo numérico y completo; binarias 0/1 sin diccionario; sin fechas ni identificadores. |
| kg_actividad | 2.600 | 10 | str (6), int64 (4) | Completo; fechas como texto; una visita por miembro; categorías muy uniformes. |
| gov_escenarios | 1.071 | 5 | str (3), float64 (2) | Completo; coordenadas fuera de Medellín; direcciones con espacios; trae barrio, no comuna. |

> En pandas 3 las columnas de texto aparecen con el tipo `str`; en pandas 2 aparecían como `object`.

## 4. Valores faltantes, tipos de datos y posibles inconsistencias

### 4.1 Valores faltantes

| Dataset | Columna | Faltantes | % | Interpretación |
|---|---|---:|---:|---|
| zf_planes | ingresos_incluidos | 5 | 83,33 | Esperado: los planes ilimitados no tienen límite de ingresos |
| zf_miembros | fecha_nacimiento | 54 | 5,95 | No se puede calcular la edad de esos miembros |
| zf_miembros | comuna | 46 | 5,07 | No se puede ubicar al miembro en su entorno |
| zf_miembros | genero | 27 | 2,97 | Perfil incompleto |
| zf_membresias | precio_pagado | 51 | 1,49 | Afecta ingresos, no la deserción |
| zf_pagos | metodo_pago | 108 | 3,02 | Afecta el análisis por medio de pago |
| zf_accesos | dispositivo | 1.140 | 2,00 | Impacto bajo: la sede tiene un solo lector |

`kg_churn`, `kg_actividad` y `gov_escenarios` no tienen valores faltantes. Ningún porcentaje supera el 6 % en columnas relevantes, así que los vacíos no impiden continuar.

### 4.2 Tipos de datos

- **8 columnas de fecha u hora se cargaron como texto (`str`):** `fecha_nacimiento` y `fecha_registro` (miembros), `fecha_inicio` y `fecha_fin` (membresías), `fecha_pago`, `fecha_hora` (accesos), `visit_date` y `check_in_time` (Kaggle). Sin convertirlas no se puede calcular la antigüedad, los días entre visitas ni la franja horaria.
- **`zf_pagos.valor` quedó como texto** porque 179 pagos tienen formato de moneda (`$90.000`). Así no se puede sumar ni promediar.
- **142 fechas de pago** están en formato `DD/MM/AAAA` en lugar de `AAAA-MM-DD`.
- `zf_planes.ingresos_incluidos` y `kg_churn.Month_to_end_contract` son conteos enteros guardados como `float64`.
- En `kg_churn`, 7 columnas son categorías sí/no guardadas como 0/1 y el dataset no indica qué significa cada código (por ejemplo, en `gender`).

### 4.3 Posibles inconsistencias

- **Categorías escritas de varias formas:** `genero` tiene 6 valores en lugar de 2 (33 registros con `f`, `Masculino`, `masculino` o `Femenino`) y 18 miembros tienen la comuna `laureles` en lugar de `Laureles-Estadio`.
- **Fechas de nacimiento de relleno:** 9 miembros nacieron el `1900-01-01` (126 años). Además hay 84 miembros de 15 a 17 años, lo que el gimnasio debe confirmar que admite.
- **Miembros duplicados:** 8 personas están inscritas dos veces (16 registros con el mismo documento). Las copias son los IDs 901 a 908, que son los 8 miembros sin ninguna membresía.
- **Estados de membresía incorrectos:** 93 membresías siguen `Activa` aunque su fecha de fin ya pasó, y por eso 41 miembros tienen más de una membresía activa.
- **Pagos:** 12 filas duplicadas (mismo `id_pago`) y 14 pagos aprobados con valor 0.
- **Accesos:**
  - 25 accesos de 20 IDs que no existen en `zf_miembros`.
  - 184 accesos `Permitido` durante una membresía `Cancelada`.
  - 17 accesos fuera del horario de la sede.
  - **675 lecturas dobles de huella**, a menos de 60 segundos del acceso anterior del mismo miembro.
- **Tiquetera:** 22 tiqueteras superan los 12 ingresos, pero sin las lecturas dobles solo queda 1 (13 ingresos). El exceso lo causa el lector, no los miembros.
- **`kg_actividad`:** las 1.350 visitas `Absent` tienen duración y calorías mayores que cero, así que `attendance_status` no es confiable.
- **`gov_escenarios`:** 22 escenarios tienen coordenadas fuera de Medellín (valores como `1.234568` o `55.555555`) y 966 direcciones tienen espacios múltiples.

## 5. Principales hallazgos de calidad por dataset

| Dataset | Problema identificado | Evidencia encontrada | Posible impacto | Acción propuesta |
|---|---|---|---|---|
| zf_miembros | Valores faltantes | `isna()`: genero 27, fecha_nacimiento 54, comuna 46 | Perfiles incompletos; sin edad | Marcar como "Sin dato"; no imputar edad; pedir el dato al renovar |
| zf_miembros | Categorías inconsistentes | genero con 6 valores; comuna `laureles` 18 veces | Grupos divididos al agrupar | Unificar con un diccionario de reemplazo (`map`/`replace`) |
| zf_miembros | Fecha de nacimiento de relleno | `1900-01-01` en 9 registros (126 años) | Edades imposibles | Convertir a `NaN`; validar el rango de edad en el formulario |
| zf_miembros | Miembros inscritos dos veces | 16 registros con documento repetido; 8 sin membresía | Infla el total de miembros | Eliminar duplicados por `documento_hash`; `UNIQUE` en MySQL |
| zf_membresias | Estado `Activa` con fecha vencida | 93 membresías; 41 miembros con más de una activa | Subestima la deserción | Recalcular el estado con `fecha_fin`; tarea automática en el backend |
| zf_membresias | Precio pagado faltante | `isna()`: 51 | Ingresos subestimados | Completar con los pagos aprobados o el precio de lista |
| zf_pagos | Monto como texto | dtype `str`; 179 valores tipo `$90.000` | No se puede sumar ni promediar | Quitar `$` y `.`; `pd.to_numeric` |
| zf_pagos | Fechas en dos formatos | 142 fechas `DD/MM/AAAA` | Conversión fallida o día y mes invertidos | `pd.to_datetime` con el formato de cada caso |
| zf_pagos | Pagos duplicados | 12 filas idénticas | Ingresos inflados | `drop_duplicates()`; `id_pago` como llave primaria |
| zf_pagos | Pagos en cero y método vacío | 14 pagos en 0; 108 sin método | Membresías aparentemente gratis | Revisar con caja; método "Sin dato" |
| zf_accesos | Fecha como texto y dispositivo vacío | `fecha_hora` tipo `str`; 1.140 sin dispositivo | No se calcula franja ni frecuencia | `pd.to_datetime`; imputar `LECTOR-01` |
| zf_accesos | Lecturas dobles de huella | 675 accesos a menos de 60 s del anterior | Sobreestima la asistencia | Eliminar accesos a menos de 60 s del anterior |
| zf_accesos | Miembros inexistentes | 25 accesos de 20 IDs no registrados | Rompe la integridad entre tablas | Excluir; llave foránea en MySQL |
| zf_accesos | Acceso con membresía cancelada | 184 accesos `Permitido` sin membresía vigente | Asistencia de quien ya no es miembro | Excluir; corregir la validación del lector |
| zf_accesos | Fuera de horario | 17 accesos entre 22:00 y 5:00 | Registros dudosos por franja | Revisar con el administrador |
| kg_churn | Códigos sin diccionario | 7 binarias 0/1; `Month_to_end_contract` float | Interpretación incierta | Documentar códigos; convertir tipos |
| kg_actividad | Ausencias con entrenamiento | 1.350 visitas `Absent` con duración y calorías > 0 | `attendance_status` no confiable | No usar esa columna; solo como referencia de horarios |
| gov_escenarios | Coordenadas imposibles | 22 escenarios fuera de Medellín | Ubicaciones erradas | Marcar como `NaN`; geocodificar desde la dirección |
| gov_escenarios | Direcciones y sin comuna | 966 direcciones con espacios; sin columna comuna | No se cruza con `zf_miembros` | Normalizar espacios; tabla barrio–comuna |

## 6. Acciones de limpieza y preparación propuestas

En orden de prioridad para la siguiente etapa:

1. **Convertir tipos:** las 8 columnas de fecha con `pd.to_datetime()` (indicando el formato de cada caso en `fecha_pago`) y `valor` a número, quitando `$` y el punto de miles.
2. **Recalcular el estado de las membresías** con `fecha_fin` y la fecha de corte, para que ninguna membresía vencida quede `Activa`.
3. **Eliminar duplicados:** los 8 miembros repetidos, los 12 pagos duplicados y las 675 lecturas dobles de huella.
4. **Excluir registros inválidos:** accesos de miembros inexistentes, accesos durante membresías canceladas y, previa revisión, accesos fuera de horario y pagos en cero.
5. **Unificar categorías** de `genero` y `comuna`, y convertir `1900-01-01` en valor faltante.
6. **Tratar los faltantes** como categoría "Sin dato" en lugar de imputarlos, porque son pocos y no se pueden inferir.
7. **Preparar los datasets externos:** documentar los códigos de `kg_churn`, descartar `attendance_status` de `kg_actividad` y corregir coordenadas y direcciones de `gov_escenarios`.
8. **Derivar variables para la pregunta:** antigüedad, frecuencia semanal de asistencia, franja horaria predominante y la variable de deserción (membresía no renovada dentro de los 30 días siguientes al vencimiento).

También se proponen mejoras al sistema Zona Fit Evolution para evitar estos problemas en los datos reales: restricción `UNIQUE` sobre el documento, llaves foráneas entre tablas, actualización automática del estado de la membresía, validación de formularios y un intervalo mínimo entre lecturas del lector de huella.

## 7. Conclusiones sobre las condiciones actuales de los datos

- **Los datos son suficientes para continuar con el proyecto, pero no se pueden analizar todavía en su estado actual.** Los faltantes son bajos; los problemas más importantes son de consistencia.
- **El hallazgo más crítico** son las 93 membresías activas que ya vencieron, porque afectan directamente la medición de la deserción, que es el centro de la pregunta analítica.
- **El segundo** son las 675 lecturas dobles de huella, que inflan la frecuencia de asistencia, otra variable de la pregunta.
- **Los datasets externos** no se pueden unir con las tablas de Zona Fit porque no comparten identificadores ni periodo. Se usarán como referencia y contexto, no para combinarse fila a fila.
- **Limitaciones que se mantienen:** los datos de Zona Fit son simulados, solo se registra la entrada al gimnasio (no la salida), no hay motivo de retiro y el periodo cubierto es de unos 21 meses. Las conclusiones de negocio deberán validarse cuando el gimnasio tenga datos reales.

Después de aplicar las acciones del punto 6, los datos estarán listos para la etapa de preparación y análisis.
