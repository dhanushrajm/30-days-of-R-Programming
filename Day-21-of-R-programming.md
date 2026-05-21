Day 21 of R Programming
================
2026-05-21

Today, I learn how to get the real time data using API keys.

``` r
library(tidyverse)
library(plotly)
library(httr2)
library(jsonlite)
```

## 1. Building the request

``` r
athens_req <- request("https://api.open-meteo.com/v1/forecast") %>% 
  req_url_query(
    latitude = 37.98,
    longitude = 23.72,
    current_weather = "true"
  )

athens_req
```

    ## <httr2_request>
    ## GET https://api.open-meteo.com/v1/forecast?latitude=37.98&longitude=23.72&current_weather=true
    ## Body: empty

## 2. Retrieve the data

``` r
athens_data <- athens_req %>% 
  req_perform() %>% 
  resp_body_json()

athens_data
```

    ## $latitude
    ## [1] 38
    ## 
    ## $longitude
    ## [1] 23.75
    ## 
    ## $generationtime_ms
    ## [1] 0.05030632
    ## 
    ## $utc_offset_seconds
    ## [1] 0
    ## 
    ## $timezone
    ## [1] "GMT"
    ## 
    ## $timezone_abbreviation
    ## [1] "GMT"
    ## 
    ## $elevation
    ## [1] 59
    ## 
    ## $current_weather_units
    ## $current_weather_units$time
    ## [1] "iso8601"
    ## 
    ## $current_weather_units$interval
    ## [1] "seconds"
    ## 
    ## $current_weather_units$temperature
    ## [1] "°C"
    ## 
    ## $current_weather_units$windspeed
    ## [1] "km/h"
    ## 
    ## $current_weather_units$winddirection
    ## [1] "°"
    ## 
    ## $current_weather_units$is_day
    ## [1] ""
    ## 
    ## $current_weather_units$weathercode
    ## [1] "wmo code"
    ## 
    ## 
    ## $current_weather
    ## $current_weather$time
    ## [1] "2026-05-21T14:15"
    ## 
    ## $current_weather$interval
    ## [1] 900
    ## 
    ## $current_weather$temperature
    ## [1] 24.9
    ## 
    ## $current_weather$windspeed
    ## [1] 6.5
    ## 
    ## $current_weather$winddirection
    ## [1] 180
    ## 
    ## $current_weather$is_day
    ## [1] 1
    ## 
    ## $current_weather$weathercode
    ## [1] 3

``` r
str(athens_data$current_weather)
```

    ## List of 7
    ##  $ time         : chr "2026-05-21T14:15"
    ##  $ interval     : int 900
    ##  $ temperature  : num 24.9
    ##  $ windspeed    : num 6.5
    ##  $ winddirection: int 180
    ##  $ is_day       : int 1
    ##  $ weathercode  : int 3

## 3. Converting it to Tibble Dataframe

``` r
weather_df <- as_tibble(athens_data$current_weather)

weather_df
```

    ## # A tibble: 1 × 7
    ##   time           interval temperature windspeed winddirection is_day weathercode
    ##   <chr>             <int>       <dbl>     <dbl>         <int>  <int>       <int>
    ## 1 2026-05-21T14…      900        24.9       6.5           180      1           3

## 4. One Full pipeline

``` r
live_data <- request("https://api.open-meteo.com/v1/forecast") %>% 
  req_url_query(
    latitude = 37.98,
    longitude = 23.72,
    current_weather = "true"
  ) %>% 
  req_perform() %>% 
  resp_body_json() %>% 
  pluck("current_weather") %>% 
  as_tibble()

live_data
```

    ## # A tibble: 1 × 7
    ##   time           interval temperature windspeed winddirection is_day weathercode
    ##   <chr>             <int>       <dbl>     <dbl>         <int>  <int>       <int>
    ## 1 2026-05-21T14…      900        24.9       6.5           180      1           3
