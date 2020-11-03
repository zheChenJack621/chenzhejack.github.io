P8105-HW3-zc2556
================
Zhe Chen
2020/10/10

# NOAA

## Preparation

``` r
library(tidyverse)
```

    ## -- Attaching packages ---------------------------------------- tidyverse 1.3.0 --

    ## √ ggplot2 3.3.2     √ purrr   0.3.4
    ## √ tibble  3.0.3     √ dplyr   1.0.2
    ## √ tidyr   1.1.2     √ stringr 1.4.0
    ## √ readr   1.3.1     √ forcats 0.5.0

    ## -- Conflicts ------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(p8105.datasets)
library(plotly)
```

    ## 
    ## Attaching package: 'plotly'

    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     last_plot

    ## The following object is masked from 'package:stats':
    ## 
    ##     filter

    ## The following object is masked from 'package:graphics':
    ## 
    ##     layout

## Clean the Data

``` r
#import clean
data("ny_noaa")

noaa = ny_noaa %>%
  janitor::clean_names()

noaa = 
  noaa %>% 
  separate(date, into = c("year", "month", "day"), convert = TRUE) %>% 
  select(
    -id
  ) %>%
  filter(
    year >=1990 & year <= 2010
  )#keep interested time interval
```

``` r
#convert units
noaa = 
  noaa %>%  
  mutate(
      tmax = as.numeric(tmax),
      tmin = as.numeric(tmin),
      snow_mm = snow,
      snow = round(snow_mm * 0.03937 * 4) / 4)
```

This dataset documented over temperature from various weather stations.

## Plot
