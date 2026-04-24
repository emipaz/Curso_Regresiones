# Supuestos de la Regresión Lineal Múltiple


La **regresión lineal múltiple** comparte esos mismos supuestos e incorpora uno nuevo.

---

# Supuestos Compartidos

Tanto la regresión lineal simple como la múltiple requieren:

1. Linealidad  
2. Observaciones independientes  
3. Normalidad de residuos  
4. Homocedasticidad  

Además, en regresión múltiple:

5. No multicolinealidad

---

# 1. Linealidad

Cada variable predictora $X_i$ debe tener una relación lineal con la variable objetivo $Y$.

$$
Y \sim X_i
$$

## Cómo evaluarlo

- Gráficos de dispersión entre cada $X_i$ y $Y$
- Tendencia aproximadamente lineal

## Ejemplo

- Precio de entradas vs ventas
- Seguidores en redes vs ventas



---

# 2. Observaciones Independientes

Cada fila del dataset debe ser independiente de las demás.

## Problemas comunes

- Personas del mismo hogar
- Mediciones repetidas del mismo individuo
- Datos agrupados sin control

## Cómo evaluarlo

Revisando el proceso de recolección de datos.

---

# 3. Normalidad de Residuos

Los errores del modelo deben seguir una distribución aproximadamente normal.

$$
e_i = y_i - \hat{y}_i
$$

## Cómo evaluarlo

- Histograma de residuos
- QQ-plot
- Test de normalidad

> Nota: Es un malentendido común pensar que las variables independientes y/o dependientes deben distribuirse normalmente cuando se realiza una regresión lineal. Éste no es el caso. Sólo se supone que los residuos del modelo son normales.

---

# 4. Homocedasticidad

La varianza de los errores debe mantenerse constante a lo largo del rango de predicciones.

$$
Var(e_i)=\sigma^2
$$

## Cómo evaluarlo

- Residuos vs valores ajustados

## Si falla

Existe **heterocedasticidad**.

---

# 5. No Multicolinealidad (Nuevo Supuesto)

Las variables independientes no deben estar altamente correlacionadas entre sí.

Es decir, no debe ocurrir:

$$
X_i \approx a + bX_j
$$

Si dos predictores explican casi lo mismo, el modelo tendrá problemas para distinguir efectos individuales.

Tenga en cuenta, sin embargo, que el supuesto de no multicolinealidad es más importante cuando se utiliza el modelo de regresión para hacer inferencias sobre los datos, porque la inclusión de datos colineales aumenta los errores estándar de las estimaciones de los parámetros beta del modelo. Pero puede haber ocasiones en las que el propósito principal de su modelo sea hacer predicciones y la necesidad de predicciones precisas supere la necesidad de hacer inferencias sobre sus datos. En este caso, incluir las variables independientes colineales puede estar justificado porque es posible que su inclusión dé lugar a mejores predicciones.

---

# Ejemplo: Venta de Entradas para Conciertos

Variables posibles:

- Seguidores en redes sociales
- Reproducciones en plataformas musicales
- Año de debut
- Precio de entrada
- Días faltantes para el concierto

## Posible multicolinealidad

- Seguidores ↔ reproducciones
- Precio ↔ días restantes (descuentos cercanos al evento)

---

## Problemas que Genera la Multicolinealidad

- Coeficientes inestables
- Interpretación difícil
- Errores estándar altos
- Variables importantes parecen no significativas

## Consideracion

Tenga en cuenta, sin embargo, que el supuesto de no multicolinealidad es más importante cuando se utiliza el modelo de regresión para hacer inferencias sobre los datos, porque la inclusión de datos colineales aumenta los errores estándar de las estimaciones de los parámetros beta del modelo. Pero puede haber ocasiones en las que el propósito principal de su modelo sea hacer predicciones y la necesidad de predicciones precisas supere la necesidad de hacer inferencias sobre sus datos. En este caso, incluir las variables independientes colineales puede estar justificado porque es posible que su inclusión dé lugar a mejores predicciones.

---

# Detección Visual con EDA

## Matriz de Dispersión

Permite observar relaciones entre pares de variables.

```python
sns.pairplot(df)
```

Buscar:

Relación lineal entre $X_i$ y $Y$
Relación lineal fuerte entre $X_i$ y $X_j$

## Detección Matemática: VIF

El Variance Inflation Factor (VIF) mide cuánto se infla la varianza de un coeficiente debido a correlación con otras variables.

$$ 
VIF = \frac{1}{1-R^{2}}
$$
	​
Donde $R_i^2$ proviene de regresionar $X_i$ contra las demás variables independientes.

Interpretación General del VIF


| VIF   | Interpretación   |
| ----- | ---------------- |
| 1     | Sin colinealidad |
| 1 - 5 | Moderada         |
| > 5   | Alta             |
| > 10  | Muy problemática |


 Los detalles del cálculo del VIF quedan fuera del alcance de este curso, pero es útil saber que $\sqrt{VIF_{i}}$ representa la cantidad en que aumenta el error estándar del coeficiente $\beta_{i}$ en relación con una situación en la que todas las variables predictoras no están correlacionadas.

Para calcular el VIF de cada variable predictora, puede utilizar la función `variance_inflation_factor()`del paquete `statsmodels`. 
 
 He aquí un ejemplo de cómo podría obtener los VIF para sus variables predictoras.


```python
from statsmodels.stats.outliers_influence import variance_inflation_factor

X = df[['col_1', 'col_2', 'col_3']]

vif = [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]

vif = zip(X, vif)

print(list(vif))

```


### Soluciones a la Multicolinealidad

1. Eliminar Variables

Quitar predictores redundantes.

2. Combinar Variables

Crear nuevas variables útiles.

Ejemplo:

- Popularidad total = seguidores + reproducciones

3. Regularización

Técnicas avanzadas
Además de las técnicas enumeradas anteriormente que se tratarán en profundidad en este curso, existen técnicas más avanzadas con las que te puedes encontrar en tu carrera como profesional de los datos, como:

- Ridge
- Lasso
- Análisis de componentes principales (PCA)

Estas técnicas pueden dar lugar a modelos más precisos y predictivos, pero pueden complicar la interpretación de los resultados de la regresión.

4. Recalcular VIF

Luego de ajustar el modelo.

## Idea Importante

Cuando tengas dudas:

- Explora los datos
- Visualiza relaciones
- Usa estadísticas de diagnóstico
- Interpreta con criterio de negocio

## Idea Final

Un buen modelo no solo ajusta bien los datos, también cumple supuestos y produce resultados confiables.

La EDA y la validación de supuestos son esenciales para construir modelos sólidos.


## Rellene el espacio en blanco: En _____ se establece que dos variables independientes (X−i y X−j) no pueden estar altamente correlacionadas entre sí. 

- [ ] sin hipótesis de homocedasticidad 
- [ ] sin hipótesis de multicolinealidad
- [ ] ninguna hipótesis de normalidad
- [ ] ninguna hipótesis de linealidad
  
Correcto

La hipótesis de no multicolinealidad establece que dos variables independientes (X-i y X−j) no pueden estar altamente correlacionadas entre sí. Esto significa que X−i y X−j no pueden estar linealmente relacionadas entre sí.
