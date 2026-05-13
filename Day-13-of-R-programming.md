Day 13 of R Programming
================
2026-05-13

Today, I am learning how to combine multiple tables by using mutating
joins functions (‘inner_join’, ‘left_join’, ‘full_join’) and filtering
join (‘anti_join’).

``` r
library(tidyverse)
```

## 1. Creating two different datasets

``` r
dojo_roster <- tibble(
  student_id = c(101, 102, 103, 104, 105),
  name = c("Alex", "Maria", "John", "Zoe", "Liam"),
  belt_rank = c("Black", "Brown", "Green", "White", "Black")
)

dojo_roster
```

    ## # A tibble: 5 × 3
    ##   student_id name  belt_rank
    ##        <dbl> <chr> <chr>    
    ## 1        101 Alex  Black    
    ## 2        102 Maria Brown    
    ## 3        103 John  Green    
    ## 4        104 Zoe   White    
    ## 5        105 Liam  Black

``` r
tournament_regs <- tibble(
  student_id = c(102, 104, 105, 999), 
  category = c("-60kg", "Kata", "+84kg", "-75kg"),
  fee_paid = c(TRUE, TRUE, FALSE, TRUE)
)

tournament_regs
```

    ## # A tibble: 4 × 3
    ##   student_id category fee_paid
    ##        <dbl> <chr>    <lgl>   
    ## 1        102 -60kg    TRUE    
    ## 2        104 Kata     TRUE    
    ## 3        105 +84kg    FALSE   
    ## 4        999 -75kg    TRUE

## 2. Inner Join

Only keeps the common ones in both the tables.

``` r
dojo_roster %>% inner_join(tournament_regs, by = 'student_id')
```

    ## # A tibble: 3 × 5
    ##   student_id name  belt_rank category fee_paid
    ##        <dbl> <chr> <chr>     <chr>    <lgl>   
    ## 1        102 Maria Brown     -60kg    TRUE    
    ## 2        104 Zoe   White     Kata     TRUE    
    ## 3        105 Liam  Black     +84kg    FALSE

## 3. Left Join (most used join)

Keeps everything in the left table and the common ones from the right
table, if anything is missing, it will fill with ‘NA’.

``` r
dojo_roster %>% left_join(tournament_regs, by = 'student_id')
```

    ## # A tibble: 5 × 5
    ##   student_id name  belt_rank category fee_paid
    ##        <dbl> <chr> <chr>     <chr>    <lgl>   
    ## 1        101 Alex  Black     <NA>     NA      
    ## 2        102 Maria Brown     -60kg    TRUE    
    ## 3        103 John  Green     <NA>     NA      
    ## 4        104 Zoe   White     Kata     TRUE    
    ## 5        105 Liam  Black     +84kg    FALSE

## 4. Full Join

Keeps everything from both the tables. Fills with NA if anything is
missing.

``` r
dojo_roster %>% full_join(tournament_regs, by = 'student_id')
```

    ## # A tibble: 6 × 5
    ##   student_id name  belt_rank category fee_paid
    ##        <dbl> <chr> <chr>     <chr>    <lgl>   
    ## 1        101 Alex  Black     <NA>     NA      
    ## 2        102 Maria Brown     -60kg    TRUE    
    ## 3        103 John  Green     <NA>     NA      
    ## 4        104 Zoe   White     Kata     TRUE    
    ## 5        105 Liam  Black     +84kg    FALSE   
    ## 6        999 <NA>  <NA>      -75kg    TRUE

## 5. Anti Join

Keeps rows in the left table that do not have a match in the right
table.

``` r
dojo_roster %>% anti_join(tournament_regs, by = 'student_id')
```

    ## # A tibble: 2 × 3
    ##   student_id name  belt_rank
    ##        <dbl> <chr> <chr>    
    ## 1        101 Alex  Black    
    ## 2        103 John  Green
