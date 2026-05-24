Day 23 of R Programming
================
2026-05-23

Today, I learn about how to connect R directly to a database using the
dbplyr package. \# install.packages(c(“DBI”, “RSQLite”, “dbplyr”))

``` r
library(tidyverse)
library(dbplyr)
library(DBI)
library(RSQLite)
```

## 1. Establishing a connection:

``` r
con <- dbConnect(RSQLite::SQLite(), "sample_data.sqlite")

dbListTables(con)
```

    ## [1] "athletes"

## 2. Writing data to the database:

``` r
a1 <- tibble(
  athlete_id = 101:105,
  name = c("Alex", "Maria", "John", "Zoe", "Liam"),
  style = c("Shotokan", "Shito-ryu", "Shotokan", "Wado-ryu", "Goju-ryu"),
  points = c(120, 150, 95, 110, 140)
)
```

## 3. Write this tibble into our database:

``` r
dbWriteTable(con, name = "athletes", value = a1, overwrite = TRUE)

dbListTables(con)
```

    ## [1] "athletes"

## 4. Querying the data using SQL:

``` r
sql_query <- "select name, style, points from athletes where points > 100 order by points desc"

top_list <- dbGetQuery(con, sql_query)
top_list
```

    ##    name     style points
    ## 1 Maria Shito-ryu    150
    ## 2  Liam  Goju-ryu    140
    ## 3  Alex  Shotokan    120
    ## 4   Zoe  Wado-ryu    110

## 5. Querying using dbplyr:

``` r
athletes_db <- tbl(con, "athletes")

head(athletes_db)
```

    ## # Source:   SQL [?? x 4]
    ## # Database: sqlite 3.53.1 [C:\Users\Admin\OneDrive\Documents\R_Programming\sample_data.sqlite]
    ##   athlete_id name  style     points
    ##        <int> <chr> <chr>      <dbl>
    ## 1        101 Alex  Shotokan     120
    ## 2        102 Maria Shito-ryu    150
    ## 3        103 John  Shotokan      95
    ## 4        104 Zoe   Wado-ryu     110
    ## 5        105 Liam  Goju-ryu     140

``` r
shotokan <-  athletes_db %>% 
  filter(style == "Shotokan") %>% 
  select(name, points)

shotokan
```

    ## # Source:   SQL [?? x 2]
    ## # Database: sqlite 3.53.1 [C:\Users\Admin\OneDrive\Documents\R_Programming\sample_data.sqlite]
    ##   name  points
    ##   <chr>  <dbl>
    ## 1 Alex     120
    ## 2 John      95

``` r
show_query(shotokan)
```

    ## <SQL>
    ## SELECT `name`, `points`
    ## FROM `athletes`
    ## WHERE (`style` = 'Shotokan')

``` r
shotokan_results <- shotokan %>% collect()

shotokan_results
```

    ## # A tibble: 2 × 2
    ##   name  points
    ##   <chr>  <dbl>
    ## 1 Alex     120
    ## 2 John      95

## 5. Disconnecting the Database:

``` r
dbDisconnect(con)
print("Disconnected successfully")
```

    ## [1] "Disconnected successfully"
