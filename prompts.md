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

## 2\. Diccionario de datos y verificación del dataset

*Usa la IA para construir el diccionario de datos (variable, descripción, tipo en Pandas, tipo de variable estadística y unidad) y para revisar si quedaron problemas de calidad pendientes de la EV05.*

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

## 3\. Carga y validación de los datos

*Usa la IA para generar o revisar el código que carga el dataset procesado con rutas relativas y valida `shape`, `dtypes` e `info()` frente al diccionario de datos.*

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