# Requerimientos: Reto Planta Física · Entregable 2: Desarrollo

MA2015.201 · Modificación justificada del algoritmo · Actualización del 7 de octubre de 2026

- Cierre: 15 de octubre de 2026, 23:59.
- Calificación sobre 100 puntos, peso de 15 % en el curso, nota compartida por equipo.
- Archivo de trabajo: `reto_planta.ipynb` (libreta acumulativa; ya contiene Investigación).
- Fuente: `docs/02-desarrollo-instrucciones-rubrica.pdf`.

## 1. Objetivo

Partir del algoritmo genético proporcionado y construir una variante modificando un operador. Conservar la versión base y añadir una variante con una modificación sustantiva en selección, cruza o mutación. Explicar qué limitación se identifica, qué se propone cambiar y por qué se espera una mejora. Comparar ambas versiones bajo las mismas condiciones y relacionar los resultados con la asignación de agua.

- Continuar en la misma libreta acumulativa.
- La modificación es obligatoria. Se evalúan su justificación, funcionamiento y comprobación.
- Un resultado igual o peor que la base puede alcanzar 100 si la evidencia y la interpretación cumplen los criterios.
- Una ejecución aislada muestra un caso, no demuestra superioridad general.

## 2. Problema mensual (no cambia)

Demandas agregadas de marzo de 2025. Cuatro genes enteros en este orden; $k_i/10$ es la fracción de agua tratada del edificio.

| Edificio | Demanda $D_i$ (m³) | Dominio de $k_i$ | Fracción tratada |
|---|---|---|---|
| Aulas 1 | 847.00 | 0, …, 8 | $k_1/10$ |
| Biblioteca | 462.00 | 0, …, 8 | $k_2/10$ |
| Cedetec | 284.21 | 0, …, 6 | $k_3/10$ |
| Aulas 2 | 683.00 | 0, …, 8 | $k_4/10$ |

$$T = \sum_{i=1}^{4} D_i k_i/10,\qquad P = 2276.21 - T,\qquad E = \max(0,\ T - 1410)$$

Minimizar $P$ con capacidad didáctica $C = 1410$ m³ y aptitud (menor es mejor):

$$F(k) = \begin{cases} P/2276.21, & T \le C \\ 1 + E/C, & T > C \end{cases}$$

- Tolerancia de $10^{-8}$ m³ al comprobar la capacidad.
- Rechazar genes inválidos sin redondearlos ni corregirlos.
- Distinguir consumos observados de la capacidad y los límites didácticos. El resultado describe un modelo académico mensual.

## 3. Comparación controlada (pasos)

1. **Conservar la base.** Identificar su código y resultados. La base usa torneo de dos, cruza de un punto, mutación discreta por gen, reemplazo generacional y una élite. Ambas versiones deben poder ejecutarse por separado.
2. **Hipótesis.** Identificar una limitación concreta de un operador y el mecanismo por el que el cambio podría mejorar la búsqueda (por ejemplo, encontrar una asignación factible con menos agua potable).
3. **Modificar un solo operador.** Selección, cruza o mutación; identificar la función o líneas cambiadas. Ejemplos (no obligatorios): torneo de tres, cruza uniforme, mutación hacia un vecino válido.
4. **Ejecutar base y variante.** Cada ejecución inicializada por separado con semilla 42, sin arrastrar estado aleatorio. Misma población inicial y condiciones comunes.
5. **Contrastar.** Presentar los dos candidatos finales y sus medidas con el mismo evaluador. Comparar agua potable solo entre candidatos factibles; un menor $P$ con exceso no es mejora factible.
6. **Interpretar.** Decir si el resultado apoya, contradice o no distingue la hipótesis, y el límite de una sola semilla. Conservar la conclusión aunque haya igualdad o empeoramiento.

No cuenta como modificación: cambiar solo semilla, tamaño de población, generaciones o probabilidad de mutación, ni cambiar nombres, comentarios o formato sin alterar el comportamiento de un operador.

### Condiciones comunes

| Condición | Valor |
|---|---|
| Población / generaciones | 20 individuos / 20 generaciones |
| Semilla / mutación | 42 / $p_m = 0.25$ por gen |
| Problema y evaluador | Mismos datos, genes, dominios, objetivo, capacidad y aptitud |
| Población inicial | Misma regla e inicialización con semilla 42 |
| Reemplazo y elitismo | Reemplazo generacional, población constante y una élite |
| Cambio experimental | Solo el operador elegido |

### Evidencia en la libreta

Hipótesis y cambio explicados, código identificado de ambas versiones, configuraciones, salidas conservadas y esta tabla:

| Medida | Base | Variante |
|---|---|---|
| Cromosoma final $(k_1, k_2, k_3, k_4)$ | | |
| Agua tratada $T$ y potable $P$ (m³) | | |
| Aptitud $F$ / exceso $E$ (m³) | | |
| Factibilidad de dominios y capacidad | | |

Entregar `.ipynb`, `pyproject.toml` y `uv.lock`. Ejecutar desde kernel reiniciado y conservar salidas. Integrar correcciones de Investigación y registro de rotación del equipo.

## 4. Rúbrica

Factores por nivel I/II/III/IV: 0.40 / 0.70 / 0.90 / 1.00. Sin evidencia: 0.

- **Omisión menor:** falta una etiqueta o explicación que no altera algoritmo, condiciones, reproducibilidad ni resultados.
- **Error de fondo:** cualquier falla que cambie esos elementos o su interpretación (nivel II o I).

### B1 · 70 puntos · Ciclo funcional y modificación justificada

| Nivel | Descriptor |
|---|---|
| IV (70) | Ciclo completo de la variante con población constante, dominios válidos y mejor individuo protegido; se identifica la función de cada paso y se justifica una modificación sustantiva a partir de una limitación y una hipótesis explícitas. |
| III (63) | Ciclo completo con población constante, genes válidos y élite protegida; cambio pertinente con una omisión menor en justificación o explicación. |
| II (49) | Solo la base sin modificación sustantiva, o un cambio con falla relevante en selección, cruza, mutación, reemplazo o elitismo. |
| I (28) | Operadores aislados o ciclo que no produce una población siguiente utilizable. |
| 0 | Sin código ni explicaciones evaluables. |

Si solo se ejecuta la base: máximo nivel II.

### B2 · 30 puntos · Reproducción y comparación controlada

| Nivel | Descriptor |
|---|---|
| IV (30) | Ambas versiones ejecutadas y repetidas desde el inicio con entorno y semilla explícitos; comparación controlada; se interpretan genes, volúmenes, aptitud y factibilidad; se explica el apoyo o falta de apoyo a la hipótesis y el límite de una sola semilla. |
| III (27) | Ambas versiones reproducidas con entorno, semilla y condiciones explícitos; comparación correcta con una omisión menor. |
| II (21) | Solo una versión, dependencia de estados no documentados, condiciones mezcladas o resultados sin vínculo con genes, volúmenes y factibilidad. |
| I (12) | Salidas sin configuración identificable ni ejecución completa. |
| 0 | Sin ejecuciones ni resultados evaluables. |

Si solo hay una versión ejecutada: máximo nivel II. Una base repetida con nombre de variante sigue siendo una sola versión.

## 5. Continuidad con Final (resumen)

Cierre: 19 de octubre de 2026, 16:10. Peso 30 %. Criterios C1/C2/C3 de 40/35/25 puntos.

1. C1: explicar una generación siguiendo candidatos concretos de padres a reemplazo, por qué menor aptitud es mejor y cómo se protege la élite.
2. C2: comparar $p_m = 0.25$ y $p_m = 0.50$ del mismo código (20 individuos, 20 generaciones, semilla 42), con gráfica de la mejor aptitud.
3. C3: interpretar la asignación física (fracciones, volúmenes por edificio, capacidad, supuestos y alcance mensual).

## 6. Lista de comprobación

- [ ] Conservar formulación y cálculo manual de Investigación.
- [ ] Identificar base, variante y el único operador modificado.
- [ ] Explicar limitación, hipótesis y relación con la búsqueda.
- [ ] Ejecutar cada versión desde el inicio con semilla 42 y repetir resultados.
- [ ] Verificar tamaño de población, dominios y protección de la élite.
- [ ] Presentar ambos cromosomas finales, $T$, $P$, $F$, $E$ y factibilidad.
- [ ] Interpretar la comparación y el alcance de una sola semilla.
- [ ] Conservar código, salidas, conclusiones y rotación del equipo.
- [ ] Entregar libreta, `pyproject.toml` y `uv.lock`.

## 7. Restricciones del equipo

- Código lo más sencillo posible: solo NumPy y Matplotlib (las del `pyproject.toml`).
- No modificar las celdas de la base; agregar celdas nuevas.
- Explicaciones en español y con palabras sencillas.
