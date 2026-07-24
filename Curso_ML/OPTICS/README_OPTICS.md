# OPTICS — Ordering Points To Identify the Clustering Structure

> **DBSCAN 2.0: Estructura de Clustering a Múltiples Escalas**

---

## 🧠 ¿Qué es en una frase?

Es una **extensión / mejora de DBSCAN** que NO te obliga a elegir `eps` de antemano. Produce un **ordenamiento lineal** de tus puntos + un **"Reachability Plot"** (gráfico de alcance) que te permite **extraer clusters a diferentes escalas (diferentes ε) en 1 sola pasada**. Ideal para clusters con **densidades muy distintas**.

---

## 📜 Origen e historia

- **Año: 1999**
- **Autores**: Mihael Ankerst, Markus M. Breunig, Hans-Peter Kriegel, Jörg Sander (Universidad de Múnich, Alemania — ¡mismo equipo que DBSCAN de 1996!)
- **Conferencia**: ACM SIGMOD (muy prestigiosa en BD / minería de datos)
- **Motivación**: DBSCAN tenía limitaciones importantes. Si tus clusters tienen densidades MUY distintas (un cluster super denso + otro super disperso), no hay un único `eps` que funcione para todos. OPTICS nació para resolver esto.
- **Legado**: En 2019 salió **HDBSCAN* (Hierarchical DBSCAN), que es la evolución más moderna (OPTICS + cortes jerárquicos automáticos). OPTICS sigue siendo clave para entenderlo.

---

## 🏗️ Fundamentos: 3 conceptos clave

OPTICS hereda de DBSCAN (`eps`, `min_samples`), pero introduce 2 distancias nuevas:

### 1️⃣ Core Distance (cd, Distancia de Núcleo)
La distancia mínima para que un punto `p` sea **core** (punto central). Si con `min_samples`-1 vecinos ya está a distancia menor a `max_eps`, entonces es core.

### 2️⃣ Reachability Distance (rd, Distancia de Alcance)
Para un punto `p` respecto a otro punto core `o`:
```
rd(p, o) = max(cd(o), distancia(p, o))
```
Es la **distancia mínima a la que tienes que "estirar" ε** desde `o` para alcanzar `p`.

### 3️⃣ Ordering (Ordenamiento)
OPTICS produce una lista ordenada de puntos. Puntos que pertenecen al **mismo cluster** aparecen **juntos y consecutivos** en el ordenamiento. Y para cada punto guarda su **rd**.

---

## 🚀 ¿Cómo funciona OPTICS paso a paso? (simplificado)

1. Elige `min_samples` y `max_eps` (si no, `max_eps = ∞`).
2. Empieza con un punto cualquiera no visitado.
3. Si es **core**:
   - Calcula su `core_distance`
   - Para cada vecino calcula su `reachability_distance`
   - Ordena los vecinos por rd (de menor a mayor = más fáciles de alcanzar)
   - Visita primero los de menor rd (algoritmo estilo Dijkstra)
4. Cada punto que visitas lo añade a la **lista ordenada** y almacena su `reachability_distance`.
5. Al final, tienes 2 arrays:
   - `ordering_`: índices de los puntos en el orden de visita
   - `reachability_`: la distancia de alcance de cada punto

> OPTICS **no asigna clusters directamente**. Produce una "estructura" desde la que tú (o el método xi) extraes clusters.

---

## 📊 Cómo leer el Reachability Plot (gráfico estrella de OPTICS)

Es un **gráfico de barras**:
- **Eje X**: los puntos, ORDENADOS por OPTICS (vecinos juntos)
- **Eje Y**: `reachability distance` (alcance)

```
      ____                    ___
     |    |                  |   |
     |    |    ___           |   |
     |    |   |   |   ____   |   |
_____|    |___|   |__|    |__|   |__
  A  B  C  D  E  F  G  H  I  J  K  L  ← X = puntos ordenados
```

- 👇 **Valles bajos consecutivos** = puntos que forman un **cluster (densos)**.
- 👆 **Picos altos** = separación **entre clusters**.
- Barras **solas muy altas** al final = **ruido / outliers**.

> **Para extraer clusters tú mismo**: dibuja una línea horizontal a altura `eps` (como en DBSCAN). Todos los valles por debajo de la línea = 1 cluster. ¡Cada `eps` da clusters distintos!

---

## 🎛️ Hiperparámetros clave

| Parámetro | Qué hace | Consejo |
|---|---|---|
| **`min_samples`** | Igual que en DBSCAN. Cuántos vecinos ≈ 1 cluster | `>= 2 * nº dimensiones`. Valores típicos: 5, 10, 20. |
| **`max_eps`** | Radio máximo de búsqueda. Por defecto: `np.inf` (todos los vecinos). | Si tu dataset es muy grande, pon un valor finito para que no tarde (ej: 2–3 veces la media de las distancias). |
| **`xi`** (auto-cluster extraction) | Umbral de "pendiente" para detectar fin/inicio de cluster (método xi). Valores típicos: `0.01` – `0.1`. | Valor por defecto `0.05`. Menor = más clusters. Mayor = menos clusters. |
| **`min_cluster_size`** | Tamaño mínimo aceptable de cluster (fracción o número). | `0.05` = "al menos 5% de los datos" evita micro-clusters falsos. |

---

## 🆚 OPTICS vs DBSCAN (comparativa directa)

| Aspecto | DBSCAN | OPTICS |
|---|---|---|
| Necesita `eps` **exacto** | ✔️ Sí (muy sensible) | ❌ No (solo `max_eps` opcional) |
| Sencillez | ✅ Más fácil | ❌ Conceptos más (rd, cd, ordering) |
| Velocidad | ⚡ Rápido | 🐢 Más lento, más memoria |
| Clusters densidades distintas | ❌ Pobre (solo 1 ε) | ✅ Excelente (una pasada, varias ε) |
| Visualización de estructura | ❌ No | ✅ Reachability Plot genial |
| Extraer clusters a **distintos ε** | ❌ Reentrena desde cero | ✅ Una sola pasada (`cluster_optics_dbscan`) |
| Detectar outliers | ✔️ (-1) | ✔️ También |
| Produce etiquetas directas | ✔️ `fit_predict` las da | ✔️ `labels_` (con xi). O `cluster_optics_dbscan` |

---

## ✅ Ventajas y ❌ Desventajas

| ✅ Ventajas | ❌ Desventajas |
|---|---|
| 🤯 **No necesitas `eps` exacto** | 🐌 **Más lento** y **más memoria** que DBSCAN (ordena con colas de prioridad) |
| 🎚️ **Maneja densidades distintas** | 📚 Conceptualmente más difícil de explicar (reachability, ordering) |
| 📊 **Reachability Plot**: muy didáctico para explicar a equipos | 🎛️ Ajustar `xi` + `min_cluster_size` a veces es prueba/error |
| 🔁 **Una sola pasada → múltiples ε** sin reentrenar | Escala mal con datasets gigantes (pero mejoró con `max_eps`) |
| Detecta outliers al igual que DBSCAN | Menos conocido: menos gente con experiencia |

---

## 🎯 ¿Cuándo usarlo?

### 👉 SÍ usarlo cuando…
- 🔍 Los clusters tienen **densidades muy distintas** (ej: una ciudad densa + pueblos pequeños dispersos)
- 📊 Quieres **explorar la estructura** de tus datos con una visualización (reachability plot)
- 🔁 Quieres probar **muchos valores de ε** sin reentrenar (muy útil en exploración)
- 🧪 Sabes que vas a usar DBSCAN, pero primero quieres explorar / decidir `eps`

### 👉 NO usarlo cuando…
- ⚡ Velocidad extrema → DBSCAN simple
- 🪐 Clusters claramente **esféricos** y de densidad similar (K-means más rápido)
- 🚀 Dataset de millones de filas → HDBSCAN si está disponible, o una muestra de OPTICS
- 🎓 Primer día de clase → empieza con K-means, luego DBSCAN, y **deja OPTICS para avanzado**

---

## 🧪 Ejemplos de la vida real

- 🏙️ **Urbanismo**: identificar barrios de distinto tamaño y densidad de población
- 🛰️ **Sensores IoT**: eventos con densidades distintas (trafico denso en hora punta vs disperso por la noche)
- 🛒 **Retail**: clusters de clientes (grandes grupos con comportamiento denso + pequeños nichos)
- 🔬 **Minería de datos**: explorar dataset desconocido y luego decidir qué eps usar para DBSCAN

---

## 💡 Trucos para la clase

1. **Explica primero DBSCAN**, luego presenta OPTICS como su evolución "con superpoderes".
2. Muestra el **reachability plot** antes de nada. Es la herramienta visual más potente.
3. Demuestra `cluster_optics_dbscan(reachability, core_distances, ordering, eps=VALOR)` con 3–4 ε distintos (como en el notebook). ¡En 1 sola pasada extraes K diferente!
4. Si usas sklearn: `OPTICS` da `labels_` por defecto (método xi). No es lo único. Muestra ambos enfoques en clase:
   - 👉 **Forma A**: `labels_` (automático con xi)
   - 👉 **Forma B**: `cluster_optics_dbscan` (tú eliges ε después)
5. Empieza con `max_eps = np.inf` para datasets pequeños. Para medianos: `max_eps = 5–10`.
6. Si tienes demasiados "micro-clusters" → aumenta `min_cluster_size` (ej: `0.1` → 10% mínimo).
7. Como **tarea para casa**: pide que el alumno compare OPTICS vs DBSCAN con datos de 2 densidades distintas y comente la diferencia.

---

## 📌 Resumen

> **OPTICS = DBSCAN sin tener que adivinar `eps`, + una exploración visual por "valles" (reachability plot), + clusters a múltiples densidades.**
