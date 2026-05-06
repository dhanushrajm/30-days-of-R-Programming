Day 6 of R Programming
================
2026-05-06

Today, we learn much more deeper about the Conditional Statements, Loops
and Vectorized Operations.

## 1. Vectorized ifelse() function:

Standard if statement only checks one value at a time. But, we usually
wants to check entire column at a time. \##### ifelse(Condition,
if_true, if_False)

``` r
athens_temps <- c(22, 38, 19, 41, 25)

status <- ifelse(athens_temps > 25, "Heatwave Warning", "Normal")

a <- data.frame(Temp = athens_temps, Status = status)
a
```

    ##   Temp           Status
    ## 1   22           Normal
    ## 2   38 Heatwave Warning
    ## 3   19           Normal
    ## 4   41 Heatwave Warning
    ## 5   25           Normal

## 2. any() and all() functions:

``` r
server_pings <- c(20, 45, 18, 90, 15)

# Did ANY server take longer than 50ms?
any(server_pings > 50) 
```

    ## [1] TRUE

``` r
# Did ALL servers respond in under 100ms?
all(server_pings < 100)
```

    ## [1] TRUE

## 3. Handling missing values:

We use the is.na() function to check if there is any missing values in
the column

``` r
missing_grade <- NA

if (is.na(missing_grade)) {
  print("Warning: Grade is missing.")
} else if (missing_grade > 50) {
  print("Pass")
} else {
  print("Fail")
}
```

    ## [1] "Warning: Grade is missing."

## 4. Loop Controls: Break and Next

- break: kills the loop completely and stops it immediately
- next: similar to continue in Python, which skips the current round of
  the loop and continue with the next one

``` r
files <- c("data1.csv", "data2.csv", "target_file.csv", "data4.csv")

for (file in files) {
  print(paste("Checking:", file))
  if (file == "target_file.csv") {
    print("Target found!")
    break 
  }
}
```

    ## [1] "Checking: data1.csv"
    ## [1] "Checking: data2.csv"
    ## [1] "Checking: target_file.csv"
    ## [1] "Target found!"

``` r
# Using 'next' to skip an iteration

for (num in 1:5) {
  if (num == 3) {
    next
  }
  print(paste("Number:", num))
}
```

    ## [1] "Number: 1"
    ## [1] "Number: 2"
    ## [1] "Number: 4"
    ## [1] "Number: 5"

## 5. Vectorization

We know that R is vectorized, so the math is entirely different compared
to other languages. So, instead of using loops for some math operations,
we can directly use the vectorization techniques to execute it faster.
Now, we will see two examples with and without vectorization.

``` r
vector_a <- 1:100000
vector_b <- 100000:1

output <- numeric(100000)
for(i in 1:100000) {
   output[i] <- vector_a[i] + vector_b[i]
}
#output #uncomment this to see how it works!
```

``` r
fast_output <- vector_a + vector_b

head(fast_output, 5)
```

    ## [1] 100001 100001 100001 100001 100001

## 6. The ‘apply()’ family:

- **`lapply()`** (List Apply): Applies a function to every item and
  always returns a list.
- **`sapply()`** (Simplified Apply): Does the exact same thing, but
  tries to simplify the result into a clean vector.

``` r
store_sales <- list(
  branch_A = c(100, 150, 120),
  branch_B = c(80, 90, 85, 110),
  branch_C = c(200, 210)
)

# Find the average (mean) sales for each branch.

# lapply
list_results <- lapply(store_sales, mean)
print("lapply results:")
```

    ## [1] "lapply results:"

``` r
list_results
```

    ## $branch_A
    ## [1] 123.3333
    ## 
    ## $branch_B
    ## [1] 91.25
    ## 
    ## $branch_C
    ## [1] 205

``` r
# sapply
vector_results <- sapply(store_sales, mean)
print("sapply results:")
```

    ## [1] "sapply results:"

``` r
vector_results
```

    ## branch_A branch_B branch_C 
    ## 123.3333  91.2500 205.0000
