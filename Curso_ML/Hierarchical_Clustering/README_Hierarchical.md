# Hierarchical Clustering — Clustering Jerárquico Aglomerativo

> **Clustering basado en Jerarquías (Construye un árbol de clusters)**

---

## 🧠 ¿Qué es en una frase?

Construye una **jerarquía de clusters fusionando (o dividiendo)** grupos de datos. El resultado se ve como un **dendrograma** (un árbol), donde eliges en qué altura "cortar" para obtener K clusters).

---

## 📜 Origen e historia

- **Década de 1960**: los métodos jerárquicos surgen en taxonomía y antropometría.
- **Autores clásicos**:
  - **Sokal & Sneath (1963)**: popularizaron métodos numéricos para taxonomía.
  - **Sibson (1973)**: formalizó SLINK (Single Linkage eficiente).
  - **Defays (1977)**: formalizó CLINK (Complete Linkage eficiente).
  - **Ward Jr. (1963)**: propuso el método Ward (minimizar varianza).
- **Uso original**: Clasificación de organismos (taxonomía biológica). Los biólogos ya llevaban siglos construyendo árboles; estos algoritmos lo automatizaron.
- **Hoy en día**: Muy usado en marketing (segmentación de clientes), biología (filogenética), y análisis textual.

---

## 🏗️ Fundamentos: dos enfoques

Existen dos familias:

| Enfoque | ¿Cómo funciona? | ¿Cuándo empiezas? | ¿Cuándo terminas? |
|---|---|---|---|
| **🔼 **Aglomerativo (bottom-up)** | Fusiona los 2 clusters más cercanos iterativamente | N clusters de 1 punto | 1 solo cluster gigante |
|🔽 **Divisivo (top-down) | Divide el cluster que menos compacto en 2 | 1 solo cluster | N clusters de 1 punto |

> El **aglomerativo es el más usado (y el que implementa `sklearn.AgglomerativeClustering`.

---

## 🚀 ¿Cómo funciona el Aglomerativo paso a paso?

Ejemplo con 5 puntos (A, B, C, D, E):

```
Paso 0: 5 clusters → {A}, {B}, {C}, {D}, {E}
Paso 1: Fusiona los más cercanos (A y B) → {A,B}, {C}, {D}, {E}
Paso 2: Fusiona siguientes más cercanos ({C y D) → {A,B}, {C,D}, {E}
Paso 3: Fusiona ({A,B} y {C,D}) → {A,B,C,D}, {E}
Paso 4: Fusiona todo → {A,B,C,D,E}
```

Cada fusión queda **grabada** en la matriz `linkage` de scipy. Con ella dibujamos el dendrograma:

```
        _____________
       |             |
  _____|___        |
 |          |       |
A  B       C  D    E
```

---

## 🎛️ Tipos de "Linkage" (criterio de fusión)

Esta es la **decisión más importante** del clustering jerárquico: ¿qué significa "distancia entre dos clusters":

| Método | Fórmula intuitiva | Comentario |
|---|---|---|
| 🛡️ **Ward** (recomendado)** | Fusiona la pareja que **menos aumente la varianza total** | El más usado. Produce clusters de tamaño similar, compactos. Sensible a outliers. |
| 🔵 **Single (mínima)** | La **distancia más pequeña** entre cualquier par de puntos de cada cluster | Puede generar "efecto cadena" (clusters alargados raros). |
| 🟣 **Complete (máxima)** | La **distancia más grande** entre cualquier par de puntos | Tiende a hacer clusters compactos y "redondos". |
| 🟢 **Average (promedio)** | El **promedio** de todas las distancias entre pares** | Término medio entre single y complete. Robusto. |
| 🟡 **Centroid** | Distancia entre los centroides | Puede dar **inversiones** (líneas que cruzan en dendrograma). |

**Regla práctica**: Empieza siempre con **Ward**. Si las formas son raras, prueba Complete o Average. Evita Single a menos que sepas lo que haces.

---

## 🎛️ Hiperparámetros clave

| Parámetro | Qué hace | Consejo |
|---|---|---|
| `n_clusters` | Número final de clusters a devolver | Si quieres **ver el dendrograma, déjalo en `None` o pon un número después del corte. |
| `linkage` | Criterio de fusión | `"ward"` por defecto; prueba `"complete"` o `"average"` alternativos. |
| `metric` | Medida de distancia | `"euclidean"` por defecto; `"manhattan"` o `"cosine"` según datos. **Ward solo funciona con euclidea**. |
| `distance_threshold` | Umbral: fusiona solo clusters con distancia < umbral | Útil si NO quieres pasar K. |

---

## ✅ Ventajas y ❌ Desventajas

| ✅ Ventajas | ❌ Desventajas |
|---|---|
| 🌳 **Dendrograma = super visual e interpretable** | ⏱️ **Lento**: O(n³) peor caso, n=10k ya pesa |
| ❓ No necesitas K *al principio (te ayuda a decidirlo) | 🔁 **No se puede deshacer**: una fusión es para siempre** |
| 📊 Determinista (mismos datos = mismo resultado | 🎯 Mala elección de linkage = clusters raros |
| 🔀 Distintas estrategias de linkage = flexibilidad | 🎈 Mal en datasets grandes |
| 🎪 Excelente en datos pequeños/medianos | 🎲 No funciona sin escalas distintas a datasets de millones de filas |

---

## 🎯 ¿Cuándo usarlo?

### 👉 SÍ usarlo cuando…
- 🧬 **Taxonomía / biología**: clasificar especies, genes, etc.
- 👥 **Pequeños datasets** (< 10k filas) donde importa interpretar la jerarquía
- 📚 **Documentos** (nlp): ver grupos de textos)
- 🛍️ **Marketing**: segmentación cliente con "árbol" de decisiones
- ❓ Cuando **no sabes cuántos clusters hay y quieres explorar K visualmente

### 👉 NO usarlo cuando…
- 🚀 **Dataset grande** (>50k): demasiado lento y memoria intensivo)
- ⚡ Predicción en **producción (los centroides no se actualizan solos con datos nuevos)
- 🌀 Clusters con formas no convexas (mejor DBSCAN o Spectral)

---

## 🌳 ¿Cómo leer un Dendrograma?

```
    ╷
    ├────────────────────────────┐
    │                            │
    ├───────────┐                   ├───┐
    │            │                   │      │
   ╷  ╷      ╷  ╷            ╷      │
   A  B      C  D            E      F

 ← Distancia de fusión (eje Y) →
```
- **Eje X**: los puntos (o clusters de puntos, cuando usas `truncate_mode`)
- **Eje Y**: **distancia** a la que se fusionó cada par
- **Altura mayor = clusters más distantes / separación entre clusters
- **Cortar** en Y = corte horizontal = obtienes clusters

> Truco: corta **dónde las líneas verticales sean MÁS LARGAS**. Esas son las "verdaderas separaciones.

---

## 🧪 Ejemplos de la vida real

- 🧬 **Bioinformática**: árboles filogenéticos (parentesco entre ADN)
- 👔 **Segmentación de clientes**: árbol de "tipos" de cliente
- 🎓 **Educación**: clasificación de perfiles de estudiantes
- 📚 **Motores de recomendación**: jerarquía de temas/artículos

---

## 💡 Trucos para la clase

1. **Estandariza** también. Ward usa distancias euclídeas, así que escala importa.
2. **Primero pinta el dendrograma **antes** de decidir K.
3. Si el dendrograma tiene muchísimas hojas, usa `truncate_mode='lastp'` con `p=30` para que se vea solo las últimas 30 fusiones.
4. **Ward** tiende a hacer clusters iguales; si hay outliers, considera **otro linkage.
5. Comparte con K-means**:
   - Pequeños: jerárquico + dendrograma
   - Grandes: K-means o MiniBatchKMeans
