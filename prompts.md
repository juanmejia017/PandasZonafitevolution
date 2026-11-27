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

---

## 4\. Análisis univariado

*Usa la IA para generar el código de medidas de tendencia central, dispersión y frecuencias, y para apoyar la interpretación de cada resultado.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Rol o persona, contexto estructurado, delimitadores, cadena de pensamiento (paso a paso), restricciones, formato de salida |
| Objetivo del prompt | Obtener el código de las medidas de tendencia central, dispersión y frecuencias, y plantillas de interpretación para completar con mis cifras reales |
| Evidencia del resultado | Sección 4 (4.1, 4.2 y 4.3) de `notebooks/analytical_report.ipynb` (commit `feat: add univariate analysis`) |

&nbsp;

```
Actúa como analista de datos que enseña estadística descriptiva con Pandas.
Contexto: proyecto de deserción del gimnasio Zona Fit Evolution. En el notebook ya están cargados dos DataFrames:
- membresias (3425 filas, una por membresía)
- miembros (900 filas, una por miembro)
Variables a describir:
"""
Cuantitativas (membresias): visitas_semana (continua, visitas/semana), antiguedad_dias (discreta, días), edad_al_inicio (discreta, años, Int16 con nulos), precio_pagado (continua, COP)
Cualitativas (membresias): nombre_plan (nominal), frecuencia (ordinal), franja_principal (ordinal, con nulos), tramo_antiguedad (ordinal), no_renovo (solo con observable == True)
Cualitativa (miembros): desertor_6m (solo con evaluable == True)
"""
Tarea, paso a paso:
1. Para las cuantitativas: una tabla con media, mediana, desviación estándar, mínimo, máximo, rango, Q1, Q3 y rango intercuartílico.
2. Para cada cualitativa: frecuencia absoluta y relativa en una sola tabla (value_counts y value_counts(normalize=True)), respetando el orden de las categorías ordinales y mostrando los nulos de franja_principal.
3. Las proporciones de no_renovo y desertor_6m con su filtro correspondiente.
Restricciones: solo pandas; sin bucles for; redondeo a 2 decimales; no calcules estadísticas sobre identificadores; no inventes columnas.
Formato de salida: un bloque de código por cada paso (3 celdas) con comentarios en español y, después de cada bloque, una plantilla de interpretación de 2 líneas con espacios [ ] para que yo complete las cifras reales.
```

**Verificación y ajustes:** ejecuté las tres celdas en el notebook completo. Revisé que no hubiera bucles `for`, que las ordinales salieran en su orden lógico (`frecuencia` y `tramo_antiguedad` con `cat.categories`; `franja_principal` con el orden mañana, tarde, noche) y que los totales cuadraran: 3.425 membresías en cada tabla de frecuencias y 3.245 edades no nulas. Contrasté con la EV07: la tasa de no renovación (21,27 % de 3.084) y la deserción a 6 meses (61,10 % de 671) coinciden con la sección 7.2 del README. Detecté que `franja_principal` tiene 14 nulos en todas las membresías y 9 entre las observables; las dos cifras son correctas porque se miden sobre bases distintas. Completé las plantillas con las cifras de las salidas, no con cifras de la IA. Ajusté la interpretación del precio: como la media está inflada por los planes largos, uso la mediana (90.000 COP) como precio típico.

---

## 5\. Análisis bivariado y por segmentos

*Usa la IA para responder las subpreguntas con `groupby()`, `agg()`, `pivot_table()` y correlaciones, y para analizar valores atípicos o, si aplica, una prueba de hipótesis.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Rol o persona, descomposición o encadenamiento de prompts, contexto estructurado, delimitadores, restricciones, formato de salida |
| Objetivo del prompt | Responder las 5 subpreguntas validadas con `groupby`, `agg` y `join`, calcular la correlación y analizar los valores atípicos |
| Evidencia del resultado | Secciones 5.1 a 5.6 de `notebooks/analytical_report.ipynb` (commit `feat: add bivariate and segment analysis`) |

&nbsp;

```
Actúa como analista de datos senior. Continúo el proyecto de deserción de Zona Fit Evolution: ya validé las subpreguntas y terminé el análisis univariado.
Contexto: en el notebook existen membresias, miembros, observables = membresias[membresias["observable"]] y evaluables = miembros[miembros["evaluable"]].
Subpreguntas validadas:
"""
1. ¿Cómo varía la deserción según el plan? (nombre_plan, tipo_plan / tipo_plan_inicial)
2. ¿Qué relación hay entre la frecuencia semanal y la deserción? (visitas_semana, frecuencia / frecuencia_inicial)
3. ¿La franja horaria se asocia con la deserción? (franja_principal / franja_inicial, excluyendo nulos)
4. ¿Cómo cambia el riesgo según la antigüedad? (tramo_antiguedad, antiguedad_dias)
5. ¿Cómo evoluciona la tasa de no renovación según el mes de inicio? (fecha_inicio, solo observables)
"""
Tarea, una celda por subpregunta:
- En las subpreguntas 1 a 3, una tabla con groupby y agg que muestre, por categoría, el número de membresías, las no renovadas y la tasa de no renovación (observables), y al lado el número de miembros y la tasa de desertor_6m (evaluables), unidas con join.
- En la subpregunta 4, la tabla por tramo_antiguedad y la correlación de Pearson entre antiguedad_dias, visitas_semana y no_renovo (convertida a entero).
- En la subpregunta 5, la tasa mensual con groupby por fecha_inicio.dt.to_period("M"), con el número de membresías observables de cada mes.
- Una celda final con los valores atípicos de visitas_semana por la regla de Tukey (Q1 − 1,5·IQR y Q3 + 1,5·IQR) y su efecto en la media.
Restricciones: solo pandas; sin bucles for; observed=True en los groupby de categorías; tasas en porcentaje con 2 decimales; no inventes columnas.
Formato de salida: un bloque de código por celda, comentado en español, sin interpretaciones (las escribo yo con mis salidas).
```

**Verificación y ajustes:** ejecuté las 7 celdas en el notebook completo. Contrasté las tasas con la EV07 (README, sección 7.2): tiquetera 28,4 %, semestral 10,5 %, frecuencia «hasta 1» 84,4 % y «más de 3» 0,6 %, y primeros 6 meses 23,9 %; coinciden. Comprobé que los totales cuadran: 3.084 membresías observables (3.075 con franja más las 9 sin franja) y 671 miembros evaluables. Al revisar las salidas detecté dos cosas que la IA no advirtió: (1) la deserción a 6 meses del plan anual (0 %) y del semestral (14,71 %) no es comparable, porque un plan de 365 o 180 días casi no puede vencerse sin renovar dentro de los primeros 180 días; lo aclaré en la interpretación. (2) Las 8 membresías atípicas (7 visitas por semana) empezaron entre el 13 y el 15 de octubre de 2026, justo antes del corte, así que son un efecto de la ventana corta y no un uso real; agregué `fecha_inicio` a la tabla de atípicos para mostrarlo. Agregué a la subpregunta 5 la columna `porcentaje_observable` para evidenciar la censura de los últimos meses (septiembre 32,52 %, octubre 1,18 %). Las interpretaciones las redacté con base en las salidas del notebook.

---

## 6\. Visualización de datos

*Usa la IA para elegir el gráfico adecuado a cada tipo de variable, generar el código con Matplotlib o Seaborn (título, ejes, unidades, leyenda) y exportar las figuras a `reports/figures/`.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Rol o persona, generación de alternativas, contexto estructurado, delimitadores, restricciones, formato de salida |
| Objetivo del prompt | Elegir la gráfica adecuada para cada variable comparando alternativas, y generar las figuras univariadas con título, ejes, unidades y exportación |
| Evidencia del resultado | Sección 4.4 de `notebooks/analytical_report.ipynb` (Figura 1 `reports/figures/univariate_distributions.png` y Figura 2 `reports/figures/price_paid_boxplot.png`); commit `feat: add univariate analysis` |

&nbsp;

```
Actúa como especialista en visualización de datos.
Contexto: en mi notebook ya calculé el análisis univariado de las membresías del gimnasio Zona Fit Evolution. Variables y tipo estadístico:
"""
visitas_semana: cuantitativa continua (visitas/semana)
precio_pagado: cuantitativa continua (COP), sesgada a la derecha
nombre_plan: cualitativa nominal (6 planes)
frecuencia: cualitativa ordinal (4 rangos)
franja_principal: cualitativa ordinal (mañana, tarde, noche)
"""
Tarea:
1. Para cada variable propón 2 alternativas de gráfica, con una ventaja y una desventaja de cada una, y recomienda una según el tipo de variable (barras, pastel, líneas, histograma, dispersión o boxplot).
2. Con las recomendadas, dame el código de una figura de 2 x 2 con matplotlib (sin seaborn) para visitas_semana, nombre_plan, frecuencia y franja_principal, y una figura aparte para precio_pagado.
Restricciones: cada gráfica con título, ejes con etiqueta y unidad y leyenda solo si aplica; las ordinales en su orden lógico; guarda cada figura con plt.savefig en ../reports/figures/ con nombres en inglés (univariate_distributions.png y price_paid_boxplot.png), dpi=150 y bbox_inches="tight"; crea la carpeta si no existe usando solo pathlib.
Formato de salida: primero una tabla con las alternativas y la recomendación, después un único bloque de código.
```

**Verificación y ajustes:** comprobé que las recomendaciones coinciden con la tabla de la EV08 (histograma para la continua, barras para la nominal y las ordinales; descarté el pastel porque pierde el orden de las ordinales y no permite comparar los planes pequeños). Ejecuté el código y revisé visualmente las dos figuras exportadas. Correcciones: (1) la primera versión usaba `boxplot(vert=False)`, que en matplotlib 3.11 está obsoleto (aviso `MatplotlibDeprecationWarning`); lo cambié por `orientation="horizontal"`, como indica la documentación; (2) los porcentajes de las barras verticales chocaban con el título, así que agregué margen con `set_ylim`; (3) el boxplot mostraba solo 6 puntos atípicos, pero calculé con la regla de Tukey que son 492 membresías (todas de planes trimestral, semestral y anual), así que agregué una anotación para que la figura no lleve a una lectura equivocada. Confirmé que los porcentajes de las etiquetas coinciden con las tablas de frecuencias de la sección 4.2.

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Refinamiento iterativo, descomposición o encadenamiento de prompts, contexto estructurado, delimitadores, restricciones, formato de salida |
| Objetivo del prompt | Generar las gráficas del análisis bivariado (Figuras 3 a 6) con el mismo estilo de la Figura 1 y exportarlas |
| Evidencia del resultado | Sección 5.7 de `notebooks/analytical_report.ipynb` y `reports/figures/` (`churn_by_plan_and_frequency.png`, `weekly_visits_by_renewal_boxplot.png`, `monthly_churn_trend.png`, `visits_vs_tenure_scatter.png`); commit `feat: export report figures` |

&nbsp;

```
Ahora necesito las gráficas del análisis bivariado, con el mismo estilo de la Figura 1 que ya tengo en el notebook (colores AZUL y AZUL_ORDINAL, rcParams y RUTA_FIGURAS ya definidos).
Contexto: ya existen las tablas plan_detalle, frecuencia_desercion, franja_desercion y tasa_mensual, y los DataFrames observables y evaluables.
Genera estas figuras:
"""
Figura 3 (churn_by_plan_and_frequency.png): 1 x 2. Izquierda: barras horizontales de tasa_no_renovacion por plan, ordenadas. Derecha: barras de tasa_no_renovacion y tasa_desercion_6m por rango de frecuencia (barras agrupadas, en orden lógico).
Figura 4 (weekly_visits_by_renewal_boxplot.png): boxplot de visitas_semana de las membresías observables según si renovaron o no.
Figura 5 (monthly_churn_trend.png): líneas con la tasa mensual de no renovación; marca con otro estilo los meses con porcentaje_observable menor a 90 % y agrega una línea horizontal con la tasa general.
Figura 6 (visits_vs_tenure_scatter.png): dispersión de antiguedad_dias contra visitas_semana de las observables, diferenciando renovó y no renovó.
"""
Restricciones: solo matplotlib y pandas; título con "Figura N.", ejes con etiqueta y unidad, leyenda solo si hay más de una serie; porcentajes como etiquetas en las barras; guarda cada figura con plt.savefig en RUTA_FIGURAS con dpi=150 y bbox_inches="tight"; no uses parámetros obsoletos de matplotlib 3.11.
Formato de salida: un bloque de código por figura.
```

**Verificación y ajustes:** ejecuté las 4 celdas sin avisos de obsolescencia (el boxplot usa `orientation` y `tick_labels`, vigentes en matplotlib 3.11) y revisé visualmente cada figura exportada. Correcciones: (1) en la Figura 5, octubre de 2026 aparecía con un pico de 100 % que deformaba la escala; comprobé en la tabla `tasa_mensual` que tiene una sola membresía observable, así que se omiten los meses con menos de 10 observables y se indica en la figura; (2) en la Figura 3, la etiqueta «Tasa general» quedaba sobre el eje; la moví arriba y agregué el número de membresías de cada plan para que se vea que el plan anual tiene solo 26 casos; (3) en la Figura 6, el texto «6 meses» quedaba fuera del área del gráfico; lo ubiqué con coordenadas relativas al eje. Confirmé que las etiquetas de porcentaje coinciden con las tablas de las secciones 5.1 y 5.2. Con estas figuras el proyecto tiene 6 visualizaciones de 5 tipos (histograma, barras, boxplot, líneas y dispersión).

---

## 7\. Hallazgos, respuesta a la pregunta y recomendaciones

*Usa la IA para redactar hallazgos (qué se encontró, con qué evidencia y qué implica), responder la pregunta analítica, proponer recomendaciones y reconocer limitaciones. Dale tus resultados reales: no le pidas que invente cifras.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Rol o persona, contexto estructurado, delimitadores, few-shot, formato de salida, autoverificación o crítica |
| Objetivo del prompt | Redactar la respuesta a la pregunta analítica, los hallazgos, las recomendaciones y las limitaciones a partir de mis resultados reales |
| Evidencia del resultado | Sección 6 (6.1 a 6.5) de `notebooks/analytical_report.ipynb` y secciones 7 a 9 de `reports/analytical_report.md` (commit `docs: add analytical report`) |

&nbsp;

```
Actúa como consultor de analítica que presenta resultados al administrador de un gimnasio.
Pregunta analítica: ¿Qué factores (tipo de plan, frecuencia de asistencia, horario de entrenamiento y antigüedad) influyen en que un miembro de Zona Fit Evolution cancele o no renueve su membresía durante sus primeros seis meses?
Mis resultados reales (salidas del notebook, no agregues otras cifras):
"""
- Deserción a 6 meses: 61,10 % de 671 miembros evaluables. No renovación por membresía: 21,27 % de 3.084 observables.
- Frecuencia (no renovación / deserción 6m): hasta 1 visita 84,43 % / 98,44 %; 1 a 2: 48,27 % / 79,19 %; 2 a 3: 6,71 % / 53,65 %; más de 3: 0,57 % / 31,19 %. Mediana de visitas: 1,17 (no renovó) vs. 3,03 (renovó). Correlación visitas_semana–no_renovo: −0,64.
- Plan: tiquetera 28,37 % / 74,68 %; ilimitados 20,37 % / 59,29 %; mensual estudiante 21,34 % / 71,04 %; mensual ilimitado 20,19 % / 66,67 %; trimestral 18,18 % / 41,43 %; semestral 10,53 %. El anual tiene solo 26 membresías observables.
- Antigüedad: 0–6 meses 23,85 %; 6–12 meses 14,44 %; más de 12 meses 12,79 %. Correlación antigüedad–no_renovo: −0,14.
- Franja: mañana 20,85 %, tarde 20,04 %, noche 23,26 % (deserción 6m de quienes empiezan de noche: 67,80 %).
- Serie mensual: estable alrededor de 21 % entre feb-2025 y jul-2026.
- Datos simulados; corte 15/10/2026; solo se registra la entrada; sin motivo de retiro.
"""
Ejemplo del formato de un hallazgo:
"""
Hallazgo 1 – La frecuencia de asistencia es el factor más asociado con la deserción.
Evidencia: la no renovación pasa de 84,43 % con hasta 1 visita semanal a 0,57 % con más de 3 (correlación −0,64).
Implicación: el número de visitas es la señal temprana más útil para detectar miembros en riesgo.
"""
Tarea:
1. Responde la pregunta analítica en un párrafo de máximo 120 palabras, citando cifras.
2. Redacta 4 hallazgos con el formato del ejemplo (el primero puede ser el del ejemplo, mejorado).
3. Propón 4 recomendaciones accionables, cada una ligada a un hallazgo, con indicador para medirla.
4. Lista las limitaciones y 3 próximos pasos.
5. Al final, revisa tu propia respuesta: confirma que cada cifra que usaste aparece en mis resultados y señala cualquier afirmación causal que los datos no permitan sostener.
Formato de salida: Markdown con los subtítulos Respuesta, Hallazgos, Recomendaciones, Limitaciones y próximos pasos, Autoverificación.
```

**Verificación y ajustes:** comparé cada cifra de la respuesta con las salidas del notebook y agregué al inicio de la sección 6 una celda (`resumen_hallazgos`) que recalcula las cifras principales desde las tablas, para que se puedan comprobar en un solo lugar; todas coinciden. La IA no agregó cifras nuevas: las líneas base de los indicadores son mis propias tasas. Revisé la autoverificación y acepté sus advertencias: la frecuencia se presenta como señal de alerta y no como causa (posible causalidad inversa), la mejor retención de los planes largos puede ser autoselección y las recomendaciones son hipótesis que se deben medir. Agregué la tabla de respuesta a cada subpregunta (6.1), que la guía pide en el Momento 6, y confirmé que el párrafo de respuesta tiene menos de 120 palabras.

---

## 8\. Informe analítico

*Usa la IA para estructurar el informe, redactar o mejorar el resumen ejecutivo, la metodología y las limitaciones, y revisar el formato APA 7.ª. Comprueba que cada referencia existe: la IA suele inventar fuentes.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Rol o persona, contexto estructurado, restricciones, formato de salida |
| Objetivo del prompt | Obtener el esquema del informe, el resumen ejecutivo, la metodología y la lista de referencias en APA 7.ª |
| Evidencia del resultado | `reports/analytical_report.md` (secciones 1, 3 y 9) y `reports/analytical_report.pdf`; commit `docs: add analytical report` |

&nbsp;

```
Actúa como redactor técnico que convierte un notebook de análisis en un informe para la gerencia de un gimnasio.
Contexto: tengo el notebook notebooks/analytical_report.ipynb con secciones 1 a 6 (planteamiento, diccionario, carga, univariado, bivariado y hallazgos) y 6 figuras en reports/figures/. Las fuentes son 5 tablas simuladas de Zona Fit Evolution, 2 datasets de Kaggle (Gym customers features and churn; Gym Members Activity Analysis) y 1 de datos.gov.co (Escenarios deportivos del INDER Medellín). Usé Python con pandas 3, matplotlib y JupyterLab, y Claude (Anthropic, modelo Claude Opus 5.5) como asistente de IA.
Tarea:
1. Propón el esquema del informe con estas 10 secciones: portada, resumen ejecutivo, contexto y pregunta analítica, datos, metodología (incluido el uso de IA), resultados, respuesta y hallazgos, recomendaciones, limitaciones y próximos pasos, y referencias.
2. Redacta el resumen ejecutivo (máximo media página) usando SOLO las cifras de la sección 6 del notebook.
3. Redacta la sección de metodología en máximo 200 palabras.
4. Escribe la lista de referencias en APA 7.ª con las fuentes de datos, la documentación de pandas y matplotlib y el asistente de IA.
Restricciones: no inventes cifras ni fuentes; si no estás seguro de un dato bibliográfico (autor, año, URL), márcalo con [verificar]; el resto del informe lo completo copiando del notebook.
Formato de salida: Markdown, con las figuras referenciadas como ![Figura N. Título](figures/archivo.png).
```

**Verificación y ajustes:** comprobé cada cifra del resumen ejecutivo y de las tablas del informe contra las salidas del notebook (secciones 4 a 6); las de la preparación de datos (sección 4.3 del informe) contra el README y los notebooks de la EV06 y la EV07. Verifiqué cada referencia en su fuente: (1) la IA presentó a los autores de Kaggle como «Kowalik, A.» y «Vinueza, A.», pero Kaggle solo muestra los nombres de usuario `anetakowalik` y `adrianvinueza`, así que cité el nombre de usuario como autor, con «s. f.» y fecha de consulta; (2) el título del dataset del INDER era inexacto: según los metadatos del portal (`/api/views/i5z5-qhf8.json`) es «Escenarios Deportivos INSTITUTO DE DEPORTES Y RECREACIÓN DE MEDELLÍN – INDER», creado en 2021 por el Instituto de Deportes y Recreación de Medellín; (3) confirmé que el DOI de pandas (10.5281/zenodo.3509134) lleva al registro de Zenodo con autor «The pandas development team», y que los DOI de McKinney (2010) y Hunter (2007) corresponden a esas publicaciones. Eliminé del contexto una afirmación general sin fuente («conseguir un miembro nuevo cuesta más que conservarlo»). Completé las secciones 2 y 4 a 8 con el contenido del notebook y exporté el PDF desde el mismo Markdown (pandoc + wkhtmltopdf); revisé las 9 páginas.

---

## 9\. Versionamiento y documentación del repositorio

*Usa la IA para redactar el README (descripción, resultados, estructura e instrucciones de ejecución), revisar `requirements.txt` y `.gitignore`, o resolver dudas de Git (ramas, fusiones, etiqueta `v1.0.0`).*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Rol o persona, contexto estructurado, delimitadores, cadena de pensamiento (paso a paso), restricciones, formato de salida |
| Objetivo del prompt | Actualizar el README para la EV09 (evidencias, resultados con figuras, estructura, instrucciones de ejecución y enlace a la bitácora) sin perder lo de la EV06 y la EV07 |
| Evidencia del resultado | `README.md`, secciones 4, 5, 8 y 9 (commit `docs: update README with results and run instructions`) |

&nbsp;

```
Actúa como mantenedor de un repositorio de ciencia de datos.
Contexto: mi README.md actual documenta la EV06 y la EV07 del proyecto de deserción de Zona Fit Evolution. Ahora debo actualizarlo para la EV09 (proyecto final) sin perder lo anterior.
Lo nuevo en el repositorio:
"""
- notebooks/analytical_report.ipynb: análisis univariado, bivariado y hallazgos
- reports/analytical_report.md y .pdf: informe analítico
- reports/figures/: 6 figuras (univariate_distributions.png, price_paid_boxplot.png, churn_by_plan_and_frequency.png, weekly_visits_by_renewal_boxplot.png, monthly_churn_trend.png, visits_vs_tenure_scatter.png)
- prompts.md: bitácora de prompts; docs/ai_conversations/: conversación de práctica
- requirements.txt ahora incluye matplotlib
"""
Tarea: indícame paso a paso qué secciones del README cambiar y dame el texto Markdown de:
1. La fila de la EV09 en la tabla de evidencias.
2. Una sección «Resultados del proyecto final (EV09)» con la respuesta a la pregunta en 3 líneas y 2 figuras embebidas (churn_by_plan_and_frequency.png y weekly_visits_by_renewal_boxplot.png).
3. La estructura del repositorio actualizada.
4. Las instrucciones para reproducir el análisis en Windows (CMD), con el orden de ejecución de los 3 notebooks.
5. Un enlace a la bitácora prompts.md.
Restricciones: usa solo las cifras de la sección 6 del informe; no cambies las secciones de la EV06 y la EV07; rutas relativas.
Formato de salida: pasos numerados y bloques de Markdown listos para pegar.
```

**Verificación y ajustes:** comprobé que las secciones 6 (EV06) y 7 (EV07) quedaron intactas y que la sección de limitaciones solo cambió de número (8 → 10). Confirmé que las cifras de la sección de resultados coinciden con la sección 6 del informe y que los enlaces relativos y las dos imágenes embebidas apuntan a archivos que existen en el repositorio. Revisé las instrucciones de ejecución contra lo que hice en mi PC: el entorno `.venv` no viene en el repositorio (está en `.gitignore`), así que el paso `python -m venv .venv` es necesario, como descubrí en el apartado 11. Agregué una frase a la descripción del proyecto para mencionar la EV09.

---

## 10\. Sustentación

*Usa la IA para estructurar la presentación de 8 a 10 minutos, escoger las visualizaciones clave o practicar con preguntas que podría hacerte el instructor.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Rol o persona, contexto estructurado, generación de alternativas, restricciones, formato de salida |
| Objetivo del prompt | Estructurar la sustentación de 8 a 10 minutos, elegir el ejemplo de la bitácora y practicar con preguntas difíciles del instructor |
| Evidencia del resultado | `docs/presentation_outline.md` (guion, ejemplo de bitácora y preguntas de práctica) |

&nbsp;

```
Actúa como instructor del SENA que evalúa la sustentación de un proyecto de ciencia de datos.
Contexto: mi proyecto analiza la deserción de miembros de Zona Fit Evolution. Tengo un informe de 9 páginas, 6 figuras y una bitácora de prompts. La sustentación dura de 8 a 10 minutos y debe cubrir: el problema y la pregunta, los datos y su preparación, 2 o 3 visualizaciones clave, la respuesta y las recomendaciones, las limitaciones y un ejemplo de mi bitácora (un prompt inicial, cómo lo refiné y cómo verifiqué el resultado).
Tarea:
1. Propón un guion de 7 diapositivas con el tiempo de cada una (total máximo 10 minutos) y qué figura usar en cada una.
2. Recomienda qué ejemplo de la bitácora mostrar: el par zero-shot / refinamiento de la carga de datos (apartado 3) o el par de visualización con generación de alternativas (apartado 6), y explica por qué.
3. Escribe 8 preguntas difíciles que me harías sobre el código, las cifras y las decisiones (por ejemplo: por qué hay dos tasas de deserción, qué significa observable, por qué la correlación no implica causa, qué hace la función desercion_por_factor), sin las respuestas.
Restricciones: no inventes cifras; las preguntas deben poder responderse con lo que hay en el notebook y la bitácora.
Formato de salida: una tabla para el guion, un párrafo para la recomendación y una lista numerada de preguntas.
```

**Verificación y ajustes:** sumé los tiempos del guion (10 minutos exactos, dentro del límite) y comprobé que cubre los seis puntos que pide la guía para la sustentación. Confirmé que cada cifra del guion aparece en el informe y en el notebook, y que las 8 preguntas se pueden responder con el notebook (secciones 1, 5 y 6) y la bitácora (tabla 12.2). Acepté la recomendación de mostrar el apartado 3 porque la mejora del prompt se ve en una sola celda que puedo ejecutar en vivo. Guardé el guion y las preguntas en `docs/presentation_outline.md` y practiqué respondiéndolas sin mirar las respuestas.

---

## 11\. Depuración y corrección de errores

*Registra aquí los prompts con los que resolviste errores de ejecución o resultados incorrectos. Incluye el mensaje de error y el código afectado dentro del prompt.*

**Prompt 1:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Zero-shot, delimitadores |
| Objetivo del prompt | Resolver el error al activar el entorno virtual en CMD |
| Evidencia del resultado | Entorno `.venv` creado en el proyecto; instrucciones de la sección 5 del `README.md` |

&nbsp;

```
C:\Users\juanm\PandasZonafitevolution>.venv\Scripts\activate
El sistema no puede encontrar la ruta especificada.
```

**Verificación y ajustes:** la IA explicó que la carpeta `.venv` no existía porque está en `.gitignore` y no viene con el repositorio, y me dio los comandos para crearla (`python -m venv .venv`), activarla e instalar `requirements.txt`. Los ejecuté: apareció `(.venv)` al inicio de la línea, la instalación terminó y JupyterLab abrió el notebook. Agregué el paso de creación del entorno a las instrucciones del README.

**Prompt 2:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Zero-shot |
| Objetivo del prompt | Saber si haber ejecutado `pip install` antes de crear el entorno virtual afectaba el proyecto |
| Evidencia del resultado | Dependencias instaladas dentro de `.venv` |

&nbsp;

```
pasa algo si hice el pip install antes de el entorno virtual?
```

**Verificación y ajustes:** la respuesta indicó que las librerías habían quedado en el Python global y que el entorno virtual no las ve, así que había que volver a instalarlas con `(.venv)` activo. Lo hice y no desinstalé las del Python global, porque otros proyectos míos pueden usarlas. Comprobé que el notebook se ejecuta con el entorno del proyecto.

**Prompt 3:**

| Campo | Registro |
| :---- | :---- |
| Herramienta y versión | Claude (Anthropic), modelo Claude Opus 5.5 |
| Técnica(s) de prompting | Zero-shot, delimitadores |
| Objetivo del prompt | Entender por qué JupyterLab marcaba el notebook como modificado (punto ●) sin haberlo editado, y si debía hacer push |
| Evidencia del resultado | `git status` limpio en `notebooks/analytical_report.ipynb` antes de cada commit |

&nbsp;

```
C:\Users\juanm\PandasZonafitevolution>git push
Everything up-to-date

C:\Users\juanm\PandasZonafitevolution>

aparece el puntito
```

*(Adjunté una captura de JupyterLab con `analytical_report.ipynb` abierto y el punto ● de cambios sin guardar.)*

**Verificación y ajustes:** la IA confirmó en GitHub que el commit ya estaba publicado (por eso salió *Everything up-to-date*) y explicó que el punto aparece porque JupyterLab ajusta metadatos al abrir el notebook. Cuando guardé sin querer, comprobé con `git diff` que solo cambiaban dos metadatos (nombre del kernel y versión de Python) y no el contenido. Desde entonces cierro el notebook con *Discard* antes de que se actualice el archivo.

---

## 12\. Resumen y reflexión sobre el uso de la IA

### 12.1 Técnicas usadas por apartado

Marca con una X las técnicas que aplicaste en cada apartado.

En total se usaron las 12 técnicas del catálogo (el mínimo exigido es 6).

| Apartado | Zero-shot | Few-shot | Rol | Contexto | Formato | Delimitadores | Restricciones | Paso a paso | Encadenamiento | Iterativo | Autoverificación | Alternativas |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| 1\. Planteamiento |  |  | X | X | X |  | X |  | X |  | X |  |
| 2\. Diccionario de datos |  | X | X | X | X | X | X | X |  |  |  |  |
| 3\. Carga y validación | X |  |  | X | X |  | X |  |  | X |  |  |
| 4\. Análisis univariado |  |  | X | X | X | X | X | X |  |  |  |  |
| 5\. Análisis bivariado |  |  | X | X | X | X | X |  | X |  |  |  |
| 6\. Visualización |  |  | X | X | X | X | X |  | X | X |  | X |
| 7\. Hallazgos |  | X | X | X | X | X |  |  |  |  | X |  |
| 8\. Informe |  |  | X | X | X |  | X |  |  |  |  |  |
| 9\. Repositorio |  |  | X | X | X | X | X | X |  |  |  |  |
| 10\. Sustentación |  |  | X | X | X |  | X |  |  |  |  | X |
| 11\. Depuración | X |  |  |  |  | X |  |  |  |  |  |  |

### 12.2 Errores de la IA que detectaste

| Apartado | Qué respondió mal la IA | Cómo lo detectaste | Cómo lo corregiste |
| :---- | :---- | :---- | :---- |
| 6. Visualización | Usó el parámetro `vert=False` en `plt.boxplot`, obsoleto en matplotlib 3.11 (se eliminará en la 3.13) | Al ejecutar la celda apareció un `MatplotlibDeprecationWarning` | Lo reemplacé por `orientation="horizontal"`, según la documentación oficial de matplotlib |
| 8. Informe | Presentó a los autores de los datasets de Kaggle como «Kowalik, A.» y «Vinueza, A.», y dio un título inexacto para el dataset del INDER | Abrí cada página de Kaggle y los metadatos de datos.gov.co: Kaggle solo muestra nombres de usuario y el título oficial del INDER es otro | Cité los nombres de usuario como autores (APA 7.ª), usé el título oficial y el año de creación (2021) y agregué la fecha de consulta |
| 5. Análisis bivariado | Entregó las tablas sin advertir que la deserción a 6 meses de los planes semestral (14,71 %) y anual (0 %) no es comparable, ni que las 8 membresías atípicas eran efecto de la ventana corta antes del corte | Revisé las salidas: un plan de 180 o 365 días casi no puede vencerse antes de los 180 días, y las 8 atípicas empezaron entre el 13 y el 15 de octubre de 2026 | Lo aclaré en las interpretaciones y en el informe (nota en la tabla de planes) y agregué `fecha_inicio` a la tabla de atípicos |

### 12.3 Reflexión final

Responde en un párrafo cada pregunta:

1. ¿En qué apartados te ayudó más la IA y por qué?  
2. ¿Qué técnica de prompting te dio mejores resultados? Da un ejemplo de cómo cambió la respuesta al aplicarla.  
3. ¿Qué decisiones del proyecto tomaste tú y no la IA?  
4. ¿Qué aprendiste sobre la forma de pedirle cosas a un asistente de IA?

**1. ¿En qué apartados te ayudó más la IA y por qué?**
El mayor aporte de la IA se dio en el análisis bivariado y la visualización de datos, al facilitar la construcción de agregaciones con `groupby`, `agg` y `join` para comparar dos tasas simultáneamente, además de lograr gráficas visualmente coherentes en menos tiempo. Asimismo, resultó clave al resolver problemas del entorno virtual, ya que aclaró el motivo de la ausencia de la carpeta `.venv` en lugar de limitarse a entregar un comando aislado.

**2. ¿Qué técnica de prompting te dio mejores resultados?**
Combinar contexto estructurado con restricciones explícitas produjo los mejores resultados. Mientras que un enfoque zero-shot en la carga de datos devolvió un ejemplo genérico con `archivo.parquet` y revisión meramente visual, especificar rutas, dimensiones esperadas y tipos de datos del diccionario —sin recurrir a bucles— permitió obtener comprobaciones automáticas mediante `assert` listas para ejecutarse y validarse.

**3. ¿Qué decisiones del proyecto tomaste tú y no la IA?**
Las definiciones centrales del estudio fueron propias: formular la pregunta analítica y sus cuatro variables (EV02), trabajar con datos simulados ante la ausencia de operación actual del gimnasio y calcular la deserción tanto por membresía como por miembro (EV07). También se mantuvo criterio propio al filtrar y ajustar cada salida de la IA: priorizar la mediana para el precio, señalar que los planes extensos no equivalen a un horizonte de seis meses, excluir octubre de 2026 de las gráficas y corregir citas bibliográficas con autorías imprecisas.

**4. ¿Qué aprendiste sobre la forma de pedirle cosas a un asistente de IA?**
Las instrucciones ambiguas generan respuestas plausibles en apariencia pero poco útiles para el proyecto, y la IA puede cometer errores con un tono convincente, como emplear parámetros desactualizados o atribuir fuentes incorrectas. En consecuencia, conviene aportar datos reales del caso, restringir explícitamente la invención de métricas y validar cada resultado corriendo el código y contrastando las referencias.

### 12.4 Conversaciones completas (opcional)

| Apartado | Enlace o archivo |
| :---- | :---- |
| Momento 1 (práctica zero-shot vs. prompt mejorado) | [`docs/ai_conversations/momento1_practice.md`](docs/ai_conversations/momento1_practice.md) |

### 12.5 Declaración de uso responsable

Declaro que los prompts registrados en esta bitácora son los que usé realmente. Verifiqué el código, las cifras y las referencias generadas con IA, y puedo explicar cada parte del proyecto durante la sustentación.

**Nombre del aprendiz:** Juan Diego Mejía Llano **Fecha:** 27 de noviembre de 2026

> En la lista de referencias del informe, cita el asistente de IA en formato APA 7.ª. Por ejemplo: OpenAI. (2025). *ChatGPT* (versión del 15 de octubre) \[Modelo de lenguaje de gran tamaño\]. [https\://chat.openai.com](https://chat.openai.com)