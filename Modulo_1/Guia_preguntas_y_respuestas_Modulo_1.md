# Guía de preguntas y respuestas – Módulo 1 (Regresión)

Este archivo contiene **preguntas de reflexión y guías de respuesta** sobre los temas del Módulo 1, escritos en mis propias palabras. No reproduce enunciados oficiales del curso; su objetivo es ayudarme a estudiar y recordar los conceptos clave.

---

## 1. Conceptos clave de regresión

**Pregunta (guía):** ¿Qué problema intenta resolver un modelo de regresión lineal?

**Idea de respuesta:**
- Busca modelar la relación entre una variable objetivo numérica (por ejemplo, ventas) y una o más variables explicativas (por ejemplo, inversión en marketing).
- Permite **predecir** valores futuros de la variable objetivo.
- Ayuda a **interpretar** cómo cambia la variable objetivo cuando cambian las variables explicativas.

---

**Pregunta (guía):** ¿Qué diferencia hay entre regresión lineal simple y múltiple?

**Idea de respuesta:**
- En la **regresión lineal simple** hay una sola variable explicativa.
- En la **regresión lineal múltiple** hay dos o más variables explicativas.
- La interpretación de los coeficientes cambia: en la múltiple, cada coeficiente se interpreta manteniendo constantes las demás variables.

---

## 2. PACE aplicado a problemas de regresión

**Pregunta (guía):** ¿Cómo aplico el enfoque PACE (Plan, Analyze, Construct, Execute/Communicate) a un problema de regresión?

**Idea de respuesta (resumen):**
- **Plan:** Clarificar el objetivo del análisis, la pregunta de negocio y las variables disponibles.
- **Analyze:** Explorar los datos (distribuciones, outliers, relaciones entre variables, correlaciones).
- **Construct:** Construir uno o varios modelos de regresión, probar supuestos, seleccionar variables.
- **Execute/Communicate:** Generar resultados, interpretar coeficientes, evaluar el desempeño del modelo y comunicar conclusiones a personas no técnicas.

---

## 3. Supuestos básicos de la regresión lineal

**Pregunta (guía):** ¿Cuáles son algunos supuestos importantes de la regresión lineal (a nivel intuitivo)?

**Idea de respuesta:**
- Relación aproximadamente **lineal** entre predictores y variable objetivo.
- **Independencia** de los errores (las observaciones no se influyen entre sí).
- **Homocedasticidad**: la variabilidad de los errores es similar a lo largo del rango de predicción.
- Errores aproximadamente **normales** (especialmente importante para inferencia).

---

## 4. Interpretación de coeficientes

**Pregunta (guía):** ¿Cómo interpreto el coeficiente de una variable en regresión lineal simple?

**Idea de respuesta:**
- Representa el cambio promedio en la variable objetivo cuando la variable explicativa aumenta en una unidad, **manteniendo todo lo demás igual** (en la simple solo hay una variable explicativa).
- El signo (+ o −) indica la dirección de la relación.

---

## 5. Evaluación del modelo

**Pregunta (guía):** ¿Qué métricas sencillas puedo usar para evaluar un modelo de regresión?

**Idea de respuesta:**
- Error cuadrático medio (MSE/MSE) o raíz del error cuadrático medio (RMSE) para medir qué tan lejos están las predicciones de los valores reales.
- Coeficiente de determinación (R²) para ver qué proporción de la variabilidad de la variable objetivo explica el modelo.
- Comparar estas métricas entre modelos distintos y con un modelo base simple.

---

## 6. Preguntas de reflexión sobre negocio

**Pregunta (guía):** ¿Cómo conecto los resultados de una regresión con la toma de decisiones?

**Idea de respuesta:**
- Traducir los coeficientes a lenguaje de negocio (por ejemplo, “por cada unidad adicional de X, esperamos un cambio promedio de Y en las ventas”).
- Usar el modelo para comparar escenarios (¿qué pasa si incre­mento cierta variable?).
- Señalar limitaciones: correlación no implica causalidad, el modelo depende de la calidad y representatividad de los datos.

---

## 7. Conexiones con el desafío del módulo

Las siguientes preguntas están pensadas para ayudarte a responder el desafío del módulo usando los **mismos términos** (regresión lineal, regresión logística, variable dependiente, variable independiente, correlación, causalidad, parámetros, coeficientes, función de enlace, etc.), pero sin copiar las preguntas originales.

---

### 7.1 Naturaleza de los modelos de regresión

**Pregunta (guía):** ¿Por qué los modelos de regresión se consideran técnicas estadísticas y no solo de programación o de aplicación?

**Idea de respuesta:**
- Porque se basan en **métodos estadísticos** para estimar la relación entre una **variable dependiente** (Y) y una o más **variables independientes** (X).
- Utilizan conceptos como parámetros poblacionales ($\mu_y$, $\beta$) y estimadores muestrales ($\hat{Y}$, $\hat{\beta}$).
- El foco está en **inferir** y **cuantificar** relaciones, no solo en ejecutar código.

Checklist mental para el desafío:
- Si la frase habla de estimar relaciones entre Y y X usando datos, piensa en "técnicas estadísticas".

---

### 7.2 Regresión lineal simple y media de Y

**Pregunta (guía):** Cuando aplicas regresión lineal simple, ¿qué cantidad estás intentando estimar para un valor concreto de X?

**Idea de respuesta:**
- Estimo la **media esperada de Y dado X**.
- Es decir, el valor promedio de la variable dependiente para un valor específico de la variable independiente.

Checklist mental para el desafío:
- Si ves "regresión lineal simple" y "dado un valor de X", asocia con "media de Y".

---

### 7.3 Variables dependiente e independiente

**Pregunta (guía):** ¿Cómo distingo claramente entre variable dependiente e independiente y qué símbolos suelen usarse para cada una?

**Idea de respuesta:**
- La **variable dependiente** es la que intento **estimar o predecir**; suele representarse por **Y**.
- Las **variables independientes** son las que uso para explicar o predecir Y; suelen representarse por **X**.
- Y "depende" de X: los cambios en X se asocian con cambios en Y.

Checklist mental para el desafío:
- "Dependiente" → resultado, respuesta, salida → Y.
- "Independiente" → predictor, explicativa, entrada → X.

---

### 7.4 Correlación positiva, negativa y causalidad

**Pregunta (guía):** ¿Cómo diferencio correlación positiva, correlación negativa y causalidad?

**Idea de respuesta:**
- **Correlación positiva:** cuando una variable aumenta, la otra tiende a **aumentar también**.
- **Correlación negativa:** cuando una variable aumenta, la otra tiende a **disminuir**.
- **Causalidad:** implica que cambios en una variable **provocan directamente** cambios en la otra.

Checklist mental para el desafío:
- Si ambas variables se mueven en la **misma dirección**, piensa en **correlación positiva**.
- Si se mueven en **direcciones opuestas**, piensa en **correlación negativa**.
- Si la frase habla de "lleva directamente a" o "provoca", piensa en **causalidad**.

---

### 7.5 Parámetros y coeficientes de regresión

**Pregunta (guía):** ¿Qué diferencia hay entre parámetros poblacionales y coeficientes de regresión estimados?

**Idea de respuesta:**
- Los **parámetros** (por ejemplo, $\mu_y$, $\beta_0$, $\beta_1$) describen la relación verdadera en la **población**, pero no los conocemos exactamente.
- Los **coeficientes de regresión estimados** (por ejemplo, $\hat{\beta}_0$, $\hat{\beta}_1$) son los valores que obtenemos a partir de la **muestra**.
- Los parámetros son "verdaderos pero desconocidos"; los coeficientes estimados son "nuestros mejores estimadores".

Checklist mental para el desafío:
- Si aparece la idea de "propiedades de la población" → **parámetros**.
- Si se habla de "betas estimadas" o "con sombrero" → **coeficientes de regresión**.

---

### 7.6 Regresión lineal vs regresión logística

**Pregunta (guía):** ¿Cuándo es más apropiado usar regresión lineal y cuándo regresión logística?

**Idea de respuesta:**
- Usa **regresión lineal** cuando la **variable dependiente es continua** (por ejemplo, ingreso, ventas, tiempo).
- Usa **regresión logística** cuando la **variable dependiente es categórica**, típicamente binaria (por ejemplo, "volverá/no volverá", "compra/no compra").
- En ambos casos puedes tener una o más variables independientes.

Checklist mental para el desafío:
- Si el problema habla de **probabilidad de que ocurra algo (sí/no)** → piensa en **regresión logística**.
- Si el resultado es un **número continuo** → piensa en **regresión lineal**.

---

### 7.7 Función de enlace

**Pregunta (guía):** ¿Qué papel juega la función de enlace en un modelo de regresión (por ejemplo, en la regresión logística)?

**Idea de respuesta:**
- Una **función de enlace** conecta matemáticamente la **variable dependiente** con las **variables independientes**.
- Transforma la escala de la variable dependiente para que el modelo lineal sea adecuado (por ejemplo, el logit en regresión logística).
- Permite expresar la relación entre Y y X de forma compatible con la naturaleza de Y (probabilidades, conteos, etc.).

Checklist mental para el desafío:
- Si la frase habla de "conectar" o "vincular" Y con X mediante una función, piensa en **función de enlace**.

---

### 7.8 Interpretación de ecuaciones de regresión

**Pregunta (guía):** Si tienes una ecuación de regresión de la forma $\hat{Y} = 3 + 4X$, ¿cómo interpretas la pendiente y la intersección?

**Idea de respuesta:**
- La **pendiente** es 4: por cada aumento de 1 unidad en X, espero en promedio un aumento de **4 unidades en Y**.
- La **intersección** (o intercepto) es 3: es el valor esperado de Y cuando X es 0.

**Pregunta (guía):** En la forma general $\hat{Y} = \beta_0 + \beta_1 X$, ¿qué significan $\beta_0$ y $\beta_1$?

**Idea de respuesta:**
- $\beta_0$ es la **intersección** (valor esperado de Y cuando X=0).
- $\beta_1$ es la **pendiente** (cambio esperado en Y cuando X aumenta en 1 unidad).
- La ecuación es **lineal** en los parámetros y en X.

Checklist mental para el desafío:
- Si la afirmación habla de "aumento de 1 en X" y cambio en Y, piensa en la **pendiente** ($\beta_1$).
- Si menciona el valor de Y cuando X es 0, piensa en la **intersección** ($\beta_0$).

---

> Nota: Este documento es de uso personal como guía de estudio. No contiene ni pretende contener enunciados textuales del curso original, sino resúmenes e interpretaciones propias de los conceptos vistos.
