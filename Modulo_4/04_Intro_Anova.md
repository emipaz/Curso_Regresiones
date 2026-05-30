# Resumen sobre ANOVA

## Importancia de Conocer Nuestros Datos
- Conocer bien los datos ayuda a determinar qué pruebas estadísticas se pueden ejecutar.
- Se han discutido variables continuas y categóricas, enfocándose principalmente en la regresión lineal.

## Introducción al ANOVA
- El Análisis de Varianza (ANOVA) examina la relación entre variables categóricas y continuas.
- ANOVA permite probar diferencias de medias entre tres o más grupos, a diferencia de las pruebas t, que comparan solo dos grupos.

## Tipos de ANOVA
### ANOVA Unidireccional
- Compara medias de una variable dependiente continua en tres o más grupos basados en una variable categórica.
- Ejemplo: Comparar la esperanza de vida de diferentes especies de mariposas.
- **Hipótesis Nula (H0)**: La esperanza de vida es igual para todas las especies.
- **Hipótesis Alternativa (H1)**: La esperanza de vida no es igual entre las especies.

### ANOVA Bidireccional
- Compara medias en función de dos variables categóricas.
- Examina interacciones entre las variables.
- Ejemplo: Esperanza de vida relacionada con especie y tamaño de mariposa.
- **Hipótesis**:
  1. **Especie**: No hay diferencia en la esperanza de vida entre especies.
  2. **Tamaño**: No hay diferencia en la esperanza de vida según el tamaño de las mariposas.
  3. **Interacción**: La especie y el tamaño no interactúan en su efecto sobre la esperanza de vida.

## Conclusión
- ANOVA es una herramienta poderosa para entender las relaciones entre variables.
- Se revisaron las diferencias entre ANOVA unidireccional y bidireccional y se establecieron hipótesis para cada prueba.
- En futuras lecciones, se explorará cómo utilizar computadoras y Python para ejecutar ANOVA.

## Rellene el espacio en blanco: Análisis de varianza es un grupo de técnicas estadísticas que comprueban la diferencia de medias entre grupos _____. 


- dos
- un número infinito de
- **tres o más**
- tres

Correcto
> El Análisis de varianza es un conjunto de técnicas estadísticas que evalúan la diferencia de medias entre tres o más grupos. Es una extensión de las pruebas t, que evalúan las medias entre varios grupos. 


# Más sobre ANOVA

## Introducción
El Análisis de Varianza (ANOVA) es un conjunto de técnicas estadísticas que prueban la diferencia de medias entre grupos. Es útil para determinar si las diferencias entre grupos, basadas en variables categóricas, son estadísticamente significativas.

## Visión General de ANOVA
La intuición detrás de ANOVA es comparar la variabilidad entre grupos con la variabilidad dentro de ellos. Si la variabilidad entre grupos es mayor, es probable que provengan de subpoblaciones significativamente diferentes.

### Tipos de ANOVA
- **ANOVA Unidireccional**: Compara las medias de una variable dependiente continua en tres o más grupos de una variable categórica.
- **ANOVA Bidireccional**: Compara las medias en función de dos variables categóricas.

## ANOVA Unidireccional: Pasos
1. Calcular las medias de los grupos y la media general.
2. Calcular la suma de cuadrados entre grupos (SSB) y dentro de los grupos (SSW).
3. Calcular los cuadrados medios para SSB y SSW.
4. Calcular el estadístico F.
5. Utilizar la distribución F y el estadístico F para obtener un Valor P y decidir sobre la hipótesis nula.

### Ejemplo Práctico
- **Hipótesis**:
  - H0: \( \mu_A = \mu_B = \mu_C \) (las medias son iguales)
  - H1: \( \text{NOT} (\mu_A = \mu_B = \mu_C) \) (las medias no son iguales)
  
#### Datos de Estudiantes
| Estudiante | Programa de estudios (X) | Nota del examen (Y) |
|------------|--------------------------|---------------------|
| 1          | A                        | 88                  |
| 2          | A                        | 79                  |
| 3          | A                        | 86                  |
| 4          | A                        | 90                  |
| 5          | B                        | 94                  |
| 6          | B                        | 84                  |
| 7          | B                        | 87                  |
| 8          | B                        | 89                  |
| 9          | C                        | 85                  |
| 10         | C                        | 76                  |
| 11         | C                        | 81                  |
| 12         | C                        | 78                  |

### Pasos Detallados
1. **Calcular Medias**:
   - Media general (MG) = 84.75

2. **Calcular Sumas de Cuadrados**:
   - SSB = 150.5
   - SSW = 167.75

3. **Calcular Cuadrados Medios**:
   - MSSB = 75.25
   - MSSW = 18.64

4. **Calcular Estadístico F**:
   - \( F = \frac{MSSB}{MSSW} = 4.04 \)

5. **Obtener Valor P**:
   - Área bajo la curva para \( F \) indica probabilidad de rechazar la hipótesis nula.

## Supuestos del ANOVA
1. Los valores dependientes de cada grupo deben proceder de distribuciones normales.
2. Las varianzas entre grupos deben ser iguales.
3. Las observaciones deben ser independientes.

## Puntos Clave
- ANOVA examina si las medias de una variable dependiente continua son significativamente diferentes según variables categóricas.
- Solo se necesita que una media sea significativamente diferente para rechazar la hipótesis nula.
- ANOVA compara la varianza entre grupos con la varianza dentro de ellos.
- Es esencial verificar que se cumplan los supuestos de ANOVA para evitar conclusiones erróneas.

