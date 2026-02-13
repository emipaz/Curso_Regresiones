# Regresión lineal

## Introducción Conceptos Fundamentales

El **análisis de regresión** se centra en estimar la relación entre **una variable dependiente** y **una o más variables independientes**. En este apartado se introduce la primera técnica de modelado: la **regresión lineal**, ampliamente utilizada para describir patrones observables en la vida diaria y en contextos profesionales.

## ¿Qué es la regresión lineal?

La **regresión lineal** es una técnica que estima la relación **lineal** entre:
- Una variable dependiente continua, generalmente representada como **y**.
- Una o más variables independientes, generalmente representadas como **x**.

La relación lineal puede visualizarse como una **línea** en una gráfica, que representa un conjunto infinito de puntos, aunque solo se observe una parte de ella.

### Ejemplos cotidianos

- A medida que una versión de software envejece, disminuyen las búsquedas en línea.
- A medida que una personalidad en redes sociales gana seguidores, aumentan las ventas de sus libros.
- La relación entre el precio de un producto y el número de ventas.

## Variables continuas y categóricas

- **Variables continuas**: pueden tomar cualquier valor real dentro de un rango.
  - Ejemplos: ventas de productos, velocidad de un vehículo, tiempo en una página web.
- **Variables categóricas**: tienen un número finito de valores posibles.
  - Ejemplos: tipo de producto, nivel educativo.

La **regresión lineal** se utiliza para estimar **variables dependientes continuas**. Existen otros modelos de regresión para variables categóricas, que se estudiarán más adelante.

## Variables dependientes e independientes

- **Variable dependiente (y)**:
  - Es la variable que el modelo estima.
  - También llamada variable de respuesta o de resultado.
- **Variables independientes (x)**:
  - Son las variables que explican o predicen el comportamiento de **y**.
  - También se denominan variables explicativas o predictoras.

### Ejemplo de pastelería

- **y**: número de rebanadas de pastel vendidas en un día.
- **x**: número de tazas de café vendidas ese día.

## Pendiente e intersección

En la regresión lineal aparecen dos conceptos clave:

- **Pendiente**:
  - Indica cuánto se espera que cambie **y** por cada aumento de una unidad en **x**.
  - Ejemplo: cuántas rebanadas de pastel se venden por cada taza de café adicional.

- **Intersección (intercepto)**:
  - Es el valor de **y** cuando **x = 0**.
  - Ejemplo: cuántas rebanadas de pastel se venden cuando no se vende café.

## Correlación

Cuando dos variables **x** e **y** están relacionadas de forma lineal, se dice que están **correlacionadas**. La estadística permite medir la **fuerza** de esta relación.

### Tipos de correlación

- **Correlación positiva**:
  - Ambas variables tienden a aumentar o disminuir juntas.
  - Ejemplo: más café vendido, más pastel vendido.

- **Correlación negativa**:
  - Cuando una variable aumenta, la otra tiende a disminuir.
  - Ejemplos:
    - Aumento en ventas de café caliente y disminución en café helado.
    - Artículos más largos y menor número de lectores que los terminan.

## Utilidad de la regresión lineal

Identificar relaciones lineales ayuda a responder preguntas como:
- ¿Qué factores están asociados con cambios en las ventas?
- ¿Qué variables influyen en la asignación de recursos?
- ¿Qué factores afectan la demanda de transporte público?

El **tamaño de la pendiente** indica cuánto aumentan o disminuyen estas variables ante cambios en los factores explicativos.

## Correlación no implica causalidad

Un punto fundamental es que **la correlación no es causalidad**:
- Que dos variables estén correlacionadas no significa que una cause a la otra.
- La **causalidad** implica una relación directa de causa y efecto y requiere métodos estadísticos y datos más rigurosos.

### Ejemplo

- A medida que una persona envejece, suele haber visitado más lugares.
- Esto no significa necesariamente que la edad cause el aumento de viajes; pueden existir otros factores asociados.

Reconocer esta diferencia es parte de las **buenas prácticas éticas** en el análisis de datos, especialmente al comunicar resultados.

## Resumen

- La **regresión lineal** modela relaciones lineales entre variables.
- La variable dependiente varía según las variables independientes.
- La **pendiente** indica el cambio en **y** por cada unidad de cambio en **x**.
- La correlación puede ser **positiva o negativa**.
- Siempre debe interpretarse con cuidado: **correlación no es causalidad**.

## Próximo paso

A continuación, se estudiarán las **bases matemáticas y estadísticas** de la regresión lineal, lo que permitirá explicar sus resultados con mayor claridad y rigor.

___

# Población, muestra y fundamentos estadísticos de la regresión lineal

## Población y muestra

En un mundo ideal, se dispondría de **todos los puntos de datos relevantes** para responder una pregunta. En estadística, a este conjunto completo se le llama **población**.

### Ejemplo

Si trabajas para una editorial y deseas entender la relación entre:
- Seguidores de un autor en redes sociales  
- Ventas de libros  

La población ideal incluiría:
- Todos los autores de libros
- Todos sus seguidores en redes sociales
- Todas las ventas de libros de todos los tiempos  

Esto es prácticamente imposible. Afortunadamente, **no es necesario analizar toda la población** para realizar un análisis de regresión significativo.

### Muestra

Una **muestra** es una parte representativa de la población. En términos estadísticos, es simplemente **una porción de los datos disponibles**.

- Cada punto de la muestra tiene valores observados de **x** y **y**.
- Los valores observados son los datos reales con los que se trabaja.
- La muestra no contiene todos los valores posibles de la población.

En el ejemplo de la editorial:
- **y (variable dependiente)**: ventas de libros  
- **x (variable independiente)**: número de seguidores en redes sociales  

Un punto observado podría ser:
- $x = 10{,}000$ seguidores  
- $y = 500$ ventas  

## Objetivo del análisis de regresión

El **análisis de regresión** busca definir una **relación matemática** entre los valores observados de $x$ y $y$ para comprender cómo interactúan.

Para un mismo valor de $x$, pueden existir muchos valores posibles de $y$. Para simplificar, la **regresión lineal** se centra en la **media de $y$ dado un valor específico de $x$**.

Esta media se representa como:
- $\mu_y$  

donde $\mu$ (mu) es la letra griega que indica **media**.

## Modelo de regresión lineal
Para definir una relación lineal se necesitan dos elementos:
- **Intersección**
- **Pendiente**

En estadística, el modelo se expresa como:

$$
\mu_y = \beta_0 + \beta_1 x
$$

donde:
- $\beta_0$ = intersección (intercepto)
- $\beta_1$ = pendiente
- $\beta_0$ y $\beta_1$ se llaman **parámetros**

### Parámetros y estimaciones

- Los **parámetros** son propiedades de la **población**.
- No se conocen sus valores reales porque no se observa toda la población.
- A partir de la muestra, se calculan **estimaciones** de los parámetros.

Las estimaciones se denotan con un **sombrero**:
- $\hat{\beta}_0$
- $\hat{\beta}_1$
- $\hat{\mu}_y$

Estas estimaciones también se conocen como **coeficientes de regresión**.

## Notación simplificada

En el curso se utiliza la forma simplificada del modelo:

$$
y = \beta_0 + \beta_1 x
$$

### Ejemplo numérico
Supongamos:
- $\beta_0 = -1$
- $\beta_1 = 5$

Sustituyendo valores de $x$:

| $x$ | $y$ |
|----|----|
| 0  | -1 |
| 1  | 4  |
| 2  | 9  |
| 3  | 14 |

Se observa un patrón claro:
- Por cada aumento de **1 unidad en $x$**, $y$ aumenta **5 unidades**.
- El valor **5** corresponde a la **pendiente $\beta_1$**.
- La pendiente indica cuánto cambia $y$ por cada cambio unitario en $x$.

## Estimación por Mínimos Cuadrados Ordinarios (MCO)

Una de las formas más comunes de calcular los coeficientes de regresión es mediante:
- **Mínimos Cuadrados Ordinarios (MCO)** u **OLS (Ordinary Least Squares)**

### Idea general de OLS

- Existen infinitas rectas posibles que podrían ajustarse a los datos.
- El objetivo es encontrar **la recta que mejor se ajuste**.
- Para ello, se minimiza la **función de pérdida**.

#### Función de pérdida

- Mide la distancia entre:
  - Valores observados
  - Valores estimados por el modelo
- OLS elige los coeficientes que **minimizan esa distancia**.

## Cierre

Con estos conceptos básicos:
- Población y muestra  
- Parámetros y coeficientes de regresión  
- Pendiente e intersección  
- Mínimos cuadrados ordinarios  

se sientan las bases para profundizar en:
- El espacio en la regresión lineal
- Cuándo usar regresión lineal
- La varianza del modelo
- La implementación de OLS en Python  

Estos temas se desarrollarán más adelante en el curso.

## Autoevaluacíon

### ¿Qué técnica estima la relación lineal entre una variable dependiente continua y una o más variables independientes?

- [x] Regresión lineal
- [ ] Validación del modelo
- [ ] Causalidad  
- [ ] Interceptar  

> La regresión lineal estima la relación lineal entre una variable dependiente continua y una o más variables independientes.

### ¿Cuál de las siguientes afirmaciones describe con exactitud las variables dependientes e independientes? Seleccione todas las que correspondan.


- [ ] La variable independiente tiende a variar en función de los valores de las variables dependientes.
- [x] Las variables independientes también se denominan variables explicativas o predictoras.
- [x] La variable dependiente tiende a variar en función de los valores de las variables independientes.
- [x] La variable dependiente es la variable que estima el modelo dado. 

> La variable dependiente es la variable que estima el modelo dado. Tiende a variar en función de los valores de las variables independientes. Las variables independientes también se denominan variables explicativas o predictoras. 

### ¿Qué término describe una relación inversa entre dos variables?

- [ ] Correlación positiva
- [ ] Pendiente
- [z] Correlación negativa
- [ ] Interceptar

> La variable dependiente es la variable que estima el modelo dado. Tiende a variar en función de los valores de las variables independientes. Las variables independientes también se denominan variables explicativas o predictoras. 

### Rellene el espacio en blanco: El objetivo del análisis de regresión es utilizar las matemáticas para definir la _____ entre las X y las Y de la muestra con el fin de comprender cómo interactúan las variables.


- [ ] independencia
- [ ] Modelo
- [ ] Valor
- [x] Relación

> El objetivo del análisis de regresión es definir una relación matemática entre las X y las Y de la muestra para comprender cómo interactúan las variables.