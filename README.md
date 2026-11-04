# Análisis de deserción de miembros – Zona Fit Evolution

Proyecto individual de ciencia de datos del programa ADSO (SENA Regional Antioquia, ficha 3223873).
**Aprendiz:** Juan Diego Mejía Llano

Este repositorio contiene la evidencia **GA1-220501094-01-AA1-EV06 – Diagnosticar la calidad de datos: preparación, exploración y documentación**: la carga, inspección y diagnóstico de calidad de los datasets del proyecto con Python y Pandas.

## 1. Descripción y propósito

Zona Fit Evolution es un sistema de gestión para un gimnasio de Medellín (miembros, planes, control de acceso con huella y pagos). El proyecto busca identificar qué hace que un miembro deje de renovar su membresía, para que el administrador pueda actuar a tiempo con los miembros en riesgo.

Antes de analizar, este diagnóstico determina si los datos están en condiciones de usarse y qué hay que limpiar.

## 2. Pregunta analítica

> ¿Qué factores (tipo de plan, frecuencia de asistencia, horario de entrenamiento y antigüedad) influyen en que un miembro de Zona Fit Evolution cancele o no renueve su membresía durante sus primeros seis meses?

## 3. Datasets

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

**Sobre los datos de Zona Fit:** el gimnasio todavía no tiene datos reales de operación, así que las cinco tablas de `data/raw/zonafit/` son una exportación **simulada** de su base de datos MySQL. No contienen datos personales: el documento de identidad está anonimizado y no hay nombres, teléfonos ni correos. El significado de cada columna está en [`data/raw/zonafit/DICCIONARIO.md`](data/raw/zonafit/DICCIONARIO.md).

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
├── README.md                        Descripción del proyecto (este archivo)
├── .gitignore                       Archivos que Git no sube (entorno virtual, temporales)
├── requirements.txt                 Dependencias de Python
├── data/
│   └── raw/                         Datos originales, sin modificar
│       ├── zonafit/                 5 tablas simuladas + DICCIONARIO.md
│       ├── kaggle/                  2 datasets de Kaggle
│       └── datos_gov/               1 dataset de datos.gov.co
├── notebooks/
│   └── diagnostico_calidad.ipynb    Carga, inspección y diagnóstico de calidad
└── reports/
    └── informe_diagnostico.md       Informe técnico del diagnóstico
```

## 5. Cómo reproducir el diagnóstico

Requisitos: Python 3 y Git. Comandos para Windows (CMD):

```cmd
git clone https://github.com/juanmejia017/PandasZonafitevolution.git
cd PandasZonafitevolution
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
jupyter lab
```

En JupyterLab abre `notebooks/diagnostico_calidad.ipynb` y elige **Run → Run All Cells**. El notebook lee los datos con rutas relativas (`../data/raw/`), así que debe ejecutarse desde la carpeta `notebooks/`.

Para ejecutarlo completo sin abrir JupyterLab:

```cmd
jupyter nbconvert --to notebook --execute --inplace notebooks\diagnostico_calidad.ipynb
```

## 6. Resultados

- **Notebook:** [`notebooks/diagnostico_calidad.ipynb`](notebooks/diagnostico_calidad.ipynb). Contiene los Momentos 1 a 4 de la guía: reconocimiento de los datasets, carga, inspección de cada DataFrame (`head`, `tail`, `shape`, `columns`, `dtypes`, `info`, `describe`) con su tabla estructural, y el diagnóstico con 19 hallazgos.
- **Informe técnico:** [`reports/informe_diagnostico.md`](reports/informe_diagnostico.md).

Hallazgos principales:

- 93 membresías siguen `Activa` aunque ya vencieron. Es el problema más crítico porque afecta la medición de la deserción.
- 675 lecturas dobles del lector de huella inflan la frecuencia de asistencia.
- 8 columnas de fecha y el monto de los pagos se cargaron como texto.
- Hay miembros y pagos duplicados, categorías escritas de varias formas y accesos de miembros que no existen.
- Los faltantes son bajos (ninguno supera el 6 % en columnas relevantes).
