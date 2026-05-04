Day 4 of R programming
================
2026-05-04

Today, I learned about the other Data Structures which are Heterogeneous
in R, namely List and Data Frame.

## 1. Creating a list

A list can store different data types of data.

``` r
a <- list(name = "R Programming", score = c(90,92,89), pass=TRUE, course="Statistics")

a
```

    ## $name
    ## [1] "R Programming"
    ## 
    ## $score
    ## [1] 90 92 89
    ## 
    ## $pass
    ## [1] TRUE
    ## 
    ## $course
    ## [1] "Statistics"

## 2. Extracting data from a list

``` r
a$name
```

    ## [1] "R Programming"

``` r
a$course
```

    ## [1] "Statistics"

``` r
a$score
```

    ## [1] 90 92 89

## 3. Creating a Data Frame:

It is a 2-dimensional structure. whereas, every column is an individual
vector.

``` r
student_id <- c(101, 102, 103, 104)
names <- c("Alex", "Maria", "John", "Zoe")
grades <- c(85.5, 92.0, 78.5, 90.0)
passed <- c(TRUE, TRUE, FALSE, TRUE)

class_data <- data.frame(student_id, names, grades, passed)
class_data
```

    ##   student_id names grades passed
    ## 1        101  Alex   85.5   TRUE
    ## 2        102 Maria   92.0   TRUE
    ## 3        103  John   78.5  FALSE
    ## 4        104   Zoe   90.0   TRUE

## 4. Exploring a Data Frame:

``` r
nrow(class_data)
```

    ## [1] 4

``` r
ncol(class_data)
```

    ## [1] 4

``` r
str(class_data)
```

    ## 'data.frame':    4 obs. of  4 variables:
    ##  $ student_id: num  101 102 103 104
    ##  $ names     : chr  "Alex" "Maria" "John" "Zoe"
    ##  $ grades    : num  85.5 92 78.5 90
    ##  $ passed    : logi  TRUE TRUE FALSE TRUE

``` r
summary(class_data)
```

    ##    student_id       names               grades        passed       
    ##  Min.   :101.0   Length:4           Min.   :78.50   Mode :logical  
    ##  1st Qu.:101.8   Class :character   1st Qu.:83.75   FALSE:1        
    ##  Median :102.5   Mode  :character   Median :87.75   TRUE :3        
    ##  Mean   :102.5                      Mean   :86.50                  
    ##  3rd Qu.:103.2                      3rd Qu.:90.50                  
    ##  Max.   :104.0                      Max.   :92.00

``` r
class_data$names
```

    ## [1] "Alex"  "Maria" "John"  "Zoe"

``` r
class_data[2,3]
```

    ## [1] 92

``` r
class_data[3,]
```

    ##   student_id names grades passed
    ## 3        103  John   78.5  FALSE

``` r
class_data[,2]
```

    ## [1] "Alex"  "Maria" "John"  "Zoe"

## 5. Modifying a Data Frame:

``` r
class_data$letter_grade <- c("B", "A", "C", "A")

class_data
```

    ##   student_id names grades passed letter_grade
    ## 1        101  Alex   85.5   TRUE            B
    ## 2        102 Maria   92.0   TRUE            A
    ## 3        103  John   78.5  FALSE            C
    ## 4        104   Zoe   90.0   TRUE            A

``` r
class_data$grades <- NULL

class_data
```

    ##   student_id names passed letter_grade
    ## 1        101  Alex   TRUE            B
    ## 2        102 Maria   TRUE            A
    ## 3        103  John  FALSE            C
    ## 4        104   Zoe   TRUE            A

## 6. Filtering in Data Frame:

``` r
toppers <- class_data[class_data$letter_grade == "A", ]
toppers
```

    ##   student_id names passed letter_grade
    ## 2        102 Maria   TRUE            A
    ## 4        104   Zoe   TRUE            A
