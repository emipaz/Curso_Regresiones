# Gaussian Mixture Models (GMM) — Modelos de Mezcla Gaussianas

> **Clustering Probabilístico (Soft Clustering + Formas Elípticas)**

---

## 🧠 ¿Qué es en una frase?

Asume que tus datos vienen de una **mezcla de K distribuciones Gaussianas** (curvas de campana). Cada punto tiene una **probabilidad** de pertenecer a cada cluster, no una etiqueta binaria). Es K-means pero "suave con elípticas".

---

## 📜 Origen e historia

- **Siglo XIX**: las distribuciones Gaussianas (normales) son descritas por Gauss.
- **1886**: Simon Newcomb usa mezcla de dos Gaussianas para modelar datos bimodales.
- **1977**: ¡Punto de inflexión: Dempster, Laird & Rubin publican el algoritmo **EM (Expectation-Maximization)**, que es el corazón de GMM. Antes era un "problema abierto desde los 60.
- **Hoy**: Muy usado en estadística, ML, y procesamiento de señales.

---

## 🏗️ Fundamentos matemáticos (intuitivo)

### K-means asume:
- Cada cluster es **esférico** (misma varianza en todas las direcciones).
- Cada punto **pertenece exactamente a un cluster** (asignación dura / hard).

### GMM asume:
- Cada cluster es una **Gaussiana multivariante** con:
  - **μ (mu, vector): centro / media**
  - **Σ (sigma, matriz de covarianza) → forma/orientación**
  - **π (pi): peso / probabilidad a priori**
- Cada punto **probabilidad** de haber venido de CADA Gaussiana (soft clustering).

```
Ejemplo en 2D con 3 Gaussianas:

     🟢  🟣
   🟢🟢  🟣
   🟢🟢  🟣🟣
🟢🟢    🟣 🔴🔴
  🟢      🔴🔴🔴
          🔴🔴
            🔴🔴
```
Cada "nube" tiene su propia **μ, Σ y π. Y cada punto pertenece con 70% cluster A, 25% B, 5% C… (no hay "0/1").

---

## 🧠 Algoritmo EM en 2 pasos (Expectation-Maximization)

GMM entrena con EM. Es un algoritmo iterativo de 2 pasos:

### Paso 1️⃣ Expectation (E-step):
Con los μ, Σ, π actuales, **calcula** para cada punto `n P(pertenece al cluster k). Estas son las **responsabilidades** (responsibilities γ(i,k)).

### Paso 2️⃣ Maximization (M-step):
Con esas responsabilidades, **actualiza** μ, Σ, π para maximizar la verosimilitud (likelihood)**.

Se repite E y M hasta convergencia.

---

## 🎛️ Tipos de `covariance_type` (clave)

Este parámetro define qué **flexibilidad** tienen los clusters.

| Tipo | Descripción visual | Cuándo usarlo | Nº params |
|---|---|---|---|
| 🔴 **`full` (por defecto)** | **Cada cluster** tiene su **propia** matriz de covarianza completa | Máxima flexibilidad (formas elípticas, orientaciones y tamaños distintos** | Alto |
| 🟣 **`tied`** | **Todos los clusters** comparten **la MISMA** matriz de covarianza | Clusters de similar forma/orientación, pero distinto centro | Medio |
| 🟢 **`diag`** | Cada cluster tiene su **propia diagonal, pero ejes alineados con coordenadas** | Clusters elípticos, pero **ejes paralelos al sistema de coord. | Bajo |
| 🟡 **`spherical`** | Cada cluster es una **esfera** (varianza = scalar). Equivale a K-means "suave" | Clusters esféricos, similar a K-means. Mínimo |
| | | | |

> Consejo: empieza con **`full`** y luego simplifica.

---

## 🎯 Elegir K: BIC y AIC

A diferencia de K-means, GMM te da herramientas para **elegir K**:

### 📐 BIC (Bayesian Information Criterion) y AIC (Akaike)

Ambos **penalizan complejidad (más K → penalización mayor). **Se busca el MÍNIMO.

Fórmula intuitiva:
```
BIC = -2 * log(Likelihood) + (penalización por nº parámetros)
```

- **Menor BIC = Mejor modelo (ajusta bien y no sobreajusta).

En sklearn:
```python
gmm.bic(X_scaled)   # ⬇️ BIC mejor
gmm.aic(X_scaled)   # ⬇️ AIC mejor
```

Gráfico: hazlo en el notebook. El **codo** marca el K óptimo.

---

## ✅ Ventajas y ❌ Desventajas

| ✅ Ventajas | ❌ Desventajas |
|---|---|
| 🔮 **Soft clustering** (asignación probabilística = más información) | 🎯 **Requiere K** (aunque BIC/AIC ayuda) |
| 🔶 **Clusters elípticos / orientables** (no solo esféricos) | 🔁 Puede quedarse en **óptimos locales** (solución: ejecutar varias veces con `n_init`) |
| 📊 **Interpretabilidad probabilística**fácil (cada cluster = una Gaussiana) | ⚠️ **Sensible a inicialización** |
| 🎲 **Modelo generativo**: puedes **generar nuevos datos** con `gmm.sample(100)` | 🧮 **Asume que cada cluster es Gaussiano (no todo lo es) |
| 🎯 Puedes detectar outliers (baja `score_samples()` y baja verosimilitud) | 📈 Pobre en datos realmente no Gaussianos |

---

## 🎯 ¿Cuándo usarlo?

### 👉 SÍ usarlo cuando…
- 🔶 Tus clusters tienen **formas alargadas / elípticas / inclinadas**
- 🔮 Quieres **probabilidades** de pertenencia (no una etiqueta 0/1)
- ❓ Quieres **detectar anomalías** (puntos con baja `score_samples`)
- 🎲 Quieres **generar datos sintéticos (`gmm.sample()`)
- 📊 Datos con **mezcla de distribuciones** conocidas (ej: salarios de dos profesiones)

### 👉 NO usarlo cuando…
- 🪐 Clusters **esféricos bien separados (K-means igual de bien y 10x más rápido)
- 🧪 Datos con **formas arbitrarias no Gaussianas (mejor DBSCAN / Spectral)
- 🚀 Dataset muy grande / producción tiempo real

---

## 🧩 GMM vs K-means

| Aspecto | K-means | GMM |
|---|---|---|
| Asignación | **Dura** (0/1) | **Suave** (probabilidad) |
| Forma clusters | Solo **esféricas** | **Elípticas** (full) |
| Necesita K | ✔️ Sí | ✔️ Sí (pero BIC/AIC ayuda) |
| Óptimo local | Sí | Sí (más opciones de EM) |
| Outliers | ❌ (los mete a un cluster) | ✔️ Sí con `score_samples()` |
| Generar datos | ❌ No | ✔️ Sí `sample()` |

---

## 🧪 Ejemplos de la vida real

- 💰 **Finanzas**: mezcla de distribuciones (salarios, precios)
- 🧬 **Bioinformática**: expresión génica en varios tipos celulares
- 🎨 **Procesamiento de imágenes**: modelar color / segmentación por textura
- 🔊 **Procesamiento de audio**: separar fuentes de voz / música
- 🔍 **Detección de fraude / anomalías: puntos con `score_samples` bajo
- 🏥 **Medicina** / diagnóstico (grupos de pacientes con síntomas)

---

## 💡 Trucos para la clase

1. **Estandariza siempre, siempre, siempre. Las Gaussianas son muy sensibles a la escala.
2. **Empieza con `covariance_type='full'** y si overfitting, prueba `diag` o `spherical`.
3. **Si tienes muchas dimensiones: prueba `diag`** (menos parámetros, menos riesgo sobreajuste).
4. **Puntos con `predict_proba(X)`: imprime las probabilidades de los primeros 5 puntos (como en el notebook. Visualiza que la suma da 1. ¡Es super didáctico!
5. **Para elegir K**: grafica BIC/AIC (como en el notebook) y busca el codo (mínimo local). Si dudas entre 2 valores, elige el **menor** (BIC es más conservador).
6. **Para outliers**: usa `gmm.score_samples(X_scaled)` — valores muy bajos = posibles outliers.
7. **Para robustez contra óptimos locales: aumenta `n_init` (ej `n_init=10`) y quizás `init_params='kmeans'` (por defecto)).
