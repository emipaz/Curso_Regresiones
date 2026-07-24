# DBSCAN — Density-Based Spatial Clustering of Applications with Noise

> **Clustering basado en Densidad**

---

## 🧠 ¿Qué es DBSCAN en una frase?

DBSCAN agrupa puntos que están **cerca y densamente concentrados**, y marca como **ruido (outlier)** a todo lo que quede aislado. A diferencia de K-means, **no necesitas decirle cuántos clusters hay**.

---

## 📜 Origen e historia

- **Año de publicación**: 1996
- **Autores**: Martin Ester, Hans-Peter Kriegel, Jörg Sander y Xiaowei Xu (Universidad de Múnich, Alemania)
- **Conferencia**: KDD (Knowledge Discovery and Data Mining)
- **Reconocimiento**: En 2014 recibió el **Premio Test of Time** del ACM SIGKDD por ser un trabajo influyente durante más de una década.
- **Motivación**: Los algoritmos de la época (K-means, jerárquico) solo encontraban clusters esféricos y necesitaban K. DBSCAN nació para clusters de **cualquier forma** y para detectar anomalías de forma natural.

---

## 🏗️ Fundamentos: 3 tipos de puntos

DBSCAN define 3 tipos de puntos según cuántos vecinos haya a su alrededor en un radio **ε (eps)**:

| Tipo de punto | Descripción |
|---|---|
| 🟢 **Core (Núcleo)** | Tiene ≥ `min_samples` puntos (incluido él mismo) dentro del radio `eps`. Es el "esqueleto" de un cluster. |
| 🟡 **Border (Borde)** | No es core, pero está dentro del radio `eps` de algún punto core. Pertenece a un cluster, pero es la "orilla". |
| 🔴 **Noise / Outlier (Ruido)** | No es core ni border. Está solo. Se etiqueta como **-1**. |

```
Ejemplo visual (min_samples=4, eps = radio del círculo):

    ● ●               ● ●
   ● ● ● ○             ○ ●           ✗
    ● ○                 ●
     ↑ core              ↑ border     ↑ noise
 (tiene 6 vecinos)   (no es core pero
                     toca a un core)
```

---

## 🚀 ¿Cómo funciona DBSCAN paso a paso?

1. **Escoge** 2 parámetros: `eps` (radio) y `min_samples` (puntos mínimos para formar densidad).
2. **Estandariza** tus datos (DBSCAN es sensible a la escala).
3. Empieza en un punto cualquiera **no visitado**:
   - Si es **core**: empieza un nuevo cluster. Visita todos los puntos alcanzables por densidad y agrégalos.
   - Si es **border** o **noise**: marca como visitado y pasa al siguiente.
4. Repite hasta que no queden puntos sin visitar.

---

## 🎛️ Hiperparámetros clave

| Parámetro | Qué hace | Consejo práctico |
|---|---|---|
| **`eps`** | Radio de la "vecindad" alrededor de cada punto | Demasiado pequeño → muchos clusters + ruido. Demasiado grande → pocos clusters. **Usar el método k-distance plot** y coger el valor del "codo". |
| **`min_samples`** | Mínimo de puntos (incluido el centro) para considerar un punto como core | Regla de oro: ≥ `2 * número de dimensiones`. Para datos ruidosos, usar valores más altos (10–20). |
| **`metric`** | Medida de distancia (por defecto: `euclidean`) | Usar `manhattan` si hay muchas dimensiones, o `cosine` para texto/embeddings. |

---

## ✅ Ventajas y ❌ Desventajas

| ✅ Ventajas | ❌ Desventajas |
|---|---|
| ❇️ **No necesita K a priori** | ❌ **Sensible a la escala**: siempre estandariza (StandardScaler / MinMaxScaler) |
| ❇️ Detecta **outliers automáticamente** (-1) | ❌ Resultados **muy dependientes** de `eps` y `min_samples` |
| ❇️ Encuentra clusters de **cualquier forma** (lunas, anillos, espirales) | ❌ **Lento** en datasets grandes (O(n²) en peor caso; usar `ball_tree` o `kd_tree` mejora) |
| ❇️ Poco sensible a inicializaciones aleatorias | ❌ **Lucha con clusters de densidades muy distintas** |
| ❇️ No asume forma esférica | ❌ Mala performance en alta dimensionalidad (maldición de la dimensionalidad) |

---

## 🎯 ¿Cuándo usar DBSCAN?

### 👉 SÍ usarlo cuando…
- 📍 Tus datos tienen **formas no convexas** (lunas, círculos, rizos)
- 🔍 Quieres **detectar anomalías** al mismo tiempo que agrupas
- ❓ No tienes ni idea de cuántos clusters hay (y no quieres usar método del codo)
- 🗺️ Datos espaciales / geolocalización (clusters de clientes por coordenadas)

### 👉 NO usarlo cuando…
- 🪐 Los clusters son claramente **esféricos y de densidad similar** (ahorra cómputo con K-means)
- 📊 Dataset **muy grande** (optar por HDBSCAN o una muestra)
- 📈 Muy alta dimensionalidad (aplica PCA / t-SNE primero)

---

## 🧪 Ejemplos de la vida real

- 🏙️ **Ciudades**: detectar barrios densos en un mapa y puntos aislados (construcciones en el campo)
- 🛒 **Fraude bancario**: transacciones "solares" → posibles fraudes; transacciones densas → comportamiento normal
- 🖼️ **Imágenes**: segmentar regiones con densidad de píxeles similares
- 📡 **Sensores IoT**: detección de lecturas anómalas en series temporales multivariantes

---

## 🧩 Comparativa rápida con K-means

| Aspecto | K-means | DBSCAN |
|---|---|---|
| ¿Necesita K? | ✔️ Sí | ❌ No |
| Maneja ruido/outliers | ❌ No (todo punto va a un cluster) | ✔️ Sí (-1) |
| Forma de clusters | Solo **esféricos** | **Cualquier forma** |
| Escala / estandarizar | Recomendado | **Obligatorio** |
| Óptimo local | Sí (sensible a inicio) | No |

---

## 💡 Trucos para la clase

1. **Primero estandariza**. Si olvidas esto, DBSCAN falla de modo espectacular.
2. Para **elegir `eps`**: usa el gráfico `NearestNeighbors` con k = `min_samples` y busca el "codo".
3. Si obtienes **demasiado ruido**: aumenta `eps` o disminuye `min_samples`.
4. Si obtienes **1 solo cluster**: disminuye `eps` o aumenta `min_samples`.
5. DBSCAN es **determinista**: mismos parámetros → mismos clusters (no hay aleatoriedad).
