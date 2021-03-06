---
title: "Intro.ggplot"
author: "Nicolas"
date: "1/9/2021"
output: 
  html_document: 
    keep_md: yes
---

# Activar paquetes


```r
library(tidyverse)
```

```
## Warning: package 'tidyverse' was built under R version 4.0.5
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --
```

```
## v ggplot2 3.3.3     v purrr   0.3.4
## v tibble  3.1.2     v dplyr   1.0.6
## v tidyr   1.1.3     v stringr 1.4.0
## v readr   1.4.0     v forcats 0.5.1
```

```
## Warning: package 'tibble' was built under R version 4.0.5
```

```
## Warning: package 'tidyr' was built under R version 4.0.5
```

```
## Warning: package 'dplyr' was built under R version 4.0.5
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(lubridate)
```

```
## Warning: package 'lubridate' was built under R version 4.0.5
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
library(scales)
```

```
## 
## Attaching package: 'scales'
```

```
## The following object is masked from 'package:purrr':
## 
##     discard
```

```
## The following object is masked from 'package:readr':
## 
##     col_factor
```

# Limpiar espacio de trabajo


```r
rm(list = ls())
```

# Importar datos


```r
saber11_2019 <- read_delim("Bases_de_datos/saber11_2019.csv", delim = ";")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_character(),
##   PERIODO = col_double(),
##   COLE_COD_DANE_ESTABLECIMIENTO = col_double(),
##   COLE_COD_DANE_SEDE = col_double(),
##   PUNT_LECTURA_CRITICA = col_double(),
##   PERCENTIL_LECTURA_CRITICA = col_double(),
##   DESEMP_LECTURA_CRITICA = col_double(),
##   PUNT_MATEMATICAS = col_double(),
##   PERCENTIL_MATEMATICAS = col_double(),
##   DESEMP_MATEMATICAS = col_double(),
##   PUNT_C_NATURALES = col_double(),
##   PERCENTIL_C_NATURALES = col_double(),
##   DESEMP_C_NATURALES = col_double(),
##   PUNT_SOCIALES_CIUDADANAS = col_double(),
##   PERCENTIL_SOCIALES_CIUDADANAS = col_double(),
##   DESEMP_SOCIALES_CIUDADANAS = col_double(),
##   PUNT_INGLES = col_double(),
##   PERCENTIL_INGLES = col_double(),
##   PUNT_GLOBAL = col_double(),
##   PERCENTIL_GLOBAL = col_double(),
##   ESTU_INSE_INDIVIDUAL = col_double()
##   # ... with 2 more columns
## )
## i Use `spec()` for the full column specifications.
```

# Extraer una muestra m??s peque??a


```r
set.seed(20210412)
saber11_2019_peq<- saber11_2019 %>% 
  slice_sample(prop = 0.1)
mean(saber11_2019_peq$PUNT_GLOBAL)
```

```
## [1] 245.1897
```

# Introducci??n a `ggplot2`

-   El paquete `ggplot2` es el mejor paquete para hacer gr??ficas en R.

-   Es el m??s completo y vers??til pues permite personalizar todos los aspectos de las gr??ficas.

-   En este paquete se hacen gr??ficas por capas.

-   La primera capa indica a R que cree la "plantilla" de la gr??fica, y los datos que se utilizar??n.

-   La siguiente capa indica el tipo de gr??fica, y las caracter??sticas de esa gr??fica, incluyendo las variables a graficar.

-   Por ejemplo, para hacer un diagrama de dispersi??n en el puntaje de matem??ticas y el ??ndice socioecon??mico individual, se usar??a la siguiente estructura:


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                     y = PUNT_MATEMATICAS))
```

![](intro.ggplot_files/figure-html/unnamed-chunk-5-1.png)<!-- -->


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                     y = PUNT_MATEMATICAS)) +
  geom_point()
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

## Aesthetics (aes)

-   **Aesthetics (aes)** se refieren a propiedades visuales de los objetos dentro de la gr??fica como: variable a graficar, tama??o, forma o color.

-   Se pueden modificar manualmente o de acuerdo con los valores de una variable.

    -   Para hacerlo manualmente, el argumento se pone por fuera de `aes()`.

    -   Para hacerlo en funci??n de una variable se pone como otro argumento dentro de `aes()`.

-   Por ejemplo, En un diagrama de dispersi??n podemos variar las siguientes propiedades est??ticas de los puntos:

| Nombre argumento | Rol                                                |
|------------------|----------------------------------------------------|
| color            | Color del punto                                    |
| size             | Tama??o del punto                                   |
| shape            | Forma del punto                                    |
| alpha            | Intensidad del color (i.e. nivel de transparencia) |

Por ejemplo, para colocar manualmente tri??ngulos en lugar de c??rculos, y que sean de color rojo, se har??a lo siguiente:


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                     y = PUNT_MATEMATICAS)) +
  geom_point(color = "Red", shape = 2)
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

Colores:

-   <https://www.nceas.ucsb.edu/~frazier/RSpatialGuides/colorPaletteCheatsheet.pdf>
-   <http://www.stat.columbia.edu/~tzheng/files/Rcolor.pdf>

Formas: ver la hoja de referencia de `ggplot2`. O ver la siguiente vi??eta:


```r
vignette("ggplot2-specs")
```

```
## starting httpd help server ... done
```

Para modificar el color en funci??n de la variable COLE_NATURALEZA, se har??a lo siguiente:


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL, 
                     y = PUNT_MATEMATICAS,
                     color = COLE_NATURALEZA)) +
  geom_point()
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

O para modificar la forma de acuerdo con los valores de la misma variables, se har??a de la siguiente manera:


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                           y = PUNT_MATEMATICAS,
                           shape = COLE_NATURALEZA, color=COLE_NATURALEZA)) +
  geom_point()
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

## Geoms

-   Geoms son objetos geom??tricos que usa ggplot para realizar las gr??ficas
-   En ggplot2 hay al menos 50 *geoms*, y hay paquetes que han creado extensiones a ggplot2 que contienen m??s geoms.
-   A la gr??fica anterior, podr??a agregar una l??nea de tendencia usando geom_smooth:


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                           y = PUNT_MATEMATICAS)) +
  geom_point() +
  geom_smooth(method = "lm")
```

```
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-11-1.png)<!-- -->


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                           y = PUNT_MATEMATICAS,
                     color=COLE_NATURALEZA)) +
  geom_point() +
  geom_smooth(method = "lm")
```

```
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-12-1.png)<!-- -->


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                           y = PUNT_MATEMATICAS)) +
  geom_point() +
  geom_smooth(method="lm", aes(color=COLE_NATURALEZA))
```

```
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-13-1.png)<!-- -->


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                           y = PUNT_MATEMATICAS)) +
  geom_point(aes(color=COLE_NATURALEZA)) +
  geom_smooth(method = "lm")
```

```
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-14-1.png)<!-- -->

En la gr??fica anterior, cambien el color de la l??nea a rojo.


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                           y = PUNT_MATEMATICAS)) +
  geom_point() +
  geom_smooth(method = "lm",color="Red")
```

```
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

Otras propiedades que se pueden modificar en la l??nea son: linetype, size, alpha, entre otros.

## Poner t??tulos y cambiar nombres de los ejes:

Para agregar un t??tulo o cambiar un nombre a los ejes, se debe agrear la capa `labs`:


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                           y = PUNT_MATEMATICAS)) +
  geom_point() +
  geom_smooth(method = "lm", color="Red") + 
  labs(title="El puntaje de matematicas es mayor", subtitle="para mayores niveles socieconomicos", x="Nivel socieconomico individual", y="Puntaje de matematicas", caption="Fuente:Saber 11 2019-2")
```

```
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

## Cambiar el aspecto general de la gr??fica (i.e. themes)

-   Las capas `theme_` de `ggplot` proveen algunas funciones est??ndar para hacer el cambio.
-   Adem??s el paquete `ggthemes` traer otros *themes* para `ggplot`.


```r
#install.packages("ggthemes")
library(ggthemes)
```

```
## Warning: package 'ggthemes' was built under R version 4.0.5
```


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                           y = PUNT_MATEMATICAS)) +
  geom_point() +
  geom_smooth(method = "lm", color="Red") + 
  labs(title="El puntaje de matematicas es mayor", subtitle="para mayores niveles socieconomicos", x="Nivel socieconomico individual", y="Puntaje de matematicas", caption="Fuente:Saber 11 2019-2") +
  theme_stata()
```

```
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-18-1.png)<!-- -->

## Guardar gr??ficas:

1.  Manualmente.
2.  Usando la funci??n `ggsave()` inmediatamente despu??s de la gr??fica. Se debe poner el nombre con la extensi??n en la que se quiera guardar la gr??fica.


```r
ggsave("dispersi??n.pdf")
```

```
## Saving 7 x 5 in image
```

```
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

```r
ggsave("dispersi??n.jpeg")
```

```
## Saving 7 x 5 in image
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).

## Warning: Removed 152 rows containing missing values (geom_point).
```


```r
grafica <- ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                           y = PUNT_MATEMATICAS)) +
  geom_point(aes(color=COLE_NATURALEZA)) +
  geom_smooth(method = "lm")
grafica
```

```
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-20-1.png)<!-- -->

```r
ggsave("dispersion2.jpeg",grafica)
```

```
## Saving 7 x 5 in image
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).

## Warning: Removed 152 rows containing missing values (geom_point).
```

## Ejercicio 1

Escriba el c??digo que deben usar para crear un diagrama de dispersi??n que relacione las variables ESTU_INSE_INDIVIDUAL y PUNT_INGLES. En lugar de puntos use +. El color de los + debe ser distinto para las categor??as de la variable COLE_BILINGUE. Incluya una l??nea de tendencia:


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = ESTU_INSE_INDIVIDUAL,
                           y = PUNT_INGLES)) +
  geom_point(shape=3, aes(color=COLE_BILINGUE) )+
  geom_smooth(method = "lm") + 
  labs(title="El puntaje de ingles es mayor", subtitle="para mayores niveles socieconomicos", x="Nivel socieconomico individual", y="Puntaje de INGLES", caption="Nicolas Pardo")+
  theme_stata()
```

```
## `geom_smooth()` using formula 'y ~ x'
```

```
## Warning: Removed 152 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 152 rows containing missing values (geom_point).
```

![](intro.ggplot_files/figure-html/unnamed-chunk-21-1.png)<!-- -->

# Geoms (Continuaci??n)

Los geoms m??s usados para los tipos de gr??ficos que con mayor frecuencia se usan en an??lisis de datos son:

+------------------------------+------------------------------------------------------------------------------------+
| Geom                         | Tipo de gr??fica                                                                    |
+==============================+====================================================================================+
| `geom_point()`               | Diagrama de dispersi??n (dos variables cuantitativas)                               |
+------------------------------+------------------------------------------------------------------------------------+
| `geom_jitter()`              | Diagrama de dispersi??n con ruido aleatorio (dos variables cuantitativas)           |
+------------------------------+------------------------------------------------------------------------------------+
| `geom_bar()`                 | Gr??fico de barras (una o dos variables cualitativas)                               |
+------------------------------+------------------------------------------------------------------------------------+
| `geom_histogram()`           | Histograma (una variable cuantitativa)                                             |
+------------------------------+------------------------------------------------------------------------------------+
| `geom_freqpoly()`            | Pol??gono de frecuencias (una variable cuantitativa)                                |
+------------------------------+------------------------------------------------------------------------------------+
| `geom_density()`             | Versi??n suavizada del histograma (una variable cuantitativa)                       |
+------------------------------+------------------------------------------------------------------------------------+
| `geom_line()`                | Gr??fico de l??neas (??til para mostrar tendencias en el tiempo)                      |
+------------------------------+------------------------------------------------------------------------------------+
| `geom_area()`                | Rellena ??reas debajo de una l??nea. Tambi??n es ??til para mostrar tendencias.        |
+------------------------------+------------------------------------------------------------------------------------+
| `geom_boxplot()`             | Diagrama de cajas y bigotes (una variable cuantitativa y una variable cualitativa) |
+------------------------------+------------------------------------------------------------------------------------+
| `geom_text()`                | Permite agregar texto a una gr??fica.                                               |
+------------------------------+------------------------------------------------------------------------------------+

## Diagrama de Barras:

Realicen un diagrama de barras para la variable FAMI_ESTRATOVIVIENDA.


```r
ggplot(data = saber11_2019_peq, 
       mapping = aes(x = FAMI_ESTRATOVIVIENDA)) +
  geom_bar()
```

![](intro.ggplot_files/figure-html/unnamed-chunk-22-1.png)<!-- -->

Modifiquen el gr??fico anterior para que:

-   Muestre la frecuencia relativa
-   El color de las barras sea verde.


```r
ggplot(data = saber11_2019_peq,
       mapping = aes(x = FAMI_ESTRATOVIVIENDA, 
                     y = stat(prop), group = 1)) +
  geom_bar(fill = "Darkgreen", color="black") 
```

![](intro.ggplot_files/figure-html/unnamed-chunk-23-1.png)<!-- -->

<https://www.r-graph-gallery.com/237-interactive-treemap.html>
