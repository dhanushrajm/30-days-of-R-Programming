Day 15 of R Programming
================
2026-05-15

# Day 15: Taming Text and Time

Today, I complete data manipulation techniques by learning how to clean
messy text with `stringr` and parse complex times with `lubridate`.

``` r
library(tidyverse)
```

## 1. Messy Log Data

``` r
raw_logs <- tibble(
  log_id = 1:4,
  event_info = c(" KATA - senior ", "kumite-Junior", " KATA - Cadet", "KUMITE - Senior "),
  registration_date = c("15-May-2026", "2026/05/16", "05-17-2026", "20260518")
)

raw_logs
```

    ## # A tibble: 4 × 3
    ##   log_id event_info         registration_date
    ##    <int> <chr>              <chr>            
    ## 1      1 " KATA - senior "  15-May-2026      
    ## 2      2 "kumite-Junior"    2026/05/16       
    ## 3      3 " KATA - Cadet"    05-17-2026       
    ## 4      4 "KUMITE - Senior " 20260518

## 2. `stringr`: Cleaning Text

``` r
clean_text_logs <- raw_logs %>% 
  mutate(
    # 1. Remove leading/trailing spaces
    event_info = str_trim(event_info),
    
    # 2. Make everything uppercase so "KATA" and "kata" are treated the same
    event_info = str_to_upper(event_info),
    
    # 3. Create a new column to flag if the event is Kumite using str_detect()
    is_kumite = str_detect(event_info, "KUMITE")
  )

clean_text_logs
```

    ## # A tibble: 4 × 4
    ##   log_id event_info      registration_date is_kumite
    ##    <int> <chr>           <chr>             <lgl>    
    ## 1      1 KATA - SENIOR   15-May-2026       FALSE    
    ## 2      2 KUMITE-JUNIOR   2026/05/16        TRUE     
    ## 3      3 KATA - CADET    05-17-2026        FALSE    
    ## 4      4 KUMITE - SENIOR 20260518          TRUE

## 3. `lubridate`: Parsing Dates

- `ymd()` for Year-Month-Day
- `mdy()` for Month-Day-Year
- `dmy()` for Day-Month-Year

``` r
# Parsing "2026/05/16" and "20260518" (Year, Month, Day)
ymd(c("2026/05/16", "20260518"))
```

    ## [1] "2026-05-16" "2026-05-18"

``` r
# Parsing "15-May-2026" (Day, Month, Year)
dmy("15-May-2026")
```

    ## [1] "2026-05-15"

``` r
# Parsing "05-17-2026" (Month, Day, Year)
mdy("05-17-2026")
```

    ## [1] "2026-05-17"

## 4. The Master Cleaning Pipeline

``` r
final_clean_logs <- raw_logs %>% 
  mutate(
    event_category = str_to_upper(str_trim(event_info)),
    
    standardized_date = parse_date_time(registration_date, orders = c("dmy", "ymd", "mdy")),
    
    reg_month = month(standardized_date, label = TRUE) 
  ) %>% 
  select(log_id, event_category, standardized_date, reg_month)

final_clean_logs
```

    ## # A tibble: 4 × 4
    ##   log_id event_category  standardized_date   reg_month
    ##    <int> <chr>           <dttm>              <ord>    
    ## 1      1 KATA - SENIOR   2026-05-15 00:00:00 May      
    ## 2      2 KUMITE-JUNIOR   2026-05-16 00:00:00 May      
    ## 3      3 KATA - CADET    2026-05-17 00:00:00 May      
    ## 4      4 KUMITE - SENIOR 2026-05-18 00:00:00 May
