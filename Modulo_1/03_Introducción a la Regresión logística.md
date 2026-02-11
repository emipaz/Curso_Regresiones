# Introducción a la regresión logística

## Probabilidad y eventos discretos

Un ejemplo clásico de probabilidad es lanzar una moneda:
- Probabilidad de **cara**: 0,5 (50 %)
- Probabilidad de **cruz**: 0,5 (50 %)

Aunque este es un caso simple, en el análisis de datos es común enfrentarse a **problemas de probabilidad más complejos**, donde intervienen múltiples factores. Para estos casos se utiliza la **regresión logística**.

## ¿Qué es la regresión logística?

La **regresión logística** es una técnica de modelado que permite estimar una **variable dependiente categórica** a partir de una o más **variables independientes**.

- La variable dependiente tiene un conjunto **discreto** de posibles resultados.
- Frecuentemente se trabaja con resultados binarios:
  - Sí / No  
  - 1 / 0  

### Ejemplos de uso

- ¿Qué factores influyen en que alguien se **suscriba o no** a un boletín?
- ¿Cuándo una persona **comenta o no** una publicación en redes sociales?
- ¿Cuál es la probabilidad de que alguien **renueve o no** su membresía?

## Ejemplo: suscripción a un boletín

Supongamos que una empresa quiere aumentar los lectores de su boletín:

- **Variable dependiente (y)**:
  - 0 = no se suscribe  
  - 1 = sí se suscribe  

- **Variable independiente (x)**:
  - Tiempo (en minutos) que el usuario pasa en la página web antes de salir  
  - Es una variable continua  

Al representar los datos en un diagrama de dispersión:
- Los valores de **y** aparecen como dos líneas horizontales:
  - y = 1 (usuarios suscritos)
  - y = 0 (usuarios no suscritos)
- El eje **x** representa el tiempo en la página web

La relación entre **x** e **y** no es una línea recta, por lo que **no es adecuada la regresión lineal**.

## Probabilidad como media

En la regresión logística, el concepto clave es que:

- La **media de y dado x** es igual a la **probabilidad de que y = 1 dado x**

Como los valores observados de **y** son solo ceros y unos:
- La suma de los valores observados es el número total de unos
- Al dividir entre el número total de observaciones, se obtiene una probabilidad

Esta probabilidad suele expresarse como:

- $P(y = 1 \mid x)$  

donde **P** representa probabilidad.


### ¿Qué técnica modela una variable categórica en función de una o varias variables independientes?

- [ ] Función de enlace
- [x] Regresión logística
- [ ] Coeficientes de regresión
- [ ] Función de pérdida

> La Regresión logística modela una variable categórica basada en una o más variables independientes. La variable dependiente en una regresión logística puede tener dos o más valores discretos posibles. 

## Función de enlace (funcion de Activacion)

Para relacionar las variables independientes con la probabilidad del resultado, la regresión logística utiliza una **función de enlace**:

- Es una función **no lineal**
- Conecta matemáticamente:
  - Las variables independientes ($x$)
  - Con la probabilidad de que $y$ tome un valor específico

Este es uno de los principales elementos que diferencia la regresión logística de la regresión lineal.

## Comparación: regresión lineal vs. regresión logística

### Tipo de variable dependiente

- **Regresión lineal**:
  - Variable dependiente continua (ej. ventas de libros)
- **Regresión logística**:
  - Variable dependiente categórica (ej. suscripción sí/no)

### Qué se modela

- **Regresión lineal**:
  - La **media** de $y$
- **Regresión logística**:
  - La **probabilidad** de un resultado (por ejemplo, $y = 1$)

### Relación matemática

- **Regresión lineal**:
  - $y$ se expresa directamente como función de $x$
- **Regresión logística**:
  - Se requiere una **función de enlace** para conectar la probabilidad con $x$

## Extensiones de la regresión logística

Aunque en este curso se enfatiza la regresión logística binaria:
- Existen versiones más complejas que permiten modelar:
  - Múltiples categorías
  - Resultados no binarios  
  - Ejemplos: tipos de productos comprados o tipos de servicios recibidos

## Próximos pasos

En secciones posteriores se estudiará:
- La **estimación por máxima verosimilitud**
- Más detalles matemáticos de la regresión logística

Gracias a la potencia computacional actual, los profesionales de datos pueden centrarse menos en los cálculos manuales y más en la **interpretación y narración de resultados**, comprendiendo siempre qué ocurre detrás del modelo.


## Comparando la regrecion logistica y la lineal
### Categorization exercise

### Fundamantal para la ciencia de datos:

- [ ] Regresión Lineal
- [ ] Regresión Logistica
- [x] Ambas

### Supone una relación lineal entre las variables independientes y la dependiente.

- [x] Regresión Lineal
- [ ] Regresión Logistica
- [ ] Ambas

### Nos permite estimar relaciones entre variables observadas
  
- [ ] Regresión Lineal
- [ ] Regresión Logistica
- [x] Ambas
  
### Las variables dependientes e independientes deben estar correlacionadas

- [x] Regresión Lineal
- [ ] Regresión Logistica
- [ ] Ambas

### Se pueden utilizar múltiples variables predictoras/independientes (X)
  
- [ ] Regresión Lineal
- [ ] Regresión Logistica
- [x] Ambas
  
### La variable de resultado (Y) es continua
  
- [x] Regresión Lineal
- [ ] Regresión Logistica
- [ ] Ambas

### La variable de resultado (Y) es categórica.

- [ ] Regresión Lineal
- [x] Regresión Logistica
- [ ] Ambas

### La función de enlace se utiliza para modelar la variable de resultado (Y)

- [ ] Regresión Lineal
- [x] Regresión Logistica
- [ ] Ambas

## Autoevaluacion

### Qué es una función no lineal que conecta o vincula matemáticamente una variable dependiente con las variables independientes?  

- [ ] Función de pérdida
- [ ] Función de regresión
- [ ] Función de relación
- [x] Función de enlace

> La función de enlace conecta, o enlaza, matemáticamente una variable dependiente con las variables independientes. Los profesionales de los datos utilizan la función de enlace para expresar la relación entre las X y la probabilidad de que Y sea igual a algún resultado.

### ¿Qué tipo de regresión modela una variable categórica en función de una o varias variables independientes?

- [ ] Coeficiente de regresión
- [ ] Regresión lineal
- [ ] Regresión ordinaria
- [x] Regresión logística

> 
> La regresión logística modela una variable categórica en función de una o más variables independientes. La variable dependiente puede tener dos o más valores discretos posibles.


