# Guion de la sustentación – EV09

**Proyecto:** Análisis de deserción de miembros – Zona Fit Evolution
**Duración:** 8 a 10 minutos

## Diapositivas

| # | Diapositiva | Contenido | Figura / apoyo | Tiempo |
|---|---|---|---|---|
| 1 | Problema y pregunta | Zona Fit Evolution: por qué importa la deserción; pregunta analítica, 4 factores y 5 subpreguntas | Ninguna (texto) | 1:00 |
| 2 | Datos y preparación | 5 tablas simuladas + 3 externas; problemas de la EV06 (Activa vencidas, duplicados, lecturas dobles) y cómo se corrigieron en la EV07; las dos medidas de deserción (observable / evaluable) | Tabla de fuentes del informe (4.1) | 1:30 |
| 3 | Panorama general | Cifras base: 21,27 % de no renovación por membresía y 61,10 % de deserción a 6 meses; perfil de planes, frecuencia y franja | Figura 1 | 1:00 |
| 4 | Hallazgo principal: frecuencia | Escalera de 84,43 % a 0,57 %; medianas de 1,17 y 3,03; umbral de 2 visitas; correlación −0,64 | Figuras 3 (derecha) y 4 | 2:00 |
| 5 | Plan, antigüedad y horario | La tiquetera, la más riesgosa; riesgo concentrado en los primeros 6 meses; el horario influye poco; por qué los planes largos no son comparables a 6 meses | Figura 3 (izquierda) y Figura 6 | 1:30 |
| 6 | Respuesta, recomendaciones y limitaciones | Párrafo de respuesta; 4 recomendaciones con indicador; datos simulados, asociación y no causa, censura al corte | Tabla de recomendaciones (informe, sección 7) | 1:30 |
| 7 | Uso de la IA (bitácora) | Ejemplo de prompt inicial → refinamiento → verificación; errores de la IA detectados (tabla 12.2) | `prompts.md` abierto en GitHub | 1:30 |
| | **Total** | | | **10:00** |

## Ejemplo de la bitácora para mostrar

Apartado 3: prompt zero-shot («¿Cómo cargo un archivo parquet en pandas…?») → prompt de refinamiento iterativo → verificación ejecutando la celda (dimensiones y 62 tipos coinciden con el diccionario). Si sobra tiempo: apartado 6 (generación de alternativas) y el error detectado (`vert=False`, obsoleto en matplotlib 3.11).

## Preguntas para practicar

1. ¿Por qué el informe tiene dos tasas de deserción (21,27 % y 61,10 %) y por qué son tan distintas si miden el mismo fenómeno?
2. ¿Qué significan `observable` y `evaluable`, y qué pasaría con las tasas si no se filtraran?
3. Explique línea por línea qué hace la función `desercion_por_factor` y por qué usa `join` con `how="outer"`.
4. La correlación entre `visitas_semana` y `no_renovo` es −0,64. ¿Por qué eso no prueba que ir más al gimnasio evite la deserción? ¿Qué otra explicación puede haber?
5. ¿Por qué el plan anual aparece con 0 % de deserción a 6 meses y 38,46 % de no renovación? ¿Se puede concluir que el plan anual retiene mejor?
6. ¿Por qué en la Figura 5 los últimos meses tienen tasas tan bajas y por qué no se graficó octubre de 2026?
7. ¿Cómo se identificaron los valores atípicos de `visitas_semana` y por qué se decidió conservarlos?
8. ¿Qué error de la IA detectó en el proyecto, cómo lo detectó y cómo lo corrigió?
