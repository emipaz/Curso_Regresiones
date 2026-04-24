# Regresión Lineal Múltiple: Variables, Coeficientes e Interpretación

Anteriormente aprendimos sobre la **regresión lineal simple**.

Por ejemplo:

> Cuantos más anuncios utiliza una empresa, más clics recibe su sitio web.

Este es un caso ideal para regresión lineal simple porque existe:

- Una variable independiente $X$
- Una variable dependiente $Y$

Donde:

- $Y$ = número de clics en el sitio web (variable continua dependiente)
- $X$ = número de anuncios (variable independiente)

---

# Cuando una Variable No es Suficiente

Una empresa también podría querer analizar características específicas de cada anuncio para entender qué factores generan más clics.

Por ejemplo:

- ¿Los anuncios más cortos reciben más clics?
- ¿Los anuncios con llamado a la acción ("donar", "suscribirse") generan mejores resultados?
- ¿La cantidad de personas en la imagen influye?
- ¿El tipo de anuncio importa?

Para responder estas preguntas utilizamos **regresión lineal múltiple**.

---

# Definición de Regresión Lineal Múltiple

La **regresión lineal múltiple** es una técnica que estima la relación lineal entre:

- Una variable dependiente continua
- Dos o más variables independientes

---

# Recordatorio: Regresión Lineal Simple

$$
Y = \beta_0 + \beta_1 X
$$

Donde:

- $\beta_0$ = intercepto
- $\beta_1$ = pendiente
- $X$ = variable independiente

Ejemplo:

- $Y$ = clics en sitio web
- $X$ = cantidad de personas en el anuncio

---

# Agregando Más Variables

Supongamos que ahora agregamos la longitud del anuncio.

$$
Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2
$$

Donde:

- $X_1$ = cantidad de personas en el anuncio
- $X_2$ = longitud del anuncio

Los subíndices ayudan a diferenciar variables independientes.

---

# Forma General del Modelo

$$
Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \cdots + \beta_n X_n
$$

Esto permite incluir tantas variables predictoras como sea necesario.

---

# Ventajas del Modelo

Aunque las matemáticas sean más complejas, la regresión múltiple mantiene grandes ventajas:

- Interpretabilidad
- Comunicación clara de resultados
- Estimación del efecto de cada variable
- Aplicabilidad en negocios y ciencia de datos

---

# Importancia de Interpretar Bien los Coeficientes

Al agregar variables, los coeficientes requieren mayor cuidado.

Cada coeficiente representa el cambio esperado en $Y$ cuando esa variable cambia, **manteniendo constantes las demás**.

---

# Dos Conceptos Clave

## 1. Codificación Dummy (Variables Categóricas)

Permite usar variables categóricas dentro del modelo.

Ejemplo:

- Anuncio impreso
- Anuncio digital

Podemos convertir categorías en variables binarias:

- Impreso = 0
- Digital = 1

---

## 2. Términos de Interacción

Permiten modelar cuando dos variables afectan juntas a $Y$.

Ejemplo:

- Longitud del anuncio
- Tipo de anuncio

Tal vez los anuncios largos funcionan mejor solo en formato digital.

Modelo con interacción:

$$
Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \beta_3(X_1X_2)
$$

---

# Idea Final

La regresión lineal múltiple amplía enormemente el poder analítico de la regresión simple.

Nos permite entender:

- Qué variables importan
- Cuánto impactan
- Cómo interactúan entre sí

Es una de las herramientas más importantes en análisis predictivo y ciencia de datos.


## Rellene el espacio en blanco: _____ es una técnica que estima la relación lineal entre una variable dependiente continua y dos o más variables independientes.

- [ ] Regresión curva singular
- [ ] Regresión curva múltiple
- [x] Regresión lineal múltiple
- [ ] Regresión lineal singular

La regresión lineal múltiple es una técnica que estima la relación lineal entre una variable dependiente continua y dos o más variables independientes. La técnica de regresión múltiple puede arrojar resultados muy interpretables y comunicables. 

## ¿Qué concepto se refiere a cómo dos variables independientes afectan conjuntamente a la variable dependiente y?

- [ ] Una codificación en caliente
- [x] Términos de interacción
- [ ] Mínimos cuadrados ordinarios
- [ ] Banda de confianza
  
