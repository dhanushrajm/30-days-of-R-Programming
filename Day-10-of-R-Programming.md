Day 10 of R Programming
================
2026-05-10

Today, I am learning about the Mutation and Arranging the data using the
dplyr package.

In Day 8, I have been how to shrink the data. Today, it’s about growing
and organizing the data.

## 1. Creating new columns using mutate():

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
## adding a new column named bmi using the height(convert into meters) and mass

starwars %>% select(name, height, mass) %>% 
  mutate(height_m = height / 100, 
         bmi = mass/(height_m ^ 2))
```

    ## # A tibble: 87 × 5
    ##    name               height  mass height_m   bmi
    ##    <chr>               <int> <dbl>    <dbl> <dbl>
    ##  1 Luke Skywalker        172    77     1.72  26.0
    ##  2 C-3PO                 167    75     1.67  26.9
    ##  3 R2-D2                  96    32     0.96  34.7
    ##  4 Darth Vader           202   136     2.02  33.3
    ##  5 Leia Organa           150    49     1.5   21.8
    ##  6 Owen Lars             178   120     1.78  37.9
    ##  7 Beru Whitesun Lars    165    75     1.65  27.5
    ##  8 R5-D4                  97    32     0.97  34.0
    ##  9 Biggs Darklighter     183    84     1.83  25.1
    ## 10 Obi-Wan Kenobi        182    77     1.82  23.2
    ## # ℹ 77 more rows

## 2. special cases of mutate:

``` r
starwars %>% select(name, height, mass) %>% 
  mutate(
    height_category <- case_when(
      height < 150 ~ "Short",
      height >= 150 & height < 190 ~ "Average",
      height >= 190 ~ "Tall",
      TRUE ~ "Unknown"
    )
  )
```

    ## # A tibble: 87 × 4
    ##    name               height  mass `... <- NULL`
    ##    <chr>               <int> <dbl> <chr>        
    ##  1 Luke Skywalker        172    77 Average      
    ##  2 C-3PO                 167    75 Average      
    ##  3 R2-D2                  96    32 Short        
    ##  4 Darth Vader           202   136 Tall         
    ##  5 Leia Organa           150    49 Average      
    ##  6 Owen Lars             178   120 Average      
    ##  7 Beru Whitesun Lars    165    75 Average      
    ##  8 R5-D4                  97    32 Short        
    ##  9 Biggs Darklighter     183    84 Average      
    ## 10 Obi-Wan Kenobi        182    77 Average      
    ## # ℹ 77 more rows

## 3. arrange() - sorting the data

``` r
starwars %>% select(name, height, mass) %>% arrange(mass)
```

    ## # A tibble: 87 × 3
    ##    name                  height  mass
    ##    <chr>                  <int> <dbl>
    ##  1 Ratts Tyerel              79    15
    ##  2 Yoda                      66    17
    ##  3 Wicket Systri Warrick     88    20
    ##  4 R2-D2                     96    32
    ##  5 R5-D4                     97    32
    ##  6 Sebulba                  112    40
    ##  7 Padmé Amidala            185    45
    ##  8 Dud Bolt                  94    45
    ##  9 Wat Tambor               193    48
    ## 10 Sly Moore                178    48
    ## # ℹ 77 more rows

``` r
starwars %>% select(name, height, mass) %>% arrange(desc(mass))
```

    ## # A tibble: 87 × 3
    ##    name                  height  mass
    ##    <chr>                  <int> <dbl>
    ##  1 Jabba Desilijic Tiure    175  1358
    ##  2 Grievous                 216   159
    ##  3 IG-88                    200   140
    ##  4 Darth Vader              202   136
    ##  5 Tarfful                  234   136
    ##  6 Owen Lars                178   120
    ##  7 Bossk                    190   113
    ##  8 Chewbacca                228   112
    ##  9 Jek Tono Porkins         180   110
    ## 10 Dexter Jettster          198   102
    ## # ℹ 77 more rows

``` r
starwars %>% select(name, height, species, mass) %>% 
  arrange(species, desc(mass))
```

    ## # A tibble: 87 × 4
    ##    name            height species   mass
    ##    <chr>            <int> <chr>    <dbl>
    ##  1 Ratts Tyerel        79 Aleena      15
    ##  2 Dexter Jettster    198 Besalisk   102
    ##  3 Ki-Adi-Mundi       198 Cerean      82
    ##  4 Mas Amedda         196 Chagrian    NA
    ##  5 Zam Wesell         168 Clawdite    55
    ##  6 IG-88              200 Droid      140
    ##  7 C-3PO              167 Droid       75
    ##  8 R2-D2               96 Droid       32
    ##  9 R5-D4               97 Droid       32
    ## 10 R4-P17              96 Droid       NA
    ## # ℹ 77 more rows

## 4. Combining all the functions:

``` r
# Find all humans heavier than 70kg. 
# Calculate their BMI. 
# Sort them so the highest BMI is at the top. 
# Show only their name, mass, and BMI.

heavy_humans_bmi <- starwars %>% 
  filter(species == "Human", mass > 70) %>% 
  mutate(
    height_m = height / 100,
    bmi = mass / (height_m ^ 2)
  ) |> 
  arrange(desc(bmi)) %>% 
  select(name, mass, bmi)

heavy_humans_bmi
```

    ## # A tibble: 18 × 3
    ##    name                mass   bmi
    ##    <chr>              <dbl> <dbl>
    ##  1 Owen Lars          120    37.9
    ##  2 Darth Vader        136    33.3
    ##  3 Beru Whitesun Lars  75    27.5
    ##  4 Wedge Antilles      77    26.6
    ##  5 Luke Skywalker      77    26.0
    ##  6 Palpatine           75    26.0
    ##  7 Lobot               79    25.8
    ##  8 Lando Calrissian    79    25.2
    ##  9 Biggs Darklighter   84    25.1
    ## 10 Han Solo            80    24.7
    ## 11 Qui-Gon Jinn        89    23.9
    ## 12 Anakin Skywalker    84    23.8
    ## 13 Mace Windu          84    23.8
    ## 14 Jango Fett          79    23.6
    ## 15 Boba Fett           78.2  23.4
    ## 16 Obi-Wan Kenobi      77    23.2
    ## 17 Raymus Antilles     79    22.4
    ## 18 Dooku               80    21.5
