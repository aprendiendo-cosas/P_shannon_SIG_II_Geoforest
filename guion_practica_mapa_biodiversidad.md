# Instrucciones para realizar la práctica denominada "Cuantificación y representación espacial de la diversidad biológica"


> + **_Versión_**: 2023-2024
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
  + Entrenar la habilidad de cuestionarse la utilidad de las variables ambientales para conseguir un objetivo concreto. 
  + Cuestionar la forma en la que obtenemos un mapa de distribución de una variable continua a partir de datos tomados de forma discreta. 
  
   
## Contextualización ecológica y estructura de la sesión

Para cuantificar la diversidad biológica se pueden utilizar muchos índices. En nuestro caso usaremos el denominado índice de Shannon-Wiever, que es uno de los más robustos y comunmente utilizados. Para su cálculo se necesita la siguiente información:

+ Delimitación espacial de la comunidad para la que queremos calcular el índice de diversidad.
+ Listado de especies existente en esa comunidad.
+ Abundancia de cada especie en dicha comunidad.

La siguiente presentación muestra los conceptos básicos necesarios para hacer la práctica. También puedes verla [aquí](https://prezi.com/view/07Hx3W5wMEZBtpdeeouO/) y descargarla [aquí](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2023-2024/presentacion/1_Geoforest_introduccion_biodiversidad.exe.zip) para Windows y [aquí](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2023-2024/presentacion/1_Geoforest_introduccion_biodiversidad.zip) para Mac. Y [aquí](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2023-2024/presentacion/1_Geoforest_introduccion_biodiversidad.pdf) la tienes en formato pdf.




<p><iframe src="https://prezi.com/view/07Hx3W5wMEZBtpdeeouO/embed" width="1200" height="900"> </iframe></p>


Para satisfacer los objetivos planteados, procederemos de la siguiente forma:

1. En primer lugar aprenderemos la mecánica del cálculo del mapa de diversidad a una escala de 250 m en el espacio protegido de Sierra Nevada (Sur de España). Es decir, asumiremos que una comunidad ecológica es una entidad de forma cuadrangular con un lado de 250 m. Esto no es así en la realidad, pero es la aproximación más fácil que tenemos a nuestro alcance. Una vez obtenido este mapa, trataremos de estudiar los patrones de cambio espacial de dicha diversidad. También identificaremos los factores abióticos que explican dichos patrones espaciales.
2. Las técnicas de análisis aprendidas en el primer punto deberán ser aplicadas a la actividad entregable de esta asignatura. Es decir, será necesario incluir un mapa de biodiversidad como elemento para realizar la estratificación del territorio. Pero deberá cambiarse el elemento geográfico utilizado para delimitar las comunidades ecológicas. En lugar de usar una malla de 250 m se usarán los contornos del mapa de vegetación a escala de detalle de Andalucía. Esto se detallará en la descripción del ejercicio (que se mostrará en un guión específico).


## Obtención de un mapa de biodiversidad: Metodología y flujo de trabajo

Como se puede observar en la presentación anterior, para calcular la diversidad de una comunidad, necesitamos dos fuentes de información:
+ Información de distribución de especies en la zona de estudio (Sierra Nevada). Es el primer paso fundamental porque necesitamos esta información para calcular el índice de Shannon. Para conseguir datos de presencia de especies en Sierra Nevada usaremos una infraestructura digital denominada [GBIF](https://www.gbif.org/) (Global Biodiversity Information Facility). Se trata de un portal desde el que se tiene acceso a millones de datos de presencia de especies procedentes de colecciones biológicas (herbarios, colecciones animales, etc.) de todo el planeta. Esta iniciativa está promovida y mantenida por multitud de países que han puesto en común toda la información de la que disponen para conocer mejor la distribución de la biodiversidad en la Tierra. Accederemos a este portal y descargaremos toda la información de presencia de especies en Sierra Nevada. Esto nos dará una idea bastante aproximada de cómo se distribuye la diversida en esta zona. En nuestro caso, GBIF aporta una enorme cantidad de registros de presencia de especies en Sierra Nevada. Durante la práctica visitamos el portal de GBIF y simulamos la descarga. Como este proceso puede tardar unas horas, utilizamos datos que fueron descargados anteriormente por el profesor. Dichos datos de presencia de especies tienen el siguiente "aspecto" cuando son visualizados en QGIS. [Aquí](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2023-2024/geoinfo/csv_gbif_sierra_nevada.zip) puedes descargar la capa con los datos de presencia de especies de Sierra Nevada. Como ves más abajo, son unos cuantos miles de puntos...

![puntos](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2023-2024/images/puntos.png)


+ Distribución de las comunidades ecológicas que conforman Sierra Nevada. Este paso es el más complejo conceptualmente, ya que las comunidades no tienen un límite espacial preciso. Es decir, están conectadas entre sí y no es fácil delimitar donde empieza una y acaba otra. En este caso usaremos una definición artificial y arbitraria de comunidad: un cuadrado de 250 m de lado. En el ejercicio que tendrás que hacer para evaluar tu aprendizaje, habrá disponible una fuente de información menos arbitraria: los polígonos de un mapa de vegetación. 

A partir de estas dos fuentes de datos obtendremos el índice de Shannon para cada una de las comunidades de Sierra Nevada. Es decir, usaremos los datos de presencia de cada especie que hay en cada una de las comunidades para calcular su índice de Shannon. En la siguiente figura puedes ver la distribución de presencias de especies en unas cuantas comunidades.

![puntos_comunidades](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2023-2024/images/grid.png)

Para ello seguiremos los pasos que se muestran en el siguiente flujo de trabajo (se ve un poco pequeño, pero si vas a la parte de abajo encontrarás una herramienta lupa para aumentar y otra para desplazarte). También puedes descargar el flujo de trabajo [aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2023-2024/presentacion/sierra_nevada_shannon_R.drawio.zip) (se abre con [esta](https://www.diagrams.net/) aplicación).



<iframe frameborder="0" style="width:100%;height:3090px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1&title=sierra_nevada_shannon_QGIS_R.drawio#R7V3rc9s2Ev9rNNPejDV8Pz7Gip32Jr1L4ra59IsGJiGJDUUoJGXL%2FesPAAm%2BAFG0xJcleTy2CFIguLu%2F3cUCu5yos%2FXuQwg2q9%2BQC%2F2JIrm7ifp%2Boig3sqTgf6TlJWkxlLRhGXpu0iTlDQ%2FePzBplFnr1nNhlLYlTTFCfuxtyo0OCgLoxKU2EIbouXzZAvluqWEDlrA0DNLw4AAfcpd99dx4lbRaipm3%2FwK95YrdWTbs5MwjcL4vQ7QN0vtNFPVev9fu0w7XgPWV3jdaARc9F5rUu4k6CxGKk0%2Fr3Qz6hLZlst3vOZuNO4RB3OQLyj3Uvn%2FaWDfOnWp9%2BfD0%2BMfm%2FkZOmRXFL4wg0MX0SQ9RGK%2FQEgXAv8tbb%2BlDQ9KthI%2Fyaz4itMGNMm78G8bxS8pssI0RblrFaz89yw89fZoIbUMnHYcyX1j%2B84sR%2F%2FvH578s8%2BH225d%2FbvRUQkC4hHHNdSn3yLMUbpAS5gNEaxiHL%2FiCEPog9p7KsgBSkVpm1%2BVkxR9Syu6hcs2on4C%2FhUxYKlQH0SaR7oW3I6S93cDQw3eHIW7Dt8BwgJ%2FypiI1ge8tA%2FzZwdSk5zJJI%2BxxQbTKeBVtgOMFy98pn1Tc4K0pPNj%2F9956iZ%2FQ9x7xX%2BAQysxdL8QjQ4QM98%2FwcR7B8AmG0%2Bhpib%2B3QEGcstmkkhFjciIymhvZIndc4JH%2FmQ6UfP7lkAjgvmO4q2UaO6vJ6XdS1aMoKaGfcyCrKalXBQxrUgt8FqJJHQJNmILhy%2F%2FI96c6O%2FyWdkcP3u9KRy%2Fp0fEoNJuiUBkVDE0Ohu9h5OCHALj1w%2B2v9xz3whVaP27xOG6fV14MHzB8yJlnbArLPNiPg85BIJklEKiyzYGACXzrIBBS2Tis7Yjd3PB0ak6PzB8Aj6xPqZ5Oim2U6KTJBkcn7LzwhJKNrijFdFMdpbAu35CPmCixB%2Fwv5JGDJVUcBfETSWeZQFQMPd%2BfIR8RkxKggPQRUx1DTvpwEacfH1Eco3V6EKaUoMoJ82HhU9Oy8lwXBsSkxCH6Dlm32AmS6E8T5taLz2EIpJy0JI6RsipN7eKP2SMAVPXK1lPYys6qZes%2BNjZrvDnZy%2BaUXYd4G2GLysyIlPA6Bl5AfUCZHvs%2B2ERezntn5fnuR%2FCCtjG7DTs6YJM64xsjA7NHCq9mZWuqFn9kgdZVrK74ZnULzyqL3BBtfmeeEmnYII846ndPmPJRWximnVJS6bf4Fwv9jLiDOn6aGT6W82P8Sy4P4xkKMMqxfJE%2BIIjiZxjFRwtKBofDgvJKUejMH9RsThIeHA8%2FprfwnP%2BANexUbYu07sliUMC8dTwrrWNYadqvY13aWU7DV%2FcGfAyjAMTwlkyhIk4esnGeMHOXOBFxoYNny3h6Fiy9eOtehaSpYTD5iYlhtSkzTXrrQ2bkvTKD6XwVmVfNbk1OZsxXmogDeqZBb33ITMdTwatT0nAyyXj%2FWh9F6chH0fnJ5Dv80CD0wHQ6vVBFkqHldAelhm9HOCiV3vpQHBonH2TGNdOuotGyW3K0pDTprQ9J4VehzKl9FZO2XZHjNUqD3vqQkwbx%2B6sr0oMroqnHuSKdrWLzAc%2F7rXPJbkjz2OjZx0n4oCp1Qy7Wvrw6bH4x0RE%2B6Ir1yky%2BCso1JlImjcHHXq%2BOyBCOiKGNyxEx%2BADrJy%2FYRheqQjKcXN0Qtn%2Bn6IbIF%2ByGvEI0LswNMfi4KtZyM34D51VQLt0N4SOsVzdkCDfE4nd3D7o0Y%2FAB1c9bGDrb6HJDIhlYriszBh9HVclMV7%2BKxnVlpkwZPrBKYmftmplzFpSLWZsxrntXx%2BGLyBIvccPGRPiw6hcUXfDijHHdxJrt4ecDqSQr4nKjItetq%2FskhY%2BsEu1rXQXlGhURp%2FaWPBHDj1PSl6TF%2BLFF7MRNRJnyDl%2Bgb3b5OfxpSf5%2FCmEEA8cjKblko7QESWK8ByPyMcB%2FtgE59Q%2Bi%2FyLoQ8fBfAUuYLfHj5OMIOmQE91yvvWBvN79aXBUwNJe5aMl7Pj0qlc6HiwNq%2F2cd4Oj8GgqSIjGm9KhlLsuui6NBA%2BQul4z6gLaJFm2LEW5USTJkFXJ0mTNkjV16kRPp4n8cKnsKouoZeuOgpRPWeBTqZ0VdDCHEO5uCzrUCPtBULCkzPZQkX71E5kCFs2ook%2BVsjRYciUjNBlt%2Bs3TLFwNTQqQ%2B3VNpp4gJERmZipiZucxzC1O0uKxhhACN8HlvkvxAL39Bmv8RShUu1yEwlR45LKdLkXgsrb2gcu7rH0Ad%2BfFBdzio2%2BFMzlqycHpoGVgPIja3kDLUvQZYrUKYpNH6gyxGeXOXFs35bti96atjaq2tm17KhV%2BKu5nx7qbD5N6gYNCrL6p9k4faTJTJ%2B%2FegwYaPIrnIJpHi471dVESe9XeFUtr86VxDDnjcEmB61O9KxXOL5T1qsI1yyoocWlqm3qtIicHhQptr8B4XejhMMjbxvhp85RhKqD1a3ftpqxpnTe1%2BtfOfsuFc2RJUep0cddWeWAcNxeJ%2Fi05k5DD0QipP1EqC4%2BsD2nIGYEKljyEmxC9kOBo2MxyxyEIogUK15dhvWXJGIP5VoYJnaSwlydF011vuI%2BHL0PlYUtg9AVfU56qMofWDMwmJoZs5b%2B9WgIWg75agv0SctgSyONy%2BPhdbk4I6SxrDXw%2FW8ZRdGndTF2vwXc4p8XDz1Jd60bFO8Mml1PXliJU14aWNbfPSH7OXAxyVsheWP%2FFXIY%2BWoZgPSlXrS6dK9auPsQpUgE7ZZWAc63YTMsuMcESxCtNlWcAm960T31%2B%2B05O%2FTm%2BzblzgNisYVmgDTN17X%2Btp6nTwvTSSCyNyu9iKkNkrqgSu%2BiMgGLqU5bWlpkMgy8NITP89AIW9TqpP%2BihHXbltHEBjN%2F8RdyweeK6nReqdBZfZZBSWNXG4qRZUE66O0S9mRXLARClNUVU6%2FPs03jKpw6yYBRa0zkS3dKWryvVz4zOdf1JN9WpWQliqezNRIMGsVR%2Bi%2FR5%2BoSNow%2FDvVipbtwik0Xhcm5Wq4ISTZCGYhpTS7SbvLN50zC7Lt6G4RK9KUlIxNbXd07DFZ%2BRCMhuiVsZuB6xW44PnkhYb4PhQWrRNjFg8Me5mi%2BFM1%2BawQOzf%2FOl8VVg%2BzRfcglkOeb2wKzfVXztjYZBjEH22%2FevOkX8%2Bao%2B%2BH%2B6i%2FCvlxf03f5q3eo7LXtFw0j4o%2FFhqvN2SbSprZaVn66PwCsZZjrdJUyE0q8IpsbiCwebGteOuwCTux2eHMOQPsyjL3Ap6EIiiEPvEROeJITRBuRsw5AtUxEakjVHhOFDJ9gOIjNs6Iv641wUEE1dEIPpIqQv%2F%2Blvb34bSORWVCy2qFSEoTYVuCB5a%2Bs4ZIW2L3x2UAvJwy5I6xu5T8MuP%2Bt%2B9PgVymOzzix2mHaldIMXTSpnK8i2yq%2BqMPHtJdtMP79sM7H8CPY2Cy9sf9fjaXLPb5GYAd%2FZ%2BtTSBJOZMrklic1e4HpPnrtF4uQwsCayHzxG5N8Gke%2Fij0QOMTnpobMFbpqdQHpvYLkePn8U26ukLdqAoCRYLO3aSTKbyajD5SP4CROcVIbAf4WffiYfSbcSzeVegLXnvyRfX6MARRTepUvydG9JlO69%2B4A1weo35EJMfR3zAv%2BZhQhfkx0x3uiUO7jlPflMhqQTbuiYpYeulbNrmbwe1Y2Sd5OIQHYmc130zHnRE%2FdEL3kseWPJa9GZ36Lnnoue%2Bi46817YrRMmZrdmHghuKOpYcp5qWdJO0U5aZHqY6VrSZNKmwpMlGrQJ7bJTGdlySOpE0eZXqmQ7KOvnJT9xoxs5B1LFm51M3BJ2MlXBe85SMqZnloVRVFlLDzP%2BFhvLUpdex4lnhrEEUuN3CzWj7BYqMlv6LJg5Wxa5hXlr%2B1EMfp%2FGiE1dZ5GpWqt32DyOa0on2KBTsFOH64GYIgPx%2BzzYrufYos6jzZzYxWbTshNczy4waJbToxXR6qYpyI%2FuztU8vyiiWCYFlQ3EFw62F6d23O27mpfmYQps%2BNXFvLqYVxezxcijVF79HIeLqb%2BZDXUnmLem0f%2BxuYqimvrtuYpv1U9U5fJK2vB%2BIktWOns%2FURCKF1443Ead2nEXgPRHQHfoUB%2BBrIgJnDvsSTxR589OVtHIbRzsKyLyH63pTp93Af%2B9n4irkqy60cy%2Bihf58ylu5IjNm1UxbyorsDBoBEUZApnHI6zxfo7h9tvUjltgqvbOeZpYKw4ZXKRjvgZRA5PW0F0cmaXTy2UmsOfLWzpZs0Sg6s7YnV8GYC3CDkNxXEERNm5xUOSTN0nW0Hy0VMjBRdgiQxqDLRp2n2l%2FwGk63dLGNd3S9k%2B3rjbsBBtWieqbgkoOvduwN5OYewIMG0%2FWWq98ehoM%2Bcnaw3adGq9%2FfUzNlsRbLrAM4RIELpmf0fh99YIWw%2FlvyPZZ6hhs3yCbtk4AT9PNV8Ptq68ddw827GEFggAF52Sq7MomEJu9v6OYn6T1aacGic7vpWXnhdkMSZ2asqZYevK3XH5AlVR1qhn56UpaxJ7CbOLbsD7IX7NyG6vCz%2FbKN9bqEAFoc9v0rpRZCAoWMIMdyaDJEmiEqCytdPP3qIQ4k5wAcidqMwPXcyD%2FJRrozJXBgVtwg15DTNu3ZmT1imQqtsCp7d%2FInkcefi9apgb%2BslyB%2F6v0iqnndSX1SsfVSv9d6xV%2Be8wYk%2Bx6ymTQDaOagJxr%2BmJVQUGFqM4MvPmmdnjuZcNhN7n1ihjHeRCKahc9CLY81H5pVzEV%2BHeh3%2B2yt%2BWAxI5u4MLzBXaWs5zPIUbcfz98eXPGs1LbM9eLPRnPWgkVb7ZIwwGJl0MU6DzyYBiCeQCfgAum0WrTiA0DqtguOKnoU7k8Z1IVSxDe080p26PRi1rV3tjr9kRrTeIL9bb16Gl0VjjQvIu8ZZDpM4e%2BcjJ%2FERibUTh0NqO63pJMNdK9FSQ8B2j4DmZTjx%2Fb5PWWMZ2DyA3UYhTP%2F8YKvGOtOFQZe8uuvkMImzxBIYG82EophbnDKirnl5ZZi8DDpQTGVbdS432PQmHYXVpLfBzmqr3yyQqHFpMlKxddflOIls7KbujDbKEYW7p%2FbRb%2FQVM4too2fG1yzKSkvEaMXFqJw6d%2FaYCNvql558BNjLITia0L6OcIhk9eslglB2P25lXL4up62YKtf%2F3X1Di%2F7Ra1ODi8u31cL2vWB1mD74HO7b%2F%2B9zQ686sLb7MOSVXNKJJAzbRUimSSpiEVwj95ApJ6938%3D"></iframe>

La ejecución del anterior flujo de trabajo se realiza usando R. Para ello iremos ejecutando secuencialmente las líneas del siguiente bloque de código. También puedes descargar el código [aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2023-2024/geoinfo/shannon_sierra_nevada.R.zip).:

```R
# Este script genera un mapa del índice de Shannon en cuadrículas de 250x250 m a partir de los daots de presencias de especies existentes en GBIF.

# 1. Establece directorio de trabajo
setwd("/Users/fjbonet/Library/CloudStorage/OneDrive-UniversidaddeCórdoba/4_docencia/SIG_II_geoforest_UCO/repos_actos_docentes/P_shannon_SIG_II_Geoforest/preparacion")

# 2. Instalar y cargar los paquetes necesarios
install.packages("sf")
library(sf)

install.packages("sqldf")
library(sqldf)

# 3. Importamos el archivo csv de GBIF con sus atributos geográficos
presencias <- read.csv("0118822-200613084148143.csv", header = TRUE, sep ="\t", dec = ".")

# 4. Convertimos la tabla importada a un objeto geográfico tipo sf
presencias_geo <- st_as_sf(presencias, coords = c("decimalLongitude", "decimalLatitude"), crs = 4326)

# 5. Reproyectamos la capa creada al sistema de coordenadas 23030 (UTM)
presencias_geo_23030 <- st_transform(presencias_geo, crs = 23030)

# 6. Creamos una malla de 250 m con la extensión y sistema de coordenadas de la capa de presencias
grid_250m <- st_make_grid(presencias_geo_23030, cellsize = c(250, 250))

# 7. Transformamos la malla obtenida (tipo sfc) a tipo espacial sf
grid_250m_sf <-st_sf(geometry = grid_250m)

# 8. Añadimos un campo llamado id_250 a la malla. Le incluimos valores secuenciales desde 1.
grid_250m_sf$id_250 <- seq(1, 67304, by = 1)

# 9. Asignamos a cada punto de presencia el código del cuadrado de la malla en el que está. Unión espacial.
presencias_x_grid <- st_join(presencias_geo_23030,left = FALSE, grid_250m_sf)

# 10. Extraemos la tabla de atributos de la capa de puntos creada y borramos todos los campos menos los dos que nos interesan. 
bio <- as.data.frame(presencias_x_grid)
bio <- bio[c('id_250', 'scientificName')]

# 11. Calcular el número de individuos por especie y por cuadrícula (num_ind_sp_cuad)
T_num_ind_sp_cuad<-sqldf("SELECT id_250, scientificName,  count(scientificName) num_ind_sp_cuad  FROM bio GROUP BY id_250, scientificName")

# 12. Calcular el número total de individuos por cuadrícula.
T_num_ind_cuad<-sqldf("SELECT id_250, sum(num_ind_sp_cuad) num_ind_cuad FROM T_num_ind_sp_cuad GROUP BY id_250")

# 13. Fusionar las tablas anteriores para calcular Pi
T_num_ind_sp_cuad_mas_num_ind_cuad<-sqldf("SELECT id_250, scientificName, num_ind_sp_cuad, num_ind_cuad FROM T_num_ind_sp_cuad LEFT JOIN T_num_ind_cuad USING(id_250)")

# 14. Calcular pi por especie y por cuadrícula.
T_num_ind_sp_cuad_mas_num_ind_cuad<-sqldf("SELECT id_250, scientificName, num_ind_sp_cuad, num_ind_cuad, (num_ind_sp_cuad*1.0/num_ind_cuad) pi FROM T_num_ind_sp_cuad_mas_num_ind_cuad")

# 15. Calcular el log2 pi por especie y por cuadrícula (log = ln). Log2(pi)=log(pi)/log(2)
T_num_ind_sp_cuad_mas_num_ind_cuad<-sqldf("SELECT id_250, scientificName, num_ind_sp_cuad, num_ind_cuad, pi, (log(pi)/log(2))*pi lnpi_pi FROM T_num_ind_sp_cuad_mas_num_ind_cuad")

# 16. Calcular H por cuadrícula
T_Shannon<-sqldf("SELECT id_250, sum(lnpi_pi)*-1 H FROM T_num_ind_sp_cuad_mas_num_ind_cuad GROUP BY id_250")

# 17. Fusionar la tabla que tiene el índice de Shannon con la malla de cuadrículas.
grid_250m_sf<-merge(x = grid_250m_sf, y = T_Shannon, by.x = "id_250", by.y = "id_250")

# 18. Exportamos la capa de la malla obtenida a un fichero de formas para visualizarlo en QGIS.
st_write(grid_250m_sf, "Shannon_250_sierra_nevada.shp", append=FALSE)


```

## Resultados esperables
El siguiente mapa muestra el resultado obtenido en esta práctica. Se trata de un fichero de formas vectorial en el que se ha asignado el valor del índice Shannon a cada cuadrícula de la malla de 250 m. 


![shannon](https://github.com/aprendiendo-cosas/P_shannon_SIG_II_Geoforest/raw/2023-2024/images/mapa_shannon.png)


En el mapa resultante se pueden identificar varios patrones de distribución espacial de la biodiversidad en Sierra Nevada. Durante la práctica reflexionamos sobre dichos patrones:

+ ¿Cómo cambia la diversidad al aumentar la altitud?

+ ¿A qué se puede deber dicho patrón?

+ ¿Crees que se repetiría el mismo patrón en otras montañas de la Tierra?

+ ¿hay algún patrón de cambio de diversidad en dirección este-oeste?

+ En caso afirmativo, ¿a qué puede deberse?

## Vídeo de la sesión



El siguiente vídeo muestra la grabación de la sesión del día 23 de noviembre. Lamentablemente está incompleta. El vídeo no se grabó correctamente a partir del minuto 2:44:00

<iframe width="560" height="515" src="https://www.youtube.com/embed/rJvTOStDAXw?si=vbKkzQ3TjqQv0ECx" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Además, en el siguiente vídeo (que sí está completo) podéis ver cómo comentamos el día 24 los resultados obtenidos. Evaluamos patrones de distribución espacial de la diversidad y tratamos de identificar las variables que explican dichos patrones.



<iframe width="560" height="515" src="https://www.youtube.com/embed/ttcaQypt6e4?si=2ahiiO13fsfZKphh" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
