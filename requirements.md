# Reto Planta Física - Desarrollo

Lo que hay que hacer (de la rúbrica 02-desarrollo-instrucciones-rubrica.pdf):

- Usar el algoritmo genético base del notebook reto_planta.ipynb y hacer una variante cambiando un solo operador (selección, cruza o mutación).
- Explicar la limitación del operador, la hipótesis y por qué esperamos que mejore.
- Correr base y variante con 20 individuos, 20 generaciones, mutación 0.25 por gen y semilla 42, cada una desde el inicio.
- No cambiar el problema: 4 genes enteros (Aulas 1, Biblioteca y Aulas 2 de 0 a 8, Cedetec de 0 a 6), fracción k/10 y capacidad de 1410 m3.
- Aptitud: F = P/2276.21 si T <= 1410 y F = 1 + E/1410 si se pasa. Menor F es mejor.
- Comparar en una tabla: cromosoma final, T, P, F, E y si cumple dominios y capacidad.
- Revisar que la población siempre sea de 20, que los genes sean válidos y que la élite se conserve.
- Repetir las dos corridas y ver que salga lo mismo.
- Interpretar el resultado aunque la variante salga igual o peor, y decir el límite de usar una sola semilla.
- Entregar el notebook con salidas, pyproject.toml y uv.lock.

Calificación: B1 ciclo y modificación justificada (70 pts) y B2 reproducción y comparación (30 pts).

Usar solo numpy y matplotlib y código sencillo.
