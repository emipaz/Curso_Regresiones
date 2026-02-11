# Función de enlace vs. función de activación

## Función de enlace (regresión logística / modelos estadísticos)

En **regresión logística** y en los **modelos lineales generalizados (GLM)**, la **función de enlace**:

- Conecta el **valor esperado de la variable dependiente** con una combinación lineal de las variables independientes.
- Transforma la probabilidad para que pueda expresarse como:
  
  $$
  g(\mathbb{E}[y \mid x]) = \beta_0 + \beta_1 x
  $$

- En regresión logística, la función de enlace más común es el **logit**:

  $$
  g(p) = \log\left(\frac{p}{1 - p}\right)
  $$

- Esta función permite modelar probabilidades (entre 0 y 1) usando una expresión lineal.

## Función de activación (machine learning / redes neuronales)

En **machine learning**, especialmente en **redes neuronales**, una **función de activación**:

- Se aplica a la salida de una combinación lineal de entradas y pesos.
- Introduce **no linealidad** en el modelo.
- Decide cómo se transforma la señal antes de pasar a la siguiente capa.

Ejemplo general:
$$
z = w^T x + b
$$

$$
a = f(z)
$$

donde $f$ es la función de activación.

## Relación entre ambas

👉 En el caso específico de la **regresión logística**:

- La **función sigmoide** actúa como **función de activación** en machine learning.
- Y esa misma sigmoide es la **inversa de la función de enlace logit** en estadística.

Es decir:

- **Función de enlace**: logit  
- **Función de activación**: sigmoide  

Ambas describen **la misma relación matemática**, pero vistas desde enfoques distintos:
- Estadístico (GLM)  
- Machine learning (modelos predictivos)

## Diferencia clave

- La **función de enlace** se define sobre la **media/probabilidad**.
- La **función de activación** se define sobre la **salida lineal del modelo**.

## Resumen rápido

- ✔️ Están matemáticamente conectadas  
- ❌ No son conceptualmente idénticas  
- 🔁 En regresión logística, **logit ↔ sigmoide** representan dos caras de la misma transformación

Esta conexión es una de las razones por las que la regresión logística puede verse como un **modelo puente entre estadística clásica y machine learning**.
