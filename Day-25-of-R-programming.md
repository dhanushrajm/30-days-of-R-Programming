Day 25 of R Programming
================
2026-05-25

Today, I learn how to make a dashboard using ‘flexdashboard’ package.

``` r
library(tidyverse)
library(flexdashboard)
library(plotly)
library(sf)
```

## 1. Simulating live satellite thermal anomaly data of last 12 hours

``` r
set.seed(42)
fire_data <- tibble(
  time = seq(Sys.time() - 43200, Sys.time(), by = "hour"),
  avg_temp_c = runif(13, 30, 42),
  fwi_index = runif(13, 20, 50),
  active_alerts = sample(0:3, 13, replace = TRUE)
)

head(fire_data)
```

    ## # A tibble: 6 × 4
    ##   time                avg_temp_c fwi_index active_alerts
    ##   <dttm>                   <dbl>     <dbl>         <int>
    ## 1 2026-05-25 07:48:25       41.0      27.7             0
    ## 2 2026-05-25 08:48:25       41.2      33.9             2
    ## 3 2026-05-25 09:48:25       33.4      48.2             0
    ## 4 2026-05-25 10:48:25       40.0      49.3             0
    ## 5 2026-05-25 11:48:25       37.7      23.5             3
    ## 6 2026-05-25 12:48:25       36.2      34.2             1

## 2. Extracting top current metrics:

``` r
current_temp <- round(last(fire_data$avg_temp_c), 1)
current_temp
```

    ## [1] 41.2

``` r
current_fwi <- round(last(fire_data$fwi_index), 1)
current_fwi
```

    ## [1] 35.4

``` r
total_alerts <- sum(fire_data$active_alerts)
total_alerts
```

    ## [1] 19
