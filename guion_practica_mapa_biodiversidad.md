# Instrucciones para realizar la práctica denominada "Cuantificación y representación espacial de la diversidad biológica"


> + **_Versión_**: 2021-2022
> + **_Asignatura_** : SIG II (Máster GEOFOREST). 
> + **_Autor_**: Curro Bonet-García (fjbonet@uco.es)
> + **_Duración_**: 3,5 horas.



## Objetivos

Esta práctica tiene los siguientes objetivos:
+ Disciplinares:
  + Reconocer el concepto de biodiversidad ya estudiado en en otras ocasiones.
  + Aprender un método para cuantificar la diversidad biológica. Índice de Shannon.
  + Aprender a generar mapas de diversidad biológica. Mapas de distribución del índice de Shannon.
  + Reconocer patrones de distribución de la diversidad en un territorio concreto (Sierra Nevada).
  + Identificar las causas de los patrones anteriores.
  + Reconocer cómo la diversidad biológica cambia su significado al hacerlo la escala espacial. 
  
+ Instrumentales:

  + Afianzar nuestro conocimiento de SIG.
  + Mejorar nuestro conocimiento de R.
  + Aprender algunos conceptos básicos de las bases de datos relacionales.  
  
   


## Contextualización ecológica

Para cuantificar la diversidad biológica se pueden utilizar muchos índices. En nuestro caso usaremos el denominado índice de Shannon-Wiever, que es uno de los más robustos y comunmente utilizados. Para su cálculo se necesita la siguiente información:

+ Delimitación espacial de la comunidad para la que queremos calcular el índice de diversidad.
+ Listado de especies existente en esa comunidad.
+ Abundancia de cada especie en dicha comunidad.

La siguiente presentación muestra los conceptos básicos necesarios para hacer la práctica. También puedes verla [aquí](https://prezi.com/view/07Hx3W5wMEZBtpdeeouO/) y descargarla [aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/presentacion/1_mapa_biodiv_shannon.exe) para Windows y [aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/presentacion/1_mapa_biodiv_shannon.zip) para Mac. Y [aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/presentacion/1_mapa_biodiv_shannon.pdf) la tienes en formato pdf.




<p><iframe src="https://prezi.com/view/07Hx3W5wMEZBtpdeeouO/embed" width="1200" height="900"> </iframe></p>



## Metodología y flujo de trabajo

Como se puede observar en la presentación anterior, para calcular la diversidad de una comunidad, necesitamos dos fuentes de información:
+ Información de distribución de especies en la zona de estudio (Sierra Nevada). Es el primer paso fundamental porque necesitamos esta información para calcular el índice de Shannon. Para conseguir datos de presencia de especies en Sierra Nevada usaremos una infraestructura digital denominada [GBIF](https://www.gbif.org/) (Global Biodiversity Information Facility). Se trata de un portal desde el que se tiene acceso a millones de datos de presencia de especies procedentes de colecciones biológicas (herbarios, colecciones animales, etc.) de todo el planeta. Esta iniciativa está promovida y mantenida por multitud de países que han puesto en común toda la información de la que disponen para conocer mejor la distribución de la biodiversidad en la Tierra. Accederemos a este portal y descargaremos toda la información de presencia de especies en Sierra Nevada. Esto nos dará una idea bastante aproximada de cómo se distribuye la diversida en esta zona. En nuestro caso, GBIF aporta una enorme cantidad de registros de presencia de especies en Sierra Nevada. Durante la práctica visitamos el portal de GBIF y simulamos la descarga. Como este proceso puede tardar unas horas, utilizamos datos que fueron descargados anteriormente por el profesor. Dichos datos de presencia de especies tienen el siguiente "aspecto" cuando son visualizados en QGIS. [Aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/geoinfo/csv_gbif_sierra_nevada.zip) puedes descargar la capa con los datos de presencia de especies de Sierra Nevada. Como ves más abajo, son unos cuantos miles de puntos...

![puntos](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/imagenes/puntos.png)



+ Distribución de las comunidades ecológicas que conforman Sierra Nevada. Este paso es el más complejo conceptualmente, ya que las comunidades no tienen un límite espacial preciso. Es decir, están conectadas entre sí y no es fácil delimitar donde empieza una y acaba otra. Usaremos un mapa de vegetación para delimitar las comunidades de Sierra Nevada. Asumiremos que cada polígono de dicho mapa es una comunidad ecológica. [Aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/geoinfo/vegetacion_snevada_23030.zip) puedes descargar el mapa de comunidades que usaremos en esta práctica. El enlace anterior contiene un fichero de formas con la delimitación de los polígonos del mapa de vegetación a escala 1:10.000. La siguiente figura muestra la delimitación de estas comunidades en Sierra Nevada. Aunque el mapa no tiene escala, podrás reconocer el contorno del espacio protegido de Sierra Nevada.

![comunidades](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/imagenes/comunidades.png)



A partir de estas dos fuentes de datos obtendremos el índice de Shannon para cada una de las comunidades de Sierra Nevada. Es decir, usaremos los datos de presencia de cada especie que hay en cada una de las comunidades para calcular su índice de Shannon. En la siguiente figura puedes ver la distribución de ocurrencias de especies en unas cuantas comunidades.

![puntos_comunidades](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/imagenes/puntos_sobre_comunidades.png)



Para ello seguiremos los pasos que se muestran en el siguiente flujo de trabajo (se ve un poco pequeño, pero si vas a la parte de abajo encontrarás una herramienta lupa para aumentar y otra para desplazarte). También puedes descargar el flujo de trabajo [aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/presentacion/sierra_nevada_shannon_QGIS_R.drawio.zip) (se abre con [esta](https://www.diagrams.net/) aplicación).

<iframe frameborder="0" style="width:100%;height:2815px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&layers=1&nav=1&title=sierra_nevada_shannon_QGIS_R.drawio#R7V3rc%2BK2Fv9rmGnvTBi%2FbT4m5NHt3d5ul73dbr9khC1AXWNT2yShf30lWfJLApxgYxPobIkt%2BXl%2BOk%2BdIw%2F08fLlIQKrxS%2BhB%2F2BpngvA%2F12oGmmgn%2FI%2Fibd1yyNtcwj5KVthYYJ%2BgemjSpvXSMPxqwtbUrC0E%2FQqtzohkEA3aTUBqIofC4fNgt9r9SwAnNYegzSMHGBD4XDviIvWaStjmbn7T9BNF%2FwO6vWKO2ZAvf7PArXAbvfQNPvzXvjnl1wCfi12H3jBfDC50KTfjfQx1EYJunW8mUMfULaMtnut%2FRmzx3BIKlzwld94v%2FuzaI%2FN5vw%2B%2Birc2O%2BGFcWe80n4K8hfw%2F6tMmGU4i%2BIyRXUQf6zfMCJXCyAi7pfcZDArctkqXPumdhkDCQHbwb4gNRQsaGoZBe5Pvj0A8jemXdA9CZubg9TqLwOyz0WK4DpzPcI74le%2FEnGCXwpdDE3voBhkuYRBt8CO9VbSM9h43RK7b7nONtqIwQiwLWpq0NTTbS2CibZ1fPKY03GLFfQ3irXcJXKD2bQcuVUtqzR1NFEaFqhPCmXSa8OnJ0gfamIqG9OrKUw0mvPc4c%2F3ljJT%2F%2F%2Fdufjj25%2Bfb5H45%2BgdDQwyKB7YZRsgjnYQD8u7z1JoeCkio75mMYrhgAf8Ek2TAEwDoJy%2FBgKkabP8j5eEix3W%2FFvtsXdvF0b8P2CrDau1CJw3Xkwh1vzQZyAqI5THYcx7AgJNmJcQR9kKCnshRtHCtzP5eAeJXqhRl6IQjdrGCE8N0hGeD4FliRwE95UxEU4KN5gLddTE3al8loQnoPxIsM8phwRzD%2FQuHWcQNaUsXC%2F96i5Ry%2FoY%2Bm%2BBe4hDKPHorwk4WEDPfPcPoYwwgzzzB%2Bmr8C2Fewm%2BaoQ6Ms6mxLlHW6JrKb0Raz2WYX3FYRhm%2FnGrsm1xj9YhtRq9%2FC2MUvAXBr6K4jTAkX4dtqygTBKCLN%2F4NPwAOiElqEy%2Bk6fpUCamxAW%2BaQK0o2oC3LFAa0pQ9NSxzTfOg3T90auptYhqv6NMjsWzDlV1D20Ea3q8xu2CKzq9z8LCnX1nQrly27SIOF7IpsYrokCPifyVsHc8r4heEkG21lGlUNyiAMyDUSKiNIpw9nCduchkkSLtlOxChBhQuGYuZTmb9AngcDmY2k0P%2Bkg3r3ANk%2F1Bl0jiKOaglwrYlpXb%2Fg9ircXsog9QRGo4Y7x2FkcOzDLsa6j8t1JcUyASig1pVK930frGKUY%2BsukO99BJtwnfDb8L39SqIhXNQyLlwsFQWjIhOMmtMWMk67DFYFwYvC1RdutZCGVYiIkXv3hEkdN8WF9KKUVOYN%2FocpOib%2BjYnfZoz31Xwf%2FyOHR8k4DDCf4hFErgFBnDzDOKk%2FFLIRvn8o7AO7NevLGAlY3xEnBcFWZapMJB6M8F5LevdofxVKXAkdBSQeuCyAhC3zC0DbJKouBm5045h4qSJeYTC%2FALbVNLFFwI7KYC27AheNt82Z4JDuVYBaW9CL3oTaKPY9ZtRs2B%2Bu%2BlqDxxDgIQbyWAyMXzB6pfZrDTIxEG4PRxe8DlV%2BreFVI0R4UX5tKD9D5NTjen%2BmGIM5H%2BVXP1DTmVkqBmKo8jsfYfrqYFrnrp8YT8E8Nr5wVW99P0sMrlzU31HUn2S%2B%2F7jqzxLjNM1i32NGzYZ9f9WfJUZldPWc1N8rMOqJ%2BrPEaAq%2B%2FVi%2FINZb9ScGWC7q7yjqzxGzg44b%2BrTEQM35qD%2BjNlxdxWUkadc68SXELMULRj0JfUpKFIi%2FfuGq3gY%2FrUuuS0fqT1VE6I%2Fs%2FomxmvMxVPuf9WKLgRmSjHhG7t%2FJJb7YYkCFyBrnglhf3T9bjLEMNMvn%2Ba8l1Ky%2F1yHvuIopca7xAebqJe%2FDW3Py99escAMf4UH8A9O0QlLHgSHSlHVAuv4J6Z8Y%2BtB1Ed4hZR3p%2FfH7pI%2BQXlEYQ%2BXKmz0VH9vzrSnS7KqSQtWGk3z3KTue%2Fds40Dzd%2B8ilhC8oKVQS4r1v7GJkO68jJDu8jLCB8sMDC6nqVlLZTBX1pJLK6aRa9Phkd7Rekd0Wnb4PS2JSgwi3jie%2Fk5vi%2F397%2BDARhViXJWu2UJalS8qyjGNWhdiirXAaFc8Hjn2trsjpV%2FGmY120Sl2IR3XFm9kriG3RSx6DVWbWrdZBEhKjDhvm%2BNenhbrlsl163MPNh%2FtdbgDwfeiH8wgsB%2BWy%2BFJfsTh%2Bn8AkJfYMuRoWYA2IXyNaxYpXrW7Fa2sFr1xvFpH8PEmN%2BK8PE4n5gF83KVNVWIaAEAW5wL9mHUvsgqVcDrGLUHDTyjEpEnYijB3nALUAg64LqwzojgiDrO5Raw2FTjRcY2LMqbs4h9OZppIvYtMF1Zsls%2Fy9%2BqUtHHFO8e4lM4aJ1pj89KnvVrDatRXsiC5FJqnvPk0e8B%2Bsv3TRpX%2BHAluVCGynJYEt5TBVnBR4Zy6J%2FLX5Cnd7JZDaK0HPn1vujpcs0zTOOI3yEGPagnhDBIH368Pn7UdOeYNqFsKWU%2BEw4UR8FNoe2exUHCp8ITm%2BEtpIjF3K1rDhbY0jqnUSuqww0lt8zrczn1WX%2BdTOQpDyx%2BlkCa2CrDSssrQcKqr9OolJOwt%2B5oFIqlZdMdpZVHPnc0vFaFWqLdOAwBPEj96oVHXeiVQ1zPLSYJmFV5Sp0mU925KpYkXKu5epkhjrKchUXlHaLVQFEetYRRGrDEfZ%2FhYJKxWpHHy1CH02EDoDn6%2B10hz49NTrKAKbwgHMucqv%2FIk0FCSGyZ3LbD1aQysOpTpnmGwljq2nGM5o9yl4I33yLRew%2BFIn%2BVPqZUqkyLDzdj6%2BZWx5luxaKXjCtShXZcgcIBPP1NGTTEzIeahx1jjMQhEnJq5jNA%2BySJNoJ7g0vaTgBJK38aX2BFgSqyCYxuQPfg42jeGTU9xwuQ6QBzzxTBjwg%2F5ep1kvyWCsD67VYQ3DiGQy1bCKCEXfhVWkaxWJpevWUKyKcFTRMHLaGlVa1x7MIULgyAaVUlNwaEavBAf%2FXsJJQvx2uDgK%2B%2BGy%2BgWXWKF295JEgMhKhSSCAlH0UVkNkghN1%2BnsNG0oT0uTiWXSuIIRVRnpBDZ%2BIMn1BBksyG7ylDJxKxPUvRLBlc8emJYY7bMNLpWLIjhvbR5yMcf7LDi0bqyIL%2F3aEw7VT1lnHgEuntHdE7g0MbQ3RaEoll6TX139pEshqVprRE7pzlCrzEtkn28qBtE0UVDpbc0M6p0E0bof907dcd8vh1ETa%2F3GwHfXPlX%2FwWCsDW7IDDsKPPSEvHUonyIseYarkJyLN8mwxOQMo93%2BoWA3TH77WNdzq7qBo11uYLwCQWlo8goNN82AIy8azafgB4V6ypiiinTrR7JJLqvQso8ZWCJ%2Fk56%2BDIMwphKhdEheGaLIKkNK32YzMXz4J%2F20WLbH4TQpoLjllmyTRzIJgCYeBfuOVbNj%2BRB%2F02W0%2FDLpqMl6MhPUzIxQMzUzzZLlmTeWrE%2BT259mboGazAY1uRXKb52CmN2a24u4oSiWST8VzKSdygvSotLdjPdJk02bCm%2BWiuE6tMu6MrLlXGwSaZ0fSS1Lfp1N3pFamLwjFd1ZZ2pT8k4mxLf0UjKynnnhKarQ0t0M32JjedSx44ThmfFYylI9NOIzDcc1o22K00sjVWbE563Na8d3n8q%2FU%2Bnt1479crP5c0sqAZFUkVSEvS0T9l8eg%2FXyESvUx3j1iNVivZDkAYZnM%2BzklNnJMSQ%2BsSQDpj1DUztPVtLrslK%2FAoySLxQ1ZGge077UtZO0LyUa%2FGJgXgzMi4F5SPRlVJmb74eBeZ5RYr3uPE7fDEzZSoPNGZinYl0aitYz69I4zzCmXjd8b%2FQrjKmL4fv%2FBygaMDOBTG1KZjCxMfFEM1FG6XQouY2LLcwwtSdJ1811IJ73w7bclx%2FbNT631FP0SSmqFaU4knxS8%2BhK0TjPJDajbtSFZVH2hZmN7VGXrR5WHb0osGI1EvO4BPF%2B3VnTNO06YOOY1ZolVZHkMaiGI%2BPG9hTrec6Lcxbbz4v9Ctvw55aHbT6hQTrH54dzjey0qf2cNDpibMn07LMWVFVJveDx1eB55vgZdX1Do1%2B%2BobHdN7yowUPUoGb3QA2eZ5zGqO1f9iubzxD9y8l6yXTgfz4y7SeprgDzCM5B4BGXkk5UCOUXR5m3EC5lnGhqrqBZDUnC29E1q3me0SKjbtJb8wWEh3GzbIH7djTrZAGCIAxOWYXqmj20qzrUVES248WKR1Gg%2FCPIZ8ZyZt2Yjtmv%2FGpTjOlc0%2FiqCjwapy0WJyJBOcJ4CweV8gFkZYuVoG5azkLuReK%2Bt4GHXMnyDDS0m7Nu6SY19PQSRvmiD1K9LJybqVvipPVcCRuGIdjUlmTC5vhquJuVVzuXCXVTgvhXyPsiE8SUoBLDV6A85sKobZduGFweZgxk6yIDyZZ0a0%2BhnmdqKueJ%2FczTr7U7%2BXPvWFSS8MsM%2BXWWH3qOMHvsXH9op3tpKiehtKrFUqojmRA5vtYSF7YUPf%2FUFqHRuRjBKAKPAXwCHhjGi1WtFI8OpWcj8KnCIphX6siUBPJMe6hqR5Sb0m9lvyofVJ4OuiMJNDNJB5quGwQL6D9BsoKp0DPYkibqEP%2B12PXMaEU6jfQ5aKePxTeMrkjOKQrmaX8QRkvgZ4eQBVav2JqqpJstq1rqRlhNBEkhRbXYmUQgiGf4ovzyQZ7e%2BhxGXvnuxdOnwP0%2Bp0roqkJTjTj5jJYaibbybbNAWQ%2FFKx8wqqLAR4Ubz%2FwQJMUH2uvtl3JNDXRw7PzEWVZXNSFuYPDy0NI3fyQfd2piGeGdq0gW2LWEW38waNzo1LjBnXttMvUnkZ1tqT7J18zPxgPgM%2BtdgPHpow%2F%2FCG5nSvw8%2Fssef3Dc%2BO7qpGLYbzf4rboGP180uScGv%2BTL1AXBVbYKH%2BlK6Klt%2BI55CJsxVaOQU6moX%2Fj3k5rmoi%2Ffru7uRt9%2B1sDE2Pz3a%2Fzx%2B68frkT1Iv3GVVeL0qtVINQmgDCVsp4XQZB9TqQJk1yKgahVPr93APgXibg2oZ9Fr2Cgt4SBVJtop6RN6sYbispF%2BtaSSKz0uM6S%2FHY99a7vfQPypVLyRlTGV%2FQFvgVaxbCoKXbxFVZBHv00LSG9B%2BJFBjnz875QuHXiWy0BoRD%2Fe4uWc%2FyGPpriX%2BASyjx6KMJPFhIy3D%2FD6WMMI8w4w%2Fhp3lIgyVKqbo0tMd14eXLTTo3cdOvadjMstcRvQ0Ub7eE5%2BOY15Xdx1F7O4x%2Bd7QnriTl%2BtzB28UuQCG5hCfkEMwadL9VJRAkT%2B1pVhgqfhO9vjNWSFEVakviq3RZriFaz9Kt7RzUHmqB1Vg7HCO1wGVCUQRLDV3VaIrSYIff57vbD9S%2BnT2rDKBtXjiJ%2BfUn2oYLWSM3j26dhXL1dpnNZvd9V7yxze%2BdzF3iBy%2FAweIzPykfXR9UEbEsXuKcpF33AlhfI%2BwoLC%2Bh3%2FwI%3D"></iframe>

La ejecución del anterior flujo de trabajo se realiza usando R. Para ello iremos ejecutando secuencialmente las líneas del siguiente bloque de código:

```R
#Este script calcula el Indice Shannon de Sierra Nevada
# usando la información existente en GBIF y un mapa de vegetación a escala 1:10.000

## Establece directorio de trabajo. Recuerda cambiarlo por el tuyo.
setwd("/Users/fjbonet_trabajo/Google_Drive/4_docencia/eco_ccaa_uco/actos_docentes/P_shannon_ecologia_ccaa/preparacion")

## Carga paquetes que necesitamos
install.packages("rgdal")
library(rgdal)

install.packages("sqldf")
library(sqldf)

## Importa la capa con las ocurrencias de GBIF
ocurrencias<-readOGR(dsn=".", layer="ocurrencias_sierra_nevada_23030", verbose = FALSE)

## Importa la capa con la delimitación de las comunidades ecológicas.
comunidades<-readOGR(dsn=".",layer="vegetacion_snevada_23030", verbose = FALSE)

## Unión espacial: asigna a cada punto el código de la comunidad en la que se encuentra.
ocurrencias$id_com <- over(ocurrencias, comunidades)$OBJECTID

## Extraer la "tabla de atributos" para hacer los cálculos del índice de Shannon
bio<-ocurrencias@data

## Calcular el índice de Shannon

### Calcular el número de individuos por especie y por comunidad (num_ind_sp_com)
T_num_ind_sp_com<-sqldf("SELECT id_com, scientific,  count(scientific) num_ind_sp_com  FROM bio GROUP BY id_com, scientific")

### Calcular el número total de individuos por comrícula.
T_num_ind_com<-sqldf("SELECT id_com, sum(num_ind_sp_com) num_ind_com FROM T_num_ind_sp_com GROUP BY id_com")

### Fusionar las tablas anteriores para calcular Pi
T_num_ind_sp_com_mas_num_ind_com<-sqldf("SELECT id_com, scientific, num_ind_sp_com, num_ind_com FROM T_num_ind_sp_com LEFT JOIN T_num_ind_com USING(id_com)")

### Calcular pi por especie y por comunidad
T_num_ind_sp_com_mas_num_ind_com<-sqldf("SELECT id_com, scientific, num_ind_sp_com, num_ind_com, (num_ind_sp_com*1.0/num_ind_com) pi FROM T_num_ind_sp_com_mas_num_ind_com")

### Calcular el log2 pi por especie y por comunidad (log = ln). Log2(pi)=log(pi)/log(2)
T_num_ind_sp_com_mas_num_ind_com<-sqldf("SELECT id_com, scientific, num_ind_sp_com, num_ind_com, pi, (log(pi)/log(2))*pi lnpi_pi FROM T_num_ind_sp_com_mas_num_ind_com")

### Calcular H por comunidad
T_Shannon<-sqldf("SELECT id_com, sum(lnpi_pi)*-1 H FROM T_num_ind_sp_com_mas_num_ind_com GROUP BY id_com")

## Fusionar la tabla que tiene el índice de Shannon con la distribución de comunidades.
comunidades<-merge(x = comunidades, y = T_Shannon, by.x = "OBJECTID", by.y = "id_com")

## Exportar la capa resultante a un shapefile.
writeOGR(comunidades, dsn=".", layer="Shannon_com_sierra_nevada", driver="ESRI Shapefile", overwrite=TRUE )

```



La siguiente presentación muestra paso a paso el flujo de trabajo. También puedes verla [aquí](https://prezi.com/view/gOJNmvizzKEsXVxEHe3I/) y descargarla [aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/presentacion/2_mapa_biodiversidad_sierra_nevada.exe) para Windows y aquí para [Mac](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/presentacion/2_mapa_biodiversidad_sierra_nevada.zip). Y [aquí](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/presentacion/2_mapa_biodiversidad_sierra_nevada.pdf) la tienes en formato pdf.




<p><iframe src="https://prezi.com/view/gOJNmvizzKEsXVxEHe3I/embed" width="1200" height="900"> </iframe></p>






## Resultados esperables
El siguiente mapa muestra el resultado obtenido en esta práctica. Se trata de un fichero de formas vectorial en el que se ha asignado el valor del índice Shannon a cada polígono del mapa de vegetación inicial. Aquí se puede descargar dicho fichero de formas.



![shannon](https://github.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/raw/2020-2021/imagenes/shannon_snev.png)



En el mapa resultante se pueden identificar varios patrones de distribución espacial de la biodiversidad en Sierra Nevada. Durante la práctica reflexionamos sobre dichos patrones:

+ ¿Cómo cambia la diversidad al aumentar la altitud?

+ ¿A qué se puede deber dicho patrón?

+ ¿Crees que se repetiría el mismo patrón en otras montañas de la Tierra?

+ ¿hay algún patrón de cambio de diversidad en dirección este-oeste?

+ En caso afirmativo, ¿a qué puede deberse?

  

## Vídeos de las sesiones

Lamentablemente en esta ocasión no grabé las sesiones. Así que tenemos que conformarnos con versiones similares de esta práctica en otros años y en otras titulaciones. Ahí va la misma práctica pero impartida para alumnos de tercer curso de biología:

<iframe width="560" height="315" src="https://www.youtube.com/embed/6OOusJU4ljs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



