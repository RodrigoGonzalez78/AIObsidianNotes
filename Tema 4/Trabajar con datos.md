## Datos numéricos: Normalización

Después de examinar tus datos con técnicas estadísticas y de visualización, debes transformarlos de manera que ayuden a tu modelo a entrenarse de forma más eficaz. El objetivo de la [**normalización**](https://developers.google.com/machine-learning/glossary?hl=es-419#normalization) es transformar las características para que estén en una escala similar. 

### Escalamiento lineal

El **[escalamiento lineal](https://developers.google.com/machine-learning/glossary?hl=es-419#scaling)** (más comúnmente abreviado como **escalamiento**) significa convertir los valores de punto flotante de su rango natural a un rango estándar, generalmente de 0 a 1 o de -1 a +1.

### Ajuste de la puntuación Z

Una **puntuación Z** es la cantidad de desviaciones estándar que tiene un valor a partir de la media. Por ejemplo, un valor que es 2 desviaciones estándar _mayor_ que la media tiene una puntuación Z de +2.0. Un valor que es 1.5 desviaciones estándar _menor_ que la media tiene una puntuación Z de -1.5.
![[Pasted image 20251202152831.png]]
### Escalamiento logarítmico

El ajuste de escala logarítmica calcula el logaritmo del valor sin procesar. En teoría, el logaritmo podría tener cualquier base; en la práctica, el ajuste logarítmico suele calcular el logaritmo natural (ln).
![[Pasted image 20251202152809.png]]

### Recorte

El [**recorte**](https://developers.google.com/machine-learning/glossary?hl=es-419#clipping) es una técnica para minimizar la influencia de los valores atípicos extremos. En resumen, el recorte suele limitar (reducir) el valor de los valores atípicos a un valor máximo específico. El recorte es una idea extraña y, sin embargo, puede ser muy eficaz.

Por ejemplo, imagina un conjunto de datos que contiene un atributo llamado `roomsPerPerson`, que representa la cantidad de habitaciones (habitaciones totales divididas por la cantidad de ocupantes) de varias casas. En el siguiente gráfico, se muestra que más del 99% de los valores de los atributos se ajustan a una distribución normal (aproximadamente, una media de 1.8 y una desviación estándar de 0.7). Sin embargo, la función contiene algunos valores atípicos, algunos de ellos extremos:
![[Pasted image 20251202152658.png]]
¿Cómo puedes minimizar la influencia de esos valores atípicos extremos? Bueno, el histograma no es una distribución uniforme, una distribución normal ni una distribución de ley de potencia. ¿Qué sucede si simplemente _limitas_ o _recortas_ el valor máximo de `roomsPerPerson` en un valor arbitrario, por ejemplo, 4.0?
![[Pasted image 20251202152747.png]]



![[Pasted image 20251202152223.png]]


Datos numéricos: discretización

