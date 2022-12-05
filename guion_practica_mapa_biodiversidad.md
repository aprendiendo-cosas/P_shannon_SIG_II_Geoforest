# Instrucciones para realizar la práctica denominada "Cuantificación y representación espacial de la diversidad biológica"


> + **_Versión_**: 2022-2023
> + **_Asignatura_** : SIG II (Máster GEOFOREST). 
> + **_Autor_**: Curro Bonet-García (fjbonet@uco.es)
> + **_Duración_**: 4 horas.


## Objetivos

Esta práctica tiene los siguientes objetivos:
+ Disciplinares:
  + Reconocer el concepto de biodiversidad ya estudiado en en otras ocasiones.
  + Aprender un método para cuantificar la diversidad biológica. Índice de Shannon.
  + Aprender a generar mapas de diversidad biológica. Mapas de distribución del índice de Shannon.
  + Reconocer patrones de distribución de la diversidad en un territorio concreto.
  + Identificar las causas de los patrones anteriores.
  + Reconocer cómo la diversidad biológica cambia su significado al hacerlo la escala espacial. 
  
+ Instrumentales:
  + Afianzar nuestro conocimiento de SIG.
  + Mejorar nuestro conocimiento de R.
  + Poner en práctica algunos conceptos ya conocidos de las bases de datos relacionales. 
  + Entrenar la habilidad de transferir conocimientos de un ámbito (territorial en este caso) a otro.
  
   
## Contextualización ecológica y estructura de la sesión

Para cuantificar la diversidad biológica se pueden utilizar muchos índices. En nuestro caso usaremos el denominado índice de Shannon-Wiever, que es uno de los más robustos y comunmente utilizados. Para su cálculo se necesita la siguiente información:

+ Delimitación espacial de la comunidad para la que queremos calcular el índice de diversidad.
+ Listado de especies existente en esa comunidad.
+ Abundancia de cada especie en dicha comunidad.

La siguiente presentación muestra los conceptos básicos necesarios para hacer la práctica. También puedes verla [aquí](https://prezi.com/view/07Hx3W5wMEZBtpdeeouO/) y descargarla [aquí](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2022-2023/presentacion/1_Geoforest_introduccion_biodiversidad.exe.zip) para Windows y [aquí](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2022-2023/presentacion/1_Geoforest_introduccion_biodiversidad.zip) para Mac. Y [aquí](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2022-2023/presentacion/1_Geoforest_introduccion_biodiversidad.pdf) la tienes en formato pdf.


<p><iframe src="https://prezi.com/view/07Hx3W5wMEZBtpdeeouO/embed" width="1200" height="900"> </iframe></p>


Para satisfacer los objetivos planteados, procederemos de la siguiente forma:

1. En primer lugar aprenderemos la mecánica del cálculo del mapa de diversidad a una escala de 250 m en el espacio protegido de Sierra Nevada (Sur de España). Es decir, asumiremos que una comunidad ecológica es una entidad de forma cuadrangular con un lado de 250 m. Esto no es así en la realidad, pero es la aproximación más fácil que tenemos a nuestro alcance. Una vez obtenido este mapa, trataremos de estudiar los patrones de cambio espacial de dicha diversidad. También identificaremos los factores abióticos que explican dichos patrones espaciales.
2. Las técnicas de análisis aprendidas en el primer punto deberán ser aplicadas a la actividad entregable de esta asignatura. Es decir, será necesario incluir un mapa de biodiversidad como elemento para realizar la estratificación del territorio. Pero deberá cambiarse el elemento geográfico utilizado para delimitar las comunidades ecológicas. En lugar de usar una malla de 250 m se usarán los contornos del mapa de vegetación a escala de detalle de Andalucía. Esto se detallará en la descripción del ejercicio (que se mostrará en un guión específico).


## Obtención de un mapa de biodiversidad: Metodología y flujo de trabajo

Como se puede observar en la presentación anterior, para calcular la diversidad de una comunidad, necesitamos dos fuentes de información:
+ Información de distribución de especies en la zona de estudio (Sierra Nevada). Es el primer paso fundamental porque necesitamos esta información para calcular el índice de Shannon. Para conseguir datos de presencia de especies en Sierra Nevada usaremos una infraestructura digital denominada [GBIF](https://www.gbif.org/) (Global Biodiversity Information Facility). Se trata de un portal desde el que se tiene acceso a millones de datos de presencia de especies procedentes de colecciones biológicas (herbarios, colecciones animales, etc.) de todo el planeta. Esta iniciativa está promovida y mantenida por multitud de países que han puesto en común toda la información de la que disponen para conocer mejor la distribución de la biodiversidad en la Tierra. Accederemos a este portal y descargaremos toda la información de presencia de especies en Sierra Nevada. Esto nos dará una idea bastante aproximada de cómo se distribuye la diversida en esta zona. En nuestro caso, GBIF aporta una enorme cantidad de registros de presencia de especies en Sierra Nevada. Durante la práctica visitamos el portal de GBIF y simulamos la descarga. Como este proceso puede tardar unas horas, utilizamos datos que fueron descargados anteriormente por el profesor. Dichos datos de presencia de especies tienen el siguiente "aspecto" cuando son visualizados en QGIS. [Aquí](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2022-2023/geoinfo/csv_gbif_sierra_nevada.zip) puedes descargar la capa con los datos de presencia de especies de Sierra Nevada. Como ves más abajo, son unos cuantos miles de puntos...

![puntos](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2022-2023/images/puntos.png)


+ Distribución de las comunidades ecológicas que conforman Sierra Nevada. Este paso es el más complejo conceptualmente, ya que las comunidades no tienen un límite espacial preciso. Es decir, están conectadas entre sí y no es fácil delimitar donde empieza una y acaba otra. En este caso usaremos una definición artificial y arbitraria de comunidad: un cuadrado de 250 m de lado. 

A partir de estas dos fuentes de datos obtendremos el índice de Shannon para cada una de las comunidades de Sierra Nevada. Es decir, usaremos los datos de presencia de cada especie que hay en cada una de las comunidades para calcular su índice de Shannon. En la siguiente figura puedes ver la distribución de ocurrencias de especies en unas cuantas comunidades.

![puntos_comunidades](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2022-2023/images/grid.png)


Para ello seguiremos los pasos que se muestran en el siguiente flujo de trabajo (se ve un poco pequeño, pero si vas a la parte de abajo encontrarás una herramienta lupa para aumentar y otra para desplazarte). También puedes descargar el flujo de trabajo [aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2022-2023/presentacion/sierra_nevada_shannon_QGIS_R.drawio.zip) (se abre con [esta](https://www.diagrams.net/) aplicación).

<iframe frameborder="0" style="width:100%;height:2913px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1&title=sierra_nevada_shannon_QGIS_R.drawio#R7V3rc5u4Fv9rPLN7Z5IBxMsfEzfNdm%2FvtFv3bm%2F3i0c2sq1bjFzASbx%2F%2FUqAeEm2cQJGib3TjUHiIc5P58k5YgBGq6f7EK6X%2FyEe8geG5j0NwLuBYVwBzaA%2FrGWbthgWMNOWRYi9tE0rGsb4b5Q26rx1gz0UZW1pU0yIH%2BN1tXFGggDN4kobDEPyWD1sTnyv0rCGC1QZBmsYz6CPhMO%2BYS9epq2u4RTtvyG8WPI76%2FYw7ZnC2Y9FSDZBdr%2BBAd5b78332QVXkF8ru2%2B0hB55LDWBuwEYhYTE6dbqaYR8Rtwq2d7v6M3HHaIgbnLCNzD2%2F%2FTm4V%2FbLfkx%2FObeWk%2FmlZ095gP0N4g%2FRzLaeMsplDwjYlfRB%2BD2cYljNF7DGet9pJOCti3jlZ91z0kQZyC7dJfQA3HM5oapsV7s%2ByPikzC5MvAgcucz2h7FIfmBSj32zEXTOe0RnzJ78AcUxuip1JQ99T0iKxSHW3oI783nWjZHr7KHfizwNkF2yLKEteUY11Y207JZtsivXlCabmTEPobwdreEr1F6Pkf2TEppzxlONU2EqhXCA7dKeH3oaiLtTQnt9aGtvZz0xmTu%2Bo9bO%2F795x9%2Fuc749vuXv69MgdDIoyIh2yVhvCQLEkD%2Frmi9LaBISJUf85GQdQbA%2F1EcbzME4CYmVXgoFcPt%2F9j5dEplu9%2FLfe%2Besoune9tsrwSrsw%2BViGzCGdrz1NlEjmG4QPGe4zLeYCTZi3GIfBjjh6oUbR0r6zCXwGid6oU5fmII3a5RiOndEZvg9BZUkaDPRVMZFOjjRUC3Z5SaSV8uoxnpPRgtc8gjxh3B4msCN6ANeJUoFv77Dq8W9Al9PKV%2F4YxRZuLhkI6MMDK8f0TTSYRCyjzX0cPiCGCPYDdgVuWcOxSZDRgir5ldcZpj9cFqNUn4fJZxGrKMqRbPiCr9HYpm9CEgbb2%2F%2FfBeVDRLsppuoqOUTGuTFtiVSetIJq1MQXQ3aRtoZmb3rZs%2FfW69wim%2FgrafKsawShVbE6miGzK92Zna5JJjH12o%2FFyzTUqUGEP%2FC3vkYJGwdWkWySZZlUB1WzEgAbtGnEgA1umjeZxtTkkck1W2E2aUSEQHxWHuJ%2BJ8iT0PBTLzR0v%2Bk87l%2FbPj8AznUlhEzj7lfAbggttRuD1VQVIERrOBp8ZhzOA4hF1ENRsX51qKZQxxkBhOerLv%2B3Ad4QLb2RL73ke4JZuY34bvHdYNLeFSc%2Ba4WCoLRk0mGA23K2TcbhmsDoIXkvVXbpOwhjXBzH69e6CkjtriwuSiCamsW%2FqPUnTEXBeLPs2I7uvFPv3HDg%2FjEQkon9IZxK6BYBQ%2FoihuPhXyGX54KhwCuzPbyhwKWN8x%2FwOjTmWqTCS%2BGOGDdvL%2B2X4USlwJnQQkSxNAonb3BaBdEpWDU8bLPCVeuogXCRYXwHaaJmIA87QM1rErcNF4u5wJDulBBWh0Bb3oTeitYq8wo%2BbT%2FuWqrzN4TAEeZiCPxJj3BaMjtV9nkIkxbud6eMHrpcqvM7waxAcvyq8L5WeKnHpa788SYzDno%2FyaB2p6M0vFQEyi%2FM5HmB4dTOvd9RPjKZTHRheuUtb3s8XgykX9nUT92WbP6s8W4zTtYq8wo%2BbTXl31Z4tRGaCfk%2Fo7AiNF1J8tRlPo7Ufggpiy6k8MsFzU30nUn2s1VH9dOf62GKg5H%2FVnNoarr7iMJKMaMF9CzEG8YKRI6FNSfcD89QtXKRv8tC%2B5Lj2pP10ToT%2Bx%2ByfGas7HUFU%2F68URAzMsGfGM3L9Xl%2FjiiAEVJmvcC2Kqun%2BOGGMZGLbP818rqNk%2FN4R3XEUJcW7oAdb6qeijWwv2%2B2m2CSmxZpjVaHiI%2FkFpWmHENgP6ZxOwrr9J8hMhH81mmO54kN%2BfPk86hPSKwhyq1tUcKPTYnW%2BdIJ1dVVKD2nKS7yFlx7N%2FWweap3ufuErwCcelIkG69z27GNsuSgTZDq8QbKGy8IVlUk3rpJxMFSlSJ%2BX2Ugh6erK7hlJkd0Sn78OKmdQwpK2j8Z%2FspvT%2FP%2B4%2FjEUhplClmiWpyTptpZpoKLyOSuYXTnyjqbxRqy7TtS8qpSnEw6ayzVIKYkd0kUdwndt0600QE2bRUauc%2FvUh2ya56Rfx46RFuiUfAPo%2B8skihKtBtdy90lcuej8kLVnpfIZcA%2FOvAcTHrBJRq3U1m9a6dlbqyjVmGcYv49R8%2F3Y%2FlhgO9FnjKkmFtQUYRfAM%2BjdZx4o6XymLI%2BoclBy0ajSKBZwYV0cFOh1gAIbVqjpLYoDLyh2NziDoRbe1JsDcpsttuL3pKPmyNH1QvV0yy59LLT3hiq8S755yG5jpi%2FFvn5U2fkHfxq8ruhG5jL77PL6nP3SQQHTj35qoBhJR7XYkqqW8Jb4EUFtmSGxL6XOp5Ta7MtNyNcWJxEgW5WPTnxmQbHsdki1be0gpGWK61ZmrO%2BLM5QmxlXXY7I5m7h4z702LEKu2toXOra2%2BRMhrDmQ8x8FuJL32GjIHpVfrdmV26mc2X8vem7ODqfk10kfKTqvNk3wcz586ugpRXEXngK73pcLk4%2B575UXTqTC6dj10DjF7sleKpDw7zrWPSQ%2B7L0ApICWmd4gSQ2QFfT8PdxlsIQ5txXd96Kllj4ChWRFdds%2FmiH5Rg41FIGgqAm2lOEfvxVk6ZTx%2FryI6LOjU0lh83PJ3lZXIfZqEMQ2L%2FIu0BfMGKiG9T%2Fdfdh9JR4h3Z2%2F0KCepicfXweYLOUsW6Tyt59ZLeka%2FIq8pD%2Bm9pVnIh9PLIsBlq8%2BuCr1rTXeO1G0yI%2FAF0tBuKg17C0HtHbdUGtalWmYJvmGxCIagJhTFxZn4ihHVzwp0JRTFsvk3LxSN1ykU%2BbI3%2FUJVkpGuXfOM8%2F1jHOMTAMkXd2w5sHUThnBbOiALy%2B6Oe1m1xfavdNMoT4smZ1jZ0n87TzF51H%2FXKXQjHfmuCwx3jPJQeE4yfNvcMZb8Wil4nYX6JOUmZ%2BE8NX1hZbfOGi8zF8Q3VjcRXgT5O25R58%2BSfPaSY8WexpfaBnDFNHwwjdgPHUceZKJ%2FZhvohYMRGNy8m21kVggK%2BKE%2FN2myfZwcrl83sFhYAcVrNFeMmigAwL4Wa6pdXbRY3K6miNG3b%2FCKIl5aQylgmEpJAf4htVcJ8fPh4igchkutAKUhrm9x9xSHkIk8jZWRSaRpInhhHOLpJk1vTRqqea0sM5U1rlGYyP80AxYlPqJSQtKpCklL8lLAMbncLAvJorV9UMQazrPgoaZxEv5pB0V4CLxmrXYCuIBabzMNMaw1xZI3lcfUT9a%2FxlgqmjRakVPAvTZqMXnbkATlDVFQgc4SAXuJP%2FU%2F792m814t%2F8wQ1%2FIYQZ85TExBB4ORMbhlqXA48PAD9jZE%2Fpar4oitCTuXbrJpScmZ7B50xwQXa%2FzHR7k%2FlbZFaxhU5hkvp56lFSts1OFiCn%2FREi%2BTkkeTbv3KNtlltaRGew5X2N%2Bmp69IQKKEvSuHFGXcmqyMu%2FKVZItiQf%2Bkn%2FjN9zg2VoIObXnHttmQLIaGRSE9dKyeH8vn67MuYxSXSadA3pNbfFZu81mpVWdVDL2isWLsWdzcswqDz8pMPosbffzWKYj5rbnxRxvKMpb1J1KWtSfMz1r0ZDdnZNbkJE2lJ0tlahPa5V052QqWtJjoLY5MzER%2BnW3RkZqLvCOVw3lnaiDyzkwi7%2BhNyJj1LEqjqEOb7Ob4lhursy47TpieOY%2BlLKVg2CJXV%2FnHmy1xDYihLrPIi9b2Vd1rTtV5vqoDTYMQQC2vlo9bsmwHliqSmrB3ZML%2B6yTYrCZUO06i9YTpuGYhwBeYke3wU%2B2b3K4p8XAluRzdmY3GefJS0xQ2oFZAT%2FI90ZbMxnOzFiX6%2BGIuXszFi7nYYk63IubieQZwQdOXIKqZi7JFvtszF1%2BNrWhqhmK2onmeIUbQNLRuqhViBGJo%2Fb8BDgeZncBeDEoMPGpNPCQG4DB9mchuM6P2ImG%2FZMW6bm8C8bxf9qeB%2FPoSU1IlFafXVNxQ8m36k6s48zyTs8ymERGed6cIZ5q7IyI7%2FaUmWk7gKCFKMlnBqIEqbGhq9h1Nca16aYyuSVIGdNOV8WN3evI8X0FzJjvMjWrFVPi45TGVz3iQvk7zycJgO29Tjem6pKrs9HrsPPPVzKaumqmWq2budtUueuxlesyQLM9zcj12noETs7G%2Fp1bmmyn6e%2BPNKlNi%2F%2FqYqS9J4j9chGgBA7ZARPoaQKgMaO%2BtgNI60JQkcZ1cB1rnGWUxmyZytV%2BD9jKuk32UqRsdOF7CICDBa1Z1wHCunbquk63lzuvdTqLorL7XRuqH5aym4RNLrZxhSwyf3CRxSR16SXyzXN%2BWs8gixF6yKJKUeypvxGVVb7VAaFpAwe6TqMXAw%2BzNp7Q4o2Dbyk0aaNEVosAor0dN0xTMV1vyruL0mrSfNf97Z%2BumuS1Wb%2Bsy7x13ia1znq3BeMrl%2BLuuJjD58%2BXM4wCReWQrgnanD88zwZLzw2HGUWvdeD7uPQuaM36ZY1%2BiogSl8xhS9igtCqO03qmX4eiuJP5%2FesUjrtEoesipVTCh4m0SYRSGcBKgB%2BjB62i5bkT7HoVgK%2FDp%2BrVZ98CHliTsZTnXunFC8Wc%2F4%2FVcNZ1Rns24J4cxNw4HBgAmwwL5D4gtYi30DHZkObrMiyx3PWa0Yp1mOo6k06dSGIVXLGUSB4u0PyDhCvr5IWyN7atsWW3Wna2sXenGVNoHcSnDstwZhzCI5vSi%2FPJBkZ35SEKvevfy6VM4%2B7FIdMlVjaYGc7UzWhosNsm3rRJlPRytfZhRFQc%2BLt147hMYlwd00OeupEqa2JvsdiAaud%2BvnGWBVlsRx5RYKrom%2BSZoG1%2Bi2LswX4lXK6CpA0DrhqNh1ZZA06W6TyI4u9J7fB2pM7PggTNUDQi5K8XEV2penAMavRFfNMdLIqlq7E2Sb1y8eUzyT0fz7xRIVmvU%2BRc12wbp6%2Feru7vh998NODa3%2F%2F4Wffzx6cOVqDaknzzt62Mjeh0GvRUYQP1F8zBfXPjAt%2BbaMLalQIgq48sbR8HWal6PIQmWgnYwGGTFJUVfqawE3P0D"></iframe>

La ejecución del anterior flujo de trabajo se realiza usando R. Para ello iremos ejecutando secuencialmente las líneas del siguiente bloque de código. También puedes descargar el código [aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2022-2023/geoinfo/shannon_sierra_nevada.R.zip).:

```R
# Este script calcula el índice Shannon de Sierra Nevada
#a una escala de 250 m usando la información existente en GBIF

## Establece directorio de trabajo
setwd("//cifs/bv2bogaf/Documents/shannon")

## Carga paquetes que necesitamos
install.packages("rgdal")
library(rgdal)

install.packages("sqldf")
library(sqldf)

## Importa la capa con las ocurrencias de GBIF
ocurrencias<-readOGR(dsn=".", layer="ocurrencias_sierra_nevada_23030", verbose = FALSE)

## Importa la capa con la malla de 250 m
grid250<-readOGR(dsn=".",layer="grid_250", verbose = FALSE)

## Unión espacial: asigna a cada punto el código de la cuadrícula en la que se encuentra.
ocurrencias$id_250 <- over(ocurrencias, grid250)$id

## Extraer la "tabla de atributos" para hacer los cálculos del índice de Shannon
bio<-ocurrencias@data

## Calcular el índice de Shannon

### Calcular el número de individuos por especie y por cuadrícula (num_ind_sp_cuad)
T_num_ind_sp_cuad<-sqldf("SELECT id_250, scientific,  count(scientific) num_ind_sp_cuad  FROM bio GROUP BY id_250, scientific")

### Calcular el número total de individuos por cuadrícula.
T_num_ind_cuad<-sqldf("SELECT id_250, sum(num_ind_sp_cuad) num_ind_cuad FROM T_num_ind_sp_cuad GROUP BY id_250")

### Fusionar las tablas anteriores para calcular Pi
T_num_ind_sp_cuad_mas_num_ind_cuad<-sqldf("SELECT id_250, scientific, num_ind_sp_cuad, num_ind_cuad FROM T_num_ind_sp_cuad LEFT JOIN T_num_ind_cuad USING(id_250)")

### Calcular pi por especie y por cuadrícula.
T_num_ind_sp_cuad_mas_num_ind_cuad<-sqldf("SELECT id_250, scientific, num_ind_sp_cuad, num_ind_cuad, (num_ind_sp_cuad*1.0/num_ind_cuad) pi FROM T_num_ind_sp_cuad_mas_num_ind_cuad")

### Calcular el log2 pi por especie y por cuadrícula (log = ln). Log2(pi)=log(pi)/log(2)
T_num_ind_sp_cuad_mas_num_ind_cuad<-sqldf("SELECT id_250, scientific, num_ind_sp_cuad, num_ind_cuad, pi, (log(pi)/log(2))*pi lnpi_pi FROM T_num_ind_sp_cuad_mas_num_ind_cuad")

### Calcular H por cuadrícula
T_Shannon<-sqldf("SELECT id_250, sum(lnpi_pi)*-1 H FROM T_num_ind_sp_cuad_mas_num_ind_cuad GROUP BY id_250")

## Fusionar la tabla que tiene el índice de Shannon con la malla de cuadrículas.
grid250<-merge(x = grid250, y = T_Shannon, by.x = "id", by.y = "id_250")

## Exportar la capa resultante a un shapefile.
writeOGR(grid250, dsn=".", layer="Shannon_250_sierra_nevada_R", driver="ESRI Shapefile", overwrite=TRUE )

```

La siguiente presentación muestra paso a paso el flujo de trabajo. También puedes verla [aquí](https://prezi.com/view/LlGhTybTfp4ILCRTR9Uh) y descargarla [aquí](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2022-2023/presentacion/2_Geoforest_shannon_Sierra_nevada.exe) para Windows y aquí para [Mac](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2022-2023/presentacion/2_Geoforest_shannon_Sierra_nevada.zip). Y [aquí](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2022-2023/presentacion/2_Geoforest_shannon_Sierra_nevada.pdf) la tienes en formato pdf.


<p><iframe src="https://prezi.com/view/LlGhTybTfp4ILCRTR9Uh/embed" width="1200" height="900"> </iframe></p>


## Resultados esperables
El siguiente mapa muestra el resultado obtenido en esta práctica. Se trata de un fichero de formas vectorial en el que se ha asignado el valor del índice Shannon a cada cuadrícula de la malla de 250 m. 


![shannon](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2022-2023/images/mapa_shannon.png)


En el mapa resultante se pueden identificar varios patrones de distribución espacial de la biodiversidad en Sierra Nevada. Durante la práctica reflexionamos sobre dichos patrones:

+ ¿Cómo cambia la diversidad al aumentar la altitud?

+ ¿A qué se puede deber dicho patrón?

+ ¿Crees que se repetiría el mismo patrón en otras montañas de la Tierra?

+ ¿hay algún patrón de cambio de diversidad en dirección este-oeste?

+ En caso afirmativo, ¿a qué puede deberse?

  



