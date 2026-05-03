Day 3 R programming
================
2026-05-03

Today, I am learning about the different Data Structures in R. the first
of many: Vectors and Matrices.

## 1. Vectors

It is a 1-dimensional list of items. To create a vector, we will use the
combine c() function.

``` r
grades = c(90,85,92,83)

names = c("A", "B", "C", "D")

grades
```

    ## [1] 90 85 92 83

## 2. Math operations in Vector

``` r
grades = grades + 5
grades
```

    ## [1] 95 90 97 88

``` r
sum(grades)
```

    ## [1] 370

``` r
mean(grades)
```

    ## [1] 92.5

``` r
max(grades)
```

    ## [1] 97

## 3. Extracting data from vectors:

``` r
names[2]
```

    ## [1] "B"

``` r
names[c(1,3)]
```

    ## [1] "A" "C"

``` r
grades[c(1,3)]
```

    ## [1] 95 97

``` r
names[-1]
```

    ## [1] "B" "C" "D"

``` r
grades[grades > 90]
```

    ## [1] 95 97

## 4. Matrices:

It is same like a vector, but it has rows and columns, so it’s
2-dimensional. Both vectors and matrices are homogeneous in R. Meaning:
each variable will have a list of items of only one data type, not a
mix.

we will use the matrix() function for this. It has byrow=TRUE/FALSE -\>
means to fill the matrix horizontally or vertically.

``` r
m = matrix(1:12, nrow=4, ncol=3, byrow=TRUE)
m
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    2    3
    ## [2,]    4    5    6
    ## [3,]    7    8    9
    ## [4,]   10   11   12

## 5. Naming Rows and Columns in the matrix

Using rownames() and colnames() function.

``` r
rownames(m) <- c("A", "B", "C", "D")
colnames(m) <- c("X", "Y", "Z")

m
```

    ##    X  Y  Z
    ## A  1  2  3
    ## B  4  5  6
    ## C  7  8  9
    ## D 10 11 12

## 6. Extracting Data from a matrix:

Similar to a vector, we will also use \[\] to extract the values, but
using both row and column.

``` r
m[2,2]
```

    ## [1] 5

``` r
m[3,]
```

    ## X Y Z 
    ## 7 8 9

``` r
m[,2]
```

    ##  A  B  C  D 
    ##  2  5  8 11

## 7. Factors (categorical vectors):

If we have text data that can be splitted into different categories like
a cluster, then we can use factor() function to do that for further
visualizations.

``` r
shirt_sizes <- c("Small", "Large","Medium", "Small","Large")

factor_sizes <- factor(shirt_sizes, levels = c("Small", "Medium", "Large"))

factor_sizes
```

    ## [1] Small  Large  Medium Small  Large 
    ## Levels: Small Medium Large

## 8. Binding Vectors into Matrix

If we have two vectors, we can bind them together into one matrix using
two functions: rbind() and cbind() functions.

``` r
fruits <- c("Apples", "Oranges", "Watermelon")
prices <- c(1.2, 0.9, 4.2)

fruit_matrix_rows <- rbind(fruits, prices)
fruit_matrix_rows
```

    ##        [,1]     [,2]      [,3]        
    ## fruits "Apples" "Oranges" "Watermelon"
    ## prices "1.2"    "0.9"     "4.2"

``` r
fruit_matrix_cols <- cbind(fruits, prices)
fruit_matrix_cols
```

    ##      fruits       prices
    ## [1,] "Apples"     "1.2" 
    ## [2,] "Oranges"    "0.9" 
    ## [3,] "Watermelon" "4.2"
