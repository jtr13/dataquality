Missing Data Lab
================

## Find snowfall data

I need to know how much snow fell *per day* in New York State in
February 2017, on a county or more detailed level. I know some
government agency measures and reports snowfall and puts the data
online. Find and download the data. *Keep detailed records of every step
of the process so you can reproduce your process. Take screenshots if
necessary.*

## Find snowfall data

<https://www.ncdc.noaa.gov/snow-and-ice/daily-snow/>

## Study the data

1.  What variables do we
    have?

<!-- end list -->

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.1.0          ✔ purrr   0.3.0     
    ## ✔ tibble  2.0.1          ✔ dplyr   0.8.0     
    ## ✔ tidyr   0.8.2          ✔ stringr 1.4.0     
    ## ✔ readr   1.3.1          ✔ forcats 0.4.0.9000

    ## ── Conflicts ────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
# https://www.ncdc.noaa.gov/snow-and-ice/daily-snow/
# Accessed 2017-10-26
# Screenshot 2017-10-26 18.45.11.png
snow <- read_csv("NY-snowfall-201702.csv",
                 skip = 1)
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_character(),
    ##   Elevation = col_double(),
    ##   Latitude = col_double(),
    ##   Longitude = col_double()
    ## )

    ## See spec(...) for full column specifications.

``` r
glimpse(snow)
```

    ## Observations: 349
    ## Variables: 34
    ## $ `GHCN ID`      <chr> "USC00300023", "US1NYER0085", "US1NYAB0023", "USW…
    ## $ `Station Name` <chr> "ADDISON", "AKRON 2.4 S", "ALBANY 0.7 SW", "ALBAN…
    ## $ County         <chr> "STEUBEN", "ERIE", "ALBANY", "ALBANY", "ALBANY", …
    ## $ Elevation      <dbl> 999, 824, 256, 312, 607, 1706, 1667, 1500, 1460, …
    ## $ Latitude       <dbl> -77.23, -78.49, -73.81, -73.81, -73.93, -77.76, -…
    ## $ Longitude      <dbl> 42.10, 42.99, 42.66, 42.74, 42.47, 42.25, 42.16, …
    ## $ `Feb 1`        <chr> "2.6", "2.2", "1.5", "1.3", "2.5", "3.0", "3.0", …
    ## $ `Feb 2`        <chr> "0.4", "M", "T", "T", "M", "0.5", "2.8", "1.0", "…
    ## $ `Feb 3`        <chr> "0.0", "M", "T", "0.0", "M", "0.4", "0.5", "0.0",…
    ## $ `Feb 4`        <chr> "0.0", "M", "0.0", "T", "M", "0.2", "0.4", "0.0",…
    ## $ `Feb 5`        <chr> "M", "M", "T", "T", "M", "0.0", "T", "0.0", "T", …
    ## $ `Feb 6`        <chr> "0.0", "M", "0.0", "T", "M", "0.4", "0.1", "0.0",…
    ## $ `Feb 7`        <chr> "M", "M", "0.0", "0.3", "M", "0.0", "M", "M", "0.…
    ## $ `Feb 8`        <chr> "M", "M", "0.4", "0.0", "M", "0.0", "M", "0.0", "…
    ## $ `Feb 9`        <chr> "3.7", "M", "5.5", "11.2", "5.0", "3.2", "2.5", "…
    ## $ `Feb 10`       <chr> "0.8", "M", "4.9", "1.0", "4.5", "0.5", "1.0", "2…
    ## $ `Feb 11`       <chr> "0.8", "M", "1.5", "0.8", "1.6", "0.4", "0.6", "0…
    ## $ `Feb 12`       <chr> "M", "M", "T", "7.6", "M", "0.0", "M", "0.0", "0.…
    ## $ `Feb 13`       <chr> "0.0", "M", "7.5", "T", "7.0", "1.6", "2.7", "2.0…
    ## $ `Feb 14`       <chr> "0.0", "M", "T", "T", "M", "0.4", "0.4", "0.0", "…
    ## $ `Feb 15`       <chr> "0.0", "M", "0.0", "T", "M", "1.1", "2.4", "2.0",…
    ## $ `Feb 16`       <chr> "3.9", "M", "0.3", "T", "M", "1.9", "3.0", "6.0",…
    ## $ `Feb 17`       <chr> "0.0", "M", "T", "T", "M", "0.2", "0.8", "0.0", "…
    ## $ `Feb 18`       <chr> "M", "M", "0.0", "0.0", "M", "0.0", "0.0", "0.0",…
    ## $ `Feb 19`       <chr> "M", "M", "0.0", "0.0", "M", "0.0", "0.0", "0.0",…
    ## $ `Feb 20`       <chr> "M", "M", "0.0", "0.0", "M", "0.0", "0.0", "0.0",…
    ## $ `Feb 21`       <chr> "M", "M", "0.0", "0.0", "M", "0.0", "0.0", "0.0",…
    ## $ `Feb 22`       <chr> "M", "M", "0.0", "0.0", "M", "0.0", "M", "0.0", "…
    ## $ `Feb 23`       <chr> "M", "M", "0.0", "M", "M", "0.0", "M", "0.0", "0.…
    ## $ `Feb 24`       <chr> "M", "M", "0.0", "0.0", "M", "0.0", "M", "0.0", "…
    ## $ `Feb 25`       <chr> "M", "M", "0.0", "0.0", "M", "0.0", "M", "0.0", "…
    ## $ `Feb 26`       <chr> "0.0", "M", "T", "T", "M", "1.0", "1.0", "0.0", "…
    ## $ `Feb 27`       <chr> "0.2", "M", "T", "0.0", "M", "0.0", "T", "0.0", "…
    ## $ `Feb 28`       <chr> "M", "M", "0.0", "0.0", "M", "0.0", "0.0", "0.0",…

2.  What is GHCN ID? What is the meaning of the characters?

GHCN stands for Global Historical Climate Network. Each `GNCN ID`
represents a unique weather station. The complete list of stations can
be found here:
<https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt>

<https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/readme.txt>

3.  What do non-numeric codes in the day columns mean?

`M` = Missing

`T` = Trace

Source: <https://www.ncdc.noaa.gov/snow-and-ice/daily-snow/>

## Mark missing data as NA

  - Indicate NA string when reading the data

<!-- end list -->

``` r
snow <- read_csv("NY-snowfall-201702.csv",
                 skip = 1,
                 na = "M")
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_character(),
    ##   Elevation = col_double(),
    ##   Latitude = col_double(),
    ##   Longitude = col_double(),
    ##   `Feb 19` = col_double(),
    ##   `Feb 20` = col_double(),
    ##   `Feb 21` = col_double(),
    ##   `Feb 22` = col_double(),
    ##   `Feb 23` = col_double(),
    ##   `Feb 25` = col_double()
    ## )

    ## See spec(...) for full column specifications.

4.  Use a heatmap style function to look for patterns in missing data.
    What do you
observe?

<!-- end list -->

  - mi::image(missing\_data.frame())

  - extracat::visna()

  - ggplot2::geom\_tile()

<!-- end list -->

``` r
extracat::visna(snow, sort = "b")
```

![](MissingDataLab-Solutions_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

5.  Does the number of missing values vary by county?

Yes

``` r
theme_dotplot <- theme_bw(16) +
  theme(axis.ticks.y = element_blank(),
        panel.grid.major.x = element_blank(),
        panel.grid.major.y = element_line(size = 0.5),
        panel.grid.minor.x = element_blank())


tidysnow <- snow %>% 
  select(`Station Name`, County, `Feb 1`:`Feb 28`) %>%
  gather(key = Day, value = Snowfall, -`Station Name`, -County)

tidysnow %>% group_by(County) %>% 
  summarize(Missing = sum(is.na(Snowfall))/n()) %>% 
  ggplot(aes(Missing, fct_reorder(County, Missing))) + 
           geom_point() + theme_dotplot
```

![](MissingDataLab-Solutions_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

6.  Does the number of missing values vary by day of the month?

7.  Does the number of missing values vary by type of day (weekday vs
    weekend)?

8.  Does the number of missing values vary by average snowfall?

9.  What is your overall conclusion regarding data quality?
