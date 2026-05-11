Day 11 of R Programming
================
2026-05-11

Today I learn how to collapse massive datasets into clean summary tables
using `summarize()` and `group_by()`.

``` r
library(tidyverse)
```

## 1. `summarize()`: Collapsing the Data

``` r
# Let's find the average height and the maximum mass of the entire Star Wars universe
starwars |> 
  summarize(
    avg_height = mean(height, na.rm = TRUE),
    max_mass = max(mass, na.rm = TRUE)
  )
```

    ## # A tibble: 1 × 2
    ##   avg_height max_mass
    ##        <dbl>    <dbl>
    ## 1       175.     1358

## 2. `group_by()` + `summarize()`

``` r
# TASK: Find the average height for each species.

starwars |> 
  group_by(species) |> 
  summarize(
    avg_height = mean(height, na.rm = TRUE)
  ) |> 
  arrange(desc(avg_height)) # Let's sort it so the tallest species are at the top!
```

    ## # A tibble: 38 × 2
    ##    species  avg_height
    ##    <chr>         <dbl>
    ##  1 Quermian       264 
    ##  2 Wookiee        231 
    ##  3 Kaminoan       221 
    ##  4 Kaleesh        216 
    ##  5 Gungan         209.
    ##  6 Pau'an         206 
    ##  7 Besalisk       198 
    ##  8 Cerean         198 
    ##  9 Chagrian       196 
    ## 10 Nautolan       196 
    ## # ℹ 28 more rows

## 3. Counting Items with `n()`

``` r
# TASK: How many characters exist for each species?
# We will calculate the count AND the average height in the same table.

species_summary <- starwars |> 
  group_by(species) |> 
  summarize(
    character_count = n(),
    avg_height = mean(height, na.rm = TRUE)
  ) |> 
  arrange(desc(character_count))

# Let's see the top of the table
head(species_summary)
```

    ## # A tibble: 6 × 3
    ##   species  character_count avg_height
    ##   <chr>              <int>      <dbl>
    ## 1 Human                 35       178 
    ## 2 Droid                  6       131.
    ## 3 <NA>                   4       175 
    ## 4 Gungan                 3       209.
    ## 5 Kaminoan               2       221 
    ## 6 Mirialan               2       168

## 4. Grouping by Multiple Columns

``` r
# TASK: Count how many characters there are by Homeworld AND Species.
# E.g., How many Human characters are from Tatooine vs Droid characters from Tatooine?

starwars |> 
  group_by(homeworld, species) |> 
  summarize(
    total_characters = n(),
    .groups = "drop" # Best practice: Always drop the invisible grouping when you are done!
  ) |> 
  arrange(desc(total_characters)) |> 
  head(10)
```

    ## # A tibble: 10 × 3
    ##    homeworld species  total_characters
    ##    <chr>     <chr>               <int>
    ##  1 Tatooine  Human                   8
    ##  2 <NA>      Human                   6
    ##  3 Naboo     Human                   5
    ##  4 Alderaan  Human                   3
    ##  5 Naboo     Gungan                  3
    ##  6 <NA>      Droid                   3
    ##  7 Corellia  Human                   2
    ##  8 Coruscant Human                   2
    ##  9 Kamino    Kaminoan                2
    ## 10 Kashyyyk  Wookiee                 2
