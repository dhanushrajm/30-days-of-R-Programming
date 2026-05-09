Day 9 of R Programming
================
2026-05-09

Today, I am learning about the Filtering and selecting the data using
the dplyr package.

- select() \<- is how we want to pick the columns.
- filter() \<- is how we want to pick the rows based on the condition.

## 1. select() function:

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
starwars %>% select(name, height, mass)
```

    ## # A tibble: 87 × 3
    ##    name               height  mass
    ##    <chr>               <int> <dbl>
    ##  1 Luke Skywalker        172    77
    ##  2 C-3PO                 167    75
    ##  3 R2-D2                  96    32
    ##  4 Darth Vader           202   136
    ##  5 Leia Organa           150    49
    ##  6 Owen Lars             178   120
    ##  7 Beru Whitesun Lars    165    75
    ##  8 R5-D4                  97    32
    ##  9 Biggs Darklighter     183    84
    ## 10 Obi-Wan Kenobi        182    77
    ## # ℹ 77 more rows

``` r
starwars %>% select(-films, -vehicles)
```

    ## # A tibble: 87 × 12
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
    ## # ℹ 3 more variables: homeworld <chr>, species <chr>, starships <list>

## 2. Helper functions in select: contains(), starts_with(), ends_with()

``` r
starwars %>% select(name, contains("color"))
```

    ## # A tibble: 87 × 4
    ##    name               hair_color    skin_color  eye_color
    ##    <chr>              <chr>         <chr>       <chr>    
    ##  1 Luke Skywalker     blond         fair        blue     
    ##  2 C-3PO              <NA>          gold        yellow   
    ##  3 R2-D2              <NA>          white, blue red      
    ##  4 Darth Vader        none          white       yellow   
    ##  5 Leia Organa        brown         light       brown    
    ##  6 Owen Lars          brown, grey   light       blue     
    ##  7 Beru Whitesun Lars brown         light       blue     
    ##  8 R5-D4              <NA>          white, red  red      
    ##  9 Biggs Darklighter  black         light       brown    
    ## 10 Obi-Wan Kenobi     auburn, white fair        blue-gray
    ## # ℹ 77 more rows

``` r
starwars %>% select(name: eye_color)
```

    ## # A tibble: 87 × 6
    ##    name               height  mass hair_color    skin_color  eye_color
    ##    <chr>               <int> <dbl> <chr>         <chr>       <chr>    
    ##  1 Luke Skywalker        172    77 blond         fair        blue     
    ##  2 C-3PO                 167    75 <NA>          gold        yellow   
    ##  3 R2-D2                  96    32 <NA>          white, blue red      
    ##  4 Darth Vader           202   136 none          white       yellow   
    ##  5 Leia Organa           150    49 brown         light       brown    
    ##  6 Owen Lars             178   120 brown, grey   light       blue     
    ##  7 Beru Whitesun Lars    165    75 brown         light       blue     
    ##  8 R5-D4                  97    32 <NA>          white, red  red      
    ##  9 Biggs Darklighter     183    84 black         light       brown    
    ## 10 Obi-Wan Kenobi        182    77 auburn, white fair        blue-gray
    ## # ℹ 77 more rows

``` r
starwars %>% select(starts_with("hair_color"), ends_with("eye_color"))
```

    ## # A tibble: 87 × 2
    ##    hair_color    eye_color
    ##    <chr>         <chr>    
    ##  1 blond         blue     
    ##  2 <NA>          yellow   
    ##  3 <NA>          red      
    ##  4 none          yellow   
    ##  5 brown         brown    
    ##  6 brown, grey   blue     
    ##  7 brown         blue     
    ##  8 <NA>          red      
    ##  9 black         brown    
    ## 10 auburn, white blue-gray
    ## # ℹ 77 more rows

## 3. Filter Basics:

``` r
starwars %>% filter(height > 170) # we have to apply this condition on the column names
```

    ## # A tibble: 55 × 14
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Luke Sk…    172    77 blond      fair       blue            19   male  mascu…
    ##  2 Darth V…    202   136 none       white      yellow          41.9 male  mascu…
    ##  3 Owen La…    178   120 brown, gr… light      blue            52   male  mascu…
    ##  4 Biggs D…    183    84 black      light      brown           24   male  mascu…
    ##  5 Obi-Wan…    182    77 auburn, w… fair       blue-gray       57   male  mascu…
    ##  6 Anakin …    188    84 blond      fair       blue            41.9 male  mascu…
    ##  7 Wilhuff…    180    NA auburn, g… fair       blue            64   male  mascu…
    ##  8 Chewbac…    228   112 brown      unknown    blue           200   male  mascu…
    ##  9 Han Solo    180    80 brown      fair       brown           29   male  mascu…
    ## 10 Greedo      173    74 <NA>       green      black           44   male  mascu…
    ## # ℹ 45 more rows
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

``` r
starwars %>% filter(species == "Droid")
```

    ## # A tibble: 6 × 14
    ##   name   height  mass hair_color skin_color  eye_color birth_year sex   gender  
    ##   <chr>   <int> <dbl> <chr>      <chr>       <chr>          <dbl> <chr> <chr>   
    ## 1 C-3PO     167    75 <NA>       gold        yellow           112 none  masculi…
    ## 2 R2-D2      96    32 <NA>       white, blue red               33 none  masculi…
    ## 3 R5-D4      97    32 <NA>       white, red  red               NA none  masculi…
    ## 4 IG-88     200   140 none       metal       red               15 none  masculi…
    ## 5 R4-P17     96    NA none       silver, red red, blue         NA none  feminine
    ## 6 BB8        NA    NA none       none        black             NA none  masculi…
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

``` r
starwars |> 
  filter(species == "Human", homeworld == "Tatooine") # comma , is treated as AND statement or & or AND
```

    ## # A tibble: 8 × 14
    ##   name      height  mass hair_color skin_color eye_color birth_year sex   gender
    ##   <chr>      <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ## 1 Luke Sky…    172    77 blond      fair       blue            19   male  mascu…
    ## 2 Darth Va…    202   136 none       white      yellow          41.9 male  mascu…
    ## 3 Owen Lars    178   120 brown, gr… light      blue            52   male  mascu…
    ## 4 Beru Whi…    165    75 brown      light      blue            47   fema… femin…
    ## 5 Biggs Da…    183    84 black      light      brown           24   male  mascu…
    ## 6 Anakin S…    188    84 blond      fair       blue            41.9 male  mascu…
    ## 7 Shmi Sky…    163    NA black      fair       brown           72   fema… femin…
    ## 8 Cliegg L…    183    NA brown      fair       blue            82   male  mascu…
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

``` r
starwars |> 
  filter(homeworld == "Naboo" | homeworld == "Coruscant")
```

    ## # A tibble: 14 × 14
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 R2-D2        96    32 <NA>       white, bl… red               33 none  mascu…
    ##  2 Palpati…    170    75 grey       pale       yellow            82 male  mascu…
    ##  3 Finis V…    170    NA blond      fair       blue              91 male  mascu…
    ##  4 Padmé A…    185    45 brown      light      brown             46 fema… femin…
    ##  5 Jar Jar…    196    66 none       orange     orange            52 male  mascu…
    ##  6 Roos Ta…    224    82 none       grey       orange            NA male  mascu…
    ##  7 Rugor N…    206    NA none       green      orange            NA male  mascu…
    ##  8 Ric Olié    183    NA brown      fair       blue              NA male  mascu…
    ##  9 Quarsh …    183    NA black      dark       brown             62 male  mascu…
    ## 10 Adi Gal…    184    50 none       dark       blue              NA fema… femin…
    ## 11 Gregar …    185    85 black      dark       brown             NA <NA>  <NA>  
    ## 12 Cordé       157    NA brown      light      brown             NA <NA>  <NA>  
    ## 13 Dormé       165    NA brown      light      brown             NA fema… femin…
    ## 14 Jocasta…    167    NA white      fair       blue              NA fema… femin…
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

## 4. Filter ‘%in%’ operator:

``` r
target_planets <- c("Tatooine", "Alderaan", "Endor")

starwars |> 
  filter(homeworld %in% target_planets)
```

    ## # A tibble: 14 × 14
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Luke Sk…    172    77 blond      fair       blue            19   male  mascu…
    ##  2 C-3PO       167    75 <NA>       gold       yellow         112   none  mascu…
    ##  3 Darth V…    202   136 none       white      yellow          41.9 male  mascu…
    ##  4 Leia Or…    150    49 brown      light      brown           19   fema… femin…
    ##  5 Owen La…    178   120 brown, gr… light      blue            52   male  mascu…
    ##  6 Beru Wh…    165    75 brown      light      blue            47   fema… femin…
    ##  7 R5-D4        97    32 <NA>       white, red red             NA   none  mascu…
    ##  8 Biggs D…    183    84 black      light      brown           24   male  mascu…
    ##  9 Anakin …    188    84 blond      fair       blue            41.9 male  mascu…
    ## 10 Wicket …     88    20 brown      brown      brown            8   male  mascu…
    ## 11 Shmi Sk…    163    NA black      fair       brown           72   fema… femin…
    ## 12 Cliegg …    183    NA brown      fair       blue            82   male  mascu…
    ## 13 Bail Pr…    191    NA black      tan        brown           67   male  mascu…
    ## 14 Raymus …    188    79 brown      light      brown           NA   male  mascu…
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

## 5. Combining it all together:

``` r
# Get a clean table showing the name, height, and mass 
# of all characters lighter than 100kg who are NOT humans.
primary_data <- starwars %>% filter(mass < 100 & species != "Human") %>% select(name, height, mass)

primary_data
```

    ## # A tibble: 29 × 3
    ##    name                  height  mass
    ##    <chr>                  <int> <dbl>
    ##  1 C-3PO                    167    75
    ##  2 R2-D2                     96    32
    ##  3 R5-D4                     97    32
    ##  4 Greedo                   173    74
    ##  5 Yoda                      66    17
    ##  6 Ackbar                   180    83
    ##  7 Wicket Systri Warrick     88    20
    ##  8 Nien Nunb                160    68
    ##  9 Nute Gunray              191    90
    ## 10 Jar Jar Binks            196    66
    ## # ℹ 19 more rows

## 6. Renaming the columns:

``` r
new_name_data <- starwars %>% rename(character_name = name, weight_kg = mass) # rename(new_name = old_name)

new_name_data 
```

    ## # A tibble: 87 × 14
    ##    character_name    height weight_kg hair_color skin_color eye_color birth_year
    ##    <chr>              <int>     <dbl> <chr>      <chr>      <chr>          <dbl>
    ##  1 Luke Skywalker       172        77 blond      fair       blue            19  
    ##  2 C-3PO                167        75 <NA>       gold       yellow         112  
    ##  3 R2-D2                 96        32 <NA>       white, bl… red             33  
    ##  4 Darth Vader          202       136 none       white      yellow          41.9
    ##  5 Leia Organa          150        49 brown      light      brown           19  
    ##  6 Owen Lars            178       120 brown, gr… light      blue            52  
    ##  7 Beru Whitesun La…    165        75 brown      light      blue            47  
    ##  8 R5-D4                 97        32 <NA>       white, red red             NA  
    ##  9 Biggs Darklighter    183        84 black      light      brown           24  
    ## 10 Obi-Wan Kenobi       182        77 auburn, w… fair       blue-gray       57  
    ## # ℹ 77 more rows
    ## # ℹ 7 more variables: sex <chr>, gender <chr>, homeworld <chr>, species <chr>,
    ## #   films <list>, vehicles <list>, starships <list>

## 7. Distinct values in a column:

``` r
starwars %>% distinct(species)
```

    ## # A tibble: 38 × 1
    ##    species       
    ##    <chr>         
    ##  1 Human         
    ##  2 Droid         
    ##  3 Wookiee       
    ##  4 Rodian        
    ##  5 Hutt          
    ##  6 <NA>          
    ##  7 Yoda's species
    ##  8 Trandoshan    
    ##  9 Mon Calamari  
    ## 10 Ewok          
    ## # ℹ 28 more rows

``` r
starwars %>% distinct(homeworld, starships)
```

    ## # A tibble: 61 × 2
    ##    homeworld starships
    ##    <chr>     <list>   
    ##  1 Tatooine  <chr [2]>
    ##  2 Tatooine  <chr [0]>
    ##  3 Naboo     <chr [0]>
    ##  4 Tatooine  <chr [1]>
    ##  5 Alderaan  <chr [0]>
    ##  6 Tatooine  <chr [1]>
    ##  7 Stewjon   <chr [5]>
    ##  8 Tatooine  <chr [3]>
    ##  9 Eriadu    <chr [0]>
    ## 10 Kashyyyk  <chr [2]>
    ## # ℹ 51 more rows

## 8. slice() - filtering by row position

``` r
starwars %>% slice(1:5)
```

    ## # A tibble: 5 × 14
    ##   name      height  mass hair_color skin_color eye_color birth_year sex   gender
    ##   <chr>      <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ## 1 Luke Sky…    172    77 blond      fair       blue            19   male  mascu…
    ## 2 C-3PO        167    75 <NA>       gold       yellow         112   none  mascu…
    ## 3 R2-D2         96    32 <NA>       white, bl… red             33   none  mascu…
    ## 4 Darth Va…    202   136 none       white      yellow          41.9 male  mascu…
    ## 5 Leia Org…    150    49 brown      light      brown           19   fema… femin…
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

``` r
starwars %>% slice_max(height, n = 3)
```

    ## # A tibble: 3 × 14
    ##   name      height  mass hair_color skin_color eye_color birth_year sex   gender
    ##   <chr>      <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ## 1 Yarael P…    264    NA none       white      yellow            NA male  mascu…
    ## 2 Tarfful      234   136 brown      brown      blue              NA male  mascu…
    ## 3 Lama Su      229    88 none       grey       black             NA male  mascu…
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>

``` r
starwars %>% slice_min(mass, n = 10)
```

    ## # A tibble: 10 × 14
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Ratts T…     79    15 none       grey, blue unknown           NA male  mascu…
    ##  2 Yoda         66    17 white      green      brown            896 male  mascu…
    ##  3 Wicket …     88    20 brown      brown      brown              8 male  mascu…
    ##  4 R2-D2        96    32 <NA>       white, bl… red               33 none  mascu…
    ##  5 R5-D4        97    32 <NA>       white, red red               NA none  mascu…
    ##  6 Sebulba     112    40 none       grey, red  orange            NA male  mascu…
    ##  7 Padmé A…    185    45 brown      light      brown             46 fema… femin…
    ##  8 Dud Bolt     94    45 none       blue, grey yellow            NA male  mascu…
    ##  9 Wat Tam…    193    48 none       green, gr… unknown           NA male  mascu…
    ## 10 Sly Moo…    178    48 none       pale       white             NA <NA>  <NA>  
    ## # ℹ 5 more variables: homeworld <chr>, species <chr>, films <list>,
    ## #   vehicles <list>, starships <list>
