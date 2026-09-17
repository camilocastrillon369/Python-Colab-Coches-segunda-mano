# Análisis de vehículos de segunda mano — Coches.net

Proyecto de extracción, limpieza y análisis de datos de vehículos de segunda mano obtenidos de Coches.net mediante técnicas de web scraping.

Este proyecto forma parte de mi Proyecto de Fin de Máster y tiene como objetivo analizar la oferta de vehículos de segunda mano y estudiar la relación entre variables como el precio, el año de matriculación, el kilometraje, la potencia, el combustible o el tipo de vehículo.

## Objetivos

Los principales objetivos del proyecto son:

* Obtener datos reales del mercado de vehículos de segunda mano mediante web scraping.
* Limpiar y estandarizar la información obtenida.
* Analizar la estructura y calidad de los datos.
* Realizar un análisis exploratorio de los datos (EDA).
* Identificar relaciones entre las principales características de los vehículos y su precio.
* Analizar la oferta según marca, modelo, combustible, transmisión y carrocería.
* Detectar valores atípicos.
* Aplicar filtros de negocio para seleccionar los vehículos relevantes para las siguientes fases del proyecto.

## Extracción de datos

Durante el proceso de extracción se probaron diferentes herramientas de web scraping.

Inicialmente se utilizó BeautifulSoup, pero los mecanismos de seguridad de la página limitaron la extracción a aproximadamente 1.000 registros. El código desarrollado se mantiene en el proyecto como parte del proceso de trabajo.

Posteriormente se utilizó Selenium, con el que se consiguió obtener una base de datos de 6.867 registros. Esta extracción se centró principalmente en vehículos de tipo furgoneta.

También se realizó una segunda extracción mediante Playwright desde la página principal de Coches.net, obteniendo 3.781 registros adicionales, principalmente de turismos.

La combinación de ambas extracciones permitió trabajar con una muestra más amplia y analizar diferentes segmentos de vehículos.

## Limpieza y preparación de los datos

Una vez obtenidos los datos, se realizó un proceso de limpieza y estandarización para poder trabajar con ellos de forma homogénea.

Entre las principales transformaciones realizadas se encuentran:

* Conversión de precio, kilómetros y potencia a formatos numéricos.
* Eliminación de símbolos, unidades y separadores de miles.
* Estandarización del año de matriculación.
* Tratamiento de valores nulos.
* Eliminación de registros duplicados.
* Comprobación de los tipos de datos.
* Exportación del dataset limpio a CSV.

Durante este proceso se eliminaron 205 registros duplicados. El resultado final fue un dataset de 9.527 registros y 10 variables, sin valores nulos.

## Variables analizadas

El dataset contiene las siguientes variables:

| Variable    | Descripción              |
| ----------- | ------------------------ |
| Marca       | Fabricante del vehículo  |
| Modelo      | Modelo comercial         |
| Precio      | Precio de venta en euros |
| Año         | Año de matriculación     |
| Kilómetros  | Kilometraje del vehículo |
| Combustible | Tipo de combustible      |
| Transmisión | Tipo de cambio           |
| Potencia    | Potencia en CV           |
| Fuente      | Origen de los datos      |
| Carrocería  | Tipo de vehículo         |

## Análisis exploratorio

El análisis parte de una revisión general del dataset para conocer su estructura, distribución y principales características.

El precio de los vehículos analizados se encuentra entre 1.499 € y 57.500 €, con un precio medio de 21.838,24 €. El año de matriculación va desde 1997 hasta 2026, mientras que el kilometraje oscila entre 1 km y 426.000 km. La potencia se encuentra entre 23 CV y 555 CV.

En cuanto a la oferta, se identificaron 57 marcas diferentes. Ford es la marca con mayor representación, con 906 vehículos.

Respecto al combustible, el diésel representa el 54 % de los registros, seguido de la gasolina (19,6 %), los híbridos (13,7 %), los eléctricos (aproximadamente un 10 %) y el gas (3 %).

La transmisión manual representa el 67,3 % de los vehículos, frente al 32,7 % de vehículos con transmisión automática.

## Relaciones entre variables

Una de las partes principales del análisis consiste en estudiar la relación entre las variables numéricas.

Las correlaciones obtenidas fueron:

| Relación            | Correlación |
| ------------------- | ----------: |
| Precio - Año        |         0,5 |
| Precio - Kilómetros |        -0,5 |
| Precio - Potencia   |         0,3 |
| Año - Kilómetros    |        -0,7 |

Los resultados muestran una relación positiva entre el año de matriculación y el precio, mientras que la relación entre precio y kilometraje es negativa. También existe una relación positiva entre potencia y precio.

La relación más fuerte se encuentra entre el año de matriculación y los kilómetros, con una correlación de -0,7.

## Visualización

Para analizar los datos de forma gráfica se utilizaron Matplotlib, Seaborn y Plotly, junto con Pandas y NumPy para la preparación y manipulación de los datos.

Entre las visualizaciones realizadas se encuentran:

* Matriz de correlación.
* Distribución de precios.
* Distribución del kilometraje.
* Distribución por año de matriculación.
* Distribución de potencia.
* Evolución del precio medio según el año.
* Relación entre precio y kilometraje.
* Relación entre precio y potencia.
* Relación entre kilometraje y año.

## Principales resultados

Algunas de las conclusiones obtenidas durante el análisis son:

* Los vehículos más recientes tienden a presentar precios más elevados.
* Los vehículos con mayor kilometraje tienden a presentar precios inferiores.
* Existe una relación positiva, aunque más moderada, entre potencia y precio.
* Los vehículos eléctricos e híbridos presentan los precios medios más elevados dentro del dataset analizado.
* Existe una diferencia considerable entre los precios medios de las distintas marcas.
* Los vehículos comerciales tienen una presencia importante en la muestra, especialmente las furgonetas.
* Los modelos con mayor número de registros son Iveco Daily, Ford Transit Connect, Ford Transit, Volkswagen Transporter y Ford Transit Courier.

## Valores atípicos

Para detectar valores atípicos se utilizó el rango intercuartílico (IQR).

En el caso del kilometraje se identificaron 247 valores atípicos, aproximadamente el 2,65 % del dataset.

En el precio se detectaron 328 valores atípicos, aproximadamente el 3,52 % de los registros. La mayor parte de estos valores se encuentra en el extremo superior de la distribución de precios.

## Filtros de negocio

Como parte del análisis se definieron una serie de criterios para seleccionar los vehículos que resultaban más relevantes para el objetivo del proyecto:

* Año de matriculación ≥ 2020
* Kilometraje ≤ 120.000 km
* Precio entre 10.000 € y 20.000 €
* Carrocería: berlina, utilitario o furgoneta

Después de aplicar estos filtros, se obtuvieron **1.632 registros**, que quedan preparados para combinarse con los datos obtenidos de otras plataformas de compraventa.

## Tecnologías utilizadas

**Python**

* Pandas
* NumPy
* Matplotlib
* Seaborn
* Plotly

**Web scraping**

* BeautifulSoup
* Selenium
* Playwright

**Entornos de trabajo**

* Google Colab

## Próximos pasos

Este dataset forma parte de un proyecto más amplio en el que se analizan diferentes plataformas de compraventa de vehículos.

El siguiente paso consiste en integrar los datos de Coches.net con los obtenidos de las demás fuentes para construir un dataset unificado y continuar con el análisis del mercado de vehículos de segunda mano.
