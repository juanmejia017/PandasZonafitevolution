# Análisis de deserción de miembros – Zona Fit Evolution

Proyecto individual de ciencia de datos del programa ADSO (SENA Regional Antioquia, ficha 3223873).
**Aprendiz:** Juan Diego Mejía Llano

Este repositorio reúne las evidencias del proyecto individual con Python y Pandas:

| Evidencia | Contenido | Notebook | Documento |
|---|---|---|---|
| GA1-220501094-01-AA1-EV06 – Diagnosticar la calidad de datos | Carga, inspección y diagnóstico de calidad de los datasets | [`notebooks/data_quality.ipynb`](notebooks/data_quality.ipynb) | [`reports/data_quality.md`](reports/data_quality.md) |
| GA1-220501094-01-AA1-EV07 – Preparación, limpieza y estructuración de datos | Limpieza, análisis por grupos, combinación y exportación de los datos | [`notebooks/data_preparation.ipynb`](notebooks/data_preparation.ipynb) | Este README (sección 7) |

## 1. Descripción y propósito

Zona Fit Evolution es un sistema de gestión para un gimnasio de Medellín (miembros, planes, control de acceso con huella y pagos). El proyecto busca identificar qué hace que un miembro deje de renovar su membresía, para que el administrador pueda actuar a tiempo con los miembros en riesgo.

Primero se diagnosticó la calidad de los datos (EV06) y después se limpiaron, analizaron y estructuraron para responder la pregunta analítica (EV07).

## 2. Pregunta analítica

> ¿Qué factores (tipo de plan, frecuencia de asistencia, horario de entrenamiento y antigüedad) influyen en que un miembro de Zona Fit Evolution cancele o no renueve su membresía durante sus primeros seis meses?

## 3. Fuentes de datos

| # | Archivo | DataFrame | Fuente | Contenido |
|---|---|---|---|---|
| 1 | `data/raw/zonafit/planes.csv` | `zf_planes` | Zona Fit (simulado) | Catálogo de planes |
| 2 | `data/raw/zonafit/miembros.csv` | `zf_miembros` | Zona Fit (simulado) | Personas inscritas |
| 3 | `data/raw/zonafit/membresias.csv` | `zf_membresias` | Zona Fit (simulado) | Compras y renovaciones de planes |
| 4 | `data/raw/zonafit/pagos.csv` | `zf_pagos` | Zona Fit (simulado) | Pagos de las membresías |
| 5 | `data/raw/zonafit/accesos.csv` | `zf_accesos` | Zona Fit (simulado) | Registros del lector de huella |
| 6 | `data/raw/kaggle/gym_churn_us.csv` | `kg_churn` | Kaggle | Clientes de gimnasio con variable de deserción |
| 7 | `data/raw/kaggle/gym_attendance_cleaned_data.csv` | `kg_actividad` | Kaggle | Visitas a gimnasio |
| 8 | `data/raw/datos_gov/escenarios_deportivos_inder.csv` | `gov_escenarios` | datos.gov.co | Escenarios deportivos del INDER Medellín |

**Sobre los datos de Zona Fit:** el gimnasio todavía no tiene datos reales de operación, así que las cinco tablas de `data/raw/zonafit/` son una exportación **simulada** de su base de datos MySQL, con fecha de corte del 15 de octubre de 2026. No contienen datos personales: el documento de identidad está anonimizado y no hay nombres, teléfonos ni correos. El significado de cada columna está en [`data/raw/zonafit/DICCIONARIO.md`](data/raw/zonafit/DICCIONARIO.md).

### Fuentes externas

| Archivo | Fuente |
|---|---|
| `gym_churn_us.csv` | [Gym customers features and churn (Kaggle)](https://www.kaggle.com/datasets/adrianvinueza/gym-customers-features-and-churn) |
| `gym_attendance_cleaned_data.csv` | [Gym Members Activity Analysis (Kaggle)](https://www.kaggle.com/datasets/anetakowalik/gym-members-activity-analysis) |
| `escenarios_deportivos_inder.csv` | [Escenarios deportivos INDER Medellín (datos.gov.co)](https://www.datos.gov.co/Deporte-y-Recreaci-n/Escenarios-Deportivos-INSTITUTO-DE-DEPORTES-Y-RECR/i5z5-qhf8) |

Los datos externos se usan con fines académicos. Todos los archivos son pequeños (menos de 3 MB cada uno), por eso se publican en el repositorio.

## 4. Estructura del repositorio

```text
PandasZonafitevolution/
├── README.md                          Descripción del proyecto (este archivo)
├── .gitignore                         Archivos que Git no sube (entorno virtual, temporales)
├── requirements.txt                   Dependencias de Python
│
├── data/
│   ├── raw/                           Datos originales, sin modificar
│   │   ├── zonafit/                   5 tablas simuladas + DICCIONARIO.md
│   │   ├── kaggle/                    2 datasets de Kaggle
│   │   └── datos_gov/                 1 dataset de datos.gov.co
│   └── processed/                     Datos limpios y tablas consolidadas (generados por data_preparation.ipynb)
│
├── notebooks/
│   ├── data_quality.ipynb             EV06: carga, inspección y diagnóstico de calidad
│   └── data_preparation.ipynb         EV07: limpieza, análisis y estructuración
│
└── reports/
    └── data_quality.md                Informe técnico del diagnóstico de calidad
```

## 5. Cómo ejecutar el proyecto

Requisitos: Python 3 y Git. Las dependencias (pandas, PyArrow y JupyterLab) están en `requirements.txt`. Comandos para Windows (CMD):

```cmd
git clone https://github.com/juanmejia017/PandasZonafitevolution.git
cd PandasZonafitevolution
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
jupyter lab
```

En JupyterLab abre los notebooks de la carpeta `notebooks/` **en este orden** y en cada uno elige **Run → Run All Cells**:

1. `data_quality.ipynb`: diagnóstico de calidad.
2. `data_preparation.ipynb`: limpieza, análisis y estructuración. Lee `data/raw/` y escribe los resultados en `data/processed/`.

Los notebooks usan rutas relativas (`../data/raw/`, `../data/processed/`), así que deben ejecutarse desde la carpeta `notebooks/`.

Para ejecutarlos completos sin abrir JupyterLab:

```cmd
jupyter nbconvert --to notebook --execute --inplace notebooks\data_quality.ipynb
jupyter nbconvert --to notebook --execute --inplace notebooks\data_preparation.ipynb
```

## 6. Resultados del diagnóstico (EV06)

El diagnóstico de [`notebooks/data_quality.ipynb`](notebooks/data_quality.ipynb) encontró 19 hallazgos, documentados en [`reports/data_quality.md`](reports/data_quality.md). Los principales:

- 93 membresías seguían `Activa` aunque ya habían vencido. Era el problema más crítico porque afecta la medición de la deserción.
- 675 lecturas dobles del lector de huella inflaban la frecuencia de asistencia.
- 8 columnas de fecha y el monto de los pagos se cargaron como texto.
- Había miembros y pagos duplicados, categorías escritas de varias formas y accesos de miembros que no existen.
- Los faltantes eran bajos (ninguno superaba el 6 % en columnas relevantes).

## 7. Preparación de los datos (EV07)

El notebook [`notebooks/data_preparation.ipynb`](notebooks/data_preparation.ipynb) aplica las lecciones 2, 3 y 4 del material *Preparar y estructurar datos con Python*. Los datos originales de `data/raw/` no se modifican.

### 7.1 Transformaciones realizadas (Lección 2: limpieza y estandarización)

Cada problema se corrige con una función reutilizable. Las funciones se encadenan en un pipeline con `pipe()` que registra filas, nulos, duplicados y memoria después de cada paso (`data/processed/cleaning_log.csv`), y el resultado se valida con `assert`.

| Dataset | Problema | Transformación | Decisión |
|---|---|---|---|
| `zf_miembros` | 8 personas inscritas dos veces | `drop_duplicates` por `documento_hash`, conservando el id más bajo | Eliminar |
| `zf_miembros` | `genero` con 6 valores; comuna `laureles` | Diccionario con `map` y `replace` → `M`, `F`, `Laureles-Estadio` | Corregir |
| `zf_miembros` | Fechas como texto; 9 nacimientos `1900-01-01` | `pd.to_datetime`; la fecha de relleno pasa a faltante | Corregir |
| `zf_miembros` | Faltantes en género (27) y comuna (46) | Categoría `Sin dato` | Conservar el registro |
| `zf_miembros` | Faltantes en fecha de nacimiento (54) | Se dejan como faltantes: no se inventan edades | Conservar |
| `zf_membresias` | 93 membresías `Activa` vencidas | Estado recalculado con `fecha_fin` y la fecha de corte | Corregir |
| `zf_membresias` | 51 precios faltantes | Suma de los pagos aprobados (49) o precio de lista (2) | Completar |
| `zf_pagos` | 12 pagos duplicados | `drop_duplicates` | Eliminar |
| `zf_pagos` | Monto como texto (`$90.000`); fechas en dos formatos | Regex + `pd.to_numeric`; `pd.to_datetime` con el formato de cada caso | Corregir |
| `zf_pagos` | 108 pagos sin método | Categoría `Sin dato` | Conservar el registro |
| `zf_accesos` | Fecha como texto; 1.140 sin dispositivo | `pd.to_datetime`; `LECTOR-01` (único lector de la sede) | Corregir |
| `zf_accesos` | 675 lecturas dobles, 25 de miembros inexistentes, 15 fuera de horario y 179 con membresía cancelada | Se excluyen los 894 accesos inválidos; a cada acceso se le asigna su membresía vigente | Eliminar |
| `kg_churn` | Nombres y tipos | Columnas en minúscula, binarias como `int8` | Corregir |
| `kg_actividad` | `attendance_status` no confiable; fechas como texto | Se elimina la columna; fecha y hora convertidas | Corregir |
| `gov_escenarios` | 22 coordenadas fuera de Medellín; 966 direcciones con espacios | Coordenadas anuladas; espacios normalizados | Corregir |

**Calidad antes y después** (tablas de Zona Fit):

| Aspecto | Antes | Después |
|---|---|---|
| Duplicados | 8 miembros, 12 pagos y 675 lecturas dobles | 0 |
| Membresías `Activa` vencidas | 93 | 0 |
| Columnas de texto | 18 (fechas y montos incluidos) | 2 (identificadores) |
| Faltantes sin tratar | 1.431 | 0 (los que quedan están justificados) |
| Accesos | 57.003 | 56.109 válidos |
| Memoria | 4.932 KB | 1.365 KB |

Los 15 problemas medibles del diagnóstico quedaron en 0 (tabla completa en `data/processed/quality_comparison.csv` y al final del notebook).

### 7.2 Indicadores (Lección 3: filtrado, ordenamiento y agrupación)

La deserción se mide por membresía: una membresía **no se renueva** si fue cancelada o si pasaron más de 30 días desde su fin sin una nueva compra. Las membresías cuyo resultado aún no se conoce al corte se excluyen.

| Factor | Indicador | Resultado |
|---|---|---|
| General | Tasa de no renovación | 21,3 % de 3.084 membresías observables |
| Tipo de plan | Tasa de no renovación por plan | Tiquetera 28,4 % vs. ilimitados 20,4 %; semestral 10,5 % |
| Frecuencia | Tasa por visitas semanales | Hasta 1 visita: 84,4 % · más de 3 visitas: 0,6 % |
| Horario | Tasa por franja predominante | Mañana 21,1 % · tarde 19,6 % · noche 23,1 % |
| Antigüedad | Tasa por antigüedad del miembro | Primeros 6 meses: 23,9 % · más de 12 meses: 12,8 % |
| Primeros seis meses | Miembros que dejan de renovar en sus primeros 180 días | 61,1 % de 671 miembros evaluables |

**Interpretación:** la frecuencia de asistencia es el factor más asociado con la deserción (por debajo de dos visitas semanales el riesgo se dispara), seguida de la antigüedad (los primeros seis meses concentran el riesgo) y del tipo de plan (la tiquetera y los planes mensuales desertan más). El horario influye poco. El dataset externo de Kaggle muestra el mismo patrón de frecuencia.

### 7.3 Datasets procesados (Lección 4: combinación y estructuración)

Las tablas de Zona Fit se combinan con `merge` usando `how="left"` y `validate` (`m:1` o `1:1`), comprobando las claves con `indicator=True` y verificando con `assert` que el número de filas no cambie y que los totales (visitas y pagos) coincidan con las tablas de origen. Los datasets externos **no se combinan** con Zona Fit porque no comparten identificadores ni periodo; se exportan limpios por separado como referencia.

Archivos generados en `data/processed/`:

| Archivo | Filas | Contenido |
|---|---:|---|
| `zonafit_memberships_analytic.csv` / `.parquet` | 3.425 | **Tabla consolidada por membresía:** plan, miembro, pagos, asistencia por franja, frecuencia, antigüedad y variable de renovación |
| `zonafit_members_analytic.csv` / `.parquet` | 900 | **Tabla consolidada por miembro:** perfil, plan y frecuencia iniciales, totales y deserción en los primeros 6 meses |
| `zonafit_plans_clean.csv` | 6 | Planes limpios |
| `zonafit_members_clean.csv` | 900 | Miembros limpios |
| `zonafit_memberships_clean.csv` | 3.425 | Membresías limpias |
| `zonafit_payments_clean.csv` | 3.560 | Pagos limpios |
| `zonafit_access_clean.csv` | 56.109 | Accesos válidos con su membresía asignada |
| `kaggle_gym_churn_clean.csv` | 4.000 | Deserción de Kaggle limpia |
| `kaggle_gym_activity_clean.csv` | 2.600 | Visitas de Kaggle limpias |
| `inder_sports_venues_clean.csv` | 1.071 | Escenarios del INDER limpios |
| `cleaning_log.csv` | 25 | Registro de cambios del pipeline de limpieza |
| `quality_comparison.csv` | 8 | Calidad de cada dataset antes y después |

Los archivos Parquet conservan los tipos de dato (fechas, categorías y enteros con nulos); los CSV se pueden abrir en Excel.

## 8. Limitaciones

- Los datos de Zona Fit son **simulados**: las conclusiones deben validarse cuando el gimnasio tenga datos reales.
- Solo se registra la entrada al gimnasio (no la salida) y no hay motivo de retiro ni fecha de cancelación.
- El periodo cubierto es de unos 21 meses, así que los miembros que se inscribieron en los últimos 7 meses todavía no se pueden evaluar en sus primeros seis meses.
- Los indicadores muestran asociaciones entre factores y deserción, no causas.
