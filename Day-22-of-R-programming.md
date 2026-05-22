Day 22 of R Programming
================
2026-05-22

Yesterday, I learned how to get data from a webpage through an API. But,
today, i am going to learn how to get the data from a webpage if it
doesn’t have an API though Web Scraping using the ‘rvest’ package.

``` r
library(tidyverse)
library(rvest)
```

## 1. Our Webpage URL

``` r
url <- "https://en.wikipedia.org/wiki/Karate_at_the_Summer_Olympics"
webpage <- read_html(url)

webpage
```

    ## {html_document}
    ## <html class="client-nojs vector-feature-language-in-header-enabled vector-feature-language-in-main-menu-disabled vector-feature-language-in-main-page-header-disabled vector-feature-page-tools-pinned-disabled vector-feature-toc-pinned-clientpref-1 vector-feature-main-menu-pinned-disabled vector-feature-limited-width-clientpref-1 vector-feature-limited-width-content-enabled vector-feature-custom-font-size-clientpref-1 vector-feature-appearance-pinned-clientpref-1 skin-theme-clientpref-day vector-sticky-header-enabled vector-toc-available skin-thumbsize-clientpref-standard" lang="en" dir="ltr">
    ## [1] <head>\n<meta http-equiv="Content-Type" content="text/html; charset=UTF-8 ...
    ## [2] <body class="skin--responsive skin-vector skin-vector-search-vue mediawik ...

## 2. Scraping the specific Text

h1 - represents the main title p - represents the paragraph

``` r
main_title <- webpage %>% 
  html_elements("h1") %>% html_text2

print(main_title)
```

    ## [1] "Karate at the 2020 Summer Olympics"

``` r
first_paragraph <- webpage %>% 
  html_elements("p") %>% 
  .[[2]] %>%  
  html_text2

print(first_paragraph)
```

    ## [1] "Karate was an event held in the 2020 Summer Olympics in Tokyo, Japan. It was the debut appearance of karate at the Summer Olympics. Karate was one of four optional sports added to the Olympic program specifically for 2020,[1] rather than as a permanent sport.[2][3] After it was announced it would not be included in 2024, in August 2022 it was announced that karate had made the shortlist for inclusion in the 2028 Games, although it was ultimately not selected.[4][5]"

## 3. Scraping html tables to tibble tables

``` r
all_tables <- webpage %>% 
  html_elements(".wikitable")

medal_table <- all_tables[[3]] %>% 
  html_table(fill = TRUE)

head(medal_table)
```

    ## # A tibble: 6 × 6
    ##   Rank  NOC       Gold Silver Bronze Total
    ##   <chr> <chr>    <int>  <int>  <int> <int>
    ## 1 1     Japan*       1      1      1     3
    ## 2 2     Spain        1      1      0     2
    ## 3 3     Egypt        1      0      1     2
    ## 4 3     Italy        1      0      1     2
    ## 5 5     Bulgaria     1      0      0     1
    ## 6 5     France       1      0      0     1
