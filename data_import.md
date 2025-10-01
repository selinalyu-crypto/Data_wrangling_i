Data Import
================

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.2     ✔ tibble    3.3.0
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.1.0     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

## Read in some data

Read in the litters dataset.

``` r
getwd() # current directory
```

    ## [1] "/Users/selinalyu/Desktop/P8105 DS I/Data Wrangling I/Data_wrangling_i"

``` r
litters_df = read_csv("./data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
names(litters_df)
```

    ## [1] "Group"             "Litter Number"     "GD0 weight"       
    ## [4] "GD18 weight"       "GD of Birth"       "Pups born alive"  
    ## [7] "Pups dead @ birth" "Pups survive"

``` r
litters_df = janitor::clean_names(litters_df)
names(litters_df)
```

    ## [1] "group"           "litter_number"   "gd0_weight"      "gd18_weight"    
    ## [5] "gd_of_birth"     "pups_born_alive" "pups_dead_birth" "pups_survive"

## Take a look at the data

``` r
litters_df # print out the dataset in the console
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>           <chr>      <chr>             <dbl>           <dbl>
    ##  1 Con7  #85             19.7       34.7                 20               3
    ##  2 Con7  #1/2/95/2       27         42                   19               8
    ##  3 Con7  #5/5/3/83/3-3   26         41.4                 19               6
    ##  4 Con7  #5/4/2/95/2     28.5       44.1                 19               5
    ##  5 Con7  #4/2/95/3-3     <NA>       <NA>                 20               6
    ##  6 Con7  #2/2/95/3-2     <NA>       <NA>                 20               6
    ##  7 Con7  #1/5/3/83/3-3/2 <NA>       <NA>                 20               9
    ##  8 Con8  #3/83/3-3       <NA>       <NA>                 20               9
    ##  9 Con8  #2/95/3         <NA>       <NA>                 20               8
    ## 10 Con8  #3/5/2/2/95     28.5       <NA>                 20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
skimr::skim(litters_df) #data summary
```

|                                                  |            |
|:-------------------------------------------------|:-----------|
| Name                                             | litters_df |
| Number of rows                                   | 49         |
| Number of columns                                | 8          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |            |
| Column type frequency:                           |            |
| character                                        | 4          |
| numeric                                          | 4          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |            |
| Group variables                                  | None       |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| group         |         0 |          1.00 |   4 |   4 |     0 |        6 |          0 |
| litter_number |         0 |          1.00 |   3 |  15 |     0 |       49 |          0 |
| gd0_weight    |        13 |          0.73 |   1 |   4 |     0 |       26 |          0 |
| gd18_weight   |        15 |          0.69 |   1 |   4 |     0 |       31 |          0 |

**Variable type: numeric**

| skim_variable   | n_missing | complete_rate |  mean |   sd |  p0 | p25 | p50 | p75 | p100 | hist  |
|:----------------|----------:|--------------:|------:|-----:|----:|----:|----:|----:|-----:|:------|
| gd_of_birth     |         0 |             1 | 19.65 | 0.48 |  19 |  19 |  20 |  20 |   20 | ▅▁▁▁▇ |
| pups_born_alive |         0 |             1 |  7.35 | 1.76 |   3 |   6 |   8 |   8 |   11 | ▁▃▂▇▁ |
| pups_dead_birth |         0 |             1 |  0.33 | 0.75 |   0 |   0 |   0 |   0 |    4 | ▇▂▁▁▁ |
| pups_survive    |         0 |             1 |  6.41 | 2.05 |   1 |   5 |   7 |   8 |    9 | ▁▃▂▇▇ |

``` r
tail(litters_df) #gives last segment of the data
```

    ## # A tibble: 6 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ## 1 Low8  #79           25.4       43.8                 19               8
    ## 2 Low8  #100          20         39.2                 20               8
    ## 3 Low8  #4/84         21.8       35.2                 20               4
    ## 4 Low8  #108          25.6       47.5                 20               8
    ## 5 Low8  #99           23.5       39                   20               6
    ## 6 Low8  #110          25.5       42.7                 20               7
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

use view(litter_df) in the console to take a look at the full dataset

## Options to read_csv

litters_df = read_csv(“./data/FAS_litters.csv”, skip = 10) skip 10 rows,
but if print to console, values become variable names litters_df =
read_csv(“./data/FAS_litters.csv”, skip = 10, col_names = FALSE) no
column names anymore, made X1, X2… as column names litters_df =
read_csv(“./data/FAS_litters.csv”, na = c(“.”, “NA”, ““)) treat those as
missing check out `?read_csv()`for more information
