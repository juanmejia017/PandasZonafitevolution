# Momento 1 – Ejercicio de práctica: prompt zero-shot vs. prompt mejorado

**Asistente:** Claude (Anthropic), modelo Claude Opus 5.5
**Fecha:** 27 de noviembre de 2026
**Objetivo:** obtener el código que calcula la media de una columna y comparar la calidad de la respuesta según la forma de pedirlo.

---

## Prompt A – Zero-shot

```text
Dame el código para calcular la media de una columna en pandas.
```

**Respuesta de la IA:**

```python
import pandas as pd

df = pd.read_csv("archivo.csv")

media = df["nombre_columna"].mean()
print(media)
```

> `mean()` calcula el promedio aritmético de la columna e ignora los valores nulos (`NaN`) por defecto. Si quieres la media de todas las columnas numéricas a la vez, usa `df.mean(numeric_only=True)`.

---

## Prompt B – Rol, contexto estructurado, restricciones y formato de salida

```text
Actúa como analista de datos que enseña Pandas a un aprendiz del SENA.
Contexto: trabajo en un notebook ubicado en notebooks/ y mi dataset procesado está en data/processed/zonafit_memberships_analytic.parquet. Columnas relevantes: visitas_semana (numérica decimal, visitas promedio por semana), precio_pagado (numérica entera, pesos colombianos) y observable (booleana, True si ya se sabe si la membresía se renovó).
Tarea: calcular la media de visitas_semana solo para las membresías con observable == True.
Restricciones: usa solo pandas, ruta relativa al notebook, sin bucles for y sin inventar columnas que no te di.
Formato de salida: un único bloque de código comentado en español y, después, una explicación de máximo 3 líneas de lo que devuelve.
```

**Respuesta de la IA:**

```python
import pandas as pd

# Cargar el dataset procesado (ruta relativa desde la carpeta notebooks/)
membresias = pd.read_parquet("../data/processed/zonafit_memberships_analytic.parquet")

# Filtrar solo las membresías cuyo resultado de renovación ya se conoce
observables = membresias[membresias["observable"]]

# Calcular la media de visitas por semana en ese subconjunto
media_visitas = observables["visitas_semana"].mean()

print(f"Media de visitas por semana (membresías observables): {media_visitas:.2f}")
```

> Devuelve un único número decimal: el promedio de visitas semanales de las membresías con `observable == True`.
> El filtro con una máscara booleana reemplaza cualquier bucle, y `mean()` omite los valores nulos si los hubiera.
> Se imprime con dos decimales para leerlo con facilidad.

---

## Comparación

| Aspecto | Prompt A (zero-shot) | Prompt B (mejorado) |
|---|---|---|
| Archivo y formato | Genérico: `archivo.csv` con `read_csv` | El dataset real en Parquet con `read_parquet` |
| Ruta | No considera dónde está el notebook | Ruta relativa correcta desde `notebooks/` (`../data/processed/`) |
| Columna | Marcador `nombre_columna` | Columna real `visitas_semana` |
| Filtro | No hay | Aplica `observable == True`, que es la condición del análisis |
| Comentarios y explicación | Mínimos | Código comentado y explicación limitada a 3 líneas |
| ¿Se puede ejecutar sin cambios? | No | Sí |

## Verificación

- Se ejecutó el código del Prompt B sobre `zonafit_memberships_analytic.parquet` (pandas 3): **media = 2,60 visitas por semana** en **3.084 membresías observables**, sin valores nulos en `visitas_semana`.
- Se confirmaron los tipos: `visitas_semana` es `float64`, `precio_pagado` es `int64` y `observable` es `bool`, así que la máscara booleana `membresias["observable"]` funciona sin compararla con `True`.
- Las 3.084 membresías observables coinciden con la cifra del README (sección 7.2, EV07).
- `read_parquet` necesita `pyarrow`, que ya está en `requirements.txt`.

## Conclusión

El prompt zero-shot entrega un patrón correcto pero genérico, que hay que adaptar a mano: nombre de archivo, formato, ruta, columna y filtro. Al añadir rol, contexto estructurado (ruta, columnas y tipos), restricciones y formato de salida, la respuesta queda lista para ejecutar en el proyecto y no inventa columnas. Esa es la estructura base que se usará en los prompts de la bitácora.
