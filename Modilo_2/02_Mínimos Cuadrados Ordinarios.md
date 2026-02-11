# Regresión Lineal Simple y Mínimos Cuadrados Ordinarios (MCO) 



En videos anteriores mencionamos que la **regresión lineal simple** es una técnica que estima la relación lineal entre:

- Una variable independiente $X$
- Una variable dependiente continua $Y$

El término *lineal* se refiere a que, al representar los datos en un plano cartesiano $(x, y)$, estos siguen una **línea recta**.

En la regresión lineal simple solo trabajamos con **dos variables**: una $X$ y una $Y$.

---

## Ecuación de la recta de regresión

La ecuación de una recta de regresión es:

$$
Y = \beta_0 + \beta_1 X
$$

Donde:

- $\beta_0$ = intercepto  
- $\beta_1$ = pendiente  

Dado un conjunto de datos, existen muchas rectas posibles que podrían ajustarse a los puntos. Sin embargo, buscamos la **recta de mejor ajuste**, es decir, aquella que **minimiza el error**.

---

## Error y residuos

El error puede entenderse como la diferencia entre:

- Los **valores observados**
- Los **valores predichos** por el modelo

Los valores predichos son las estimaciones de $Y$ para cada $X$ según el modelo.

La diferencia entre el valor observado y el valor predicho se denomina **residuo**.

### Ecuación del residuo

En forma general:

Residuo = Valor observado − Valor predicho


En notación matemática:

$$
\varepsilon_i = Y_i - \hat{Y}_i
$$

Donde:

- $\varepsilon_i$ = residuo del punto $i$
- $Y_i$ = valor observado
- $\hat{Y}_i$ = valor predicho
- $\varepsilon$ es la letra griega épsilon (asociada a error)

Cada punto de datos tiene su propio residuo.

Es importante destacar que, para los estimadores de **Mínimos Cuadrados Ordinarios (MCO)**, la **suma de los residuos es igual a cero**.

---

## Suma de Residuos al Cuadrado (SSR) Sum of Squared Residuals
 
Para medir el error total del modelo:

1. Elevamos al cuadrado cada residuo.
2. Sumamos todos los residuos al cuadrado.

Esto se conoce como **Suma de Residuos al Cuadrado (SSR)**.

La SSR es:

$$
SSR = \sum (Y_i - \hat{Y}_i)^2
$$

Representa la suma de las diferencias al cuadrado entre cada valor observado y su valor predicho.

---

## Mínimos Cuadrados Ordinarios (MCO), Ordinary Least Squares (OLS) en ingles

La técnica utilizada para encontrar la mejor recta es **Mínimos Cuadrados Ordinarios (MCO)**.

MCO es un método que:

- Minimiza la suma de los residuos al cuadrado.
- Permite estimar los parámetros del modelo de regresión lineal.

Mediante MCO obtenemos:

- $\hat{\beta}_0$
- $\hat{\beta}_1$

El símbolo "sombrero" (^) indica que se trata de una **estimación** del parámetro poblacional.

Los parámetros reales ($\beta_0$, $\beta_1$) son características de la población, pero como solo tenemos una muestra, buscamos una **estimación razonable**.

---

## Ejemplo conceptual

Supongamos que probamos distintas rectas:

### Primer intento:
- Pendiente = 1  
- Intercepto = 2.5  

Calculamos:
- Valores predichos
- Residuos
- SSR

La recta se ajusta, pero podría mejorar.

### Segundo intento:
- Pendiente = 1.25  
- Intercepto = 3  

Volvemos a calcular residuos y SSR. Parece un mejor ajuste, pero aún no sabemos si es el óptimo.

Probar manualmente muchas rectas sería ineficiente.

---

## Solución con Python y MCO

En Python, el algoritmo de **MCO** prueba múltiples combinaciones y encuentra automáticamente la recta que minimiza la SSR.

Con MCO obtenemos:

- $\hat{\beta}_0 = 1.5$
- $\hat{\beta}_1 = 3.2$

Esta es la recta de mejor ajuste para los datos.

---

## Estimación de coeficientes beta

Podría seguir ajustando la pendiente y el intercepto, y luego calcular los valores predichos, los residuos y los residuos al cuadrado. Pero realmente no hay forma de estar seguro de haber encontrado la línea de mejor ajuste. Mediante matemáticas avanzadas, se han derivado algunas fórmulas para encontrar los coeficientes beta que minimizan el error.

Hay múltiples maneras de escribir las fórmulas para encontrar los coeficientes beta. Para la regresión lineal simple, una forma de escribir las fórmulas es la siguiente:

### Estimación de la pendiente

$$
\hat{\beta}_1 = 
\frac{
\sum_{i=1}^{n} (X_i - \bar{X})(Y_i - \bar{Y})
}{
\sum_{i=1}^{n} (X_i - \bar{X})^2
}
$$

Donde:

- $\hat{\beta}_1$ = estimación de la pendiente  
- $X_i$, $Y_i$ = valores individuales de la muestra  
- $\bar{X}$, $\bar{Y}$ = medias muestrales  
- $n$ = tamaño de la muestra  

---

### Estimación del intercepto

$$
\hat{\beta}_0 = \bar{Y} - \hat{\beta}_1 \bar{X}
$$

Donde:

- $\hat{\beta}_0$ = estimación del intercepto  

---

## Nota Importante

No se le pedirá que calcule los coeficientes beta manualmente sin ayuda de un ordenador. Sin embargo, puede ser interesante explorar estas fórmulas si desea profundizar en el tema.

Se han proporcionado recursos adicionales para quienes estén interesados en comprender con mayor detalle la derivación matemática.



## Próximos pasos

Más adelante analizaremos:

- **Valores p**
- **Intervalos de confianza**
- Interpretación de la incertidumbre en los parámetros

Ahora que comprendemos la regresión lineal simple y el método MCO, regresaremos al marco **PACE** para examinar los **supuestos del modelo** que deben cumplirse antes de aplicar esta herramienta.
