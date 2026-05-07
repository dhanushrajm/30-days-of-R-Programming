Day 7 of R programming
================
2026-05-07

Today, I learned more about Functions, with multiple arguments, default
arguments.

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
