Day 12 of R Programming
================
2026-05-12

Today, I am learning about how to clean the dataset and handle the
missing values.

## 1. Sample messy Dataset:

``` r
library(tibble)
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.5.3

    ## Warning: package 'dplyr' was built under R version 4.5.2

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ purrr     1.1.0
    ## ✔ forcats   1.0.1     ✔ readr     2.1.5
    ## ✔ ggplot2   4.0.0     ✔ stringr   1.5.2
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
messy_data <- tibble(
  student_id = 1:5,
  name = c("Alex", "Maria", NA, "Zoe", "Liam"),
  score = c(85, NA, 78, 90, NA),
  status = c("Pass", "Fail", "Pass", NA, "Pass")
)

messy_data
```

    ## # A tibble: 5 × 4
    ##   student_id name  score status
    ##        <int> <chr> <dbl> <chr> 
    ## 1          1 Alex     85 Pass  
    ## 2          2 Maria    NA Fail  
    ## 3          3 <NA>     78 Pass  
    ## 4          4 Zoe      90 <NA>  
    ## 5          5 Liam     NA Pass

## 2. Checking for missing values

``` r
messy_data %>% 
  filter(is.na(name))
```

    ## # A tibble: 1 × 4
    ##   student_id name  score status
    ##        <int> <chr> <dbl> <chr> 
    ## 1          3 <NA>     78 Pass

``` r
messy_data %>% 
  filter(!is.na(name))
```

    ## # A tibble: 4 × 4
    ##   student_id name  score status
    ##        <int> <chr> <dbl> <chr> 
    ## 1          1 Alex     85 Pass  
    ## 2          2 Maria    NA Fail  
    ## 3          4 Zoe      90 <NA>  
    ## 4          5 Liam     NA Pass

``` r
colSums(is.na(messy_data))
```

    ## student_id       name      score     status 
    ##          0          1          2          1

## 3. Dropping the missing data

``` r
clean_data <- messy_data %>% 
  drop_na()

clean_data
```

    ## # A tibble: 1 × 4
    ##   student_id name  score status
    ##        <int> <chr> <dbl> <chr> 
    ## 1          1 Alex     85 Pass

## 4. Replacing missing data

``` r
fixed_data <- messy_data %>% 
  mutate(
    score = replace_na(score, 0),
    name = replace_na(name, "Unknown Student"),
    status = replace_na(status, "Pending")
  )

fixed_data
```

    ## # A tibble: 5 × 4
    ##   student_id name            score status 
    ##        <int> <chr>           <dbl> <chr>  
    ## 1          1 Alex               85 Pass   
    ## 2          2 Maria               0 Fail   
    ## 3          3 Unknown Student    78 Pass   
    ## 4          4 Zoe                90 Pending
    ## 5          5 Liam                0 Pass
