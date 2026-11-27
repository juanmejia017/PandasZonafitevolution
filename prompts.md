# Bitácora de prompts – Proyecto final de ciencia de datos

**Evidencia:** GA1-220501094-01-AA1-EV09 – Proyecto final: informe analítico de la idea de proyecto de ciencia de datos

> **Instrucciones para el aprendiz**

> En este proyecto final debes usar asistentes de inteligencia artificial (ChatGPT, Claude, Gemini, Copilot u otros) para apoyar **cada apartado** del desarrollo. Esta bitácora es la evidencia de ese uso. Guárdala como `prompts.md` en la raíz de tu repositorio y actualízala mientras avanzas, no al final.

> 1. Registra **mínimo 1 y máximo 3 prompts por apartado**. Elige los más relevantes: los que generaron la versión inicial y los que corrigieron o mejoraron el resultado.  
> 2. Copia cada prompt **completo y literal**, tal como lo escribiste. No lo resumas ni lo reescribas después.  
> 3. Indica la o las **técnicas de prompting** que aplicaste. Usa los nombres del catálogo de la sección 0\.  
> 4. Enlaza la **evidencia del resultado**: el commit, la celda del notebook, la figura o la sección del informe donde quedó lo que generó la IA.  
> 5. Explica cómo **verificaste y ajustaste** la respuesta. La IA se equivoca: inventa columnas, funciones, cifras y referencias. Tú eres responsable de todo lo que entregas, y en la sustentación tendrás que explicar cualquier línea de código o cifra del informe.  
> 6. Si quieres, adjunta la conversación completa como enlace compartido o archivo en la carpeta `docs/ai_conversations/`.

> **Uso responsable:** no pegues datos personales, sensibles o con restricciones de distribución en un asistente de IA. Si tu dataset los tiene, comparte con la IA solo la estructura (nombres de columnas, tipos y unas filas de ejemplo anonimizadas o inventadas).

---

## Ficha del proyecto

| Campo | Registro |
| :---- | :---- |
| Aprendiz | Juan Diego Mejía Llano |
| Ficha | 3223873 |
| Nombre del proyecto | Análisis de deserción de miembros – Zona Fit Evolution |
| Pregunta analítica | ¿Qué factores (tipo de plan, frecuencia de asistencia, horario de entrenamiento y antigüedad) influyen en que un miembro de Zona Fit Evolution cancele o no renueve su membresía durante sus primeros seis meses? |
| URL del repositorio | https://github.com/juanmejia017/PandasZonafitevolution |
| Asistentes de IA usados (nombre y versión o modelo) | Claude (Anthropic), modelo Claude Opus 5.5 |

---

## Índice

0. [Catálogo de técnicas de prompting](#0-catálogo-de-técnicas-de-prompting)  
1. [Planteamiento: pregunta analítica y subpreguntas](#1-planteamiento-pregunta-analítica-y-subpreguntas)  
2. [Diccionario de datos y verificación del dataset](#2-diccionario-de-datos-y-verificación-del-dataset)  
3. [Carga y validación de los datos](#3-carga-y-validación-de-los-datos)  
4. [Análisis univariado](#4-análisis-univariado)  
5. [Análisis bivariado y por segmentos](#5-análisis-bivariado-y-por-segmentos)  
6. [Visualización de datos](#6-visualización-de-datos)  
7. [Hallazgos, respuesta a la pregunta y recomendaciones](#7-hallazgos-respuesta-a-la-pregunta-y-recomendaciones)  
8. [Informe analítico](#8-informe-analítico)  
9. [Versionamiento y documentación del repositorio](#9-versionamiento-y-documentación-del-repositorio)  
10. [Sustentación](#10-sustentación)  
11. [Depuración y corrección de errores](#11-depuración-y-corrección-de-errores)  
12. [Resumen y reflexión sobre el uso de la IA](#12-resumen-y-reflexión-sobre-el-uso-de-la-ia)

---

## 0\. Catálogo de técnicas de prompting

Usa estos nombres en el campo «Técnica(s) de prompting». Un mismo prompt puede combinar varias.

| Técnica | En qué consiste | Ejemplo breve |
| :---- | :---- | :---- |
| **Zero-shot** | Pedir la tarea directamente, sin ejemplos. | «Explica qué mide la desviación estándar.» |
| **Few-shot** | Dar uno o varios ejemplos del resultado esperado para que la IA siga el patrón. | «Así redacté un hallazgo: \[…\]. Redacta los demás con el mismo formato.» |
| **Rol o persona** | Asignar a la IA un rol experto. | «Actúa como analista de datos senior…» |
| **Contexto estructurado** | Dar la información necesaria: proyecto, pregunta, columnas, tipos de datos, objetivo. | «Mi dataset tiene estas columnas y tipos: \[…\].» |
| **Formato de salida** | Indicar cómo debe ser la respuesta: tabla, lista, código comentado, Markdown, extensión. | «Responde con una tabla de 4 columnas.» |
| **Delimitadores** | Separar con marcas claras las instrucciones de los datos o el código. | «Revisa el código entre \`\`\`: \[…\]» |
| **Restricciones** | Poner límites explícitos: librerías permitidas, longitud, lo que no debe hacer. | «Usa solo Pandas y Matplotlib; no uses bucles for.» |
| **Cadena de pensamiento (paso a paso)** | Pedir que razone o explique por etapas antes de concluir. | «Explica paso a paso por qué elegirías ese gráfico.» |
| **Descomposición o encadenamiento de prompts** | Dividir una tarea grande en varios prompts sucesivos, cada uno sobre la salida del anterior. | Prompt 1: subpreguntas → Prompt 2: análisis de cada una. |
| **Refinamiento iterativo** | Corregir o mejorar la respuesta anterior con instrucciones nuevas. | «Bien, pero agrega etiquetas a los ejes y la unidad.» |
| **Autoverificación o crítica** | Pedir que la IA revise su propia respuesta o la tuya y señale errores. | «Revisa si esta interpretación se sostiene con estos resultados.» |
| **Generación de alternativas** | Pedir varias opciones para comparar y elegir. | «Propón 3 formas de visualizar esta relación y sus ventajas.» |

---

## Cómo registrar cada prompt

Copia este bloque para cada prompt. En los apartados de abajo ya está preparado.

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Nombre del asistente y modelo |
| Técnica(s) de prompting | Nombres del catálogo |
| Objetivo del prompt | Qué querías obtener |
| Evidencia del resultado | Enlace al commit, celda, archivo o sección |

&nbsp;

```
Pega aquí el prompt completo, tal como lo escribiste.
```

**Verificación y ajustes:** qué revisaste (ejecutaste el código, comparaste con la documentación, contrastaste cifras con el notebook), qué corregiste y qué descartaste de la respuesta.

---

## 1\. Planteamiento: pregunta analítica y subpreguntas

*Usa la IA para revisar la pregunta analítica de la EV02 y dividirla en 3 a 5 subpreguntas que se puedan responder con tu dataset.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Contexto estructurado, restricciones |
| Objetivo del prompt | Obtener una guía para implementar la EV09 en mi repositorio existente, incluida la división de la pregunta analítica en subpreguntas |
| Evidencia del resultado | `docs/ai_conversations/` (conversación completa) y sección 3 de `reports/analytical_report.md` |

&nbsp;

```
[Adjunto: guía GA1-220501094-01-AA1-EV09 (.txt)] https://github.com/juanmejia017/PandasZonafitevolution.git
Estimados aprendices,

Les comparto las indicaciones esenciales para el desarrollo de la evidencia **GA1-220501094-01-AA1-EV09 – Proyecto final: informe analítico de la idea de proyecto de ciencia de datos con apoyo de inteligencia artificial**.

-----

🎯 Objetivo Principal
Finalizar su proyecto individual realizando el análisis descriptivo y visual de su dataset para responder a la pregunta analítica con evidencia real, organizando un repositorio técnico reproducible en GitHub y utilizando la IA de forma estratégica, crítica y documentada.

-----

📌 Puntos Clave de la Entrega

  - **Repositorio de GitHub (v1.0.0):** Debe incluir el notebook de análisis (`analytical_report.ipynb`), mínimo 5 visualizaciones exportadas (`reports/figures/`), el informe analítico (`.md` y `.pdf`), el archivo `README.md` actualizado y la bitácora de prompts (`prompts.md`).
  - **Uso de la Bitácora (`prompts.md`):** En el enlace de la entrega en Classroom encontrarán la plantilla para la bitácora. Es obligatorio registrar allí los prompts utilizados, las técnicas aplicadas, la verificación del resultado y utilizar al menos 6 técnicas distintas de prompting a lo largo del desarrollo.
  - **Técnicas de Prompting a Estudiar:** Revisen el material de formación de *Ingeniería de Prompts* para aplicar correctamente técnicas como: asignación de rol, contexto estructurado, especificación de formato de salida, aplicación de restricciones, few-shot, paso a paso, encadenamiento de prompts, refinamiento iterativo y autoverificación.
  - **Sustentación:** Deberán presentar sus hallazgos (8-10 min), mostrar un ejemplo del uso y refinamiento de sus prompts, y estar en capacidad de explicar cualquier cifra o línea de código generada con apoyo de la IA.

-----

⏱️ Duración: 12 horas.

Todos los detalles conceptuales y la estructura específica de cada apartado se encuentran disponibles en la guía de la evidencia publicada en Classroom. Quedo atento a sus dudas durante el proceso.

no hagas nada aun,simplemente dame una guia de como podemos implementar todo estas especificaciones dentro del proyecto alojado en este repositorio
```

**Verificación y ajustes:** comprobé que la IA revisó el repositorio real antes de proponer (README, `data/processed/` y las tablas analíticas) y que las columnas de cada subpregunta existen en `zonafit_memberships_analytic` y `zonafit_members_analytic` (`tipo_plan`, `no_renovo`, `observable`, `visitas_semana`, `franja_principal`, `tramo_antiguedad`, `desertor_6m`). Mantuve la estrategia de una sola rama, `feature/analytical-report`, porque la guía exige allí los 8 commits. La subpregunta 5 (evolución mensual) queda como opcional y se valida en el prompt 2.

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Rol o persona, contexto estructurado, formato de salida, autoverificación o crítica, descomposición o encadenamiento de prompts |
| Objetivo del prompt | Validar que las subpreguntas del prompt 1 se puedan responder solo con las columnas reales y que cubran la pregunta analítica |
| Evidencia del resultado | Sección 3 de `reports/analytical_report.md` y encabezado de subpreguntas en `notebooks/analytical_report.ipynb` |

&nbsp;

```
Actúa como analista de datos senior que revisa el planteamiento de un proyecto.
Proyecto: deserción de miembros en el gimnasio Zona Fit Evolution (datos simulados, fecha de corte 15/10/2026).
Pregunta analítica: ¿Qué factores (tipo de plan, frecuencia de asistencia, horario de entrenamiento y antigüedad) influyen en que un miembro de Zona Fit Evolution cancele o no renueve su membresía durante sus primeros seis meses?
Tipo de análisis: descriptivo con componente diagnóstico.
Tablas disponibles:
- zonafit_memberships_analytic (una fila por membresía): nombre_plan, tipo_plan, fecha_inicio, observable (bool), no_renovo (bool), visitas_semana (float), frecuencia (categoría ordenada), franja_principal (mañana/tarde/noche), tramo_antiguedad (categoría ordenada), antiguedad_dias (int).
- zonafit_members_analytic (una fila por miembro): tipo_plan_inicial, frecuencia_inicial, franja_inicial, evaluable (bool), desertor_6m (bool).
Subpreguntas propuestas:
1. ¿Cómo varía la tasa de no renovación por tipo de plan?
2. ¿Qué relación hay entre la frecuencia semanal y la no renovación?
3. ¿La franja horaria influye en la deserción?
4. ¿Cómo cambia el riesgo según la antigüedad, en especial en los primeros 6 meses?
5. ¿Cómo evolucionan las altas y la no renovación mes a mes?
Tarea: revisa si cada subpregunta se puede responder SOLO con estas columnas y si entre todas cubren la pregunta principal. Si alguna sobra o falta, dilo y propón el ajuste.
Formato de salida: una tabla con las columnas subpregunta, tabla y columnas que usa, filtro necesario, operación de Pandas, gráfica recomendada y veredicto (se mantiene / se ajusta / se elimina). Después, máximo 4 líneas con las debilidades del planteamiento.
```

**Verificación y ajustes:** comprobé cada observación de la IA cargando las tablas en Pandas: `tipo_plan` solo tiene 2 valores (Ilimitado y Tiquetera), así que para el detalle uso `nombre_plan` (6 planes); `franja_principal` tiene 9 membresías sin franja (sin visitas), que se excluyen; la proporción de membresías observables cae en los últimos meses (septiembre de 2026: 33 %; octubre: 1 %), lo que confirma la censura; y "altas" no se puede medir con las columnas que di. Acepté medir cada factor también por miembro (`desertor_6m`, 671 miembros evaluables). Subpreguntas definitivas: (1) deserción según el plan; (2) frecuencia semanal de asistencia y deserción; (3) franja horaria y deserción; (4) riesgo según la antigüedad y deserción en los primeros 6 meses; (5) tasa de no renovación según el mes de inicio, solo con membresías observables.

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

---

## 2\. Diccionario de datos y verificación del dataset

*Usa la IA para construir el diccionario de datos (variable, descripción, tipo en Pandas, tipo de variable estadística y unidad) y para revisar si quedaron problemas de calidad pendientes de la EV05.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Rol o persona, contexto estructurado, delimitadores, few-shot, restricciones, formato de salida |
| Objetivo del prompt | Construir el diccionario de datos de las dos tablas analíticas (variable, descripción, tipo en Pandas, tipo estadístico y unidad) |
| Evidencia del resultado | Sección «Diccionario de datos» de `notebooks/analytical_report.ipynb` y sección 4 de `reports/analytical_report.md` |

&nbsp;

```
Actúa como analista de datos que documenta un proyecto académico.
Necesito el diccionario de datos de dos tablas procesadas del proyecto de deserción de miembros de Zona Fit Evolution (datos simulados, corte 15/10/2026).
Columnas y tipos de Pandas reales (salida de dtypes):
"""
zonafit_memberships_analytic (3425 filas, una por membresía): id_membresia (int16), id_miembro (int16), id_plan (int8), fecha_inicio (datetime64[us]), fecha_fin (datetime64[us]), precio_pagado (int64), estado (category), siguiente_inicio (datetime64[us]), dias_hasta_siguiente (float64), renovada (bool), observable (bool), no_renovo (bool), numero_membresia (int64), antiguedad_dias (int64), nombre_plan (str), tipo_plan (category), duracion_dias (int16), precio (int32), genero (category), fecha_nacimiento (datetime64[us]), comuna (category), canal_captacion (category), fecha_registro (datetime64[us]), pagado_aprobado (int64), pagado_pendiente (int64), pagado_rechazado (int64), numero_pagos (int64), visitas_mañana (int16), visitas_tarde (int16), visitas_noche (int16), visitas (int16), primera_visita (datetime64[us]), ultima_visita (datetime64[us]), visitas_semana (float64), frecuencia (category), franja_principal (str), tramo_antiguedad (category), edad_al_inicio (Int16), pago_completo (bool)

zonafit_members_analytic (900 filas, una por miembro): id_miembro (int16), documento_hash (str), genero (category), fecha_nacimiento (datetime64[us]), comuna (category), canal_captacion (category), fecha_registro (datetime64[us]), membresias (int64), ultima_fecha_fin (datetime64[us]), membresias_no_renovadas (int64), visitas_totales (int16), total_pagado (int64), plan_inicial (str), tipo_plan_inicial (category), visitas_semana_inicial (float64), franja_inicial (str), fecha_alta (datetime64[us]), primera_no_renovacion (datetime64[us]), evaluable (bool), desertor_6m (bool), frecuencia_inicial (category), edad_al_alta (Int16), activo_al_corte (bool)
"""
Ejemplos del formato que espero:
| variable | descripción | tipo en Pandas | tipo estadístico | unidad |
|---|---|---|---|---|
| visitas_semana | Promedio de visitas por semana durante la membresía | float64 | Cuantitativa continua | visitas/semana |
| frecuencia | Rango de visitas semanales (hasta 1, más de 1 a 2, más de 2 a 3, más de 3) | category | Cualitativa ordinal | — |
Tarea: completa una tabla por cada dataset con todas sus columnas, en el orden dado.
Restricciones: usa solo los cuatro tipos estadísticos (cualitativa nominal, cualitativa ordinal, cuantitativa discreta, cuantitativa continua); no inventes columnas; usa "—" cuando no haya unidad; si una descripción es una suposición tuya, márcala con (verificar).
Formato de salida: dos tablas en Markdown y, al final, máximo 5 líneas con las columnas cuya clasificación sea discutible y por qué.
```

**Verificación y ajustes:** comprobé que las dos tablas tienen las 39 y 23 columnas en el orden dado, sin columnas inventadas, y que los tipos en Pandas coinciden con `dtypes`. Contrasté las descripciones con `data/raw/zonafit/DICCIONARIO.md` (estados, canales, tipos de plan, COP) y con el código de `notebooks/data_preparation.ipynb` (EV07): las franjas son mañana 5:00–11:59, tarde 12:00–17:59 y noche 18:00–21:59; `renovada` usa 30 días de gracia; `evaluable` exige 180 + 30 días desde la fecha de alta; y `desertor_6m` compara la primera no renovación con la fecha de alta + 180 días. Acepté las clasificaciones discutibles con su justificación: fechas y montos como continuas, edad y días como discretas, franja como ordinal, e identificadores y booleanos como nominales. Coinciden con la tabla de la EV08.

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Rol o persona, contexto estructurado, delimitadores, cadena de pensamiento (paso a paso), restricciones, formato de salida |
| Objetivo del prompt | Comprobar con `assert` que los problemas del diagnóstico (EV06) quedaron resueltos y que se cumplen las reglas del análisis antes de empezar |
| Evidencia del resultado | Celda «Verificación de calidad» de `notebooks/analytical_report.ipynb` |

&nbsp;

```
Actúa como analista de datos que audita la calidad antes de iniciar un análisis.
Contexto: en la EV07 limpié los datos del gimnasio Zona Fit Evolution y generé dos tablas en data/processed/: zonafit_memberships_analytic.parquet (una fila por membresía) y zonafit_members_analytic.parquet (una fila por miembro). Trabajo en notebooks/ con pandas 3.
Problemas que encontró el diagnóstico (EV06) y que deberían estar resueltos:
"""
- membresías con estado Activa aunque ya vencieron (fecha de corte 2026-10-15)
- miembros y pagos duplicados
- fechas y montos cargados como texto
- categorías de genero escritas de varias formas
- faltantes sin tratar en genero y comuna
"""
Tarea: dame, paso a paso, el código de una celda que compruebe con assert que cada problema quedó resuelto en las dos tablas, y que además verifique estas reglas: no_renovo solo puede ser True si observable es True; desertor_6m solo se interpreta cuando evaluable es True; visitas_semana no es negativa; visitas es la suma de visitas_mañana, visitas_tarde y visitas_noche.
Restricciones: usa solo pandas; un assert por regla con un mensaje claro en español; sin bucles for; no inventes columnas fuera de las del diccionario de datos.
Formato de salida: primero los pasos numerados en máximo 6 líneas, después un único bloque de código comentado.
```

**Verificación y ajustes:** ejecuté la celda sobre las dos tablas y pasaron todos los `assert`: membresías (3425, 39), miembros (900, 23) y 671 miembros evaluables. Ajusté la comprobación de pagos duplicados: como la tabla de pagos no está en las tablas analíticas, se valida de forma indirecta (`pagado_aprobado <= precio_pagado`; el cociente máximo es 1,0). Encontré que 81 miembros no evaluables tienen `desertor_6m = True` (desertaron pronto, pero su alta es reciente), lo que confirma que la tasa de deserción a 6 meses debe calcularse solo con `evaluable == True`. Por eso esa regla se comprueba con la fecha de alta y no con el valor de `desertor_6m`.

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

---

## 3\. Carga y validación de los datos

*Usa la IA para generar o revisar el código que carga el dataset procesado con rutas relativas y valida `shape`, `dtypes` e `info()` frente al diccionario de datos.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Zero-shot |
| Objetivo del prompt | Obtener una primera versión del código para cargar un archivo Parquet y comprobar la carga |
| Evidencia del resultado | Punto de partida de la celda «Carga y validación» de `notebooks/analytical_report.ipynb` (commit `feat: add data dictionary and load processed data`) |

&nbsp;

```
¿Cómo cargo un archivo parquet en pandas y compruebo que se cargó bien?
```

**Verificación y ajustes:** la respuesta era correcta pero genérica: usaba `archivo.parquet`, una sola tabla y solo inspección visual (`shape`, `dtypes`, `info()`, `head()`), sin comparar contra nada. Confirmé en la documentación de pandas que `read_parquet` requiere `pyarrow` (ya está en `requirements.txt`). No la usé tal cual; la mejoré con el prompt 2.

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Refinamiento iterativo, contexto estructurado, restricciones, formato de salida |
| Objetivo del prompt | Adaptar el código del prompt 1 a mis dos tablas y validar dimensiones y tipos contra el diccionario de datos |
| Evidencia del resultado | Celda «Carga y validación» de `notebooks/analytical_report.ipynb` (commit `feat: add data dictionary and load processed data`) |

&nbsp;

```
Bien, pero hay que adaptarlo a mi proyecto. Mejora el código anterior con estos cambios:
1. Carga las dos tablas reales con rutas relativas desde notebooks/: ../data/processed/zonafit_memberships_analytic.parquet y ../data/processed/zonafit_members_analytic.parquet.
2. Valida con assert que tienen 3425 x 39 y 900 x 23.
3. Compara los dtypes de cada tabla con el diccionario de datos usando un diccionario de Python {columna: tipo esperado} y muestra las columnas que no coincidan, sin bucles for.
4. Muestra info() de las dos tablas.
Restricciones: solo pandas, comentarios en español y nombres de variables en español.
Formato de salida: un único bloque de código para una celda del notebook.
```

**Verificación y ajustes:** ejecuté la celda dentro del notebook completo (Reiniciar y ejecutar todo): las dimensiones son (3425, 39) y (900, 23) y no hay columnas con tipo distinto al del diccionario. Comprobé que la comparación sin bucles funciona porque `pd.DataFrame` alinea las dos `Series` por nombre de columna, así que una columna faltante o sobrante aparecería con `NaN`. Revisé que los 62 tipos esperados coinciden uno a uno con la tabla del diccionario de datos (apartado 2). Comparado con el prompt 1, el código pasó de una inspección visual a una validación automática con `assert`.

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

---

## 4\. Análisis univariado

*Usa la IA para generar el código de medidas de tendencia central, dispersión y frecuencias, y para apoyar la interpretación de cada resultado.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

---

## 5\. Análisis bivariado y por segmentos

*Usa la IA para responder las subpreguntas con `groupby()`, `agg()`, `pivot_table()` y correlaciones, y para analizar valores atípicos o, si aplica, una prueba de hipótesis.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

---

## 6\. Visualización de datos

*Usa la IA para elegir el gráfico adecuado a cada tipo de variable, generar el código con Matplotlib o Seaborn (título, ejes, unidades, leyenda) y exportar las figuras a `reports/figures/`.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

---

## 7\. Hallazgos, respuesta a la pregunta y recomendaciones

*Usa la IA para redactar hallazgos (qué se encontró, con qué evidencia y qué implica), responder la pregunta analítica, proponer recomendaciones y reconocer limitaciones. Dale tus resultados reales: no le pidas que invente cifras.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

---

## 8\. Informe analítico

*Usa la IA para estructurar el informe, redactar o mejorar el resumen ejecutivo, la metodología y las limitaciones, y revisar el formato APA 7.ª. Comprueba que cada referencia existe: la IA suele inventar fuentes.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

---

## 9\. Versionamiento y documentación del repositorio

*Usa la IA para redactar el README (descripción, resultados, estructura e instrucciones de ejecución), revisar `requirements.txt` y `.gitignore`, o resolver dudas de Git (ramas, fusiones, etiqueta `v1.0.0`).*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

---

## 10\. Sustentación

*Usa la IA para estructurar la presentación de 8 a 10 minutos, escoger las visualizaciones clave o practicar con preguntas que podría hacerte el instructor.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

---

## 11\. Depuración y corrección de errores

*Registra aquí los prompts con los que resolviste errores de ejecución o resultados incorrectos. Incluye el mensaje de error y el código afectado dentro del prompt.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión |  |
| Técnica(s) de prompting |  |
| Objetivo del prompt |  |
| Evidencia del resultado |  |

&nbsp;

```

```

**Verificación y ajustes:**

---

## 12\. Resumen y reflexión sobre el uso de la IA

### 12.1 Técnicas usadas por apartado

Marca con una X las técnicas que aplicaste en cada apartado.

| Apartado | Zero-shot | Few-shot | Rol | Contexto | Formato | Delimitadores | Restricciones | Paso a paso | Encadenamiento | Iterativo | Autoverificación | Alternativas |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| 1\. Planteamiento |  |  |  |  |  |  |  |  |  |  |  |  |
| 2\. Diccionario de datos |  |  |  |  |  |  |  |  |  |  |  |  |
| 3\. Carga y validación |  |  |  |  |  |  |  |  |  |  |  |  |
| 4\. Análisis univariado |  |  |  |  |  |  |  |  |  |  |  |  |
| 5\. Análisis bivariado |  |  |  |  |  |  |  |  |  |  |  |  |
| 6\. Visualización |  |  |  |  |  |  |  |  |  |  |  |  |
| 7\. Hallazgos |  |  |  |  |  |  |  |  |  |  |  |  |
| 8\. Informe |  |  |  |  |  |  |  |  |  |  |  |  |
| 9\. Repositorio |  |  |  |  |  |  |  |  |  |  |  |  |
| 10\. Sustentación |  |  |  |  |  |  |  |  |  |  |  |  |
| 11\. Depuración |  |  |  |  |  |  |  |  |  |  |  |  |

### 12.2 Errores de la IA que detectaste

| Apartado | Qué respondió mal la IA | Cómo lo detectaste | Cómo lo corregiste |
| :---- | :---- | :---- | :---- |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

### 12.3 Reflexión final

Responde en un párrafo cada pregunta:

1. ¿En qué apartados te ayudó más la IA y por qué?  
2. ¿Qué técnica de prompting te dio mejores resultados? Da un ejemplo de cómo cambió la respuesta al aplicarla.  
3. ¿Qué decisiones del proyecto tomaste tú y no la IA?  
4. ¿Qué aprendiste sobre la forma de pedirle cosas a un asistente de IA?

### 12.4 Conversaciones completas (opcional)

| Apartado | Enlace o archivo |
| :---- | :---- |
|  |  |

### 12.5 Declaración de uso responsable

Declaro que los prompts registrados en esta bitácora son los que usé realmente. Verifiqué el código, las cifras y las referencias generadas con IA, y puedo explicar cada parte del proyecto durante la sustentación.

**Nombre del aprendiz:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ **Fecha:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_

> En la lista de referencias del informe, cita el asistente de IA en formato APA 7.ª. Por ejemplo: OpenAI. (2025). *ChatGPT* (versión del 15 de octubre) \[Modelo de lenguaje de gran tamaño\]. [https\://chat.openai.com](https://chat.openai.com)