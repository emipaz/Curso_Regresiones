# Spectral Clustering — Clustering Espectral

> **Clustering basado en Grafos y Álgebra Lineal (Vectores propios)**

---

## 🧠 ¿Qué es en una frase?

Convierte tus datos en un **grafo** (puntos = nodos, similitudes = aristas) y usa **valores y vectores propios (el "espectro")** para transformar los datos a un nuevo espacio donde K-means funciona genial… incluso con formas imposibles (círculos, lunas).

---

## 📜 Origen e historia

- **Raíces matemáticas (siglo XIX)**: teoría de grafos espectral (estudia grafos a través de matrices de adyacencia y Laplacianas).
- **1973**: **Fiedler** publica "Algebraic connectivity of graphs" — demuestra que el **2º vector propio de la Laplaciana** da una buena partición binaría de un grafo (corte espectral).
- **2000**: se populariza en ML con dos papers clave:
  - **Ng, Jordan & Weiss** (2002): *"On Spectral Clustering: Analysis and an algorithm"* (algoritmo moderno estándar).
  - **Shi & Malik (2000)**: *Normalized Cuts and Image Segmentation* (lo usaron para segmentar píxeles de imágenes).
- **Hoy**: muy usado en **visión por computador (segmentación de imágenes), NLP (clúster de textos) y datos con estructuras no lineales.

---

## 🏗️ Fundamentos (intuitivo, sin ecuaciones pesadas)

La idea clave: **K-means falla con círculos concéntricos porque las "medias" (centros) caen en el punto medio, no en cada anillo.** Spectral Clustering **transforma el espacio** antes de usar K-means.

### Paso 1: Construir un grafo de similitud

Imagina tus 400 puntos de `make_circles`:
- Cada punto → un **nodo**
- Cada par de puntos → una **arista** con peso = *qué tan similares son* (RBF, kNN, etc.)

Si dos puntos están en el **mismo círculo**, la similitud es **alta**.
Si están en **distinto círculo**, la similitud es **baja**.

### Paso 2: Calcular la "Laplaciana" del grafo

La matriz Laplaciana L = D - A (D = grado, A = adyacencia). Esta matriz **codifica la estructura del grafo**.

### Paso 3: Calcular vectores propios

Tomamos los **K primeros vectores propios** (no trivialidades) de L. Cada fila de esta matriz es una **"nueva representación" de tu punto.

### Paso 4: Aplicar K-means sobre estos vectores

Ahora sí: en este nuevo espacio, los círculos son esferas separadas, y **K-means lo clava perfectamente.

---

## 🚀 ¿Cómo funciona (algoritmo de Ng, Jordan & Weiss)? Resumen de 4 pasos

1. **A = Matriz de afinidad**: `A[i,j] = sim(x_i, x_j)` (RBF o kNN)
2. **L = Matriz Laplaciana normalizada**
3. **U = primeros K vectores propios** de L
4. **K-means** sobre las filas de U

---

## 🎛️ Hiperparámetros clave

| Parámetro | Qué hace | Consejo |
|---|---|---|
| `n_clusters` | Número de clusters K | **Sí tienes que pasar K**, igual que K-means. |
| **`affinity`** | Cómo medir similitudes | **`rbf`** (predeterminado) o **`nearest_neighbors`** (más usado). |
| **`gamma`** (para `rbf`) | Ancho del kernel RBF `exp(-gamma * ||x-y||²)`. Gamma alto = similitud "local". Gamma bajo = similitud "global". | Empieza en `1/n_features` o prueba valores logarítmicos: 0.1, 1, 10, 50. |
| **`n_neighbors`** (para `nearest_neighbors`) | Conecta cada punto con sus K vecinos más cercanos. | Buena alternativa a RBF si no quieres tocar gamma. Prueba 5–20. |
| `assign_labels` | Cómo asignar etiquetas finales: `'kmeans'` (por defecto) o `'discretize'`. | Deja `'kmeans'` salvo que tengas problemas de convergencia. |

---

## ✅ Ventajas y ❌ Desventajas

| ✅ Ventajas | ❌ Desventajas |
|---|---|
| ✨ **Formas NO convexas / arbitrarias** (círculos, lunas, espirales) | 🔥 **Requiere K** (igual que K-means) |
| 🌀 **No asume esféricidad** de los clusters | 💥 **Muy lento y pesado** en grandes datasets (O(n³)) |
| 📈 Menor sensibilidad a inicializaciones que K-means solo | ⚠️ **Sensible a escala** → estandariza siempre |
| 🧠 Basado en teoría sólida (álgebra lineal) | 🎛️ Ajuste de `gamma` o `n_neighbors` a veces es prueba y error |
| 🖼️ Excelente en imágenes y grafos | 📊 No escala bien: n > 10k ya es caro |

---

## 🎯 ¿Cuándo usarlo?

### 👉 SÍ usarlo cuando…
- 🟢🟣 Tus datos tienen **formas complejas no linealmente separables** (círculos, lunas, etc.)
- 🖼️ **Segmentación de imágenes** (objetos dentro de fotos)
- 👥 **Community detection** en redes sociales (clusters de amistades)
- 🔬 Datos con estructuras tipo "grafo" o manifold (datos en subespacios curvos)

### 👉 NO usarlo cuando…
- 🪐 Clusters son **esféricos / bien separados (K-means es 100x más rápido)
- 🚀 Dataset **grande (n > 10k)
- 🏭 Producción / pipeline a tiempo real (costo computacional muy alto)

---

## 🧩 Comparativa: ¿Cuándo usar cada afinidad?

| `affinity` | Mejor para | Ventaja |
|---|---|---|
| `rbf` | Datos con geometría suave | Control fino con `gamma` |
| `nearest_neighbors` | Datos con k-vecinos bien definidos (manifolds) | Menos parámetros frágiles |

> Si tus clusters son **muy separados**, `nearest_neighbors` suele ser más robusto.
> Si son **densos / mezclados** pero con geometría rara, `rbf` + probar varios `gamma`.

---

## 🧪 Ejemplos de la vida real

- 🖼️ **Segmentación de imágenes (semántica):** separar primer plano / fondo
- 👥 **Análisis de redes** (Twitter, Facebook): detección de comunidades
- 📚 **Text mining (NLP):** clusters de documentos con temas similares
- 🧬 **Bioinformática:** agrupación de perfiles de expresión génica
- 🎵 **Recomendación musical:** agrupar canciones según similitudes de features

---

## 💡 Trucos para la clase

1. **Compara Spectral vs K-means** usando `make_circles` o `make_moons` (como en el notebook). ¡La diferencia es el "efecto wow" de la clase!
2. Si usas **`rbf`** y obtienes clusters mal:
   - Gamma **muy alto** → demasiados clusters pequeños
   - Gamma **muy bajo** → pocos clusters (todo se une)
   - Haz un gráfico de 4 subplots con varios `gamma` (como en el ejemplo)
3. Si usas **`nearest_neighbors`** y falla: aumenta `n_neighbors` (10 → 15 → 20).
4. Spectral **no predice nuevos datos** nativamente (sklearn). Se usa para data exploration, no tanto para pipelines de inferencia.
