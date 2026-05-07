Day 7 of R programming
================
2026-05-07

Today, I learned more about Functions, with multiple arguments, default
arguments and the scope of variables.

## 1. Creating a function:

``` r
c_to_f <-  function(temp_c){
  temp_f <-  (temp_c * 9/5) + 32
  return(temp_f)
}

c_to_f(25)
```

    ## [1] 77

``` r
c_to_f(40)
```

    ## [1] 104

## 2. With multiple arguments and default values also:

``` r
final_grade <- function(final_exam_score, a1=100, a2=100, bonus){
  if(bonus == TRUE){
    return((final_exam_score * 0.70) + (a1 * 0.15) + (a2 * 0.15) + 0.05)
  } else {
    return((final_exam_score * 0.70) + (a1 * 0.15) + (a2 * 0.15))
  }
}

final_grade(85, bonus=FALSE)
```

    ## [1] 89.5

``` r
final_grade(70, bonus= TRUE)
```

    ## [1] 79.05

## 3. Scope of the variables:

``` r
a1 <- 100 #global variables
a2 <- 100

final_grade <- function(final_exam_score, bonus=TRUE){
  
  assignment_total <<- (a1 + a2) * 0.30 # <<- this operator is used to define global variable inside a function
  bonus_score <- 0.15
  
  if(bonus == TRUE){
    return((final_exam_score * 0.70) + assignment_total + bonus_score)
  } else {
    return((final_exam_score * 0.70) + assignment_total)
  }
}

final_grade(70)
```

    ## [1] 109.15

``` r
a1
```

    ## [1] 100

``` r
assignment_total #global variable
```

    ## [1] 60

``` r
#bonus_score #local variable, it can be only accessed inside the function, uncomment this, it will give an error
```
