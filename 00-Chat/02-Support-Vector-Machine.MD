<link rel="stylesheet" type="text/css" href="styles.css">
<link rel="stylesheet" href="github-markdown.css">
<script src="https://cdn.jsdelivr.net/npm/katex/dist/katex.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/katex/dist/contrib/auto-render.min.js" onload="renderMathInElement(document.body);"></script>
<div class="container">


<div class="header">
  <h1>Support Vector Machine</h1>
  <h3>P25 LDS1051 1: Reconocimiento de Patrones</h3>
  <p>24 de Enero de 2025</p>
</div

<div style="text-align: center;">
  <a href="https://www.youtube.com/watch?v=_YPScrckx28">Support Vector Machine</a>
</div>

  <div class="bubble right">
¿Qué son las Support Vector Machine? 
  </div class="bubble right">

  <div class="bubble right">
Luego tengo que aprender el método del Kernel 
  </div class="bubble right">

  <div class="bubble right">
Y repasar programación lineal
  </div class="bubble right">

  <div class="bubble right">
No la hubiera metido con Benito
  </div class="bubble right">


  <div class="bubble left">


Las **Support Vector Machines (SVM)** son un método de aprendizaje supervisado utilizado principalmente para tareas de clasificación y regresión. Se basan en encontrar un hiperplano óptimo que separe los datos en diferentes clases con el mayor margen posible. Fueron introducidas por **Vladimir Vapnik** y sus colegas en los años 90, y son conocidas por su capacidad para manejar problemas de alta dimensionalidad y clasificadores no lineales mediante el uso de *kernels*.



  </div class="bubble left">
  <div class="bubble left">

 Concepto clave
En términos simples, una SVM busca un hiperplano (en un espacio de varias dimensiones) que divida los datos de manera que las clases estén lo más separadas posible. Este hiperplano se define por maximizar el margen, es decir, la distancia mínima entre los puntos de cada clase (llamados *support vectors*) y el hiperplano.






  </div class="bubble left">
  <div class="bubble left">

 Funcionamiento
1. **Separación lineal (caso simple)**:
   - En problemas linealmente separables, SVM encuentra un hiperplano que divide perfectamente las dos clases.
   - Los *support vectors* son los puntos más cercanos al hiperplano; son críticos porque determinan su posición.

   La ecuación del hiperplano es:
   $$
   w^T x + b = 0
   $$
   Donde $w$ es el vector normal al hiperplano y $b$ es el sesgo (*bias*).

2. **Margen máximo**:
   - El margen es la distancia entre el hiperplano y los *support vectors*. La SVM maximiza este margen, lo que mejora la capacidad del modelo para generalizar en datos no vistos.

3. **Casos no lineales**:
   - En muchos casos, los datos no son linealmente separables. Para solucionar esto, SVM utiliza un truco matemático conocido como el **kernel trick**. 
   - El truco consiste en proyectar los datos a un espacio de características de mayor dimensión donde sí sean separables linealmente.

4. **Kernels comunes**:
   - **Lineal**: Para problemas que son separables linealmente.
   - **Polinómico**: Mapea los datos a un espacio polinómico de mayor dimensión.
   - **RBF (Radial Basis Function)** o **Gaussiano**: Ideal para datos no lineales; es uno de los más populares.
   - **Sigmoide**: Similar a las redes neuronales.






  </div class="bubble left">
  <div class="bubble left">

 Optimización
El problema que SVM resuelve se formula como una tarea de optimización convexa:
$$
\min_{w, b} \frac{1}{2} \|w\|^2 \quad \text{sujeto a: } y_i (w^T x_i + b) \geq 1, \, \forall i
$$
Donde:
- $y_i$ son las etiquetas (+1 o -1).
- $x_i$ son las características del dato $i$.

Si los datos no son completamente separables, se introduce un término de relajación ($\xi_i$) para penalizar errores, conocido como **SVM con margen suave**:
$$
\min_{w, b, \xi} \frac{1}{2} \|w\|^2 + C \sum_{i=1}^n \xi_i
$$
Aquí, $C$ controla el balance entre maximizar el margen y minimizar los errores de clasificación.






  </div class="bubble left">
  <div class="bubble left">

 Ventajas
1. Eficiente para conjuntos de datos con muchas dimensiones.
2. Robusto contra sobreajuste, especialmente en problemas de clasificación binaria.
3. Puede manejar datos no lineales gracias a los *kernels*.



  </div class="bubble left">
  <div class="bubble left">

 Desventajas
1. No es ideal para conjuntos de datos grandes, ya que el costo computacional aumenta con el número de muestras.
2. La elección del kernel y los hiperparámetros ($C$, parámetros del kernel) puede ser complicada.
3. En casos con ruido significativo o clases solapadas, puede no funcionar bien.






  </div class="bubble left">
  <div class="bubble left">

 Aplicaciones
- Clasificación de texto y spam.
- Reconocimiento de imágenes y patrones.
- Detección de anomalías.
- Bioinformática, como clasificación de genes.

¿Quieres ejemplos prácticos de implementación en Python? 😊








  </div class="bubble left">
  <div class="bubble right">
Explicame por que la ecuación del hiperplano es esa y dame un ejemplo en 1, 2 y 3 dimensiones


  </div class="bubble right">





  <div class="bubble left">

 **Por qué la ecuación del hiperplano es $w^T x + b = 0$**

Un hiperplano es una generalización de una "línea recta" en dimensiones superiores. Formalmente, un hiperplano es una subvariedad de $n-1$ dimensiones en un espacio $n$-dimensional que divide dicho espacio en dos mitades.

1. **Geometría del hiperplano**:
   - La ecuación $w^T x + b = 0$ representa un conjunto de puntos $x \in \mathbb{R}^n$ que satisface la condición de estar sobre el hiperplano.
   - $w^T x$ (o $\langle w, x \rangle$) es el producto punto entre $w$ (un vector normal al hiperplano) y $x$ (un punto en el espacio). Esto da una medida de cómo $x$ está alineado con la dirección de $w$.

2. **Interpretación del término $b$**:
   - $b$ es el término independiente que desplaza el hiperplano desde el origen. Si $b = 0$, el hiperplano pasa por el origen. Si $b \neq 0$, el hiperplano se traslada en la dirección de $w$.

3. **Condición de clasificación**:
   - Si $w^T x + b > 0$, el punto $x$ está en un lado del hiperplano.
   - Si $w^T x + b < 0$, el punto $x$ está en el otro lado.
   - Si $w^T x + b = 0$, el punto $x$ está exactamente sobre el hiperplano.

El hiperplano divide el espacio en dos regiones, y esta propiedad es fundamental para la clasificación binaria.






  </div class="bubble left">
  <div class="bubble left">

 **Ejemplo en 1D**

En 1D, un "hiperplano" se reduce a un punto en la recta. Supongamos que:

$$
w = 2, \quad b = -4
$$

La ecuación del hiperplano es:
$$
2x - 4 = 0 \implies x = 2
$$

- El punto $x = 2$ es el "hiperplano".
- Los puntos a la izquierda ($x < 2$) están en una clase ($2x - 4 < 0$).
- Los puntos a la derecha ($x > 2$) están en otra clase ($2x - 4 > 0$).






  </div class="bubble left">
  <div class="bubble left">

 **Ejemplo en 2D**

En 2D, un hiperplano es una línea. Supongamos que:

$$
w = \begin{bmatrix} 1 \\ -1 \end{bmatrix}, \quad b = -1
$$

La ecuación del hiperplano es:
$$
w^T x + b = 0 \implies 1 \cdot x_1 - 1 \cdot x_2 - 1 = 0 \implies x_1 - x_2 = 1
$$

Esta es la ecuación de una línea que pasa por los puntos:
- Si $x_1 = 2$, entonces $x_2 = 1$.
- Si $x_1 = 1$, entonces $x_2 = 0$.

El hiperplano divide el plano en dos regiones:
- $x_1 - x_2 > 1$: Una clase.
- $x_1 - x_2 < 1$: Otra clase.






  </div class="bubble left">
  <div class="bubble left">

 **Ejemplo en 3D**

En 3D, un hiperplano es un plano. Supongamos que:

$$
w = \begin{bmatrix} 2 \\ 3 \\ -1 \end{bmatrix}, \quad b = 6
$$

La ecuación del hiperplano es:
$$
w^T x + b = 0 \implies 2x_1 + 3x_2 - x_3 + 6 = 0
$$

Este es el plano que satisface la ecuación. Por ejemplo:
- Si $x_1 = 0$ y $x_2 = 0$, entonces $x_3 = 6$.
- Si $x_1 = 1$ y $x_2 = 1$, entonces $x_3 = 11$.

Este plano divide el espacio 3D en dos regiones:
- $2x_1 + 3x_2 - x_3 + 6 > 0$: Una clase.
- $2x_1 + 3x_2 - x_3 + 6 < 0$: Otra clase.










  </div class="bubble left">
  <div class="bubble right">
¿Pero que representa el vector $w$? 


  </div class="bubble right">
  <div class="bubble left">


El vector $\mathbf{w}$ en la ecuación del hiperplano $\mathbf{w}^T \mathbf{x} + b = 0$ tiene una interpretación geométrica clave. 



  </div class="bubble left">
  <div class="bubble left">

 **¿Qué representa $\mathbf{w}$?**
El vector $\mathbf{w}$:
1. **Es el vector normal al hiperplano**:
   - $\mathbf{w}$ es perpendicular (u ortogonal) al hiperplano.
   - Indica la dirección en la que la función de decisión $\mathbf{w}^T \mathbf{x} + b$ cambia más rápidamente.

2. **Define la orientación del hiperplano**:
   - La dirección de $\mathbf{w}$ dicta cómo está "inclinado" el hiperplano en el espacio.
   - Cambiar la magnitud de $\mathbf{w}$ no cambia la orientación, pero sí afecta el tamaño del margen.

3. **Controla la clasificación**:
   - $\mathbf{w} \cdot \mathbf{x} + b > 0$: Los puntos están en un lado del hiperplano (una clase).
   - $\mathbf{w} \cdot \mathbf{x} + b < 0$: Los puntos están en el otro lado (otra clase).

4. **Magnitud de $\mathbf{w}$**:
   - La norma $\| \mathbf{w} \|$ (magnitud del vector $\mathbf{w}$) está relacionada con el margen que separa las clases. 
   - Maximizar el margen equivale a minimizar $\| \mathbf{w} \|$, ya que un margen más grande reduce la probabilidad de errores de clasificación.






  </div class="bubble left">
  <div class="bubble left">

 **Ejemplo con interpretación geométrica**

Supongamos que estamos en 2D y $\mathbf{w} = [1, -2]$ y $b = 3$. El hiperplano es:
$$
1 \cdot x_1 - 2 \cdot x_2 + 3 = 0
$$



  </div class="bubble left">
  <div class="bubble left">

 **Paso 1: Orientación de $\mathbf{w}$**
El vector $\mathbf{w} = [1, -2]$:
- Tiene dirección $(1, -2)$.
- Es perpendicular a la línea $x_1 - 2x_2 + 3 = 0$.



  </div class="bubble left">
  <div class="bubble left">

 **Paso 2: Clasificación**
- Si $x_1 - 2x_2 + 3 > 0$, el punto está en una clase.
- Si $x_1 - 2x_2 + 3 < 0$, el punto está en la otra clase.
  


  </div class="bubble left">
  <div class="bubble left">

 **Paso 3: Ejemplo visual**
Imagina un punto $\mathbf{x} = [2, 1]$:
$$
\mathbf{w}^T \mathbf{x} + b = 1 \cdot 2 - 2 \cdot 1 + 3 = 3
$$
Como $3 > 0$, este punto está en la clase positiva.






  </div class="bubble left">
  <div class="bubble left">

 **Intuición física de $\mathbf{w}$**
- Puedes pensar en $\mathbf{w}$ como un vector que apunta hacia el lado positivo del hiperplano.
- La longitud del vector $\mathbf{w}$ afecta cuánto "peso" tienen las características en la clasificación.











  </div class="bubble left">
  <div class="bubble right">
¿Y en SVM tenemos que encontrar los $w_i$? 


  </div class="bubble right">
  <div class="bubble left">



En el contexto de **Support Vector Machines (SVM)**, no es necesario encontrar un conjunto de componentes $W_i$ por separado. El vector $\mathbf{w}$ es un **único vector** en el espacio de características, y **no se descompone en componentes $W_i$** de manera explícita en la formulación estándar. 

Sin embargo, lo que sucede es que el vector $\mathbf{w}$ está compuesto por las **componentes** de las características del espacio. Vamos a desglosarlo con más detalle.



  </div class="bubble left">
  <div class="bubble left">

 **El vector $\mathbf{w}$ en SVM**

La idea principal en SVM es encontrar el hiperplano que separa las clases de manera óptima. Este hiperplano se describe mediante la ecuación:
$$
\mathbf{w}^T \mathbf{x} + b = 0
$$
Aquí:

- $\mathbf{w} = [w_1, w_2, \dots, w_d]$ es un **vector de pesos** de dimensión $d$, donde $d$ es el número de características del problema (dimensiones del espacio de características).
- $\mathbf{x} = [x_1, x_2, \dots, x_d]$ es el vector de características de un punto de datos en ese espacio.
- $b$ es el **término de sesgo** o "bias", que ajusta el desplazamiento del hiperplano.



  </div class="bubble left">
  <div class="bubble left">

 **¿Qué son los $w_i$?**

Los $w_i$ son simplemente las componentes de **$\mathbf{w}$**. Es decir, si tienes un espacio de características de dimensión $d$, entonces el vector $\mathbf{w}$ tendrá $d$ componentes, $w_1, w_2, \dots, w_d$, que corresponden a cada una de las características en el espacio de características.

Por ejemplo:
- Si tienes un conjunto de datos en 2 dimensiones, es decir, $\mathbf{x} = [x_1, x_2]$, entonces el vector $\mathbf{w}$ será $\mathbf{w} = [w_1, w_2]$.
- Si el espacio tiene 3 dimensiones, entonces $\mathbf{w} = [w_1, w_2, w_3]$.

Estos componentes no se eligen individualmente como $w_1, w_2, \dots, w_d$, sino que se determinan **en conjunto** a través de la optimización que realiza SVM.



  </div class="bubble left">
  <div class="bubble left">

 **El proceso de optimización**

El objetivo de SVM es encontrar el **vector $\mathbf{w}$** (y el sesgo $b$) que maximice el margen entre las clases. Esto se logra resolviendo un problema de optimización. En su forma básica, el problema es:

$$
\min_{\mathbf{w}, b} \frac{1}{2} \|\mathbf{w}\|^2 \quad \text{sujeto a} \quad y_i (\mathbf{w}^T \mathbf{x}_i + b) \geq 1, \quad \forall i
$$

Aquí, no estamos buscando individualmente los $w_i$, sino el vector completo $\mathbf{w}$ que satisface estas condiciones. El vector $\mathbf{w}$ se ajusta de manera que el margen (la distancia entre el hiperplano y los puntos más cercanos de las clases) se maximice.



  </div class="bubble left">
  <div class="bubble left">

 **Resumen de lo que estamos buscando**

1. **El vector $\mathbf{w}$**: Es el vector que define la dirección del hiperplano y cuya magnitud está relacionada con el margen.
   - Los **componentes $w_i$** corresponden a cada dimensión del espacio de características, pero se optimizan juntos en lugar de ser encontrados de forma independiente.
   
2. **Optimización**: El proceso de optimización de SVM ajusta $\mathbf{w}$ y $b$ para maximizar el margen y lograr la mejor separación posible entre las clases, sujeto a las restricciones de clasificación.




En resumen, en SVM no buscamos individualmente los $W_i$, sino que determinamos el vector $\mathbf{w} = [w_1, w_2, \dots, w_d]$ a través de un proceso de optimización que resuelve el problema de maximizar el margen. El $\mathbf{w}$ es el vector completo que describe el hiperplano, y sus componentes $w_i$ corresponden a las diferentes dimensiones del espacio de características. 

¿Te gustaría ver cómo se implementa este proceso en Python o en otro contexto?







  </div class="bubble left">
  <div class="bubble right">
Dame un ejemplo



  </div class="bubble right">
  <div class="bubble left">

Claro, para identificar los componentes $W_i$ de $\mathbf{w}$ en el contexto de un problema de clasificación con **Support Vector Machines (SVM)**, primero debemos entender cómo se resuelve el problema de optimización que define $\mathbf{w}$. A continuación, te guiaré por el proceso paso a paso con un ejemplo simple.



  </div class="bubble left">
  <div class="bubble left">

 **Paso 1: Plantear el problema de clasificación**
Imagina que tienes un conjunto de datos de dos dimensiones (2D) y deseas usar una SVM para clasificarlos. El problema será el siguiente:

$$
y_i (\mathbf{w}^T \mathbf{x}_i + b) \geq 1 \quad \text{para todo} \, i
$$
donde:
- $\mathbf{x}_i = [x_{i1}, x_{i2}]$ son los vectores de características de tus puntos de datos.
- $y_i$ son las etiquetas de clase, que son $\pm 1$ (para clasificación binaria).
- $\mathbf{w} = [w_1, w_2]$ es el vector de pesos que queremos encontrar, y $b$ es el sesgo.



  </div class="bubble left">
  <div class="bubble left">

 **Paso 2: Definir un conjunto de datos de ejemplo**
Supón que tienes un conjunto de datos simple con 4 puntos en 2D, etiquetados como $+1$ o $-1$:

| $x_1$ | $x_2$ | $y$ |
|:--------:|:--------:|:------:|
|    2     |    3     |   +1   |
|    4     |    1     |   +1   |
|    3     |    4     |   -1   |
|    1     |    2     |   -1   |

Estos datos están representados en 2 dimensiones, y queremos encontrar un hiperplano de separación.



  </div class="bubble left">
  <div class="bubble left">

 **Paso 3: Formulación del problema**
La ecuación para el hiperplano es:
$$
w_1 x_1 + w_2 x_2 + b = 0
$$
Queremos encontrar los valores de $w_1$, $w_2$ y $b$ que separen las clases de manera óptima.



  </div class="bubble left">
  <div class="bubble left">

 **Paso 4: Resolver el problema de optimización**
Para resolver el problema de optimización, podemos usar un enfoque estándar que SVM utiliza: **programación cuadrática**. Sin embargo, en la práctica, es mucho más sencillo usar una biblioteca como `scikit-learn` para encontrar estos parámetros.

 **Paso 5: Interpretar los resultados**
Supongamos que el resultado del modelo es algo como esto:

```
w_1, w_2: [ 1.2 -0.8]
b: -0.5
```

Esto significa que el vector $\mathbf{w}$ es:

$$
\mathbf{w} = [1.2, -0.8]
$$

Y el valor de $b$ es $-0.5$.



  </div class="bubble left">
  <div class="bubble left">

 **Interpretación**:
- $w_1 = 1.2$ es el peso asociado a la característica $x_1$ (la primera columna de tus datos).
- $w_2 = -0.8$ es el peso asociado a la característica $x_2$ (la segunda columna de tus datos).
- $b = -0.5$ es el sesgo, que ajusta el desplazamiento del hiperplano.

Estos valores nos dicen cómo se orienta el hiperplano en el espacio de características. El hiperplano que separa las clases tiene la siguiente ecuación:

$$
1.2 \cdot x_1 - 0.8 \cdot x_2 - 0.5 = 0
$$



  </div class="bubble left">
  <div class="bubble left">

 **Paso 6: Visualizar el hiperplano**
Para visualizar el hiperplano, podemos graficar los datos y el plano de separación:

```python
import matplotlib.pyplot as plt



  </div class="bubble left">
  <div class="bubble left">

 Dibujar los puntos
plt.scatter(X[:, 0], X[:, 1], c=y, cmap='coolwarm', s=100)



  </div class="bubble left">
  <div class="bubble left">

 Dibujar el hiperplano
x_values = np.linspace(0, 5, 100)
y_values = -(svm.coef_[0][0] * x_values + svm.intercept_) / svm.coef_[0][1]
plt.plot(x_values, y_values, label="Hiperplano")

plt.xlabel('x1')
plt.ylabel('x2')
plt.legend()
plt.show()
```



  </div class="bubble left">
  <div class="bubble left">

 **Resumen**
1. **Identificar los $W_i$**: Los componentes $w_1, w_2, \dots, w_d$ corresponden a las **componentes del vector de pesos $\mathbf{w}$** en el espacio de características.
2. Estos valores se encuentran resolviendo un **problema de optimización** que busca el hiperplano óptimo de separación.
3. En lugar de hacerlo manualmente, usamos herramientas como **`scikit-learn`** para obtener los valores de $\mathbf{w}$ y $b$ de manera eficiente.


  </div class="bubble left">
  <div class="bubble right">
Escribe el problema de optimización y explícame que significa


  </div class="bubble right">
  <div class="bubble left">

El **problema de optimización** en Support Vector Machines (SVM) tiene como objetivo encontrar el **hiperplano** que separa las dos clases de manera óptima, es decir, el hiperplano que maximiza el **margen** (la distancia entre el hiperplano y los puntos más cercanos de cada clase). Este enfoque está relacionado con un problema de **programación cuadrática**.

Vamos a desglosar el **problema de optimización** de SVM de forma detallada.






  </div class="bubble left">
  <div class="bubble left">

 **Formulación del problema de optimización de SVM**

El objetivo es encontrar un hiperplano que se define por los parámetros $\mathbf{w}$ (el vector de pesos) y $b$ (el sesgo) de manera que el margen entre las clases sea maximizado, sujeto a las siguientes condiciones de clasificación.



  </div class="bubble left">
  <div class="bubble left">

 1. **Ecuación del hiperplano**:
El hiperplano que separa las clases está dado por la ecuación:

$$
\mathbf{w}^T \mathbf{x} + b = 0
$$

Donde:
- $\mathbf{w}$ es el vector de pesos.
- $\mathbf{x}$ es el vector de características de un punto de datos.
- $b$ es el sesgo que ajusta el desplazamiento del hiperplano.



  </div class="bubble left">
  <div class="bubble left">

 2. **Condiciones de clasificación (restricciones)**:
Para que el modelo SVM sea correcto, los puntos de cada clase deben estar correctamente clasificados y separados por el hiperplano. Las restricciones son las siguientes:
- Para los puntos de la clase $+1$, se requiere que:

$$
\mathbf{w}^T \mathbf{x}_i + b \geq 1, \quad \forall y_i = +1
$$

- Para los puntos de la clase $-1$, se requiere que:

$$
\mathbf{w}^T \mathbf{x}_i + b \leq -1, \quad \forall y_i = -1
$$

Estas condiciones aseguran que:
- Los puntos de la clase $+1$ están en un lado del hiperplano, y los puntos de la clase $-1$ están en el otro lado.
- El margen entre el hiperplano y los puntos de cada clase es lo más grande posible.



  </div class="bubble left">
  <div class="bubble left">

 3. **Maximización del margen**:
El **margen** se define como la distancia entre el hiperplano y el punto más cercano de cada clase. Para que el margen sea máximo, la siguiente expresión debe ser minimizada:

$$
\text{Margen} = \frac{1}{\|\mathbf{w}\|}
$$

Esto se debe a que el margen $\gamma$ está relacionado con la magnitud del vector $\mathbf{w}$. La minimización de $\|\mathbf{w}\|^2$ es equivalente a maximizar el margen, ya que la distancia es inversamente proporcional a $\|\mathbf{w}\|$.



  </div class="bubble left">
  <div class="bubble left">

 4. **El problema de optimización completo**:

El problema de optimización se puede plantear como:

$$
\min_{\mathbf{w}, b} \frac{1}{2} \|\mathbf{w}\|^2
$$

Sujeto a las restricciones:

$$
y_i (\mathbf{w}^T \mathbf{x}_i + b) \geq 1, \quad \forall i
$$



  </div class="bubble left">
  <div class="bubble left">

 **Explicación paso a paso del problema de optimización**



  </div class="bubble left">
  <div class="bubble left">

 **1. Objetivo: Minimizar $\frac{1}{2} \|\mathbf{w}\|^2$**
- Este término busca minimizar la magnitud de $\mathbf{w}$, lo que a su vez maximiza el margen entre las clases. El factor $\frac{1}{2}$ es simplemente para simplificar la derivada en la optimización, no cambia el objetivo.
- Minimizar $\|\mathbf{w}\|^2$ es equivalente a maximizar el **margen**, es decir, hacer que el hiperplano esté lo más alejado posible de los puntos más cercanos de cada clase.



  </div class="bubble left">
  <div class="bubble left">

 **2. Restricciones: $y_i (\mathbf{w}^T \mathbf{x}_i + b) \geq 1$**
- Para cada punto $\mathbf{x}_i$ con su etiqueta correspondiente $y_i$, debemos asegurarnos de que se cumpla una de las dos condiciones:
  - Si $y_i = +1$, el punto debe estar en el lado positivo del hiperplano, es decir, $\mathbf{w}^T \mathbf{x}_i + b \geq 1$.
  - Si $y_i = -1$, el punto debe estar en el lado negativo del hiperplano, es decir, $\mathbf{w}^T \mathbf{x}_i + b \leq -1$.

Estas restricciones aseguran que los puntos de cada clase estén correctamente clasificados y separados por el hiperplano.






  </div class="bubble left">
  <div class="bubble left">

 **Interpretación geométrica**

- **El vector $\mathbf{w}$**: Es el **vector normal** al hiperplano. La magnitud de $\mathbf{w}$ está relacionada con el margen; por lo tanto, minimizar $\|\mathbf{w}\|^2$ es equivalente a maximizar el margen.
- **El sesgo $b$**: Ajusta la posición del hiperplano. Si $b = 0$, el hiperplano pasa por el origen, pero si $b \neq 0$, el hiperplano se desplaza a lo largo del espacio de características.



  </div class="bubble left">
  <div class="bubble left">

 **¿Cómo se resuelve este problema?**

El problema de optimización es un **problema de programación cuadrática**. En la práctica, se resuelve usando algoritmos como **el método de optimización de cuadrática secuencial (SQP)** o el uso de **métodos de optimización convexa** como el algoritmo de **punto interior**.

En **`scikit-learn`**, el solver SVM utiliza estos algoritmos de optimización para encontrar los valores de $\mathbf{w}$ y $b$ que minimizan el margen y satisfacen las restricciones de clasificación.






  </div class="bubble left">
  <div class="bubble left">

 **Resumen de lo que significa el problema de optimización**
1. El objetivo es **maximizar el margen** entre las clases, lo que es equivalente a **minimizar $\|\mathbf{w}\|^2$**.
2. Las restricciones garantizan que los puntos estén correctamente clasificados, es decir, que estén en el lado correcto del hiperplano.
3. La solución a este problema nos da el **vector de pesos $\mathbf{w}$** y el **sesgo $b$**, que definen el hiperplano óptimo de separación.

Este enfoque garantiza que SVM encuentre el mejor hiperplano en cuanto a separación de clases y minimización de errores.