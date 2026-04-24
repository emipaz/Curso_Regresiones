# Variables Categóricas y One-Hot Encoding en Regresión Múltiple

Como profesional del análisis de datos, muchas veces trabajarás con variables que **no son continuas**, sino **categóricas**.

## Ejemplos en anuncios web

- Blanco y negro vs color
- Tiene llamado a la acción vs no tiene
- Plataforma de streaming A, B o C

Estas variables pueden influir en la cantidad de clics recibidos.

---

# Problema: La Computadora Necesita Números

Los modelos de regresión trabajan con valores numéricos, por lo tanto debemos transformar categorías en números.

Existen dos técnicas principales:

- **One-Hot Encoding**
- **Label Encoding**

En este contenido nos enfocamos en **One-Hot Encoding**.

---

# ¿Qué es One-Hot Encoding?

Es una técnica que convierte una variable categórica en una o varias variables binarias:

- 1 = presencia de la categoría
- 0 = ausencia de la categoría

---

# Ejemplo 1: Llamado a la Acción (Sí / No)

Creamos una nueva variable:

$$
X_{action}
$$

Donde:

- Si el anuncio tiene llamado a la acción: $X_{action}=1$
- Si no lo tiene: $X_{action}=0$

---

# Modelo de Regresión

$$
Y=\beta_0+\beta_1X_1+\beta_2X_2+\beta_{action}X_{action}
$$

Donde:

- $X_1$ = número de personas en el anuncio
- $X_2$ = longitud del anuncio
- $X_{action}$ = llamado a la acción

---

# Interpretación de $\beta_{action}$

Si dos anuncios tienen el mismo:

- número de personas
- longitud

Pero uno tiene llamado a la acción y otro no, entonces:

$$
\beta_{action}
$$

representa la diferencia esperada en clics entre ambos anuncios.

---

# Ejemplo 2: Plataforma de Streaming (A, B, C)

Supongamos tres plataformas:

- Servicio A
- Servicio B
- Servicio C

Como solo se publica en una plataforma a la vez, necesitamos representar tres categorías.

---

# ¿Cuántas Variables Binarias Necesitamos?

Para $k$ categorías, usamos:

$$
k-1
$$

variables binarias.

Entonces, para 3 categorías:

$$
3-1=2
$$

Creamos:

- $X_{A}$
- $X_{B}$

Y la categoría restante (**Servicio C**) será la referencia.

---

# Codificación

| Servicio | $X_A$ | $X_B$ |
|--------|------|------|
| A | 1 | 0 |
| B | 0 | 1 |
| C | 0 | 0 |

---

# Modelo con Variables Dummy

$$
Y=\beta_0+\beta_1X_1+\beta_2X_2+\beta_AX_A+\beta_BX_B
$$

No aparece $X_C$ porque el servicio C es la categoría base.

---

# Interpretación de Coeficientes

## $\beta_A$

Diferencia esperada en clics entre:

- anuncio en servicio A
- anuncio equivalente en servicio C

## $\beta_B$

Diferencia esperada en clics entre:

- anuncio en servicio B
- anuncio equivalente en servicio C

---

# ¿Por Qué No Incluir Servicio C?

Porque si agregamos A, B y C al mismo tiempo se genera **multicolinealidad perfecta** (dummy variable trap).

Por eso siempre se elimina una categoría y se usa como referencia.

---

# Aplicación en Python

Usualmente se realiza con:

```python
pd.get_dummies(df, drop_first=True)
```

o con

```python
OneHotEncoder()
```

## Idea Final

One-Hot Encoding permite incluir variables categóricas en modelos de regresión lineal múltiple transformándolas en variables binarias.

Esto permite medir el impacto de categorías como:

- tipo de anuncio
- plataforma
- color
- presencia de llamado a la acción

Es una herramienta esencial en ciencia de datos.

## ¿Qué técnica de transformación de datos convierte una variable categórica en varias variables binarias?

- [ ] Regresión múltiple
- [ ] R cuadrado ajustado
- [x] Una codificación One-Hot
- [ ] Codificación de etiquetas

Correcto
Comentarios: La codificación one-hot es una técnica de transformación de datos que convierte una variable categórica en varias variables binarias. Los profesionales de los datos utilizan la codificación one-hot cuando hay una variable categórica independiente y necesitan representar la categoría como números.


