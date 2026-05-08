Day 8 of R Programming
================
2026-05-08

We are done with the Phase-1 successfully. Moving on to Phase-2, where
we will see about the Data Manipulation techniques using Tidyverse
package.

## 1. Important Operations in Tidyverse

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.5.3

    ## Warning: package 'dplyr' was built under R version 4.5.2

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
starwars
```

    ## # A tibble: 87 × 14
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Luke Sk…    172    77 blond      fair       blue            19   male  mascu…
    ##  2 C-3PO       167    75 <NA>       gold       yellow         112   none  mascu…
    ##  3 R2-D2        96    32 <NA>       white, bl… red             33   none  mascu…
    ##  4 Darth V…    202   136 none       white      yellow          41.9 male  mascu…
    ##  5 Leia Or…    150    49 brown      light      brown           19   fema… femin…
    ##  6 Owen La…    178   120 brown, gr… light      blue            52   male  mascu…
    ##  7 Beru Wh…    165    75 brown      light      blue            47   fema… femin…
    ##  8 R5-D4        97    32 <NA>       white, red red             NA   none  mascu…
    ##  9 Biggs D…    183    84 black      light      brown           24   male  mascu…
    ## 10 Obi-Wan…    182    77 auburn, w… fair       blue-gray       57   male  mascu…
    ## # ℹ 77 more rows
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

``` r
# as_tibble() is the modern dataset function for converting data.frame()

round(mean(c(10.5, 11, 24, 35)))
```

    ## [1] 20

``` r
c(10.5, 11, 24, 35) %>% 
  mean() %>% 
  round()
```

    ## [1] 20

``` r
tall_humans <- starwars %>%         
  filter(species == "Human") %>%     
  filter(height > 180) %>%            
  select(name, homeworld, height)   

tall_humans
```

    ## # A tibble: 15 × 3
    ##    name                homeworld    height
    ##    <chr>               <chr>         <int>
    ##  1 Darth Vader         Tatooine        202
    ##  2 Biggs Darklighter   Tatooine        183
    ##  3 Obi-Wan Kenobi      Stewjon         182
    ##  4 Anakin Skywalker    Tatooine        188
    ##  5 Boba Fett           Kamino          183
    ##  6 Qui-Gon Jinn        <NA>            193
    ##  7 Padmé Amidala       Naboo           185
    ##  8 Ric Olié            Naboo           183
    ##  9 Quarsh Panaka       Naboo           183
    ## 10 Mace Windu          Haruun Kal      188
    ## 11 Cliegg Lars         Tatooine        183
    ## 12 Dooku               Serenno         193
    ## 13 Bail Prestor Organa Alderaan        191
    ## 14 Jango Fett          Concord Dawn    183
    ## 15 Raymus Antilles     Alderaan        188

``` r
# %>% is the old tidyverse pipe
# |> is the new tidyverse pipe, both does the same thing
```
