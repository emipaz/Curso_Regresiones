# Interpretación de Resultados en Regresión Lineal Múltiple

Ya aprendimos anteriormente cómo interpretar una **regresión lineal simple**.

Por ejemplo, entre:

- Temperatura
- Ventas de café helado

Un gráfico de dispersión podría mostrar una relación creciente.

---

# Ejemplo de Regresión Simple

Supongamos el modelo:

$$
Ventas = -44 + 2.2 \cdot Temperatura
$$

## Interpretación

Por cada aumento de **1 grado** en la temperatura:

$$
Ventas \uparrow 2.2
$$

ventas adicionales de café helado, en promedio.

---

# Limitación del Modelo Simple

La temperatura explica parte importante de las ventas, pero no todo.

También pueden influir factores controlables por la empresa:

- Publicidad cercana
- Ubicación de la tienda
- Cercanía al transporte público
- Competencia cercana

---

# Modelo con Variable Binaria: Publicidad

Agregamos una variable:

$$
X_{ad}
$$

Donde:

- $X_{ad}=1$ si hay anuncio cerca
- $X_{ad}=0$ si no hay anuncio

---

# Modelo

$$
Ventas = \beta_0 + \beta_T X_T + \beta_{ad}X_{ad}
$$

Donde:

- $X_T$ = temperatura
- $X_{ad}$ = anuncio

---

# Interpretación del Anuncio

## Caso 1: Hay anuncio

Temperatura = 75°F

$$
Ventas=\beta_0+\beta_T(75)+\beta_{ad}(1)
$$

## Caso 2: No hay anuncio

$$
Ventas=\beta_0+\beta_T(75)+\beta_{ad}(0)
$$

$$
Ventas=\beta_0+\beta_T(75)
$$

## Conclusión

$\beta_{ad}$ representa el aumento promedio de ventas asociado con tener publicidad cercana, manteniendo constante la temperatura.

---

# Modelo con Variable Continua: Distancia al Transporte

Nueva variable:

$$
X_{transporte}
$$

Distancia en kilómetros a:

- Bus
- Tren
- Metro

---

# Modelo

$$
Ventas=\beta_0+\beta_T X_T+\beta_D X_D
$$

Donde:

- $X_T$ = temperatura
- $X_D$ = distancia al transporte

---

# Interpretación de Coeficientes

## Temperatura

Por cada aumento de 1 grado, manteniendo fija la distancia:

$$
Ventas \uparrow \beta_T
$$

## Distancia

Por cada kilómetro adicional lejos del transporte, manteniendo fija la temperatura:

$$
Ventas \downarrow \beta_D
$$

(si $\beta_D < 0$)

---

# Regla Fundamental

En regresión múltiple, cada coeficiente se interpreta:

> Manteniendo constantes las demás variables.

---

# Términos de Interacción

A veces una variable cambia el efecto de otra.

Ejemplo:

- En días fríos, la cercanía al transporte puede importar más.
- En días muy calurosos, la temperatura domina.

---

# Modelo con Interacción

$$
Ventas=\beta_0+\beta_T X_T+\beta_D X_D+\beta_I(X_T \cdot X_D)
$$

---

# ¿Qué Significa la Interacción?

El efecto de la temperatura depende de la distancia al transporte, y viceversa.

No existe un único efecto fijo.

---

# Ejemplo Intuitivo

Si $\beta_I < 0$:

- En tiendas lejanas al transporte, subir temperatura aumenta menos ventas.

Si $\beta_I > 0$:

- En tiendas cercanas al transporte, el calor impulsa más ventas.

---

# Resumen General

## Sin interacción

Cada variable tiene un efecto fijo.

## Con interacción

El efecto de una variable depende del valor de otra.

---

# Habilidades Clave del Analista

Debes aprender a:

- Construir modelos
- Interpretar coeficientes
- Traducir resultados al negocio
- Contar historias con datos

---

# Idea Final

La regresión múltiple permite entender fenómenos reales mucho mejor que la regresión simple.

Y los términos de interacción ayudan a capturar relaciones más complejas entre variables.

## Rellene el espacio en blanco: Un término de interacción representa la relación entre dos variables independientes y el cambio en la media de la variable _____.

- [ ] global
- [ ] instancia
- [ ] independiente
- [x] dependiente

Un término de interacción representa la relación entre dos variables independientes y el cambio en la media de la variable dependiente. Normalmente, es el producto de las dos variables independientes.