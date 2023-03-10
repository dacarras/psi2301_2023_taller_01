Taller 01
================
dacarras
Thu Mar 09, 2023

# Introducción

- El siguiente documento es una colección breve de funciones básicas
  para producir resultados.

- Existen diferentes maneras de producir resultados en r. En este curso,
  emplearemos la generación de resultados mediante códigos
  reproducibles. Es decir, que son códigos que pueden ser ejecutados, y
  debieran producir el mismo resultado en diferentes equipos, y en
  diferentes momentos.

- Para lograr lo anterior, el código escrito debe cumplir ciertas
  características. Una de ellas, es que la secuencia de comandos
  empleados pueda ser ejecutada por un documento dinámico. El presente
  código esta escrito de esta forma. Una vez ejecutado, debiera poder
  ejecutarse completo, y producir un output en html.

- En particular, vamos a revisar diferentes funciones en `R` para abrir
  datos, y para manejar datos. Emplearemos funciones de R base, y de la
  libreria `dplyr`, la cual es una librería muy versatil para el manejo
  de datos (ver *[cheat
  sheet](https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf)*)

# Instalar librerias

``` r
#------------------------------------------------------------------------------
# instalar librerias
#------------------------------------------------------------------------------

#----------------------------------------------------------
# librerias
#----------------------------------------------------------

install.packages('tidyverse') # incluye a dplyr y ggplot2
                              # junto a otras librerias útiles

install.packages('dplyr')     # para manejo de datos

install.packages('knitr')     # para mostrar tablas como texto plano

install.packages('readxl')    # para abrir archivos en excel

install.packages('haven')     # para abrir datos de diferentes de otros software estadisticos

install.packages('devtools')  # para instalar librerias desde github

install.packages("moments")   # para obtener asimetria
```

# Ejercicio 1. Abrir datos

## Cargar datos desde tabla escrita

``` r
#------------------------------------------------------------------------------
# datos
#------------------------------------------------------------------------------

#----------------------------------------------------------
# tabla 3.2
#----------------------------------------------------------

data_table_3_2 <- read.table(
text="
person  y x x_q xy
1 2 8 64  16
2 3 9 81  27
3 3 9 81  27
4 4 10  100 40
5 7 6 36  42
6 5 7 49  35
7 5 4 16  20
8 7 5 25  35
9 8 3 9 24
10  9 1 1 9
11  9 2 4 18
12  10  2 4 20

",
header=TRUE, stringsAsFactors = FALSE)

#--------------------------------------
# mostrar tabla
#--------------------------------------

knitr::kable(data_table_3_2)
```

| person |   y |   x | x_q |  xy |
|-------:|----:|----:|----:|----:|
|      1 |   2 |   8 |  64 |  16 |
|      2 |   3 |   9 |  81 |  27 |
|      3 |   3 |   9 |  81 |  27 |
|      4 |   4 |  10 | 100 |  40 |
|      5 |   7 |   6 |  36 |  42 |
|      6 |   5 |   7 |  49 |  35 |
|      7 |   5 |   4 |  16 |  20 |
|      8 |   7 |   5 |  25 |  35 |
|      9 |   8 |   3 |   9 |  24 |
|     10 |   9 |   1 |   1 |   9 |
|     11 |   9 |   2 |   4 |  18 |
|     12 |  10 |   2 |   4 |  20 |

## Abrir datos desde archivo (`*.xlsx`)

``` r
#------------------------------------------------------------------------------
# abrir datos desde excel
#------------------------------------------------------------------------------

#----------------------------------------------------------
# tabla 3.2
#----------------------------------------------------------

data_from_excel <- readxl::read_xlsx('table_3_2.xlsx')

#--------------------------------------
# mostrar tabla
#--------------------------------------

knitr::kable(data_from_excel)
```

| person |   y |   x | x_q |  xy |
|-------:|----:|----:|----:|----:|
|      1 |   2 |   8 |  64 |  16 |
|      2 |   3 |   9 |  81 |  27 |
|      3 |   3 |   9 |  81 |  27 |
|      4 |   4 |  10 | 100 |  40 |
|      5 |   7 |   6 |  36 |  42 |
|      6 |   5 |   7 |  49 |  35 |
|      7 |   5 |   4 |  16 |  20 |
|      8 |   7 |   5 |  25 |  35 |
|      9 |   8 |   3 |   9 |  24 |
|     10 |   9 |   1 |   1 |   9 |
|     11 |   9 |   2 |   4 |  18 |
|     12 |  10 |   2 |   4 |  20 |

## Abrir datos desde archivo (`*.csv`)

``` r
#------------------------------------------------------------------------------
# abrir datos desde archivo csv
#------------------------------------------------------------------------------

#----------------------------------------------------------
# tabla 3.2
#----------------------------------------------------------

data_from_csv_file <- read.csv('table_3_2.csv')

#--------------------------------------
# mostrar tabla
#--------------------------------------

knitr::kable(data_from_csv_file)
```

| person |   y |   x | x_q |  xy |
|-------:|----:|----:|----:|----:|
|      1 |   2 |   8 |  64 |  16 |
|      2 |   3 |   9 |  81 |  27 |
|      3 |   3 |   9 |  81 |  27 |
|      4 |   4 |  10 | 100 |  40 |
|      5 |   7 |   6 |  36 |  42 |
|      6 |   5 |   7 |  49 |  35 |
|      7 |   5 |   4 |  16 |  20 |
|      8 |   7 |   5 |  25 |  35 |
|      9 |   8 |   3 |   9 |  24 |
|     10 |   9 |   1 |   1 |   9 |
|     11 |   9 |   2 |   4 |  18 |
|     12 |  10 |   2 |   4 |  20 |

## Abrir datos desde archivo (`*.sav`)

``` r
#------------------------------------------------------------------------------
# abrir datos desde archivo csv
#------------------------------------------------------------------------------

#----------------------------------------------------------
# tabla 3.2
#----------------------------------------------------------

data_from_sav_file <- haven::read_sav('table_3_2.sav')

#--------------------------------------
# mostrar tabla
#--------------------------------------

knitr::kable(data_from_sav_file)
```

| person |   y |   x | x_q |  xy |
|-------:|----:|----:|----:|----:|
|      1 |   2 |   8 |  64 |  16 |
|      2 |   3 |   9 |  81 |  27 |
|      3 |   3 |   9 |  81 |  27 |
|      4 |   4 |  10 | 100 |  40 |
|      5 |   7 |   6 |  36 |  42 |
|      6 |   5 |   7 |  49 |  35 |
|      7 |   5 |   4 |  16 |  20 |
|      8 |   7 |   5 |  25 |  35 |
|      9 |   8 |   3 |   9 |  24 |
|     10 |   9 |   1 |   1 |   9 |
|     11 |   9 |   2 |   4 |  18 |
|     12 |  10 |   2 |   4 |  20 |

## Abrir datos desde url

``` r
#------------------------------------------------------------------------------
# abrir datos desde archivo en una url
#------------------------------------------------------------------------------

#----------------------------------------------------------
# url datos
#----------------------------------------------------------

url_location <- url('https://github.com/dacarras/psi2301_2023_tarea_test/raw/main/ingresos_2016.rds')

#--------------------------------------
# abrir datos
#--------------------------------------

data_inc <- readRDS(url_location)

#--------------------------------------
# inspeccionar datos
#--------------------------------------

dplyr::glimpse(data_inc)
```

    ## Rows: 1,120
    ## Columns: 4
    ## $ hinc   <dbl> 128.00000, 511.87225, 731.02267, 471.20375, 819.23280, 444.6939…
    ## $ sex    <dbl> 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, …
    ## $ edu    <dbl+lbl>  8, 11, 15, 12, 11, 14, 12, 18, 12,  7, 12, 17,  0,  3, 12,…
    ## $ home_n <dbl> 5, 4, 3, 4, 4, 4, 4, 4, 4, 3, 4, 2, 4, 3, 2, 6, 12, 3, 2, 5, 2,…

``` r
#----------------------------------------------------------
# url datos
#----------------------------------------------------------

url_location <- url('https://github.com/dacarras/psi4035_examples/raw/master/data/smoking.dta')

#--------------------------------------
# abrir datos
#--------------------------------------

data_smoking <- haven::read_dta(url_location)

#--------------------------------------
# inspeccionar datos
#--------------------------------------

dplyr::glimpse(data_smoking)
```

    ## Rows: 8,604
    ## Columns: 24
    ## $ momid    <dbl> 14, 14, 14, 25, 25, 25, 39, 39, 39, 48, 48, 60, 60, 71, 71, 7…
    ## $ idx      <dbl> 1, 2, 3, 1, 2, 3, 1, 2, 3, 1, 2, 1, 2, 1, 2, 3, 1, 2, 1, 2, 1…
    ## $ stateres <dbl+lbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ mage     <dbl> 16, 17, 20, 23, 24, 26, 36, 38, 39, 30, 32, 23, 26, 20, 22, 2…
    ## $ meduc    <dbl> 10, 10, 10, 11, 11, 11, 14, 14, 14, 12, 12, 13, 13, 10, 10, 1…
    ## $ mplbir   <dbl+lbl> 47, 47, 47, 31, 31, 31, 30, 30, 30, 34, 34, 41, 41, 18, 1…
    ## $ nlbnl    <dbl> 0, 1, 2, 2, 3, 4, 2, 3, 4, 3, 4, 0, 1, 0, 1, 2, 2, 3, 2, 3, 0…
    ## $ gestat   <dbl> 24, 42, 39, 41, 37, 40, 41, 40, 39, 39, 38, 43, 37, 40, 41, 4…
    ## $ birwt    <dbl> 2790, 2693, 3600, 2778, 2835, 3402, 2948, 3487, 3345, 2880, 3…
    ## $ cigs     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 99, 40, 0, 0, 99, 20, 10, 0, 0, 0,…
    ## $ smoke    <dbl+lbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 0, 0, …
    ## $ male     <dbl+lbl> 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1, 0, 0, 1, 1, 1, …
    ## $ year     <dbl> 0, 1, 4, 2, 3, 5, 1, 3, 5, 0, 1, 0, 3, 0, 2, 3, 0, 2, 0, 3, 0…
    ## $ married  <dbl> 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ hsgrad   <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ somecoll <dbl> 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0, 0, 1, 1, 0, 0, 0…
    ## $ collgrad <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1…
    ## $ magesq   <dbl> 256, 289, 400, 529, 576, 676, 1296, 1444, 1521, 900, 1024, 52…
    ## $ black    <dbl+lbl> 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, …
    ## $ kessner2 <dbl> 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0…
    ## $ kessner3 <dbl> 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ novisit  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pretri2  <dbl> 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0…
    ## $ pretri3  <dbl> 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…

## Abrir datos desde una libreria

``` r
#------------------------------------------------------------------------------
# abrir datos desde libreria
#------------------------------------------------------------------------------

#----------------------------------------------------------
# instalar libreria
#----------------------------------------------------------

# devtools::install_github('dacarras/psi2301',force = TRUE)

#----------------------------------------------------------
# cargar datos desde libreria
#----------------------------------------------------------

data_smoking <- psi2301::smoking

# Nota: requiere saber el nombre de los datos de forma previa.

#--------------------------------------
# inspeccionar datos
#--------------------------------------

dplyr::glimpse(data_smoking)
```

# Ejercicio 2. Inspeccionar datos

## Cuántos datos tenemos en sesión

``` r
#------------------------------------------------------------------------------
# inspeccionar session
#------------------------------------------------------------------------------

#----------------------------------------------------------
# lista de objetos creados
#----------------------------------------------------------

ls()
```

    ##  [1] "cars"               "data_balance"       "data_first_base"   
    ##  [4] "data_first_born"    "data_from_csv_file" "data_from_excel"   
    ##  [7] "data_from_sav_file" "data_inc"           "data_model"        
    ## [10] "data_n500"          "data_prop"          "data_prop_20"      
    ## [13] "data_raw"           "data_selected"      "data_selected_base"
    ## [16] "data_smoking"       "data_table_3_2"     "datos_idps"        
    ## [19] "datos_tarea"        "hist_info"          "mode"              
    ## [22] "texto_en_codigo"    "url_location"       "valor_mediana"

## Contar filas `nrow()`

``` r
#------------------------------------------------------------------------------
# informacion de filas
#------------------------------------------------------------------------------

#----------------------------------------------------------
# filas de tabla 3.2
#----------------------------------------------------------

nrow(data_table_3_2)
```

    ## [1] 12

``` r
#----------------------------------------------------------
# cantidad de casos en data_inc
#----------------------------------------------------------

nrow(data_inc)
```

    ## [1] 1120

``` r
#----------------------------------------------------------
# cantidad de casos en data_smoking
#----------------------------------------------------------

nrow(data_smoking)
```

    ## [1] 8604

## Contar columnas `ncol()`

``` r
#------------------------------------------------------------------------------
# informacion de columnas
#------------------------------------------------------------------------------

#----------------------------------------------------------
# columnas de tabla 3.2
#----------------------------------------------------------

nrow(data_table_3_2)
```

    ## [1] 12

``` r
#----------------------------------------------------------
# variables de data_inc
#----------------------------------------------------------

ncol(data_inc)
```

    ## [1] 4

``` r
#----------------------------------------------------------
# nombres de las variables
#----------------------------------------------------------

names(data_inc)
```

    ## [1] "hinc"   "sex"    "edu"    "home_n"

``` r
#----------------------------------------------------------
# cantidad de variables de data_smoking
#----------------------------------------------------------

ncol(data_smoking)
```

    ## [1] 24

## Dimensionaes de una tabla `dim()`

``` r
#------------------------------------------------------------------------------
# informacion de las dimensiones de una tabla (filas, columnas)
#------------------------------------------------------------------------------

#----------------------------------------------------------
# dimensiones de data_smoking
#----------------------------------------------------------

dim(data_smoking)
```

    ## [1] 8604   24

## Inspeccionar datos `dplyr::glimpse()`

``` r
#------------------------------------------------------------------------------
# inspeccionar datos de forma rápida
#------------------------------------------------------------------------------

#--------------------------------------
# inspeccionar datos de tabla 3_2
#--------------------------------------

dplyr::glimpse(data_table_3_2)
```

    ## Rows: 12
    ## Columns: 5
    ## $ person <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12
    ## $ y      <int> 2, 3, 3, 4, 7, 5, 5, 7, 8, 9, 9, 10
    ## $ x      <int> 8, 9, 9, 10, 6, 7, 4, 5, 3, 1, 2, 2
    ## $ x_q    <int> 64, 81, 81, 100, 36, 49, 16, 25, 9, 1, 4, 4
    ## $ xy     <int> 16, 27, 27, 40, 42, 35, 20, 35, 24, 9, 18, 20

``` r
#--------------------------------------
# inspeccionar datos de ingresos
#--------------------------------------

dplyr::glimpse(data_inc)
```

    ## Rows: 1,120
    ## Columns: 4
    ## $ hinc   <dbl> 128.00000, 511.87225, 731.02267, 471.20375, 819.23280, 444.6939…
    ## $ sex    <dbl> 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, …
    ## $ edu    <dbl+lbl>  8, 11, 15, 12, 11, 14, 12, 18, 12,  7, 12, 17,  0,  3, 12,…
    ## $ home_n <dbl> 5, 4, 3, 4, 4, 4, 4, 4, 4, 3, 4, 2, 4, 3, 2, 6, 12, 3, 2, 5, 2,…

``` r
#----------------------------------------------------------
# inspeccionar datos data_smoking
#----------------------------------------------------------

dplyr::glimpse(data_smoking)
```

    ## Rows: 8,604
    ## Columns: 24
    ## $ momid    <dbl> 14, 14, 14, 25, 25, 25, 39, 39, 39, 48, 48, 60, 60, 71, 71, 7…
    ## $ idx      <dbl> 1, 2, 3, 1, 2, 3, 1, 2, 3, 1, 2, 1, 2, 1, 2, 3, 1, 2, 1, 2, 1…
    ## $ stateres <dbl+lbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ mage     <dbl> 16, 17, 20, 23, 24, 26, 36, 38, 39, 30, 32, 23, 26, 20, 22, 2…
    ## $ meduc    <dbl> 10, 10, 10, 11, 11, 11, 14, 14, 14, 12, 12, 13, 13, 10, 10, 1…
    ## $ mplbir   <dbl+lbl> 47, 47, 47, 31, 31, 31, 30, 30, 30, 34, 34, 41, 41, 18, 1…
    ## $ nlbnl    <dbl> 0, 1, 2, 2, 3, 4, 2, 3, 4, 3, 4, 0, 1, 0, 1, 2, 2, 3, 2, 3, 0…
    ## $ gestat   <dbl> 24, 42, 39, 41, 37, 40, 41, 40, 39, 39, 38, 43, 37, 40, 41, 4…
    ## $ birwt    <dbl> 2790, 2693, 3600, 2778, 2835, 3402, 2948, 3487, 3345, 2880, 3…
    ## $ cigs     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 99, 40, 0, 0, 99, 20, 10, 0, 0, 0,…
    ## $ smoke    <dbl+lbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 0, 0, …
    ## $ male     <dbl+lbl> 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1, 0, 0, 1, 1, 1, …
    ## $ year     <dbl> 0, 1, 4, 2, 3, 5, 1, 3, 5, 0, 1, 0, 3, 0, 2, 3, 0, 2, 0, 3, 0…
    ## $ married  <dbl> 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ hsgrad   <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ somecoll <dbl> 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0, 0, 1, 1, 0, 0, 0…
    ## $ collgrad <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1…
    ## $ magesq   <dbl> 256, 289, 400, 529, 576, 676, 1296, 1444, 1521, 900, 1024, 52…
    ## $ black    <dbl+lbl> 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, …
    ## $ kessner2 <dbl> 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0…
    ## $ kessner3 <dbl> 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ novisit  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pretri2  <dbl> 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0…
    ## $ pretri3  <dbl> 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…

# Ejercicio 3. Crear subconjuntos de datos

## Filtrar casos por una condicion

``` r
#------------------------------------------------------------------------------
# filtrar casos
#------------------------------------------------------------------------------

#--------------------------------------
# seleccionar casos con filter
#--------------------------------------

library(dplyr)
data_first_born <- data_smoking %>%
                   dplyr::filter(idx == 1) %>%
                   mutate(kg = birwt/1000)

# Nota: seleccionamos los datos del primer nacido.
#       esto nos garantiza de que tengamos datos independientes.
#       De lo contrario, tendriamos nacidos que provienen de las mismas
#       madres.

#--------------------------------------
# seleccionar casos con codigo base
#--------------------------------------

data_first_base <- data_smoking[data_smoking$idx==1,]
```

## Seleccionar Columnas

``` r
#------------------------------------------------------------------------------
# seleccionar variables
#------------------------------------------------------------------------------

#--------------------------------------
# seleccionar variables
#--------------------------------------

data_selected <- data_first_born %>%
dplyr::select(
    kg,        # peso al nacer en kilogramos
    mage,      # edad de la madre al nacimiento del recien nacido
    hsgrad,    # escolaridad: terminó educación formal
    somecoll,  # escolaridad: cuenta con algunos años de escolaridad terciaria
    collgrad,  # escolaridad: cuenta con estudios terciarios finalizados
    black,     # madre de color
    novisit,   # sin visita de control prenatal (1 = sin visitas, 0 = con visitas)
    smoke      # fuma
    ) %>%
dplyr::glimpse()
```

    ## Rows: 3,978
    ## Columns: 8
    ## $ kg       <dbl> 2.790, 2.778, 2.948, 2.880, 3.714, 3.203, 3.450, 3.345, 2.892…
    ## $ mage     <dbl> 16, 23, 36, 30, 23, 20, 25, 34, 30, 28, 29, 26, 21, 29, 23, 2…
    ## $ hsgrad   <dbl> 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 1, 0…
    ## $ somecoll <dbl> 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1…
    ## $ collgrad <dbl> 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0…
    ## $ black    <dbl+lbl> 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ novisit  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ smoke    <dbl+lbl> 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, …

``` r
#--------------------------------------
# seleccionar casos con codigo base
#--------------------------------------

data_selected_base <- data_first_born[,c('kg','mage', 'hsgrad', 'somecoll', 'collgrad', 'black', 'novisit', 'smoke')]
```

## Crear muestra de datos `dplyr::slice_sample()`

``` r
#------------------------------------------------------------------------------
# muestreo de casos
#------------------------------------------------------------------------------

#--------------------------------------
# fijar seed
#--------------------------------------

set.seed(20230309)

#--------------------------------------
# sample
#--------------------------------------

data_n500 <- data_first_born %>%
             dplyr::slice_sample(n = 500)

data_prop_20 <- data_first_born %>%
                dplyr::slice_sample(prop = .20)
```

## Crear muestra de datos por grupo `dplyr::slice_sample(data = ., by = 'grupo', prop = .2)`

``` r
#------------------------------------------------------------------------------
# muestreo de casos
#------------------------------------------------------------------------------

#--------------------------------------
# fijar seed
#--------------------------------------

set.seed(20230309)

#--------------------------------------
# frecuencia
#--------------------------------------

dplyr::count(data_first_born, smoke)
```

    ## # A tibble: 2 × 2
    ##   smoke             n
    ##   <dbl+lbl>     <int>
    ## 1 0 [Nonsmoker]  3417
    ## 2 1 [Smoker]      561

``` r
#--------------------------------------
# balanced sample
#--------------------------------------

data_balance <- data_first_born %>%
                dplyr::slice_sample(by = 'smoke', n = 500)


dplyr::count(data_balance, smoke)
```

    ## # A tibble: 2 × 2
    ##   smoke             n
    ##   <dbl+lbl>     <int>
    ## 1 0 [Nonsmoker]   500
    ## 2 1 [Smoker]      500

``` r
#--------------------------------------
# balanced sample
#--------------------------------------

data_prop <- data_first_born %>%
             dplyr::slice_sample(by = 'smoke', prop = .50)


dplyr::count(data_prop, smoke)
```

    ## # A tibble: 2 × 2
    ##   smoke             n
    ##   <dbl+lbl>     <int>
    ## 1 0 [Nonsmoker]  1708
    ## 2 1 [Smoker]      280

# Ejercicio 4. Revisar tabla

## Contar casos segun condicion `dplyr::count()`

``` r
#------------------------------------------------------------------------------
# frecuencia de casos
#------------------------------------------------------------------------------

#--------------------------------------
# frecuencia
#--------------------------------------

dplyr::count(data_first_born, smoke)
```

    ## # A tibble: 2 × 2
    ##   smoke             n
    ##   <dbl+lbl>     <int>
    ## 1 0 [Nonsmoker]  3417
    ## 2 1 [Smoker]      561

``` r
#--------------------------------------
# balanced sample, frecuencia
#--------------------------------------

dplyr::count(data_balance, smoke)
```

    ## # A tibble: 2 × 2
    ##   smoke             n
    ##   <dbl+lbl>     <int>
    ## 1 0 [Nonsmoker]   500
    ## 2 1 [Smoker]      500

``` r
#--------------------------------------
# proportional sample, frecuencia
#--------------------------------------

dplyr::count(data_prop, smoke)
```

    ## # A tibble: 2 × 2
    ##   smoke             n
    ##   <dbl+lbl>     <int>
    ## 1 0 [Nonsmoker]  1708
    ## 2 1 [Smoker]      280

## Tabla de frecuencia

``` r
#------------------------------------------------------------------------------
# frecuencia de casos
#------------------------------------------------------------------------------

#--------------------------------------
# frecuencia
#--------------------------------------

dplyr::count(data_first_born, smoke)
```

    ## # A tibble: 2 × 2
    ##   smoke             n
    ##   <dbl+lbl>     <int>
    ## 1 0 [Nonsmoker]  3417
    ## 2 1 [Smoker]      561

``` r
#--------------------------------------
# balanced sample, frecuencia
#--------------------------------------

dplyr::count(data_balance, smoke)
```

    ## # A tibble: 2 × 2
    ##   smoke             n
    ##   <dbl+lbl>     <int>
    ## 1 0 [Nonsmoker]   500
    ## 2 1 [Smoker]      500

``` r
#--------------------------------------
# proportional sample, frecuencia
#--------------------------------------

dplyr::count(data_prop, smoke)
```

    ## # A tibble: 2 × 2
    ##   smoke             n
    ##   <dbl+lbl>     <int>
    ## 1 0 [Nonsmoker]  1708
    ## 2 1 [Smoker]      280

## Inspeccionar muestra de casos

``` r
#------------------------------------------------------------------------------
# inspeccionar datos
#------------------------------------------------------------------------------

#--------------------------------------
# glimpse
#--------------------------------------

dplyr::glimpse(data_first_born)
```

    ## Rows: 3,978
    ## Columns: 25
    ## $ momid    <dbl> 14, 25, 39, 48, 60, 71, 73, 86, 110, 115, 138, 142, 151, 156,…
    ## $ idx      <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ stateres <dbl+lbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ mage     <dbl> 16, 23, 36, 30, 23, 20, 25, 34, 30, 28, 29, 26, 21, 29, 23, 2…
    ## $ meduc    <dbl> 10, 11, 14, 12, 13, 10, 14, 17, 16, 17, 17, 14, 12, 17, 12, 1…
    ## $ mplbir   <dbl+lbl> 47, 31, 30, 34, 41, 18, 47, 17, 18, 41, 37,  4, 18, 22, 4…
    ## $ nlbnl    <dbl> 0, 2, 2, 3, 0, 0, 2, 2, 0, 0, 0, 1, 1, 0, 0, 1, 3, 0, 1, 1, 1…
    ## $ gestat   <dbl> 24, 41, 41, 39, 43, 40, 41, 38, 39, 40, 39, 39, 43, 38, 40, 4…
    ## $ birwt    <dbl> 2790, 2778, 2948, 2880, 3714, 3203, 3450, 3345, 2892, 3880, 3…
    ## $ cigs     <dbl> 0, 0, 0, 99, 0, 99, 0, 0, 0, 0, 0, 0, 5, 0, 0, 10, 0, 0, 0, 2…
    ## $ smoke    <dbl+lbl> 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, …
    ## $ male     <dbl+lbl> 0, 1, 1, 1, 0, 1, 1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 0, 1, …
    ## $ year     <dbl> 0, 2, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ married  <dbl> 0, 0, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ hsgrad   <dbl> 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 1, 0…
    ## $ somecoll <dbl> 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1…
    ## $ collgrad <dbl> 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0…
    ## $ magesq   <dbl> 256, 529, 1296, 900, 529, 400, 625, 1156, 900, 784, 841, 676,…
    ## $ black    <dbl+lbl> 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ kessner2 <dbl> 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0…
    ## $ kessner3 <dbl> 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ novisit  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pretri2  <dbl> 0, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0…
    ## $ pretri3  <dbl> 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ kg       <dbl> 2.790, 2.778, 2.948, 2.880, 3.714, 3.203, 3.450, 3.345, 2.892…

``` r
dplyr::glimpse(data_balance)
```

    ## Rows: 1,000
    ## Columns: 25
    ## $ momid    <dbl> 25641, 21074, 5909, 14595, 38536, 27191, 66553, 3636, 48145, …
    ## $ idx      <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ stateres <dbl+lbl>  8, 50, 16, 35, 31, 12, 38, 10, 50, 23, 34, 29, 29,  4,  …
    ## $ mage     <dbl> 20, 18, 21, 27, 32, 23, 32, 27, 33, 27, 33, 23, 22, 23, 37, 3…
    ## $ meduc    <dbl> 12, 10, 12, 16, 16, 14, 16, 16, 14, 16, 16, 14, 11, 13, 16, 1…
    ## $ mplbir   <dbl+lbl> 41, 26, 10, 27,  8, 51, 28, 12, 28,  6, 40, 20, 31, 21, 1…
    ## $ nlbnl    <dbl> 1, 1, 0, 1, 1, 0, 1, 0, 0, 0, 0, 1, 3, 0, 3, 0, 0, 4, 0, 1, 1…
    ## $ gestat   <dbl> 40, 37, 33, 39, 39, 43, 39, 39, 38, 39, 37, 41, 38, 40, 42, 4…
    ## $ birwt    <dbl> 3260, 3204, 3374, 3714, 3115, 2999, 3610, 3487, 3459, 2450, 2…
    ## $ cigs     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ smoke    <dbl+lbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ male     <dbl+lbl> 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 1, 1, 0, 1, 1, 1, 1, 1, 0, …
    ## $ year     <dbl> 1, 0, 0, 0, 1, 1, 2, 0, 1, 1, 2, 1, 0, 0, 0, 0, 2, 2, 1, 1, 1…
    ## $ married  <dbl> 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ hsgrad   <dbl> 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ somecoll <dbl> 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 1…
    ## $ collgrad <dbl> 0, 0, 0, 1, 1, 0, 1, 1, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0, 1, 0…
    ## $ magesq   <dbl> 400, 324, 441, 729, 1024, 529, 1024, 729, 1089, 729, 1089, 52…
    ## $ black    <dbl+lbl> 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ kessner2 <dbl> 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ kessner3 <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ novisit  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pretri2  <dbl> 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pretri3  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ kg       <dbl> 3.260, 3.204, 3.374, 3.714, 3.115, 2.999, 3.610, 3.487, 3.459…

``` r
dplyr::glimpse(data_prop)
```

    ## Rows: 1,988
    ## Columns: 25
    ## $ momid    <dbl> 413, 16411, 69495, 19872, 50084, 89045, 23226, 10590, 48962, …
    ## $ idx      <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ stateres <dbl+lbl>  1, 39, 44, 47,  2, 38,  3, 26, 51, 10, 19, 25, 25, 34, 1…
    ## $ mage     <dbl> 32, 20, 29, 24, 25, 30, 28, 31, 32, 28, 34, 22, 20, 33, 32, 3…
    ## $ meduc    <dbl> 16, 12, 16, 16, 14, 11, 12, 16, 12, 16, 15, 14, 12, 17, 16, 1…
    ## $ mplbir   <dbl+lbl> 15, 37, 35, 19, 28, 16, 51, 31, 24, 32, 39, 37, 41,  6, 1…
    ## $ nlbnl    <dbl> 0, 0, 0, 0, 0, 5, 0, 3, 2, 0, 1, 0, 1, 0, 0, 0, 0, 2, 1, 1, 0…
    ## $ gestat   <dbl> 39, 39, 41, 39, 39, 40, 41, 36, 40, 39, 38, 41, 41, 40, 39, 4…
    ## $ birwt    <dbl> 3629, 3155, 3430, 3480, 3911, 3544, 3629, 3884, 3657, 4111, 2…
    ## $ cigs     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ smoke    <dbl+lbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ male     <dbl+lbl> 0, 1, 0, 0, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1, …
    ## $ year     <dbl> 0, 0, 2, 0, 2, 3, 1, 2, 1, 0, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1…
    ## $ married  <dbl> 1, 0, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ hsgrad   <dbl> 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1…
    ## $ somecoll <dbl> 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0…
    ## $ collgrad <dbl> 1, 0, 1, 1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 1, 0, 1, 0, 1, 0, 0…
    ## $ magesq   <dbl> 1024, 400, 841, 576, 625, 900, 784, 961, 1024, 784, 1156, 484…
    ## $ black    <dbl+lbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, …
    ## $ kessner2 <dbl> 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1…
    ## $ kessner3 <dbl> 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ novisit  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pretri2  <dbl> 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1…
    ## $ pretri3  <dbl> 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ kg       <dbl> 3.629, 3.155, 3.430, 3.480, 3.911, 3.544, 3.629, 3.884, 3.657…

# Ejercicio 5. Extrear valores

## Tabla de datos como matriz

``` r
#------------------------------------------------------------------------------
# datos
#------------------------------------------------------------------------------

#----------------------------------------------------------
# tabla 3.2
#----------------------------------------------------------

data_table_3_2 <- read.table(
text="
person  y x x_q xy
1 2 8 64  16
2 3 9 81  27
3 3 9 81  27
4 4 10  100 40
5 7 6 36  42
6 5 7 49  35
7 5 4 16  20
8 7 5 25  35
9 8 3 9 24
10  9 1 1 9
11  9 2 4 18
12  10  2 4 20

",
header=TRUE, stringsAsFactors = FALSE)

#--------------------------------------
# mostrar tabla
#--------------------------------------

knitr::kable(data_table_3_2)
```

| person |   y |   x | x_q |  xy |
|-------:|----:|----:|----:|----:|
|      1 |   2 |   8 |  64 |  16 |
|      2 |   3 |   9 |  81 |  27 |
|      3 |   3 |   9 |  81 |  27 |
|      4 |   4 |  10 | 100 |  40 |
|      5 |   7 |   6 |  36 |  42 |
|      6 |   5 |   7 |  49 |  35 |
|      7 |   5 |   4 |  16 |  20 |
|      8 |   7 |   5 |  25 |  35 |
|      9 |   8 |   3 |   9 |  24 |
|     10 |   9 |   1 |   1 |   9 |
|     11 |   9 |   2 |   4 |  18 |
|     12 |  10 |   2 |   4 |  20 |

``` r
#--------------------------------------
# extraer valores de tabla, empleando coordenadas
#--------------------------------------

# valor 12, de la variable y
data_table_3_2[12, 'y']
```

    ## [1] 10

``` r
# valor 10, de la variable x
data_table_3_2[12, 'x']
```

    ## [1] 2

``` r
# valor 45, de la variable smoke
data_first_born[45, 'smoke']
```

    ## # A tibble: 1 × 1
    ##   smoke        
    ##   <dbl+lbl>    
    ## 1 0 [Nonsmoker]

# Ejercicio 6. Descriptivos

## Tabla de frecuencia

``` r
#------------------------------------------------------------------------------
# tabla cruzada
#------------------------------------------------------------------------------

#--------------------------------------
# frecuencia
#--------------------------------------

data_balance %>%
dplyr::count(smoke, collgrad)
```

    ## # A tibble: 4 × 3
    ##   smoke         collgrad     n
    ##   <dbl+lbl>        <dbl> <int>
    ## 1 0 [Nonsmoker]        0   284
    ## 2 0 [Nonsmoker]        1   216
    ## 3 1 [Smoker]           0   461
    ## 4 1 [Smoker]           1    39

``` r
#--------------------------------------
# tabla cruzada
#--------------------------------------

data_balance %>%
xtabs(~ smoke + collgrad, data = .)
```

    ##      collgrad
    ## smoke   0   1
    ##     0 284 216
    ##     1 461  39

## Tabla de porcentajes

``` r
#------------------------------------------------------------------------------
# tabla cruzada
#------------------------------------------------------------------------------

#--------------------------------------
# mostrar tabla
#--------------------------------------

data_balance %>%
xtabs(~ smoke + collgrad, data = .) %>%
proportions(., 1)
```

    ##      collgrad
    ## smoke     0     1
    ##     0 0.568 0.432
    ##     1 0.922 0.078

## Descriptivos de tendencia central

``` r
#------------------------------------------------------------------------------
# descriptivos
#------------------------------------------------------------------------------

#----------------------------------------------------------
# url datos
#----------------------------------------------------------

url_location <- url('https://github.com/dacarras/psi2301_2023_tarea_test/raw/main/ingresos_2016.rds')

#--------------------------------------
# abrir datos
#--------------------------------------

data_inc <- readRDS(url_location)


# -------------------------------------
# sacar valores no válidos
# -------------------------------------

data_model <- data_inc %>%
              mutate(year_edu = as.numeric(na_if(edu,- 88)))

#--------------------------------------
# función para obtener moda
#--------------------------------------

# función para obtener moda
mode <- function(v) {
   uniqv <- unique(v)
   uniqv[which.max(tabulate(match(v, uniqv)))]
# source: https://www.tutorialspoint.com/r/r_mean_median_mode.htm
}


#--------------------------------------
# tendencia central
#--------------------------------------

data_model %>%
summarize(
moda    = mode(hinc),
mediana = median(hinc, na.rm = TRUE),
media   = mean(hinc, na.rm = TRUE)
) %>%
knitr::kable(., digits = 2)
```

| moda | mediana |  media |
|-----:|--------:|-------:|
|  150 |  307.63 | 502.87 |

## Descriptivos de posicion (e.g., percentiles)

``` r
#------------------------------------------------------------------------------
# descriptivos
#------------------------------------------------------------------------------

#--------------------------------------
# percentiles
#--------------------------------------

data_model %>%
summarize(
percentil_25 = quantile(hinc, probs = .25, na.rm = TRUE),
percentil_50 = quantile(hinc, probs = .50, na.rm = TRUE),
percentil_75 = quantile(hinc, probs = .75, na.rm = TRUE)
) %>%
knitr::kable(., digits = 2)
```

| percentil_25 | percentil_50 | percentil_75 |
|-------------:|-------------:|-------------:|
|       179.09 |       307.63 |       580.77 |

## Descriptivos de variabilidad

``` r
#------------------------------------------------------------------------------
# descriptivos
#------------------------------------------------------------------------------

# -------------------------------------
# medidas de variabilidad
# -------------------------------------

data_model %>%
summarize(
minimo = min(hinc, na.rm = TRUE),
maximo = max(hinc, na.rm = TRUE),
percentil_25 = quantile(hinc, probs = .25, na.rm = TRUE),
percentil_75 = quantile(hinc, probs = .75, na.rm = TRUE),
desviacion_estandar = sd(hinc, na.rm = TRUE)
) %>%
mutate(rango = maximo - minimo) %>%
mutate(rango_intercuartil = percentil_75 - percentil_25) %>%
knitr::kable(., digits = 2)
```

| minimo |  maximo | percentil_25 | percentil_75 | desviacion_estandar |   rango | rango_intercuartil |
|-------:|--------:|-------------:|-------------:|--------------------:|--------:|-------------------:|
|      0 | 6663.79 |       179.09 |       580.77 |              604.29 | 6663.79 |             401.67 |

## Asimetria de distribuciones

``` r
#------------------------------------------------------------------------------
# descriptivos
#------------------------------------------------------------------------------

# -------------------------------------
# peso del primer hijo
# -------------------------------------

hist(data_first_born$kg)
moments::skewness(data_first_born$kg, na.rm = TRUE)

# -------------------------------------
# ingresos de los hogares
# -------------------------------------

hist(data_model$hinc)
moments::skewness(data_model$hinc, na.rm = TRUE)

# -------------------------------------
# apoyo a la equidad de genero
# -------------------------------------

hist(psi2301::iccs_09_chl$GENEQL)
moments::skewness(psi2301::iccs_09_chl$GENEQL, na.rm = TRUE)
```
