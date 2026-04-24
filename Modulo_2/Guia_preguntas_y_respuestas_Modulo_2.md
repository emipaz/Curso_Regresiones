# Guía de preguntas y respuestas – Módulo 2 (Regresión lineal simple)

Este archivo contiene **preguntas de reflexión y guías de respuesta** sobre los temas del Módulo 2, escritos en mis propias palabras. No reproduce enunciados oficiales del curso; su objetivo es ayudarme a estudiar y recordar los conceptos clave.

---

## 1. Diferencia entre valores observados y predichos

**Pregunta (guía):** ¿Cómo se llama la diferencia entre los valores reales y los valores predichos por una recta de regresión?

**Idea de respuesta:**
- Esa diferencia se llama **residuo**.
- El residuo mide cuánto se desvía el valor real del valor que predice el modelo para ese mismo punto.
- Analizar los residuos ayuda a evaluar la calidad del ajuste del modelo.

---

## 2. Método para estimar parámetros en regresión lineal

**Pregunta (guía):** ¿Qué método matemático se utiliza para encontrar los parámetros (pendiente e intercepto) de una recta de regresión lineal?

**Idea de respuesta:**
- Se utiliza el método de **Mínimos Cuadrados Ordinarios (MCO)**.
- Este método busca los valores de los parámetros que minimizan la suma de los residuos al cuadrado.
- Así se obtiene la mejor recta posible según el criterio de menor error cuadrático.

---

## 3. Supuestos de la regresión lineal simple

**Pregunta (guía):** ¿Qué significa que los residuos sean aleatorios y no sigan un patrón?

**Idea de respuesta:**
- Significa que se cumple el supuesto de **homoscedasticidad**.
- Los errores del modelo deben tener varianza constante para cualquier valor de X.
- Si los residuos muestran un patrón (por ejemplo, forma de U), puede indicar problemas de linealidad o heteroscedasticidad.

---

## 4. Interpretación de la matriz de dispersión

**Pregunta (guía):** ¿Para qué sirve una matriz de dispersión en el análisis de regresión?

**Idea de respuesta:**
- Permite visualizar la **relación** entre pares de variables.
- Ayuda a identificar correlaciones, patrones y posibles relaciones lineales o no lineales.

---

## 5. R al cuadrado y explicación de la variabilidad

**Pregunta (guía):** ¿Qué mide el estadístico R al cuadrado en un modelo de regresión lineal?

**Idea de respuesta:**
- Mide la **proporción de la variación** en la variable dependiente que es explicada por la variable independiente.
- Un valor alto indica que el modelo explica bien los datos; un valor bajo, que hay mucha variabilidad no explicada.

---

## 6. Correlación entre variables

**Pregunta (guía):** ¿Qué significa que la correlación entre la altitud y la presión atmosférica sea negativa?

**Idea de respuesta:**
- Significa que a mayor altitud, menor presión atmosférica.
- La correlación negativa indica que las variables se mueven en sentido opuesto.

---

## 7. Punto de las medias en la recta de regresión

**Pregunta (guía):** ¿Qué punto está siempre en la recta de regresión de dos variables?

**Idea de respuesta:**
- El punto formado por la media de X y la media de Y: (x̄, ȳ).
- La recta de regresión siempre pasa por ese punto.

---

## 8. Cálculo de los coeficientes de la recta

**Pregunta (guía):** ¿Cómo se calculan los coeficientes beta cero (intercepto) y beta uno (pendiente) en regresión lineal simple?

**Idea de respuesta:**
- Se calculan usando las fórmulas de mínimos cuadrados:
  - β₁ = Cov(X, Y) / Var(X)
  - β₀ = ȳ - β₁x̄
- El objetivo es minimizar la suma de los residuos al cuadrado.

---

## 9. Diagnóstico de supuestos a través de residuos

**Pregunta (guía):** ¿Qué indica si los residuos del modelo tienen forma de U cuando se grafican contra los valores predichos?

**Idea de respuesta:**
- Indica que no se cumple el supuesto de **linealidad** y/o **homoscedasticidad**.
- Puede ser necesario transformar variables o usar otro tipo de modelo.

---

## 10. Experimentos aleatorios y controlados

**Pregunta (guía):** ¿Qué caracteriza a un experimento aleatorio y controlado en análisis de datos?

**Idea de respuesta:**
- Se busca que las diferencias entre grupos sean observables y medibles.
- Se utiliza para argumentar causalidad entre variables.
- No siempre es posible controlar todos los factores, pero se intenta minimizar sesgos.

---

