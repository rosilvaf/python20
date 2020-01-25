# Minería de datos de marketing bancario
Predicción de la tasa de suscripción de un conjunto de datos de marketing bancario.

El conjunto de datos es del [Repositorio de aprendizaje automático UCI] (https://archive.ics.uci.edu/ml/datasets/bank+marketing).



# Introducción
Este proyecto tiene como objetivo predecir la suscripción del depósito en función del conjunto de datos proporcionado. El conjunto de datos proviene de campañas de marketing directo de una institución bancaria portuguesa.
Se proporcionan 21 atributos que se pueden dividir en la información del cliente del banco, los datos de la campaña y el índice social y económico.
El detalle de los atributos se encuentra a continuación.

| Attribute | Description | Type |
| --- | --- | --- |
| age | Age of the client | Ratio |
| job | Client&#39;s occupation | Nominal |
| marital | Marital status | Nominal |
| education | Client&#39;s education level | Nominal |
| default | Indicates whether the client has credit in default | Nominal |
| housing | Indicates whether the client has a housing loan | Nominal |
| loan | Indicates whether the client as a personal loan | Nominal |
| contact | Type of contact communication | Nominal  |
| month | Month that last contact was made | Nominal  |
| day\_of\_week | Day that last contact was made | Nominal  |
| duration | Duration of last contact in seconds | Ratio  |
| campaign | Number of contacts performed during this campaign for this client (including last contact) | Ratio |
| pdays | Number of days since the client was last contacted in a previous campaign | Ratio  |
| previous | Number of contacts performed before this campaign for this client | Ratio |
| poutcome | Outcome of the previous marketing campaign | Nominal  |
| emp.var.rate  | Employment variation rate (quarterly indicator) | Ratio |
| cons.price.idx  | Consumer price index (monthly indicator) | Ratio |
| cons.conf.idx  | Consumer confidence index (monthly indicator) | Ratio |
| euribor3m | Euribor 3-month rate (daily indicator) | Ratio |
| nr.employed | Number of employees (quarterly indicator) | Ratio |
| Final\_Y | The subscription of the deposit | Norminal |

El informe registra el proceso de prueba y error, y finalmente proporciona el mejor enfoque para el problema de predicción. Sklearn es el marco principal utilizado en este proyecto.
# Limpieza de datos y preprocesamiento
## Limpieza de datos
La limpieza de datos consiste en el llenado de los valores faltantes, la fijación de inconsistencias, la eliminación de valores atípicos y la reducción de la duplicación.
### Valores faltantes
Hay seis atributos que contienen valores faltantes que son & # 39; trabajo & # 39 ;, & # 39; marital & # 39 ;, & # 39; educación & # 39 ;, & # 39; default & # 39 ;, & # 39; vivienda & # 39 ;, y & # 39; préstamo & # 39 ;,
Como ninguno de ellos es de tipo numérico, se rellenan por modo. Por ejemplo, todos los valores faltantes en & # 39; trabajo & # 39; son reemplazados por & # 39; collar azul & # 39 ;.
### Inconsistencia
De acuerdo con la descripción del atributo, un valor de & # 39; 999 & # 39; en los & # 39; pdays & # 39; significa que el cliente es nuevo. Por lo tanto, el correspondiente '' poutcome '' sería & # 39; inexistente & # 39 ;. Sin embargo, algunas entradas son inconsistentes con esta regla. Entonces, se eliminan.
### Valores atípicos
Como la mayoría de los valores en los puntos de datos están dentro del rango normal, es razonable entrenar el modelo sin valores atípicos. Al hacerlo, el modelo debe predecir bien en los puntos de datos normales. El rango de valores atípicos se identifica mediante el diagrama de caja.
Por ejemplo, toda la duración superior a 500s se tratan como valores atípicos.
### Duplicación
Reducir la duplicación ayuda a mejorar el rendimiento del modelo.
## Preprocesamiento de datos
### Codificación en caliente
Como los datos nominales no se pueden usar en muchos clasificadores, todos los datos nominales están codificados por one-hot. Esto se hace mediante la función dummy () en Pandas.
### Normalización
Para reducir la complejidad del cálculo y hacer que el peso del valor sea el mismo, se realiza la normalización de la puntuación z. La puntuación Z normaliza los puntos de datos en la zona de la esfera que es mejor para el vecino K más cercano (KNN). KNN es el clasificador asignado en este proyecto.El F score es 0.458.

### Árbol de decisión
La selección de funciones se realiza primero. Según el gráfico, nueve características son la mejor opción.
Figura 4 Números de características diferentes en el árbol de decisión
Las caracteristicas son & # 39; edad & # 39 ;, & # 39; duración & # 39 ;, & # 39; cons.conf.idx & # 39 ;, & # 39; euribor3m & # 39 ;, & # 39; marital \ _single & # 39 ;, & # 39; education \ _university.degree & # 39 ;, & # 39; housing \ _no & # 39 ;, y & # 39; poutcome \ _success & # 39 ;.
### Bosque aleatorio
El F score final del bosque aleatorio es 0.630. La matriz de confusión se muestra a continuación.
### Aumento de gradiente
Figura 7 Matriz de confusión del aumento de gradiente
El score F es 0.636
### Comparacion
| **Classifier** | **F score** |
| --- | --- |
| Gradient boosting | 0.636 |
| Decision tree | 0.626 |
| Random forest | 0.630 |
| KNN | 0.458 |
Tabla de comparacion F score
## Mejor clasificador - Aumento de gradiente
Las características seleccionadas son:
- age
- duration
- conf.idx
- euribor3m
- marital\_single
- education\_university.degree
- housing\_no
- poutcome\_success
Los ajustes de parametros son n\estimators=113, learning\_rate=0.2, max\_depth=3, subsample=1, criterion: &#39;friedman\_mse&#39;
El F score es 0.636, y la precisión correspondiente es 92.20% . El resultado se basa en la división del conjunto de datos de entrenamiento local en el que el 80% son datos de entrenamiento y el 20% son datos de prueba.



```python

```
