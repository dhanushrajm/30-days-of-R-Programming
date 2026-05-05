Day 5 of R programming
================
2026-05-05

Today, I learned about another Data Structure: Arrays and after that,
Conditions and loop Statements.

## 1. Creating an Array

``` r
a <- c("Toy Story", "The Artist", "The Avengers Endgame", "Captain America", "Iron Man", "Thor", "Loki", "Game of Thrones", "911", "Money Heist")
a #by default, it's arranged in the order of columns
```

    ##  [1] "Toy Story"            "The Artist"           "The Avengers Endgame"
    ##  [4] "Captain America"      "Iron Man"             "Thor"                
    ##  [7] "Loki"                 "Game of Thrones"      "911"                 
    ## [10] "Money Heist"

``` r
a_array <- array(a, dim = c(4,3))
a_array
```

    ##      [,1]                   [,2]              [,3]         
    ## [1,] "Toy Story"            "Iron Man"        "911"        
    ## [2,] "The Artist"           "Thor"            "Money Heist"
    ## [3,] "The Avengers Endgame" "Loki"            "Toy Story"  
    ## [4,] "Captain America"      "Game of Thrones" "The Artist"

## 2. Conditions (If-else statement)

``` r
movie_year <- 2022
if(movie_year > 2020){
  print("The movie is new")
} else {
  print("The movie is not new")
}
```

    ## [1] "The movie is new"

## 3. Logical statements

\<, \>, \<=, \>=, ==, &, \|, !, !=, %in% -\> (is found in?)

## 4. For Loop

``` r
year <- c(2000:2010)

for (yr in year){
  print(yr)
}
```

    ## [1] 2000
    ## [1] 2001
    ## [1] 2002
    ## [1] 2003
    ## [1] 2004
    ## [1] 2005
    ## [1] 2006
    ## [1] 2007
    ## [1] 2008
    ## [1] 2009
    ## [1] 2010

``` r
for (yr in year){
  if (yr >2005){
    print(paste("The year is ", yr))
  } 
}
```

    ## [1] "The year is  2006"
    ## [1] "The year is  2007"
    ## [1] "The year is  2008"
    ## [1] "The year is  2009"
    ## [1] "The year is  2010"

## 5. While Loop

``` r
year <- 1995

while (year <=1999){
  print(paste("This year is ", year, " and it's in 19th Century"))
  year <-  year + 1
}
```

    ## [1] "This year is  1995  and it's in 19th Century"
    ## [1] "This year is  1996  and it's in 19th Century"
    ## [1] "This year is  1997  and it's in 19th Century"
    ## [1] "This year is  1998  and it's in 19th Century"
    ## [1] "This year is  1999  and it's in 19th Century"

Now, I started with the Functions in R

## 6. Pre-defined Functions

``` r
ratings <-  c(1, 4, 3, 5, 2)
mean(ratings)
```

    ## [1] 3

``` r
sort(ratings)
```

    ## [1] 1 2 3 4 5

``` r
sort(ratings, decreasing=TRUE)
```

    ## [1] 5 4 3 2 1

``` r
max(ratings)
```

    ## [1] 5

## 7. User-defined Functions

``` r
hello <- function(){
  print("Hello World")
}
hello
```

    ## function () 
    ## {
    ##     print("Hello World")
    ## }

``` r
add <- function(x,y){
  return(x+y)
}
add(3,4)
```

    ## [1] 7

``` r
movie <- c("Iron Man", "Money Heist", "The Avengers", "The Batman")
year <- c(2010, 2020, 2015, 2017)
avg_rating <- c(4.5, 4.3, 4.0, 4.1)
movie_data <- data.frame(movie, year, avg_rating)
movie_data
```

    ##          movie year avg_rating
    ## 1     Iron Man 2010        4.5
    ## 2  Money Heist 2020        4.3
    ## 3 The Avengers 2015        4.0
    ## 4   The Batman 2017        4.1

``` r
## Default input values in functions
isGoodRating <- function(rating, threshold = 4.2){
  if(rating < threshold){
    return("NO")
  } else {
    return("YES")
  }
}

isGoodRating(4.0)
```

    ## [1] "NO"

``` r
isGoodRating(4.5)
```

    ## [1] "YES"

``` r
## Nested Functions

b <- function(movie_name, my_threshold = 4.3){
  rating <- movie_data[movie_data[,1]==movie_name, "avg_rating"]
  isGoodRating(rating, threshold = my_threshold)
}

b("Iron Man")
```

    ## [1] "YES"

``` r
b("Money Heist", 4.5)
```

    ## [1] "NO"
