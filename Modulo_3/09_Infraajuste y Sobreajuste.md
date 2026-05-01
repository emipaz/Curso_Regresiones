# 📊 Infraajuste y Sobreajuste en Regresión Múltiple

## 🧠 Idea principal
Un modelo de regresión múltiple se construye con datos de muestra para aplicarse a datos no vistos. Para que sea fiable, debe evitar dos problemas clave: **infraajuste** y **sobreajuste**.

---

## ⚠️ Formas en que un modelo puede ser poco fiable

### 🔹 Infraajuste (Underfitting)
Ocurre cuando el modelo **no capta el patrón subyacente** de los datos.

- Se caracteriza por un **R-cuadrado bajo**.
- Posibles causas:
  - Predictores irrelevantes o débiles.
  - Falta de variables importantes.
  - Tamaño de muestra insuficiente.
- Consecuencia:
  - No funciona bien ni en datos de entrenamiento ni en datos nuevos.

**Ejemplo:**
Un modelo que predice el precio de un coche usando solo el color y el año probablemente fallará por no incluir variables como kilometraje o marca.

---

## 🔀 División de datos

Antes de entrenar el modelo:

- **Datos de entrenamiento:** se usan para construir el modelo.
- **Datos de prueba (o validación):** se usan para evaluar su rendimiento.

Este proceso se llama **muestreo de retención**.

---

### 🔸 Sobreajuste (Overfitting)
Ocurre cuando el modelo se ajusta **demasiado bien a los datos de entrenamiento**, pero falla con datos nuevos.

- Aprende tanto la **señal** como el **ruido**.
- Tiene:
  - Buen rendimiento en entrenamiento.
  - Mal rendimiento en prueba.

**Problema clave:**
El modelo se vuelve demasiado específico y no generaliza.

---

## 📈 R-cuadrado y su problema

- El **R-cuadrado** mide qué proporción de la variabilidad del resultado explica el modelo.
- ⚠️ Problema:
  - **Siempre aumenta al agregar más variables**, incluso si no son relevantes.
  - Puede dar una **falsa sensación de mejora**.

---

## ✅ R-cuadrado ajustado

El **R-cuadrado ajustado** corrige este problema:

- Penaliza la inclusión de variables irrelevantes.
- Solo aumenta si los nuevos predictores son útiles.
- Es mejor para comparar modelos con distinto número de variables.

---

## ⚖️ Sesgo vs Varianza

- **Alto sesgo → Infraajuste**
- **Alta varianza → Sobreajuste**

Existe un equilibrio inevitable:

> Reducir el sesgo aumenta la varianza, y viceversa.

🎯 Objetivo: lograr un balance adecuado.

---

### 🔎 Aclaración: "sesgo" y "varianza" en distintos dominios

Es frecuente confundir términos porque se usan en contextos distintos. Aquí una guía clara para no mezclar dominios.

**Analogía rápida**
- **Sesgo:** los dardos apuntan sistemáticamente lejos del centro (error sistemático).
- **Varianza:** los dardos están muy dispersos entre sí (inestabilidad).
- **Desviación estándar:** medida de esa dispersión (raíz cuadrada de la varianza).

**Definiciones formales estimador $\hat\theta$**
- Bias: $$\mathrm{Bias}(\hat\theta)=\mathbb{E}[\hat\theta]-\theta.$$
- Varianza: $$\mathrm{Var}(\hat\theta)=\mathbb{E}\big[(\hat\theta-\mathbb{E}[\hat\theta])^2\big].$$
- Desviación estándar: $$\mathrm{SD}(\hat\theta)=\sqrt{\mathrm{Var}(\hat\theta)}.$$
- Error cuadrático medio: $$\mathrm{MSE}(\hat\theta)=\mathbb{E}[(\hat\theta-\theta)^2]=\mathrm{Bias}(\hat\theta)^2+\mathrm{Var}(\hat\theta).$$

**¿Por qué se confunden? — dominios y ejemplos**
- **Sesgo de muestreo**: la muestra no representa la población (p. ej. encuestas solo a jóvenes). Es una fuente de error sistemático, distinto de la fórmula del bias de un estimador aunque ambos causan errores sistemáticos.
- **Sesgo del modelo (ML)**: asunciones del modelo (p. ej. linealidad) que producen error sistemático (underfitting).
- **Varianza (estadística)**: propiedad de una distribución (como arriba).
- **Varianza del modelo (ML)**: sensibilidad del modelo a diferentes muestras de entrenamiento (alta varianza → overfitting).
- **Desviación estándar** es simplemente la raíz cuadrada de la varianza — misma información en otra escala.

Regla práctica:
- Si hablas de que la muestra es no representativa → hablas de **sesgo de muestreo**.
- Si hablas de comportamiento en repeticiones muestrales → hablas de **bias/variance estadístico**.
- Si hablas de ajuste entrenamiento vs prueba → hablas de **sesgo/varianza en ML** (under/overfitting).

**Ejemplo simple**  
Estimar la media poblacional:
- Tomar siempre una muestra sesgada → sesgo de muestreo (estimador sistemáticamente equivocado).
- Usar la media muestral $\bar X$ con muestras aleatorias: $\mathrm{Bias}(\bar X)=0$ y $\mathrm{Var}(\bar X)=\sigma^2/n$. La desviación estándar de $\bar X$ es $\sigma/\sqrt{n}$ (error estándar).

**Mini-experimento reproducible (ver empíricamente bias y varianza)**

```python
import numpy as np

def bias_var_sim(degree=1, n=50, reps=1000):
    x = np.linspace(-1,1,n)
    f = lambda x: x**2
    x0 = 0.1
    preds = []
    for _ in range(reps):
        y = f(x) + np.random.normal(0,0.3,size=n)
        coef = np.polyfit(x,y,deg=degree)
        p = np.poly1d(coef)(x0)
        preds.append(p)
    preds = np.array(preds)
    bias = preds.mean() - f(x0)
    var = preds.var()
    return bias, var

# Probar degree=1 (alto sesgo), degree=2 (ajuste correcto), degree=9 (alta varianza)
```

## 🧩 Conclusiones clave

- El infraajuste y el sobreajuste afectan la fiabilidad del modelo.
- Evaluar tanto datos de entrenamiento como de prueba es esencial.
- Un R-cuadrado alto no garantiza un buen modelo.
- El R-cuadrado ajustado es una métrica más confiable.
- No se pueden eliminar completamente estos problemas, pero sí reducirlos significativamente.

---