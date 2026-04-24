# Regresión Lineal Múltiple en Python con Statsmodels

Ahora pasamos de la teoría a la práctica usando **Python**.

Al igual que en regresión lineal simple, el modelo busca minimizar:

$$
\sum (y_i-\hat{y}_i)^2
$$

Es decir, la **suma de residuos al cuadrado**.

---

# Dataset de Pingüinos

Usaremos nuevamente el dataset de pingüinos para predecir:

$$
Masa\ corporal
$$

a partir de otras variables.

## Variables disponibles

- `body_mass_g`
- `bill_length_mm`
- `sex`
- `species`

---

### Vista Rápida de los Datos

```python
penguins.head()
```

## Definir Variables

### Variable Dependiente

```python
y = penguins["body_mass_g"]
```

### Variables Independientes

```python
X = penguins[["bill_length_mm", "sex", "species"]]
```

## Separar Entrenamiento y Prueba

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.30,
    random_state=42
)
```

Explicación

test_size=0.30

- Reserva el 30% de los datos para prueba.

random_state=42

- Permite reproducir exactamente la misma división.

## Crear Modelo con Statsmodels

```python
import statsmodels.formula.api as smf

formula = "body_mass_g ~ bill_length_mm + C(sex) + C(species)"
```

**Importante**

`C(...)` indica que la variable es categórica.

Statsmodels automáticamente crea variables dummy.

## Ajustar Modelo

model = smf.ols(formula=formula, data=penguins).fit()

## Ver Resumen Estadístico

print(model.summary())

## Interpretación de Coeficientes

Variable C(sex)[T.male]

Si:
- macho = 1
- hembra = categoría base

Entonces el coeficiente indica diferencia entre machos y hembras manteniendo constantes otras variables.

Resultado: 

+528.95 g

Los machos pesan aproximadamente 528.95 gramos más que hembras equivalentes.

Además:

- mismo pico
- misma especie

## Significancia Estadística

El valor p es muy pequeño:

- p < 0.05

Por lo tanto, el coeficiente es estadísticamente significativo.

## Variable Continua: Longitud del Pico

- Coeficiente: 35.55

Interpretación:

Si dos pingüinos tienen mismo sexo y especie, pero uno tiene pico 1 mm más largo:

Masa corporal ↑35.55 g

## Métrica del Modelo: $R^2$

Resultado:

$R^2 = 0.85$

Interpretación

El modelo explica aproximadamente:

85%

de la variabilidad en la masa corporal.

## ¿Es Bueno?

En principio, sí.

Pero en regresión múltiple también debemos revisar:

- Ajusted $R^2$
- RMSE
- MAE
- Supuestos del modelo
- Multicolinealidad
- Residuos

## Ventaja de Statsmodels

Entrega automáticamente:

- Coeficientes
- Error estándar
- Estadístico t
- Valor p
- Intervalos de confianza
- $R^2$
- F-statistic

## Código Completo

```python
import pandas as pd
import statsmodels.formula.api as smf
from sklearn.model_selection import train_test_split

X = penguins[["bill_length_mm", "sex", "species"]]
y = penguins["body_mass_g"]

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.30, random_state=42
)

formula = "body_mass_g ~ bill_length_mm + C(sex) + C(species)"

model = smf.ols(formula=formula, data=penguins).fit()

print(model.summary())
```

 ## Idea Final

Construir modelos en Python es rápido.

El verdadero valor del analista está en:

- elegir variables correctas
- interpretar coeficientes
- validar supuestos
- comunicar hallazgos al negocio



## Rellene el espacio en blanco: Un término de interacción representa cómo la relación entre dos variables independientes se asocia con los cambios en la _____ de la variable dependiente.

. [ ] categoría
. [ ] tasa de cambio
. [x] media
. [ ] multicolinealidad

Un término de interacción representa cómo se asocia la relación entre dos variables independientes con los cambios en la media de la variable dependiente. Normalmente, los profesionales de los datos representan un término de interacción como el producto de las dos variables independientes en cuestión.

## ¿Cuál de los siguientes estadísticos relevantes puede encontrarse utilizando la función OLS de statsmodel? Seleccione todas las que correspondan.

- [x] Valores P
- [x] Coeficientes
- [ ] Factores de inflación de la varianza 
- [x] Errores estándar

Los coeficientes, los errores estándar, los valores p y los estadísticos t pueden hallarse utilizando la función OLS de statsmodel.