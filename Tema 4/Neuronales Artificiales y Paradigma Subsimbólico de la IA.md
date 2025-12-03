### 1. El Paradigma Subsimbólico y las RNA

Las Redes Neuronales Artificiales (RNA) son modelos bioinspirados diseñados para simular el aprendizaje y conocimiento humano.

- **Características Clave:**
    - **Aprendizaje adaptativo:** Requieren patrones de entrenamiento y algoritmos para ajustar su comportamiento .
    - **Auto-organización:** Permite la generalización de la información.
    - **Tolerancia a fallos:** Pueden aprender de patrones con ruido, distorsión o incompletos.
    - **Operación en tiempo real:** Capacidad para procesar grandes volúmenes de datos.
- **Fundamento Teórico:** Se basa en la propuesta de **Donald Hebb**, quien postuló que el aprendizaje es el resultado del fortalecimiento de las conexiones sinápticas entre neuronas que se activan simultáneamente.
    

---

### 2. La Neurona: Biológica vs. Artificial

El documento establece una analogía directa entre la biología y el modelo computacional.

- **Estructura:**
    - **Entradas ($X_n$):** equivalen a las **dendritas** (recepción de señales).
    - **Pesos ($W_n$):** equivalen a las **sinapsis**. Determinan la intensidad o importancia de la conexión. Son la memoria a largo plazo de la red
    - **Función de Agregación ($\Sigma$):** equivale al **cuerpo celular** (soma). Realiza una suma ponderada de las entradas ($z = \sum x_i \cdot w_i$) .
    - **Función de Activación ($f$):** Decide si la neurona se dispara, simulando el potencial de acción.
    - **Salida ($Y$):** equivale al **axón** (transmisión de señales).
---

### 3. Aprendizaje y Conocimiento

En las RNA, el aprendizaje se define como el proceso de ajustar los pesos de las conexiones para almacenar información.

- **Tipos de Aprendizaje:**
    - **Supervisado:** Dirigido por tareas (clasificación/regresión) con datos etiquetados.
    - **No Supervisado:** Dirigido por datos (clustering/segmentación) para encontrar patrones ocultos.
    - **Semisupervisado:** Combina datos etiquetados y no etiquetados.
    - **Por Refuerzo:** El algoritmo aprende a reaccionar al ambiente mediante recompensas.

---

### 4. Arquitectura y Topología

La arquitectura define cómo se interconectan las neuronas y se organizan en capas.

- **Capas:**
    - **Capa de Entrada:** Interfaz con el mundo real, no realiza cálculos.
    - **Capas Ocultas:** Procesan la información entre la entrada y la salida.
    - **Capa de Salida:** Proporciona el resultado final.
- **Clasificación por Conexiones:**
    - **Feedforward (Hacia adelante):** Unidireccional, sin ciclos. Típico del Perceptrón Multicapa (MLP).
    - **Recurrentes:** Tienen retroalimentación (feedback). Tienen "memoria" y son útiles para reconocimiento de voz (ej. Red de Hopfield).
    - **Totalmente vs. Parcialmente Conectadas:** Depende de si todas las neuronas de una capa se unen con todas las de la siguiente.
        

---

### 5. Funciones de Activación

Limitan el rango de amplitud de la salida de la neurona (usualmente a $[0, 1]$ o $[-1, 1]$) e introducen no linealidad.
- **Umbral / Escalón:** Salida binaria (0 o 1). Útil para clasificación simple.
![[Pasted image 20251202163525.png]]
- **Lineal:** No limita la respuesta. Usada en aproximación o regresión.
- **Logística (Sigmoide):** Continua en $[0, 1]$. Diferenciable.

![[Pasted image 20251202163008.png]]
- **Tangente Hiperbólica:** Continua en $[-1, 1]$. Propiedades analíticas importantes.
![[Pasted image 20251202163111.png]]
- **ReLU (Rectified Linear Unit):** Opción por defecto en aprendizaje profundo (Deep Learning) y redes convolucionales (CNN) por su simplicidad de cálculo .
![[Pasted image 20251202163152.png]]
- **SoftMax:** Generalización de la logística para clasificación multiclase (convierte valores en probabilidades).
- ![[Pasted image 20251202163857.png]]

---

### 6. Algoritmos de Aprendizaje y Optimización

- **Backpropagation (Retropropagación):** Algoritmo estándar.
    1. **Fase hacia adelante:** Calcula la salida de la red (señales funcionales).
    2. **Fase hacia atrás:** Calcula el error desde la salida y lo propaga hacia las capas anteriores para ajustar los pesos (señales de error).
- **Descenso del Gradiente:** Algoritmo de optimización para encontrar el mínimo de la función de error. Utiliza una **Tasa de Aprendizaje** (learning rate) para determinar el tamaño del paso.
    - _Variantes:_ Estocástico (SGD), Adam, RMSProp .
- **Generalización vs. Sobreajuste (Overfitting):**
    - Se busca que la red generalice (funcione bien con datos nuevos) y no solo memorice los datos de entrenamiento (sobreajuste).
    - El sobreajuste ocurre cuando la red se ajusta demasiado a los datos de entrenamiento, perdiendo la capacidad de interpolar correctamente.

https://www.geeksforgeeks.org/machine-learning/neural-networks-a-beginners-guide/ 
https://www.datacamp.com/es/tutorial/what-is-a-confusion-matrix-in-machine-learning

![[Pasted image 20251125164019.png]]

### 1. El Concepto Básico: "Pérdida" (Loss)

Imagina que eres un arquero tirando flechas a una diana.

- El centro de la diana es el **Valor Real**.
- Donde cae tu flecha es el **Valor Predicho**.
- La distancia entre ambos es el **Error**.
La "Función de Pérdida" es simplemente una forma matemática de sumar todos esos errores para darle una "calificación" a tu puntería. Si la pérdida es baja, tu modelo es bueno. Si es alta, es malo.

---

### 2. Familia 1: Los "Absolutos" (L1 y MAE)

Aquí nos importa la distancia directa, sin trucos.

- **Pérdida L1 (Suma de Errores Absolutos):**
    - _¿Qué es?_ Simplemente mides la distancia de cada error y las sumas todas. Usamos el "valor absoluto" ($|...|$) porque no importa si te pasaste por arriba o por abajo, el error sigue siendo un error positivo.
    - _Ejemplo:_ Te equivocaste por 5 en una, y por 3 en otra. Pérdida total = 8.
- **MAE (Error Absoluto Medio):**
    - _¿Qué es?_ Es el **promedio** de la L1. Divide la suma total entre el número de ejemplos ($N$).
    - _Intuición:_ Te dice, en promedio, por cuánto te estás equivocando. "Mi modelo de predicción de precios de casas se equivoca, en promedio, por $5,000 dólares". Es muy fácil de interpretar para humanos.

---

### 3. Familia 2: Los "Cuadráticos" (L2 y MSE)

Aquí es donde la cosa cambia. En lugar de sumar la distancia, **elevamos la distancia al cuadrado** antes de sumar.

- **Pérdida L2 (Suma de Errores al Cuadrado):**
    - _¿Qué es?_ Tomas la diferencia y la multiplicas por sí misma.
    - _¿Por qué haríamos esto?_ Para **castigar los errores grandes**.
    - _Ejemplo:_
        - Si tu error es 2, el castigo es $2^2 = 4$.
        - Si tu error es 10, el castigo es $10^2 = 100$.
    - Nota cómo el error solo creció 5 veces (de 2 a 10), pero el castigo creció 25 veces (de 4 a 100). A L2 no le gustan nada los errores grandes.
        
- **ECM / MSE (Error Cuadrático Medio):**
    
    - _¿Qué es?_ Es el **promedio** de la L2.
    - _Problema:_ Como elevaste al cuadrado, las unidades cambian. Si predecías "dólares", ahora tienes "dólares cuadrados". Es difícil de interpretar intuitivamente.

---

### 4. El Puente: RMSE (Raíz del Error Cuadrático Medio)

- **RMSE:**
    
    - _¿Qué es?_ A la fórmula anterior (MSE) le aplicamos una raíz cuadrada al final.
    - _¿Para qué?_ Para volver a las unidades originales. Si el MSE estaba en "dólares cuadrados", el RMSE vuelve a estar en "dólares".
    - _Ventaja:_ Mantiene la propiedad de "castigar" severamente los errores grandes (porque viene del MSE), pero el resultado final es un número que puedes entender (como el MAE).

---

### Resumen: ¿Cuál debo usar?

|**Métrica**|**¿Cuándo usarla?**|**¿Cómo se comporta con "Valores Atípicos" (Outliers)?**|
|---|---|---|
|**MAE (L1)**|Cuando quieres una interpretación simple del error promedio.|**Robusto:** Ignora un poco los datos locos o errores puntuales muy grandes.|
|**MSE (L2)**|Cuando es crítico **no cometer errores grandes**.|**Sensible:** Un solo error grande inflará mucho este número.|
|**RMSE**|Cuando quieres penalizar errores grandes pero necesitas que el resultado sea legible en las unidades originales.|**Sensible:** Igual que el MSE, pero más fácil de leer.|

## Métricas de clasificacion
### 1. La Base: Matriz de Confusión (Confusion Matrix)

Antes de ver las fórmulas, necesitamos entender los cuatro posibles resultados de una predicción. Imagina un modelo médico que predice si un paciente tiene una enfermedad (**Positivo**) o está sano (**Negativo**).
![[Pasted image 20251202122019.png]]
https://developers.google.com/machine-learning/crash-course/classification/thresholding?hl=es-419

- **Verdaderos Positivos (TP):** El paciente está enfermo y el modelo dijo "Enfermo". (Acierto)
- **Verdaderos Negativos (TN):** El paciente está sano y el modelo dijo "Sano". (Acierto)
- **Falsos Positivos (FP):** El paciente está sano, pero el modelo dijo "Enfermo". (Alarma falsa / Error Tipo I)
- **Falsos Negativos (FN):** El paciente está enfermo, pero el modelo dijo "Sano". (Caso perdido / Error Tipo II)
---
### 2. Las Métricas Clave

A partir de esos cuatro valores, calculamos las métricas.
#### A. Exactitud (Accuracy)

Es la métrica más intuitiva: ¿Qué porcentaje de las veces tuvo razón el modelo?
$$Accuracy = \frac{TP + TN}{TP + TN + FP + FN}$$
- **Cuándo usarla:** Cuando tus clases están **balanceadas** (tienes la misma cantidad de ejemplos positivos y negativos).
- **Trampa:** Si tienes 95 pacientes sanos y 5 enfermos, un modelo que diga siempre "Sano" tendrá 95% de accuracy, pero es inútil para detectar la enfermedad. Aquí falla la exactitud.
#### B. Precisión (Precision)

Responde a: **"De todos los que el modelo etiquetó como positivos, ¿cuántos lo eran realmente?"**

$$Precision = \frac{TP}{TP + FP}$$

- **Enfoque:** Calidad de la predicción positiva.
- **Ejemplo:** En un **filtro de Spam**. Quieres estar muy seguro de que si clasificas un correo como spam, realmente lo sea. No quieres borrar un correo importante de trabajo por error (Falso Positivo). Aquí buscas alta Precisión.
#### C. Sensibilidad o Exhaustividad (Recall)

Responde a: **"De todos los casos positivos reales que existen, ¿cuántos fue capaz de encontrar el modelo?"**
$$Recall = \frac{TP}{TP + FN}$$

- **Enfoque:** Cantidad de positivos encontrados.
- **Ejemplo:** En **detección de cáncer** o **fraude bancario**. Prefieres tener algunas falsas alarmas (baja precisión) con tal de detectar a _todas_ las personas enfermas o transacciones fraudulentas. Un Falso Negativo aquí es muy peligroso.
#### D. F1-Score

Es la media armónica entre Precisión y Recall. Combina ambas en un solo número.

$$F1 = 2 \cdot \frac{Precision \cdot Recall}{Precision + Recall}$$

- **Cuándo usarla:** Es ideal cuando necesitas un equilibrio entre Precisión y Recall, o cuando tus datos están **desbalanceados**.
---
### 3. Resumen Comparativo

|**Métrica**|**Pregunta clave**|**Usar cuando...**|
|---|---|---|
|**Accuracy**|¿Cuánto acierta en total?|Las clases están balanceadas (50/50).|
|**Precision**|¿Qué tan confiable es el positivo?|Los Falsos Positivos son costosos (ej. Spam).|
|**Recall**|¿Cuántos positivos encontró?|Los Falsos Negativos son peligrosos (ej. Medicina).|
|**F1-Score**|¿Cuál es el balance general?|Las clases están desbalanceadas.|

---
### 4. Curva ROC y AUC

Finalmente, para modelos que dan probabilidades (como una regresión logística), usamos la curva ROC.

![Imagen de ROC curve interpretation](https://encrypted-tbn3.gstatic.com/licensed-image?q=tbn:ANd9GcQIPpCKbPcmG8ffnn3UbBzfAJrpjQmSBZjv8z8VKJfk4Lwn6mkKXzu78WikY4XKpQ0zUdwXLf2U8g2k4ufox-m2hFfwi2kD01Er7VdldME2ccnCMf4)

- **Curva ROC:** Gráfica que enfrenta la tasa de Verdaderos Positivos (Recall) contra la tasa de Falsos Positivos.
- **AUC (Area Under Curve):** Es el área bajo esa curva.
    - **0.5:** El modelo adivina al azar (malo).
    - **1.0:** El modelo es perfecto.
    - Generalmente, un AUC > 0.8 se considera bueno.

## Hiperparametros
### 1. Tasa de Aprendizaje (Learning Rate)

La [**tasa de aprendizaje**](https://developers.google.com/machine-learning/glossary?hl=es-419#learning-rate) es un número de punto flotante que estableces y que influye en la rapidez con la que converge el modelo. Si la tasa de aprendizaje es demasiado baja, el modelo puede tardar mucho en converger. Sin embargo, si la tasa de aprendizaje es demasiado alta, el modelo nunca converge, sino que oscila entre los pesos y la ordenada al origen que minimizan la pérdida. El objetivo es elegir una tasa de aprendizaje que no sea demasiado alta ni demasiado baja para que el modelo converja rápidamente.
La tasa de aprendizaje determina la magnitud de los cambios que se deben realizar en los pesos y el sesgo durante cada paso del proceso de descenso de gradientes. El modelo multiplica el gradiente por la tasa de aprendizaje para determinar los parámetros del modelo (valores de peso y sesgo) para la siguiente iteración. En el tercer paso del [descenso del gradiente](https://developers.google.com/machine-learning/crash-course/linear-regression/gradient-descent?hl=es-419), la "pequeña cantidad" que se debe mover en la dirección de la pendiente negativa se refiere a la tasa de aprendizaje.

Imagina que estás en la cima de una montaña a oscuras y quieres bajar al punto más bajo (el error mínimo).

- **Learning Rate Alto (Pasos gigantes):** Bajas muy rápido, pero corres el riesgo de pasarte del punto más bajo y saltar al otro lado del valle. El modelo se vuelve inestable y nunca converge.
- **Learning Rate Bajo (Pasos de bebé):** Es seguro y preciso, pero tardarás una eternidad en llegar abajo. Además, podrías quedarte atascado en un pequeño hueco que no es el punto más bajo real (mínimo local).
- **Learning Rate Ideal:** Pasos lo suficientemente grandes para avanzar rápido, pero lo suficientemente pequeños para aterrizar suavemente en el mínimo.

> **Nota:** Un valor común para empezar es $0.01$ o $0.001$, pero depende mucho del problema.

---

### 2. Tamaño del Lote (Batch Size)

El [**tamaño del lote**](https://developers.google.com/machine-learning/glossary?hl=es-419#batch-size) es un hiperparámetro que hace referencia a la cantidad de [**ejemplos**](https://developers.google.com/machine-learning/glossary?hl=es-419#example) que el modelo procesa antes de actualizar sus pesos y sesgos. Es posible que pienses que el modelo debería calcular la pérdida para _cada_ ejemplo del conjunto de datos antes de actualizar los pesos y la desviación. Sin embargo, cuando un conjunto de datos contiene cientos de miles o incluso millones de ejemplos, no es práctico usar el lote completo.

- **Descenso de gradientes estocástico (SGD)**: El descenso de gradientes estocástico usa solo un ejemplo (un tamaño de lote de uno) por iteración. Cuando se dan demasiadas iteraciones, el SGD funciona, pero es muy ruidoso. El "ruido" hace referencia a las variaciones durante el entrenamiento que hacen que la pérdida aumente en lugar de disminuir durante una iteración. El término "estocástico" indica que el ejemplo que comprende cada lote se elige de forma aleatoria.
![[Pasted image 20251202124228.png]]
- **Descenso de gradientes estocástico de minilote (SGD de minilote)**: El descenso de gradientes estocástico de minilote es un equilibrio entre el lote completo y el SGD. Para una cantidad de  de datos, el tamaño del lote puede ser cualquier número mayor que 1 y menor que . El modelo elige los ejemplos incluidos en cada lote de forma aleatoria, calcula el promedio de sus gradientes y, luego, actualiza los pesos y el sesgo una vez por iteración.    
![[Pasted image 20251202124322.png]]

![[Pasted image 20251202124044.png]]
https://developers.google.com/machine-learning/crash-course/linear-regression/hyperparameters?hl=es-419
---

### 3. Épocas (Epochs)

Una **época** ocurre cuando el modelo ha visto **el set de datos completo una vez**.
Como usamos _batches_, una época se compone de varios pasos (iteraciones).
- _Ejemplo:_ Si tienes 1000 datos y un Batch Size de 100.
- El modelo necesita **10 pasos** (iteraciones) para completar **1 época**.

Si pones **pocas épocas**, el modelo no termina de aprender (Underfitting). Si pones **demasiadas**, el modelo se aprende los datos de memoria y deja de generalizar (Overfitting).

---

### Resumen de la relación

Para visualizarlo, imagina que estás aprendiendo a tocar una canción:

1. **Batch Size:** ¿Practicas compás por compás (pequeño) o tocas la canción entera antes de corregir errores (grande)?
2. **Learning Rate:** ¿Haces cambios drásticos en tu forma de poner los dedos (alto) o haces ajustes milimétricos (bajo)?
3. **Epochs:** ¿Cuántas veces repites la canción completa durante la semana?

### Tabla de Ajuste Rápido

|**Hiperparámetro**|**Si es muy bajo...**|**Si es muy alto...**|
|---|---|---|
|**Learning Rate**|El entrenamiento es eterno.|El error explota o nunca baja.|
|**Batch Size**|El entrenamiento es ruidoso y lento.|Falta de memoria (OOM) o generaliza peor.|
|**Épocas**|El modelo no aprende nada (Underfitting).|El modelo memoriza todo (Overfitting).|



https://cs231n.github.io/neural-networks-3/#update