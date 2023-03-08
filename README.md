# Manejo de Datos Faltantes: Detección y Exploración

## Índice

* [Descripción del proyecto](#descripción-del-proyecto)
* [1. Identificación de valores faltantes](#1-identificación-de-valores-faltantes)
* [2. Unificar el formato de los valores faltantes](#2-reemplazar-los-valores-faltantes-para-trabajar-todo-estos-con-el-mismo-formato)
* [2.1. Valores faltantes explicitos](#21-los-valores-faltantes-explicitos-son-aquellos-en-los-que-se-puede-identificar-de-forma-directa-por-ejemplo-esta-el-valor-en-na--o-expresado-de-alguna-manera-en-la-variable)
* [2.1. Valores faltantes implicitos](#22-los-valores-faltantes-implicitos-se-refiere-a-todo-aquello-que-se-entiende-que-está-incluido)
* [3. Detección y manipulación de valores faltantes](#3-detección-y-manipulación-de-valores-faltantes)
* [4. Búsqueda de relaciones de valores faltantes](#4-busqueda-de-relaciones-de-valores-faltantes)
* [5. ELiminació de valores faltantes](#5-eliminación-de-valores-faltantes)
* [6. Tratamiento de valores faltantes](#6-tratamiento-de-valores-faltantes)


# Descripción del proyecto 
A los largo de este archivo describe un paso a paso de como detectar y abordar los valores faltantes o también llamados outliers, basado en el curo de Platzi Curso de Manejo de Datos Flatantes: Detección y Exploración ditacto por el profesor Jesús Velez.

Este documento se divide en 6 pasos a la hora de tratar con este tipo de datos:

## 1. Identificación de valores faltantes
Identificar como aparecen los valores faltantes en los datos a trabajar, en ocasiones los valores valtantes pueden aparecer como: 'NA', '#NA','N A', 'nan', 'N/A', 'missing',  o si son variables numericas pueden aparecer como: -9, -99,-999, -9999, 99, 9999, 0, entre otros. En estos casos si ejecutamos una linea de código para detectar los outliers esta nos dará un cero. 

Por este motivo es conveniente identificar de que formas pueden aparecer nuestros valores faltantes para que sean reemplazados y unificados en un único formato, ya que en muchas ocasiones no se puede modificar directamente el archivo que se esta leyendo.

## 2. Reemplazar los valores faltantes para trabajar todo estos con el mismo formato
Despues de identificar la forma en la que parecen estos valores faltantes es posible reemplazar estos por el formato que se crea mas conveniente, por ejemplo ```np.nan``` o ```"NA"```

Tambien debe considerarse que existen dos formas en las que podemos tener valores faltantes:
### 2.1. **Los valores faltantes explicitos**, son aquellos en los que se puede identificar de forma directa, por ejemplo, esta el valor en NA, "", o expresado de alguna manera en la variable.
### 2.2. **Los valores faltantes implicitos**, se refiere a todo aquello que se entiende que está incluido
pero sin ser expresado de forma directa o explícitamente.”

Un valor faltante implícito indica que el valor faltante <b>debería estar incluido</b>en el conjunto de datos del análisis, <b>sin que éste lo diga</b> o lo <b>especifique</b>.Por lo general, son valores que podemos encontrar al pivotar nuestros datoso contabilizar el número de apariciones de combinaciones de las variables de estudio.</p>

Una manera de identificar los valores implicitos es pivotarlos ```df.pivot_wider()``` y cuantificar la existencia de las n-tuplas. para este caso lo ideal es exponer las filas faltantes implicitas a explicitas, es decir, agregar estas filas de los implicitas a los datos


## 3. Detección y manipulación de valores faltantes 

Es este punto se muestran algunas funciones creadas (funciones extendidas de la API de Pandas) utilies a la hora de realizar el analisis de los valores faltantes y algunas visualizaciones iniciales de valores faltantes.

## 4. Busqueda de relaciones de valores faltantes

## 5. ELiminación de valores faltantes
<div class="alert alert-warning", role="alert">
    <b style="font-size: 1.5em;">🚧 Advertencia</b>
    <br>
    <br>
    <p>
    La eliminación de valores faltantes <b>asume</b> que los valores faltantes están perdidos
    completamente al azar (<code>MCAR</code>). En cualquier otro caso, realizar una
    eliminación de valores faltantes podrá ocasionar <b>sesgos</b> en los
    análisis y modelos subsecuentes.
    </p>
</div>

## 6. Tratamiento de valores faltantes

Cuando se trata de valores faltantes tenemos dos aproximaciones para el tratamiento de los mismos:

* **Eliminacion de valores faltantes:** La eliminación de valores faltantes asume que los valores faltantes están perdidos completamente al azar (MCAR). En cualquier otro caso, realizar una eliminación de valores faltantes podrá ocasionar sesgos en los análisis y modelos subsecuentes. Por tanto, es importante investigar que mecanismos tienen los datos para asi evitar los sesgos a la hora de eliminarlos
* **Imputacion de valores faltantes:** consiste en añadir valores en los datos faltantes para mantener el registro en el dataset

Para el análisis de valores faltantes se debe iniciar por el análisis de preguntas simples, que lleven a un número como:

* Cuantos valores deberian existir en el conjunto de datos?

También es conveniente construir resumenes por variables y observaciones:

* Cuantos valores faltantes existen por cada variable?
* ¿Cuantas variables tiene X numero de valores faltantes?
* ¿Cuantas observaciones tiene X numero de valores faltantes?
* Cuenta los registros con datos faltantes
Salir de la caja y hacer mas preguntas
* ¿Cuantos valores faltantes tengo en una variable cada X pasos? para el caso de trabajar con series de tiempo
* ¿Cual es la racha de valores completos y faltantes en una variable?

Para eso se ha construido un conjunto de funciones que nos pueden reponder aestas preguntas con df.missing.


* missing_variable_summary() #metodo para obtener tabla con el conteo de datos faltantes en todas las columnas

* missing_variable_table() #metodo para obtener tabla agrupada por el conteo de datos faltantes en todas las columnas

* missing_variable_table método que permite ver cuantas variables tienen un numero de valores faltantes.
 n_missing_in_variable: cantidad de valores faltantes que tiene
 n_variables: cantidad de columnas con n valores faltantes
 
* missing_case_summary método que permite ver en cada fila cuantas columnas  tienen valores faltantes

* missing_case_table método que permite ver las filas con numeros de valores faltantes, por ejemplo: x filas tiene n valores faltantes y esto representa % de filas

* missing_variable_span: muy util para series de tiempo, ordenandolo por una fecha por ejemplo span_every romper el conjunto de datos en 50 bloques cada uno, en las primeras (span_counter) en las primeras 50 filas tenemos n valores faltantes(ver col n_missing), seguido por n2 valores completos (ver n_complete) y esto representa un % de valores faltantes y % de valores completos

* missing_variable_run: Permite ver la racha de valores faltantes para ver si cada tantas filas se presenta un valor faltante

Para tener la visualización de valores faltantes se tienen las funciones:

* missing_variable_plot: Permite visualizar de manera ordenada de mayor a menor la cantidad de valores faltantes por columna

* missing_case_plot: Grafico de barras que permite visualizar la en el eje x, la frecuencia de valores faltantes por fila (cuantas variables son faltantes en las filas) y en el eje y el numero de casos con esa cantidad de variables faltantes.

* missing_variable_span_plot: ver la variable por la cantidad en la que queremos romper el conjunto de datos, por example 

* missing_upsetplot Ver si los valores faltantes provienen de observaciones conjuntas. 




