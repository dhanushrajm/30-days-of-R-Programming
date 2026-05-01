Day 2: Data Types and Variables
================
02-05-2026

Today, I have learned about **Variables and Data Types** in R.

## 1. Naming Variables

``` r
user_age <- 28
user_age
```

    ## [1] 28

``` r
.a <- 5 # if a variable starts with . then it's value won't be saved in the environment
.a
```

    ## [1] 5

## 2. The Data Types in R

The four primary types are:

``` r
# Numeric
my_height <- 1.85

# Integer
my_children <- 2L

# Character
my_name <- "Alex"

# Logical
is_student <- TRUE
```

## 3. Checking Data Types using class() function:

``` r
class(my_height)    
```

    ## [1] "numeric"

``` r
class(my_children)  
```

    ## [1] "integer"

``` r
class(my_name)      
```

    ## [1] "character"

``` r
class(is_student)   
```

    ## [1] "logical"

## 4. Coercion (Converting Data Types into another using as.data_type() function

``` r
fake <- "500"  

class(fake) 
```

    ## [1] "character"

``` r
real_number <- as.numeric(fake)
class(real_number) 
```

    ## [1] "numeric"

``` r
real_number + 10   
```

    ## [1] 510

------------------------------------------------------------------------
