<link rel="stylesheet" type="text/css" href="styles.css">
<link rel="stylesheet" href="github-markdown.css">
<script src="https://cdn.jsdelivr.net/npm/katex/dist/katex.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/katex/dist/contrib/auto-render.min.js" onload="renderMathInElement(document.body);"></script>
<div class="container">


<div class="header">
  <h1>Cross-Validation</h1>
  <h3>P25 LDS1051 1: Reconocimiento de Patrones</h3>
  <p>24 de Enero de 2025</p>
</div



  <div class="bubble right">
explicame que es cross-validation


  </div class="bubble right">
  <div class="bubble left">

**Cross-validation** es una técnica estadística utilizada principalmente en **aprendizaje automático** y **modelos predictivos** para evaluar el rendimiento de un modelo y medir su capacidad de generalización. Es decir, ayuda a estimar qué tan bien funcionará un modelo cuando se enfrente a datos nuevos que no se usaron durante su entrenamiento.

El objetivo de cross-validation es reducir el **sesgo** y la **varianza** en la evaluación del modelo y obtener un resultado más confiable sobre su desempeño.






  </div class="bubble left">
  <div class="bubble left">

 **¿Cómo funciona?**
1. **División de los datos**: El conjunto de datos se divide en varias partes o subconjuntos llamados **folds**.
2. **Entrenamiento y validación**:
   - Se entrena el modelo en algunos de los folds (conocidos como el conjunto de **entrenamiento**) y se evalúa en el fold restante (conjunto de **validación**).
   - Este proceso se repite varias veces, utilizando diferentes combinaciones de folds como entrenamiento y validación.
3. **Promedio de resultados**: Finalmente, los resultados de las evaluaciones (por ejemplo, precisión, error, etc.) se promedian para obtener una estimación global del rendimiento del modelo.






  </div class="bubble left">
  <div class="bubble left">

 **Tipos de Cross-Validation**
1. **K-Fold Cross-Validation**: 
   - El conjunto de datos se divide en **K** partes de tamaño similar.
   - El modelo se entrena en **K-1 folds** y se valida en el fold restante.
   - Este proceso se repite **K veces**, cambiando el fold de validación en cada iteración.
   - Ejemplo: Si tienes un dataset con 100 observaciones y eliges $ K = 5 $, cada fold tendrá 20 observaciones, y el modelo se entrenará en 80 datos y se evaluará en 20, alternando el fold de validación.

2. **Leave-One-Out Cross-Validation (LOOCV)**:
   - Cada observación del conjunto de datos se utiliza una vez como conjunto de validación, mientras que el resto se usa para entrenar el modelo.
   - Es un caso extremo de K-Fold donde $ K = N $ (siendo $ N $ el número de datos).
   - Es computacionalmente costoso para datasets grandes.

3. **Stratified K-Fold Cross-Validation**:
   - Similar a K-Fold, pero asegura que la proporción de clases (en problemas de clasificación) se mantenga en cada fold. Esto es útil cuando los datos están desbalanceados.

4. **Time Series Cross-Validation**:
   - Diseñado específicamente para datos secuenciales o de series temporales.
   - Divide los datos respetando el orden temporal (no se mezcla información futura con la del pasado).






  </div class="bubble left">
  <div class="bubble left">

 **Ventajas del Cross-Validation**
- Proporciona una mejor estimación de la capacidad de generalización de un modelo.
- Ayuda a prevenir el **overfitting** (ajuste excesivo) al usar datos de validación diferentes en cada iteración.
- No desperdicia datos, ya que cada observación se usa tanto para entrenamiento como para validación.






  </div class="bubble left">
  <div class="bubble left">

 **Desventajas**
- Puede ser computacionalmente costoso, especialmente con datasets grandes o modelos complejos.
- Si el dataset tiene alta varianza, puede haber fluctuaciones significativas entre los resultados de cada fold.







  </div class="bubble left">
  <div class="bubble right">
que son los folds? 


  </div class="bubble right">
  <div class="bubble left">

Los **folds** son divisiones o particiones del conjunto de datos que se crean durante el proceso de **cross-validation**. Cada fold es un subconjunto del dataset original que se utiliza de manera estratégica para entrenar y validar un modelo. 

La idea es dividir los datos en varias partes (generalmente de tamaño similar) y alternar entre cuáles se usan para entrenamiento y cuáles para validación.






  </div class="bubble left">
  <div class="bubble left">

 **¿Cómo funcionan los folds en Cross-Validation?**
1. Supongamos que tienes un dataset con 100 observaciones.
2. Si decides realizar una **K-Fold Cross-Validation** con $K = 5$:
   - Se dividirá el dataset en **5 folds** (subconjuntos) iguales, es decir, cada fold tendrá 20 observaciones.
   - En cada iteración:
     - **$K-1$** folds se usan para **entrenar** el modelo.
     - El fold restante se usa para **validar** el modelo.
   - Esto se repite $K$ veces (en este caso, 5), alternando cuál fold se usa como conjunto de validación.






  </div class="bubble left">
  <div class="bubble left">

 **Visualización de los folds**
Imagina que tienes un dataset con los índices de las observaciones representados del 1 al 10:



  </div class="bubble left">
  <div class="bubble left">

 **División en 5 folds:**
- Fold 1: [1, 2]
- Fold 2: [3, 4]
- Fold 3: [5, 6]
- Fold 4: [7, 8]
- Fold 5: [9, 10]



  </div class="bubble left">
  <div class="bubble left">

 **Iteraciones en el proceso de K-Fold:**
1. **Primera iteración**:  
   - Entrenamiento: [3, 4, 5, 6, 7, 8, 9, 10]  
   - Validación: [1, 2]

2. **Segunda iteración**:  
   - Entrenamiento: [1, 2, 5, 6, 7, 8, 9, 10]  
   - Validación: [3, 4]

3. **Tercera iteración**:  
   - Entrenamiento: [1, 2, 3, 4, 7, 8, 9, 10]  
   - Validación: [5, 6]

4. **Cuarta iteración**:  
   - Entrenamiento: [1, 2, 3, 4, 5, 6, 9, 10]  
   - Validación: [7, 8]

5. **Quinta iteración**:  
   - Entrenamiento: [1, 2, 3, 4, 5, 6, 7, 8]  
   - Validación: [9, 10]






  </div class="bubble left">
  <div class="bubble left">

 **¿Por qué son importantes los folds?**
- Los folds permiten garantizar que **todas las observaciones del dataset se utilicen tanto para entrenamiento como para validación** en algún momento.
- Ayudan a medir el desempeño del modelo de manera más robusta, ya que no dependemos de una única división del dataset (como sucede en una simple partición entrenamiento/validación).
- En problemas de clasificación, cuando se usa **Stratified K-Fold**, los folds también respetan la proporción de las clases, asegurando una evaluación más representativa.











  </div class="bubble left">
  <div class="bubble right">
luego de la iteracion de los folds, que te queda? 


  </div class="bubble right">
  <div class="bubble left">

Luego de realizar todas las iteraciones de los folds en un proceso de **cross-validation**, lo que te queda es un conjunto de **métricas de desempeño** (como precisión, error, recall, etc.) calculadas para cada fold durante las evaluaciones. Estas métricas representan cómo se comportó el modelo en cada iteración cuando se validó con un fold diferente.






  </div class="bubble left">
  <div class="bubble left">

 **¿Qué haces con estas métricas?**
1. **Promedias las métricas**:  
   - Una vez que tienes el desempeño del modelo en cada fold, tomas el promedio de esas métricas para obtener una medida general del rendimiento del modelo.  
   - Por ejemplo, si calculaste la **precisión** en 5 folds y obtuviste los siguientes valores:  
     $$
     \text{Precisión por fold: } 0.88, 0.85, 0.90, 0.87, 0.89
     $$
     El promedio sería:  
     $$
     \text{Precisión promedio: } 
     \\
     \frac{0.88 + 0.85 + 0.90 + 0.87 + 0.89}{5} = 0.878
     $$
     Este promedio te da una idea general de qué tan bien funciona el modelo.

2. **Calculas la desviación estándar**:  
   - También puedes calcular la **desviación estándar** de las métricas para ver qué tan consistente es el modelo.  
   - Si la desviación estándar es alta, significa que el modelo tiene un rendimiento inconsistente entre los folds, lo cual puede ser una señal de problemas como un dataset pequeño o desequilibrado.

3. **Usas el promedio para comparar modelos**:  
   - Si estás probando varios modelos o configuraciones (hiperparámetros), puedes comparar el desempeño promedio entre ellos para seleccionar el modelo más robusto.






  </div class="bubble left">
  <div class="bubble left">

 **¿Qué más te queda después de los folds?**
En términos de utilidad práctica, te quedan:
1. **El modelo entrenado en cada iteración**:  
   - Aunque generalmente no los conservas todos, en algunos casos puedes guardar el modelo final entrenado en la última iteración o uno que entrenes nuevamente usando **todos los datos**.

2. **El mejor modelo (opcional)**:  
   - Si estás utilizando cross-validation dentro de un proceso de búsqueda de hiperparámetros, puedes identificar la combinación de parámetros que maximiza el desempeño promedio.

3. **Una evaluación confiable**:  
   - El resultado del cross-validation es más confiable que evaluar el modelo en una única partición de datos. Esto te ayuda a tener mayor confianza en el rendimiento del modelo en datos nuevos.






  </div class="bubble left">
  <div class="bubble left">

 **Ejemplo práctico**
Imagina que estás probando un modelo de clasificación y utilizas 5-Fold Cross-Validation para calcular la precisión. Obtuviste:

- Fold 1: 0.90  
- Fold 2: 0.85  
- Fold 3: 0.88  
- Fold 4: 0.87  
- Fold 5: 0.89  

De aquí obtienes:
- **Precisión promedio**: $\frac{0.90 + 0.85 + 0.88 + 0.87 + 0.89}{5} = 0.878$  
- **Desviación estándar**: Mide la variabilidad entre los folds, lo que podría ser útil para evaluar la estabilidad del modelo.

En resumen, al finalizar el proceso de cross-validation, tienes una **evaluación más robusta** del rendimiento del modelo y, dependiendo del caso, un modelo final que puedes ajustar o usar para predicciones.








  </div class="bubble left">
  <div class="bubble right">
explicame las metricas, como precision, folds, recall, etc...


  </div class="bubble right">
  <div class="bubble left">
Las métricas de evaluación son herramientas esenciales en **aprendizaje automático** para medir el desempeño de un modelo predictivo. Estas métricas dependen del tipo de problema (clasificación, regresión, etc.) y ayudan a determinar qué tan bien funciona un modelo en diferentes aspectos. Vamos a explicarlas con un enfoque en problemas de clasificación, donde conceptos como **precisión (accuracy)**, **recall (sensibilidad)** y otras métricas son más comunes.






  </div class="bubble left">
  <div class="bubble left">

 **1. Métricas básicas en clasificación**
Estas métricas se basan en la **matriz de confusión**, que es un resumen de las predicciones de un modelo comparadas con los valores reales.



  </div class="bubble left">
  <div class="bubble left">

 **Matriz de confusión (para problemas binarios)**:
|                 | Predicción Positiva (1) | Predicción Negativa (0) |
|-----------------|--------------------------|--------------------------|
| **Clase Positiva (1)** | Verdaderos Positivos (**TP**) | Falsos Negativos (**FN**) |
| **Clase Negativa (0)** | Falsos Positivos (**FP**)     | Verdaderos Negativos (**TN**) |

- **TP (True Positives)**: Predicciones correctas de la clase positiva.  
- **FN (False Negatives)**: Errores donde la clase positiva fue predicha como negativa.  
- **FP (False Positives)**: Errores donde la clase negativa fue predicha como positiva.  
- **TN (True Negatives)**: Predicciones correctas de la clase negativa.






  </div class="bubble left">
  <div class="bubble left">

 **Métricas derivadas**:

1. **Precisión (Accuracy)**:
   - Mide el porcentaje de predicciones correctas (tanto positivas como negativas) sobre el total de observaciones.  
   - Fórmula:  
     $$
     \text{Precisión} = \frac{TP + TN}{TP + TN + FP + FN}
     $$
   - **Ejemplo**: Si tienes 80 predicciones correctas (TP+TN) de un total de 100 datos, la precisión es $ \frac{80}{100} = 0.8 $ o 80%.

   - **Limitación**: No es confiable si las clases están desbalanceadas. Por ejemplo, en un dataset donde el 95% son de la clase 0, un modelo que siempre predice 0 tendrá una precisión del 95%, pero no será útil.

  </div class="bubble left">
  <div class="bubble left">

2. **Precisión (Precision)**:
   - De todas las predicciones positivas que hizo el modelo, mide cuántas son correctas.  
   - Fórmula:  
     $$
     \text{Precision} = \frac{TP}{TP + FP}
     $$
   - **Ejemplo**: Si el modelo predijo 50 veces la clase positiva, pero solo 40 de esas fueron correctas, la precisión será $ \frac{40}{50} = 0.8 $.

   - **Uso**: Es importante cuando **el costo de un falso positivo es alto**. Por ejemplo, en detección de fraudes, prefieres tener menos falsos positivos.

  </div class="bubble left">
  <div class="bubble left">

3. **Recall (Sensibilidad o Tasa de Verdaderos Positivos)**:
   - Mide la capacidad del modelo para identificar correctamente los casos positivos.  
   - Fórmula:  
     $$
     \text{Recall} = \frac{TP}{TP + FN}
     $$
   - **Ejemplo**: Si hay 100 casos positivos reales y el modelo identificó 80 correctamente, el recall será $ \frac{80}{100} = 0.8 $.

   - **Uso**: Es crucial cuando quieres **minimizar los falsos negativos**, como en diagnósticos médicos.

  </div class="bubble left">
  <div class="bubble left">

4. **F1-Score**:
   - Es la **media armónica** entre precisión y recall. Se usa cuando buscas un balance entre ambos.  
   - Fórmula:  
     $$
     \text{F1} = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}
     $$
   - **Ejemplo**: Si la precisión es 0.8 y el recall es 0.9:
     $$
     \text{F1} = 2 \cdot \frac{0.8 \cdot 0.9}{0.8 + 0.9} = 0.85
     $$

   - **Uso**: Es útil cuando las clases están desbalanceadas y necesitas evaluar el modelo en términos de ambas métricas.

  </div class="bubble left">
  <div class="bubble left">

5. **Especificidad (Specificity o Tasa de Verdaderos Negativos)**:
   - Mide la capacidad del modelo para identificar correctamente los casos negativos.  
   - Fórmula:  
     $$
     \text{Especificidad} = \frac{TN}{TN + FP}
     $$






  </div class="bubble left">
  <div class="bubble left">

 **2. Métricas en regresión**
En problemas de regresión (donde el objetivo es predecir valores continuos), se usan métricas diferentes:

  </div class="bubble left">
  <div class="bubble left">

1. **Error Absoluto Medio (MAE)**:
   - Mide el error promedio absoluto entre las predicciones y los valores reales.  
   - Fórmula:  
     $$
     \text{MAE} = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|
     $$
   - **Uso**: Fácil de interpretar, pero no captura bien errores grandes.

  </div class="bubble left">
  <div class="bubble left">

2. **Error Cuadrático Medio (MSE)**:
   - Penaliza más los errores grandes al elevar al cuadrado las diferencias.  
   - Fórmula:  
     $$
     \text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
     $$

  </div class="bubble left">
  <div class="bubble left">

3. **Raíz del Error Cuadrático Medio (RMSE)**:
   - Es la raíz cuadrada del MSE, lo que lo hace interpretable en las mismas unidades de los datos.  
   - Fórmula:  
     $$
     \text{RMSE} = \sqrt{\text{MSE}}
     $$

  </div class="bubble left">
  <div class="bubble left">

4. **Coeficiente de Determinación ($R^2$)**:
   - Mide qué tan bien el modelo explica la variabilidad de los datos.  
   - Valor entre 0 y 1, donde 1 indica un ajuste perfecto.  
   - Fórmula:  
     $$
     R^2 = 1 - \frac{\text{Suma de errores al cuadrado (RSS)}}{\text{Suma total de cuadrados (TSS)}}
     $$






  </div class="bubble left">
  <div class="bubble left">

 **3. ¿Cómo elegir una métrica?**
La elección depende del problema:
- Si **las clases están desbalanceadas**, enfócate en **recall**, **precision** o **F1-score**.
- Si **los errores grandes son críticos**, usa **MSE** o **RMSE**.
- Para problemas generales de clasificación, **accuracy** es un buen punto de partida, pero verifica que no sea engañosa en datasets desbalanceados.

  </div class="bubble left">
  <div class="bubble right">
en Cross-Validation solo quieres conocer las métricas para distintos training sets? 


  </div class="bubble right">
  <div class="bubble left">

En **cross-validation**, no solo quieres conocer las métricas para distintos training sets, sino que el objetivo principal es evaluar la **capacidad de generalización del modelo** al medir su desempeño en distintos **validation sets** (subconjuntos de datos que no se usan para entrenar en cada iteración). Es decir, se busca responder preguntas como:

- ¿Qué tan bien funcionará el modelo con datos **nuevos** que nunca ha visto antes?
- ¿El modelo tiene un rendimiento **consistente** en diferentes particiones del dataset?
- ¿Hay problemas de **overfitting** o **underfitting**?

En pocas palabras, cross-validation te da una **estimación robusta del desempeño del modelo** al simular su comportamiento en situaciones del mundo real, donde no tendrás acceso a los datos de validación.






  </div class="bubble left">
  <div class="bubble left">

 **¿Qué pasa exactamente en cross-validation?**
1. Divides los datos en **K folds** (subconjuntos).  
2. Realizas $K$ iteraciones:  
   - En cada iteración:
     - Entrenas el modelo con $K-1$ folds (**training set**).
     - Evalúas el modelo en el fold restante (**validation set**).
   - Obtienes las métricas (por ejemplo, precisión, recall, error, etc.) en el **validation set**.
3. Al final, calculas:
   - **Promedio de las métricas** obtenidas en las $K$ iteraciones, para tener una evaluación general del modelo.
   - **Desviación estándar**, para medir la variabilidad del desempeño.






  </div class="bubble left">
  <div class="bubble left">

 **¿Por qué evaluar en distintos training sets y validation sets?**
Al evaluar el modelo en diferentes divisiones del dataset, puedes:
1. **Reducir el sesgo de la evaluación**:  
   Si usas siempre los mismos datos de validación, podrías sobreoptimizar el modelo para esos datos, lo que no asegura un buen desempeño en otros datasets. Cross-validation evita este problema.

2. **Medir la variabilidad del desempeño**:  
   Algunas particiones pueden ser más difíciles que otras (por ejemplo, si contienen outliers o clases desbalanceadas). Evaluar en múltiples folds permite entender si el modelo es robusto o si tiene un desempeño inconsistente.

3. **Aprovechar todo el dataset**:  
   Cada observación del dataset se utiliza tanto para entrenar como para validar, lo que es especialmente importante cuando el dataset es pequeño.






  </div class="bubble left">
  <div class="bubble left">

 **¿Qué se hace con las métricas obtenidas?**
Una vez que tienes las métricas de cada fold, puedes:
1. **Estimar el rendimiento del modelo** en datos desconocidos (promedio de las métricas).
2. **Comparar modelos**: Si estás evaluando diferentes algoritmos o hiperparámetros, puedes usar las métricas promedio para determinar cuál tiene mejor desempeño.
3. **Detectar problemas en el modelo**:  
   - Si las métricas varían mucho entre los folds (alta desviación estándar), puede ser una señal de que:
     - El modelo es sensible a pequeñas variaciones en los datos.
     - Hay un problema de datos desbalanceados o insuficientes.
   - Si las métricas son consistentemente bajas, el modelo podría estar **underfitting**.






  </div class="bubble left">
  <div class="bubble left">

 **Ejemplo práctico**
Supongamos que estás usando 5-Fold Cross-Validation con un modelo de clasificación y obtienes las siguientes precisiones por fold:

| Iteración (Fold) | Precisión |
|------------------|-----------|
| Fold 1           | 0.85      |
| Fold 2           | 0.87      |
| Fold 3           | 0.83      |
| Fold 4           | 0.88      |
| Fold 5           | 0.86      |

1. **Promedio de precisión**:
   $$
   \text{Promedio} =\\
   \frac{0.85 + 0.87 + 0.83 + 0.88 + 0.86}{5} = \\ 0.858
   $$

2. **Desviación estándar**:
   $$
   \text{Desviación estándar} =\\ \sqrt{\frac{1}{5} \sum_{i=1}^{5} (\text{Precisión}_i - \text{Promedio})^2}
   $$
   Esto te dirá qué tan variable es el desempeño del modelo.






  </div class="bubble left">
  <div class="bubble left">

 **Conclusión**
En cross-validation, el objetivo no es solo obtener métricas para distintos training sets, sino evaluar el **comportamiento global del modelo** considerando todas las particiones posibles del dataset. Esto permite estimar su rendimiento real y asegurarte de que es un modelo robusto para datos nuevos.