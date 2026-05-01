# ⚖️ Sesgo, Varianza y Regularización en Regresión

## 🧠 Idea principal
El **sobreajuste** está relacionado con el equilibrio entre **sesgo** y **varianza**. Para mejorar la capacidad de generalización de un modelo, se utilizan técnicas de **regularización**, que introducen sesgo para reducir la varianza.

---

## ⚖️ Equilibrio entre sesgo y varianza

- **Sesgo (bias):**
  - Simplifica el modelo mediante suposiciones.
  - Alto sesgo → modelo demasiado simple → **infraajuste**.

- **Varianza (variance):**
  - Mide la sensibilidad del modelo a los datos de entrenamiento.
  - Alta varianza → modelo muy complejo → **sobreajuste**.

📌 Objetivo:
Lograr un equilibrio que minimice el error en datos no observados.

---

## 📉 Regularización

La **regularización** es un conjunto de técnicas que:

- Reducen los coeficientes del modelo.
- Introducen **cierto sesgo** para disminuir la varianza.
- Ayudan a prevenir el **sobreajuste**.

---

## 🔧 Tipos de regresión regularizada

### 🔹 Regresión Lasso

- Reduce algunos coeficientes a **cero**.
- Elimina variables irrelevantes automáticamente.
- Útil para **selección de variables**.

---

### 🔹 Regresión Ridge

- Reduce la magnitud de los coeficientes.
- **No elimina variables**.
- Ideal cuando se desea mantener todos los predictores.

---

### 🔹 Regresión Elastic Net

- Combina **Lasso** y **Ridge**.
- Permite:
  - Selección de variables
  - Reducción de coeficientes
- Útil cuando no está claro qué variables conservar.

---

## ⚠️ Consideraciones

- La regularización mejora el rendimiento en datos nuevos.
- Sin embargo:
  - Los coeficientes se vuelven **más difíciles de interpretar**.
- Es especialmente útil en **grandes conjuntos de datos**.

---

## 🧩 Conclusiones clave

- El sobreajuste está ligado a una alta varianza.
- El infraajuste está ligado a un alto sesgo.
- No se puede eliminar completamente el trade-off entre sesgo y varianza.
- La regularización ayuda a encontrar un mejor equilibrio.
- Lasso, Ridge y Elastic Net son herramientas clave en este proceso.

---