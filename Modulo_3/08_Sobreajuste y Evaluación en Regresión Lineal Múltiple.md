# Sobreajuste y Evaluación en Regresión Lineal Múltiple

Hasta ahora extendimos la **regresión lineal simple** hacia la **regresión lineal múltiple**, una herramienta poderosa para estimar una variable continua usando varias variables independientes.

Sin embargo, toda herramienta tiene limitaciones.

---

# Recordatorio: ¿Qué es $R^2$?

El coeficiente de determinación mide la proporción de variabilidad de la variable dependiente explicada por el modelo.

$$
R^2 = \frac{\text{Varianza explicada}}{\text{Varianza total}}
$$

Valores posibles:

$$
0 \leq R^2 \leq 1
$$

---

# Interpretación

- $R^2 = 0$ → el modelo no explica nada  
- $R^2 = 1$ → explica perfectamente los datos  
- $R^2 = 0.80$ → explica el 80% de la variabilidad de $Y$

---

# Problema en Regresión Múltiple

Cuando agregamos nuevas variables al modelo:

$$
Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + ... + \beta_nX_n
$$

el valor de $R^2$ **nunca disminuye**.

Siempre se mantiene igual o aumenta.

---

# ¿Por Qué Es un Problema?

Porque una variable nueva puede:

- no aportar información real
- introducir ruido
- complicar el modelo
- mejorar artificialmente $R^2$

Esto puede dar la falsa impresión de que el modelo es mejor.

---

# Sobreajuste (Overfitting)

El **sobreajuste** ocurre cuando el modelo aprende demasiado bien los datos de entrenamiento, incluyendo ruido y patrones accidentales.

Como resultado:

- funciona excelente en entrenamiento
- falla en datos nuevos
- no generaliza a la población

---

# Idea Visual

## Modelo sano

Aprende patrones reales.

## Modelo sobreajustado

Memoriza el dataset.

---

# Causas Comunes del Sobreajuste

- Demasiadas variables
- Modelo excesivamente complejo
- Poco volumen de datos
- Variables irrelevantes
- Colinealidad alta

---

# Cómo Detectarlo

## Separación Train/Test

Reservamos parte de los datos para prueba.

```python
train_test_split(...)
```
Entrenamos con una parte y evaluamos con otra.

Si:

- desempeño alto en train
- desempeño bajo en test

hay probable sobreajuste.

## $R^2$ Ajustado

Es una versión corregida de $R^2$ que penaliza variables innecesarias.

$$
R^2_{\text{ajustado}} = 1 - \left(\frac{(1 - R^2)(n - 1)}{n - p - 1}\right)
$$

Donde:

- $n$ = número de observaciones
- $p$ = número de predictores

## Ventaja del $R^2$ Ajustado

A diferencia de $R^2$:

- puede subir
- puede bajar

Si agregas una variable inútil, puede disminuir.

### ¿Cuándo Usar Cada Métrica?

$R^2$

- Útil para interpretar cuánto explica el modelo.

$R^2$ Ajustado

- Útil para comparar modelos con distinta cantidad de variables.

Ejemplo Conceptual

| Modelo | Variables | $R^2$ | $R^2_{adj}$ |
| ------ | --------- | ----- | ----------- |
| A      | 2         | 0.78  | 0.77        |
| B      | 8         | 0.81  | 0.74        |

Aunque B tiene mayor $R^2$, A generaliza mejor.

## Próximo Paso: Selección de Variables

Necesitamos decidir:

- qué variables incluir
- cuáles eliminar
- cuáles realmente aportan valor

Esto lleva a técnicas como:

- Forward Selection
- Backward Elimination
- Stepwise Selection
- Lasso
- Ridge

## Idea Final

No busques solo maximizar $R^2$.

Busca modelos que sean:

- precisos
- interpretables
- simples
- robustos
- generalizables

El mejor modelo no es el más complejo, sino el que mejor funciona en datos nuevos.