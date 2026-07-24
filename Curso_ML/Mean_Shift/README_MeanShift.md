# Mean Shift — Desplazamiento Medio

> **Clustering basado en Modas / Densidad (encuentra K automáticamente)**

---

## 🧠 ¿Qué es en una frase?

Busca las **modas** (zonas de máxima densidad) de tu distribución de datos, moviendo cada punto iterativamente **hacia donde haya más vecinos** (hacia la moda más cercana). Los puntos que acaben en la misma moda forman el mismo cluster. Como bonus: **encuentra K automáticamente**.

---

## 📜 Origen e historia

- **Año: 1975**
- **Autor: Fukunaga y Hostetler** (paper: "The Estimation of the Gradient of a Density Function, with Applications in Pattern Recognition")
- **Popularizado en 1999** por **Dorin Comaniciu y Peter Meer** (Rutgers University), en el artículo *Mean Shift: A Robust Approach Toward Feature Space Analysis* — extendieron la idea original y lo usaron para **segmentación de imágenes y seguimiento de objetos**.
- **Impacto**: se convirtió en herramienta estándar de visión por computador durante los 2000 (antes del deep learning para tracking y segmentación).

---

## 🏗️ Fundamentos: la "Ventana" y el "Vector Mean Shift"

### Concepto clave:

En cada punto, calculamos el **"vector Mean Shift"**: la diferencia entre
1. La **media (centroide) de los vecinos que caen dentro de una ventana (bandwidth)**
2. La **posición actual del punto**

Si este vector no es cero → movemos el punto hacia esa media y repetimos. Si es (casi) cero → **llegamos a una moda** (la máxima densidad local).

```
Ventana = h (bandwidth)

Paso 1 (punto solitario):     Paso 2 (acercándose):    Paso 3 (moda):

· · ·  ·  ·                   · · · · ·               · · · ● ·  ← ¡Moda!
 ·  ●   · ·                    ·  · ●  ·                ·  ·  ·  ·
  · ·  · ·      ——→             · ● · ·     ——→          ·  ·  · ·
 ·  · · ·                        ·  ·  · ·               · ·  ·  ·

   ↑ punto                          ↑ se mueve
```

Todos los puntos que converjan a la MISMA moda (mismo centro) → **mismo cluster**.

---

## 🚀 ¿Cómo funciona Mean Shift paso a paso?

1. Elige un **`bandwidth (h)`**: el radio/ventana alrededor de cada punto.
2. Para cada punto **x**:
   - a. Calcula la media de TODOS los puntos que caigan dentro de una ventana centrada en x.
   - b. Desplaza x hacia esa media.
   - c. Repite a y b hasta que el desplazamiento sea muy pequeño (convergencia).
3. Después de mover todos los puntos:
   - Los puntos que hayan acabado en **la misma posición (mismo centro de convergencia)** forman el mismo cluster.
4. El número K de clusters = **número de modas distintas** encontradas.

> Truco de sklearn: usa `bin_seeding=True` para que no empiece el algoritmo en cada punto, sino en una "rejilla de bins", mucho más rápido.

---

## 🎛️ Hiperparámetros clave

| Parámetro | Qué hace | Consejo |
|---|---|---|
| **`bandwidth`** | Radio de la ventana. **PARÁMETRO MÁS IMPORTANTE**. | Demasiado pequeño → K muy grande (muchos micro-clusters). Demasiado grande → K muy pequeño (pocos clusters). **Usa `estimate_bandwidth()`** de sklearn para una estimación automática sensata. |
| `bin_seeding` | Si `True`, inicializa en bins (más rápido). | **Siempre `True`** (no hay razón para `False` en práctica). |
| `cluster_all` | Si `True`, todos los puntos van a un cluster (incluso aislados). Si `False`, outliers se etiquetan como -1 | Úsalo con `False` si quieres detección de outliers al estilo DBSCAN. |
| `seeds` | Puntos iniciales para empezar | Déjalo en `None` (automático). |

### Cómo estimar `bandwidth` automáticamente:

```python
from sklearn.cluster import estimate_bandwidth
bw = estimate_bandwidth(X_scaled, quantile=0.15, n_samples=300)
```
- `quantile` (0–1): porcentaje de distancias usadas para bw.
  - `quantile` **bajo** (~0.05): bw pequeño → K grande
  - `quantile` **alto** (~0.5): bw grande → K pequeño

---

## ✅ Ventajas y ❌ Desventajas

| ✅ Ventajas | ❌ Desventajas |
|---|---|
| ❇️ **No necesita K** (lo calcula solo) | ⏱️ **Lento**: iterativamente mueve cada punto, en alto dimensionalidad pesa mucho |
| 🎯 Detecta automáticamente clusters de cualquier forma (no solo esféricos) | 🎛️ **Sensible a bandwidth**: si eliges mal, todo se rompe |
| 📍 Los centroides son **modas reales** (zonas de alta densidad, no medias "vacías") | 🐌 Muy lento en datasets grandes (n > 10k) |
| 🔁 **Determinista** (mismo bw = mismo resultado, no hay aleatoriedad) | 🤕 Pobre en dimensiones altas (maldición de la dimensionalidad) |
| Opcionalmente puede etiquetar ruido (`cluster_all=False`) | Puede dar clusters muy desiguales en tamaño |

---

## 🎯 ¿Cuándo usarlo?

### 👉 SÍ usarlo cuando…
- ❓ **No sabes cuántos clusters hay** y quieres explorar K automáticamente
- 🖼️ **Visión por computador / imágenes** (segmentación, seguimiento de objetos)
- 🎨 **Compresión / cuantización de color** (paletas de color)
- 🔍 Exploración rápida: ejecútalo primero para ver cuántos clusters sugiere el algoritmo

### 👉 NO usarlo cuando…
- 🚀 Dataset grande (n > 10k): el costo computacional es muy alto
- 🎯 Ya tienes claro K → K-means o GMM son más rápidos y estables
- 🚁 Producción a tiempo real: la iteración por punto es lenta
- 🧊 Clusters bien separados y esféricos → K-means es más económico

---

## 🧩 Comparativa: Mean Shift vs DBSCAN vs K-means

| Aspecto | K-means | Mean Shift | DBSCAN |
|---|---|---|---|
| ¿Necesita K? | ✔️ Sí | ❌ No | ❌ No |
| Hiperparámetro clave | `n_clusters` | `bandwidth` | `eps` + `min_samples` |
| Forma del cluster | Esférico | Basado en densidad | Basado en densidad |
| Maneja outliers | ❌ | Opcional (`cluster_all=False`) | ✔️ Sí (-1) |
| Velocidad | ⚡ Alta | 🐌 Baja | 🐢 Media |
| Determinista | ❌ (depende de init) | ✔️ | ✔️ |

---

## 🧪 Ejemplos de la vida real

- 🎨 **Cuantización de color**: reducir paleta RGB de 16M colores a 16
- 👤 **Tracking en vídeo**: seguir una persona/objeto moviéndose entre frames
- 🏙️ **Segmentación de imágenes**: separar cielo, suelo, objetos
- 🌌 **Astronomía**: detectar cúmulos de galaxias por densidad
- 🚕 **Movilidad urbana**: detectar zonas / paradas frecuentes de taxis

---

## 💡 Trucos para la clase

1. **Siempre estandariza** (StandardScaler) las variables antes de Mean Shift.
2. Empieza **siempre** con `estimate_bandwidth()` y prueba varios `quantile` (0.08, 0.15, 0.25, 0.4) como en el notebook. Es la forma menos frustrante.
3. Si obtienes **muchos clusters** → aumenta el `quantile` (o el `bandwidth`).
4. Si obtienes **1 solo cluster** → reduce el `quantile` (o el `bandwidth`).
5. Usa siempre `bin_seeding=True` (ahorra mucho tiempo).
6. Si el número de clusters es alto y tu dataset es grande, considera **DBSCAN** primero (más rápido).
