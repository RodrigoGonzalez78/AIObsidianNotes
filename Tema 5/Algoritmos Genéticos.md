### 1. Introducción y Concepto Fundamental

Los Algoritmos Genéticos son una técnica de búsqueda y optimización inspirada en la selección natural de Darwin. La premisa central es que el azar en la variación, combinado con la selección de los más aptos, es una herramienta poderosa para resolver problemas complejos.
- **Analogía Biológica:** Se crean simulaciones donde individuos (soluciones candidatas) compiten en un entorno hostil. Solo los que tienen mejores características sobreviven lo suficiente para reproducirse, transmitiendo sus rasgos positivos y generando una paulatina adaptación al medio.
- **Proceso Básico:** Se parte de una población inicial (generalmente aleatoria para evitar sesgos). Se evalúa cada individuo con una función de aptitud (_fitness_). Los mejores se seleccionan y se cruzan (reproducción sexual) o mutan (cambios aleatorios) para crear una nueva generación. Este ciclo se repite hasta encontrar una solución satisfactoria.

### 2. Historia de la Computación Evolutiva

El desarrollo de los AG no fue lineal, sino que surgió de varias corrientes independientes:
- **Años 50 y 60 (Los Precursores):** Biólogos evolutivos comenzaron a simular la evolución en computadoras. En 1962, investigadores como G.E.P. Box y G.J. Friedman desarrollaron algoritmos inspirados en la evolución para optimización, aunque tuvieron poco impacto inicial.
- **1965 - Estrategia Evolutiva (Ingo Rechenberg):** Introdujo una técnica donde un "padre" mutaba para producir un descendiente. Se conservaba el mejor de los dos. No había población ni cruzamiento, pareciéndose más a un algoritmo de "ascenso de colina" (_hill climbing_).
- **1966 - Programación Evolutiva (Fogel, Owens y Walsh):** Representaban soluciones como máquinas de estado finito. Al igual que Rechenberg, usaban mutación y selección, pero ignoraban el cruzamiento.
- **1975 - El Hito de John Holland:** Su libro _"Adaptation in Natural and Artificial Systems"_ es la piedra angular de los AG. Fue el primero en sistematizar el uso de **mutación, selección y cruzamiento** (recombinación) de forma conjunta. Introdujo el concepto de "esquema" para dar una base teórica sólida.
- **La Tesis de Kenneth De Jong (1975):** Demostró el potencial práctico de los AG en funciones de prueba con paisajes de optimización ruidosos y discontinuos.

### 3. Formalización Matemática

Desde un punto de vista formal, un AG busca resolver un Problema de Optimización:

Dado un dominio $D$ y una función $f: D \rightarrow \mathbb{R}$, se busca encontrar un elemento $x^* \in D$ tal que $f(x^*)$ sea el mínimo (o máximo) global.
- **Codificación:** El AG no trabaja directamente sobre $D$, sino sobre una representación codificada (genotipo), habitualmente binaria. Se define una función inyectiva $e: D \rightarrow S^k$ (donde $S$ es el alfabeto, e.j., $\{0,1\}$).
- **Función Objetivo:** El algoritmo optimiza la función $g = f \circ e^{-1}$ sobre el espacio de búsqueda.
- **Paisaje de Fitness:** Se visualiza como un terreno con picos (óptimos) y valles. La dificultad radica en evitar quedarse atrapado en **óptimos locales** (picos falsos que son mejores que sus vecinos inmediatos pero peores que la solución real).
    

### 4. Métodos de Selección (Detallados)

La selección determina qué individuos pasan sus genes a la siguiente generación. Existen diversas estrategias:

1. **Selección Elitista:** Garantiza que el mejor (o los mejores) individuos de la generación actual pasen intactos a la siguiente. Evita que la solución óptima se pierda por azar.
2. **Proporcional a la Aptitud (Rueda de Ruleta):** La probabilidad de ser elegido es proporcional al _fitness_. Si un individuo es el doble de bueno que otro, tiene el doble de probabilidades de ser padre.
3. **Selección Escalada:** A medida que la población mejora, las diferencias de aptitud se reducen. Este método "escala" o exagera esas pequeñas diferencias para mantener la presión selectiva y evitar el estancamiento.
4. **Selección por Torneo:** Se eligen subgrupos aleatorios de individuos que compiten entre sí. El mejor de cada subgrupo gana el derecho a reproducirse. Es eficiente y fácil de implementar.
5. **Selección por Rango:** Se ignora el valor numérico exacto del fitness y se usa el orden (ranking). Esto evita que un "super-individuo" domine la población prematuramente al inicio (lo que reduciría la diversidad).
    

### 5. Reproducción y Mutación: El Motor de Búsqueda

- **Cruzamiento (Crossover):** Es el operador principal. Combina partes de dos padres para crear hijos. Su poder radica en que permite probar nuevas combinaciones de "bloques de construcción" (esquemas) exitosos.
- **Mutación:** Introduce cambios aleatorios pequeños en el código genético. Su función vital es mantener la **diversidad genética** y evitar que el algoritmo quede atrapado irremediablemente en un óptimo local.
- **Paralelismo Implícito:** Una de las grandes ventajas teóricas. Al evaluar un solo individuo, el AG está, en realidad, muestreando y obteniendo información sobre muchos hiperplanos (patrones de bits) simultáneamente.

### 6. Desventajas y Limitaciones Críticas

Aunque poderosos, los AG no son una bala de plata:
- **Costo Computacional:** Si la función de evaluación es compleja (e.j., requiere una simulación física lenta), el AG puede ser inviable por el tiempo que tarda en evaluar miles de individuos.
- **Convergencia Prematura:** A veces, la población se vuelve demasiado similar muy rápido, convergiendo a un óptimo local y perdiendo la capacidad de encontrar el óptimo global.
- **Escalabilidad:** Funcionan peor a medida que aumenta la complejidad y el número de variables, especialmente si hay relaciones no lineales intrincadas entre ellas (el espacio de búsqueda crece exponencialmente).
- **Falta de Criterio de Parada Claro:** Como no se conoce la solución perfecta de antemano, es difícil saber cuándo el algoritmo ha encontrado la "mejor" solución posible o si solo está estancado.
- **Caja Negra:** Es difícil entender _por qué_ una solución es buena o cómo llegó el algoritmo a ella. Además, configurar los parámetros (tasa de mutación, tamaño de población) requiere mucha pericia y "arte".


https://www.cs.us.es/~fsancho/Blog/posts/Algoritmos_Geneticos.md.html

