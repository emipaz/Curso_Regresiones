# Resumen: Pruebas de Chi-cuadrado

## 🔄 Transición desde Pruebas T

**Contexto previo:**
- Pruebas t (una y dos colas) → comparan medias de dos grupos
- Regresión lineal → enfocada en variables continuas

**Nuevo enfoque:**
- Pruebas de chi-cuadrado → para **variables categóricas**
- Comparan datos esperados vs observados

## 📊 1. Prueba de Bondad de Ajuste (χ²)

### Definición
Determina si **una variable categórica observada** sigue una distribución esperada

### Ejemplo: Ventas de Palomitas en Cine

**Situación:**
- Tamaños: pequeña, mediana, grande, extra grande
- Afirmación del empleado: 25% de ventas para cada tamaño
- Muestra: 100 compradores

**Valores esperados:**
- 25% × 100 = 25 personas por cada tamaño

### Hipótesis

**H₀ (Nula):**
- La variable **sigue la distribución esperada**
- 25 personas compran cada tamaño

**H₁ (Alternativa):**
- La variable **NO sigue la distribución esperada**
- Los datos observados difieren significativamente

**Fórmula del Estadístico**

χ² = Σ [(Observado - Esperado)² / Esperado]

**Proceso:**

- **Calcular** χ²
- Obtener **valor p**
- **Decidir** si rechazar H₀


## 🔗 2. Prueba de Independencia (χ²)

**Definición:**

Determina si dos variables categóricas están asociadas entre sí
(También llamada prueba de homogeneidad)
Ejemplo: Clima y Ventas de Palomitas

**Variables:**

- Clima: llueve / no llueve
- Ventas: >100 personas / ≤100 personas

**Datos recopilados**:

- Total: 275 días
- 83 días llovió / 192 días no llovió
- 135 días >100 ventas / 140 días ≤100 ventas

**Hipótesis H₀ (Nula)**:

Las variables son independientes
NO están asociadas entre sí

**H₁ (Alternativa)**:

Las variables NO son independientes
SÍ están asociadas entre sí

**Tabla de Contingencia 2×2**

Se construye tabla de conteos cruzados con todas las combinaciones
Cálculo de Valores Esperados

Valor Esperado (i,j) = (Total fila i × Total columna j) / Total general

**Fundamento**:

Basado en definición de independencia

$P(A y B) = P(A) × P(B)$

**Fórmula del Estadístico**

χ² = Σ [(Observado - Esperado)² / Esperado]

(Misma fórmula que bondad de ajuste)
Proceso:

- Construir tabla 2×2
- Calcular valores esperados
- Calcular χ²
- Obtener valor p
- Determinar si las variables son independientes

🎯 Puntos Clave

- Bondad de ajuste: 1 variable categórica vs distribución esperada
- Independencia: relación entre 2 variables categóricas
- Ambas usan la misma fórmula de χ²
- Se calcula valor p para tomar decisión
- Conectan con conceptos previos de pruebas de hipótesis
- Permiten responder preguntas sobre variables categóricas

📌 Próximos Pasos

Revisar supuestos de las pruebas χ²
Profundizar en la realización de las pruebas
Aplicar a más casos con variables categóricas