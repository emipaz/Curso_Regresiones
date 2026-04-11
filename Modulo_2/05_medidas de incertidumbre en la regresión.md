# Interpretar las medidas de incertidumbre en la regresión

## Objetivo de la lectura

En esta lectura se explora la incertidumbre en el análisis de regresión a través de:

- Intervalos de confianza  
- Bandas de confianza  
- Valores p  

---

## Repaso de conceptos

La regresión lineal simple se puede expresar como:

$$
y = \beta_{0} + \beta_{1} X
$$

Dado que el análisis de regresión utiliza estimaciones, siempre existe incertidumbre. Para representarla, se agrega un término de error:

$$
y = \beta_{0} + \beta_{1} X + \epsilon
$$

Donde:

- $\epsilon$ representa el error (epsilon)  
- Cada punto tiene un **residuo** (diferencia entre valor real y predicho)  

---

## Medidas de incertidumbre

Podemos cuantificar la incertidumbre mediante:

- **Intervalos de confianza** de los coeficientes $\beta$  
- **Valores p** de los coeficientes  
- **Bandas de confianza** de la regresión  

### Definiciones clave

- **Intervalo de confianza:** rango de valores que describe la incertidumbre de una estimación  
- **Valor p:** probabilidad de observar resultados tan extremos como los obtenidos si la hipótesis nula es verdadera  

---

## Interpretación de resultados

En el modelo de regresión:

- $\hat{\beta}_{1} = 141.1904$  

Interpretación:

> Por cada milímetro adicional en la longitud del pico, la masa corporal aumenta en aproximadamente 141.19 gramos.

- **Valor p:** 0.000 (< 0.05) → estadísticamente significativo  
- **Intervalo de confianza (95 %):** [131.788, 150.592]  

---

## Valores p e hipótesis

En regresión, se realiza una prueba de hipótesis para cada coeficiente:

- **Hipótesis nula ($H_{0}$):**
$$
\beta_{1} = 0
$$

- **Hipótesis alternativa ($H_{1}$):**
$$
\beta_{1} \neq 0
$$

Dado que el valor p < 0.05:

- Se **rechaza $H_{0}$**  
- Existe evidencia de relación entre $X$ y $y$  

---

## Intervalos de confianza

Un intervalo de confianza del 95 % significa:

- Hay un 95 % de probabilidad de que el intervalo contenga el verdadero valor del parámetro  
- Existe un 5 % de probabilidad de que no lo contenga  

Interpretación más precisa:

> Si repitiéramos el experimento muchas veces, el 95 % de los intervalos construidos contendrían el valor real de $\beta_{1}$.

---

## Bandas de confianza

Debido a la incertidumbre en los coeficientes, también hay incertidumbre en las predicciones.

### Definición

- **Banda de confianza:** área alrededor de la línea de regresión que representa la incertidumbre de las predicciones  

### Características

- Rodea la línea de regresión  
- Es más estrecha cerca de la media de los datos  
- Se ensancha en los extremos  
- Resume los intervalos de confianza para todos los valores de $X$  

---

## Puntos clave

- La regresión siempre implica incertidumbre  
- Esta se mide con:
  - Intervalos de confianza  
  - Valores p  
  - Bandas de confianza  
- Para cada coeficiente, se prueba si:
$$
\beta = 0
$$
- Si el valor p es bajo, el coeficiente es significativo  

# Métricas de evaluación de la regresión lineal simple

## Introducción

En esta lectura se presenta una visión más completa de las métricas de evaluación utilizadas en la regresión lineal simple. Entre las principales métricas se encuentran:

- $R^{2}$ (coeficiente de determinación)  
- MSE (error cuadrático medio)  
- MAE (error absoluto medio)  

También se introducen métricas adicionales como AIC y BIC.

---

## Revisión de métricas principales

### $R^{2}$: Coeficiente de determinación

El coeficiente de determinación mide la proporción de la variabilidad de la variable dependiente $Y$ que es explicada por la(s) variable(s) independiente(s) $X$.

Se calcula como:

$$
R^{2} = 1 - \frac{\text{Suma de residuos al cuadrado}}{\text{Suma total de cuadrados}}
$$

Características:

- Toma valores entre 0 y 1  
- Un valor cercano a 1 indica mejor ajuste  

Ejemplo:

- $R^{2} = 0.85$ significa que el 85 % de la variación de $Y$ es explicada por $X$  

---

### MSE: Error cuadrático medio

El MSE mide el promedio de los errores al cuadrado entre los valores predichos y los reales:

$$
MSE = \frac{1}{n} \sum (y_{i} - \hat{y}_{i})^{2}
$$

Características:

- Penaliza fuertemente errores grandes  
- Sensible a valores atípicos  

---

### MAE: Error absoluto medio

El MAE mide el promedio del valor absoluto de los errores:

$$
MAE = \frac{1}{n} \sum |y_{i} - \hat{y}_{i}|
$$

Características:

- Más robusto frente a valores atípicos  
- No penaliza tanto los errores grandes  

---

## Otras métricas de evaluación

### AIC y BIC

- **AIC (Criterio de Información de Akaike)**  
- **BIC (Criterio de Información Bayesiano)**  

Se utilizan para:

- Comparar modelos  
- Evaluar el equilibrio entre ajuste y complejidad  

---

### $R^{2}$ ajustado

Es una versión modificada de $R^{2}$ que:

- Tiene en cuenta el número de variables independientes  
- Penaliza modelos innecesariamente complejos  

---

## Puntos clave

- Existen múltiples métricas para evaluar modelos de regresión  
- $R^{2}$ es la más común, pero no siempre suficiente  
- MSE y MAE permiten evaluar errores de predicción  
- AIC y BIC ayudan a comparar modelos  
- La elección de la métrica depende del contexto y los datos  

---