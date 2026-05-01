# 📊 Selección de Variables en Regresión Múltiple

## 🧠 Idea principal
El **sobreajuste** ocurre cuando un modelo se adapta demasiado a los datos de entrenamiento y no generaliza bien. Para mejorar la calidad del modelo, se utiliza el **R² ajustado**, que penaliza variables innecesarias. La **selección de variables** ayuda a construir modelos más eficientes y fiables.

---

## 🔍 ¿Qué es la selección de variables?

También conocida como **selección de características**, es el proceso de decidir qué variables independientes incluir en un modelo.

- Es un proceso **iterativo**.
- Mejora con la experiencia e intuición del analista.
- Busca un equilibrio entre:
  - Modelo demasiado simple ❌
  - Modelo demasiado complejo ❌

---

## ⚙️ Técnicas principales

### ➡️ Selección hacia adelante (Forward Selection)

- Comienza con un **modelo nulo** (sin variables).
- Se agregan variables **una a una**.
- En cada paso:
  - Se elige la variable que más mejora el modelo.
- Se detiene cuando:
  - No hay mejoras significativas.

---

### ⬅️ Eliminación hacia atrás (Backward Elimination)

- Comienza con el **modelo completo** (todas las variables).
- Se eliminan variables **una a una**.
- En cada paso:
  - Se elimina la variable menos relevante.
- Se detiene cuando:
  - No se pueden eliminar más variables sin afectar el modelo.

---

## 📏 Criterio de decisión: Prueba F

- Se utiliza la **prueba F de suma extra de cuadrados**.
- Compara:
  - Un modelo **completo** vs un modelo **reducido**.
- Evalúa cuánta varianza adicional explica un modelo más complejo.

### 📌 Interpretación

- Se basa en el **valor p**:
  - Valor p bajo → la variable aporta información significativa.
  - Valor p alto → la variable puede ser irrelevante.

---

## ⚖️ Importancia del R² ajustado

- Penaliza la inclusión de variables innecesarias.
- Es más confiable que el R² simple al comparar modelos.
- Ayuda a evitar el **sobreajuste**.

---

## 🧩 Conclusiones clave

- La selección de variables es esencial para construir buenos modelos.
- Las técnicas principales son:
  - Selección hacia adelante
  - Eliminación hacia atrás
- La prueba F ayuda a decidir qué variables incluir o eliminar.
- El proceso es iterativo y mejora con la práctica.
- Estas técnicas son la base para métodos más avanzados.

---

## ¿Cuál es el proceso para determinar qué variables o características incluir en un modelo determinado?

+ [ ] Selección de avance
+ ✔️ Selección de variables
+ [ ] Prueba F de suma de cuadrados extra
+ [ ] Eliminación hacia atrás

Correcto
La selección de variables es el proceso de determinar qué variables o características incluir en un modelo determinado. La selección de variables es iterativa. 