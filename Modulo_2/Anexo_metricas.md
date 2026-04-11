# Selección probabilística de modelos: AIC, BIC y MDL

## Introducción

La **selección de modelos** consiste en elegir el mejor modelo entre un conjunto de candidatos.

Existen varios enfoques:

- Conjuntos de entrenamiento, validación y prueba  
- Métodos de remuestreo (como validación cruzada)  
- Métodos probabilísticos  

Los métodos probabilísticos utilizan métricas que combinan:

- **Rendimiento del modelo**
- **Complejidad del modelo**

---

## Selección probabilística de modelos

Este enfoque evalúa modelos usando criterios que consideran:

- Qué tan bien el modelo se ajusta a los datos (log-verosimilitud)  
- Qué tan complejo es (número de parámetros)  

Ventajas:

- No requiere conjunto de prueba  
- Usa todos los datos disponibles  

Limitaciones:

- No considera la incertidumbre del modelo  
- Puede favorecer modelos demasiado simples  

---

## Log-verosimilitud

En estimación de máxima verosimilitud, se busca maximizar:

$$
P(X; \theta)
$$

Para múltiples observaciones:

$$
P(x_{1}, x_{2}, ..., x_{n}; \theta)
$$

Se suele usar logaritmos:

$$
\sum_{i=1}^{n} \log(P(x_{i}; \theta))
$$

---

## Criterios principales

### AIC (Criterio de Información de Akaike)

Se basa en probabilidad frecuentista.

$$
AIC = -\frac{2}{N} LL + \frac{2k}{N}
$$

o en regresión lineal:

$$
AIC = n \cdot \log(MSE) + 2k
$$

Donde:

- $n$: número de datos  
- $k$: número de parámetros  
- $LL$: log-verosimilitud  

**Interpretación:**

- Se elige el modelo con menor AIC  
- Penaliza menos la complejidad → favorece modelos más complejos  

---

### BIC (Criterio de Información Bayesiano)

Basado en probabilidad bayesiana.

$$
BIC = -2LL + \log(n) \cdot k
$$

o en regresión:

$$
BIC = n \cdot \log(MSE) + k \cdot \log(n)
$$

**Interpretación:**

- Se elige el modelo con menor BIC  
- Penaliza más la complejidad → favorece modelos más simples  

**Propiedad importante:**

- Si el modelo verdadero está en el conjunto, BIC tiende a seleccionarlo cuando $n \to \infty$

---

### MDL (Longitud Mínima de Descripción)

Basado en teoría de la información.

$$
MDL = L(h) + L(D | h)
$$

Donde:

- $L(h)$: bits necesarios para describir el modelo  
- $L(D | h)$: bits necesarios para describir los datos dado el modelo  

También puede expresarse como:

$$
MDL = -\log(P(\theta)) - \log(P(y | X, \theta))
$$

**Interpretación:**

- Se elige el modelo con menor MDL  
- Busca el mejor equilibrio entre simplicidad y ajuste  
- Relacionado con la navaja de Occam  

---

## Comparación entre AIC, BIC y MDL

| Métrica | Penalización de complejidad | Tendencia |
|--------|---------------------------|----------|
| AIC | Baja | Modelos más complejos |
| BIC | Alta | Modelos más simples |
| MDL | Similar a BIC | Balance teórico |

---

## Ejemplo en regresión lineal

Se entrena un modelo con:

- 100 observaciones  
- 2 variables → 3 parámetros (incluyendo intercepto)  

Resultados:

- Parámetros: 3  
- $MSE \approx 0.01$  

Cálculo de métricas:

$$
AIC \approx -451.616
$$

$$
BIC \approx -450.020
$$

Interpretación:

- Ambos valores son similares  
- Se selecciona el modelo con menor valor  

---

## Puntos clave

- La selección de modelos busca elegir el mejor entre varios candidatos  
- AIC, BIC y MDL combinan ajuste y complejidad  
- Todos se basan en log-verosimilitud  
- Se minimizan para elegir el mejor modelo  
- AIC favorece modelos complejos  
- BIC y MDL favorecen modelos más simples  

---