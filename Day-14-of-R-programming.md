Day 14 of R Programming
================
2026-05-14

Today, I am learning about how to reshape the data using pivot
functions.

## 1. Creating a wide data

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.1     ✔ stringr   1.5.2
    ## ✔ ggplot2   4.0.0     ✔ tibble    3.3.0
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.1.0     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
kata_scores_wide <- tibble(
  players = c("A", "B", "C", "D"),
  j_1 = c(7.5, 8.2, 6.9, 8.5),
  j_2 = c(7.8, 8.0, 7.1, 8.4),
  j_3 = c(7.4, 8.5, 6.8, 8.8)
)

kata_scores_wide
```

    ## # A tibble: 4 × 4
    ##   players   j_1   j_2   j_3
    ##   <chr>   <dbl> <dbl> <dbl>
    ## 1 A         7.5   7.8   7.4
    ## 2 B         8.2   8     8.5
    ## 3 C         6.9   7.1   6.8
    ## 4 D         8.5   8.4   8.8

## 2. pivot_longer()

``` r
kata_scores_long <- kata_scores_wide %>%
  pivot_longer(
    cols = c(j_1, j_2, j_3),
    names_to = "judge",
    values_to = "score"
  )

kata_scores_long
```

    ## # A tibble: 12 × 3
    ##    players judge score
    ##    <chr>   <chr> <dbl>
    ##  1 A       j_1     7.5
    ##  2 A       j_2     7.8
    ##  3 A       j_3     7.4
    ##  4 B       j_1     8.2
    ##  5 B       j_2     8  
    ##  6 B       j_3     8.5
    ##  7 C       j_1     6.9
    ##  8 C       j_2     7.1
    ##  9 C       j_3     6.8
    ## 10 D       j_1     8.5
    ## 11 D       j_2     8.4
    ## 12 D       j_3     8.8

## 3. pivot_wider()

Making the long data back to same wide data.

``` r
kata_wide <- kata_scores_long %>% 
  pivot_wider(
    names_from = judge,
    values_from = score
  )

kata_wide
```

    ## # A tibble: 4 × 4
    ##   players   j_1   j_2   j_3
    ##   <chr>   <dbl> <dbl> <dbl>
    ## 1 A         7.5   7.8   7.4
    ## 2 B         8.2   8     8.5
    ## 3 C         6.9   7.1   6.8
    ## 4 D         8.5   8.4   8.8

## 4. Analyzing the long data

``` r
kata_scores_long %>% 
  group_by(players) %>% 
  summarize(final_score = mean(score)) %>% 
  arrange(desc(final_score))
```

    ## # A tibble: 4 × 2
    ##   players final_score
    ##   <chr>         <dbl>
    ## 1 D              8.57
    ## 2 B              8.23
    ## 3 A              7.57
    ## 4 C              6.93

## 5. Cleaning the data

``` r
clean_data <-  kata_scores_wide %>% 
  pivot_longer(
    cols = starts_with("j"),
    names_to = "judge_number",
    values_to = "score"
  ) %>% 
  mutate(
    judge_number = str_replace(judge_number, "j_", "")
  )

clean_data
```

    ## # A tibble: 12 × 3
    ##    players judge_number score
    ##    <chr>   <chr>        <dbl>
    ##  1 A       1              7.5
    ##  2 A       2              7.8
    ##  3 A       3              7.4
    ##  4 B       1              8.2
    ##  5 B       2              8  
    ##  6 B       3              8.5
    ##  7 C       1              6.9
    ##  8 C       2              7.1
    ##  9 C       3              6.8
    ## 10 D       1              8.5
    ## 11 D       2              8.4
    ## 12 D       3              8.8
