Day 24 of R Programming
================
2026-05-24

Today, I am learning about the Functional Programming in R using purrr
package.

``` r
library(tidyverse)
```

## 1. Nested API-style Data:

``` r
kata_api_response <- list(
  list(athlete_id = 101, name = "Alex", style = "Shotokan", scores = c(8.5, 8.2, 8.8, 8.4)),
  list(athlete_id = 102, name = "Maria", style = "Shito-ryu", scores = c(7.9, 8.1, 8.0, 8.2)),
  list(athlete_id = 103, name = "John", style = "Wado-ryu", scores = c(9.0, 8.9, 9.2, 9.1))
)

str(kata_api_response)
```

    ## List of 3
    ##  $ :List of 4
    ##   ..$ athlete_id: num 101
    ##   ..$ name      : chr "Alex"
    ##   ..$ style     : chr "Shotokan"
    ##   ..$ scores    : num [1:4] 8.5 8.2 8.8 8.4
    ##  $ :List of 4
    ##   ..$ athlete_id: num 102
    ##   ..$ name      : chr "Maria"
    ##   ..$ style     : chr "Shito-ryu"
    ##   ..$ scores    : num [1:4] 7.9 8.1 8 8.2
    ##  $ :List of 4
    ##   ..$ athlete_id: num 103
    ##   ..$ name      : chr "John"
    ##   ..$ style     : chr "Wado-ryu"
    ##   ..$ scores    : num [1:4] 9 8.9 9.2 9.1

## 2. map() vs. map\_\*()

map() - always returns a list map_chr(), map_dbl(), map_lgl() -
type_safe variants of map()

``` r
names_vector <- map_chr(kata_api_response, "name")
print(names_vector)
```

    ## [1] "Alex"  "Maria" "John"

``` r
id_vector <- map_dbl(kata_api_response, "athlete_id")
print(id_vector)
```

    ## [1] 101 102 103

## 3. Anonymous Functions:

``` r
average_scores <- map_dbl(kata_api_response, \(x) mean(x$scores))

print(average_scores)
```

    ## [1] 8.475 8.050 9.050

## 4. List to Data Frames:

``` r
clean_kata_data <- tibble(
  id = map_dbl(kata_api_response, "athlete_id"),
  athlete = map_chr(kata_api_response, "name"),
  karate_style = map_chr(kata_api_response, "style"),
  final_score = map_dbl(kata_api_response, \(x) mean(x$scores))
)

clean_kata_data %>% arrange(desc(final_score))
```

    ## # A tibble: 3 × 4
    ##      id athlete karate_style final_score
    ##   <dbl> <chr>   <chr>              <dbl>
    ## 1   103 John    Wado-ryu            9.05
    ## 2   101 Alex    Shotokan            8.48
    ## 3   102 Maria   Shito-ryu           8.05
