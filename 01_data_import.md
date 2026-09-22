Data Import
================
2026-09-22

This file is for doing data import

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.2.1     ✔ readr     2.2.0
    ## ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ## ✔ ggplot2   4.0.3     ✔ tibble    3.3.1
    ## ✔ lubridate 1.9.5     ✔ tidyr     1.3.2
    ## ✔ purrr     1.2.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(readxl)
library(haven)
```

``` r
getwd()
```

    ## [1] "C:/Users/brome/Downloads/data science/data_wrangling_i"

``` r
## [1] "C:/Users/brome/Downloads/data science/data_wrangling_i"
```

Import our first dataset

``` r
litters_df =
  read_csv(file = "data/FAS_litters.csv")
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
litters_df = janitor::clean_names(litters_df)

names(litters_df)
```

    ## [1] "group"           "litter_number"   "gd0_weight"      "gd18_weight"    
    ## [5] "gd_of_birth"     "pups_born_alive" "pups_dead_birth" "pups_survive"

``` r
view(litters_df)
```

import second dataset

``` r
pups_df =
  read_csv("data/FAS_pups.csv", skip = 3, na = c("","NA","."))
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
read_csv(
        file = "C:/Users/brome/Downloads/data science/data_wrangling_i/data/FAS_litters.csv",
        skip = 3)
```

    ## Rows: 46 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Con7, #5/5/3/83/3-3, 26, 41.4
    ## dbl (4): 19, 6, 0, 5
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## # A tibble: 46 × 8
    ##    Con7  `#5/5/3/83/3-3` `26`  `41.4`  `19`   `6`   `0`   `5`
    ##    <chr> <chr>           <chr> <chr>  <dbl> <dbl> <dbl> <dbl>
    ##  1 Con7  #5/4/2/95/2     28.5  44.1      19     5     1     4
    ##  2 Con7  #4/2/95/3-3     <NA>  <NA>      20     6     0     6
    ##  3 Con7  #2/2/95/3-2     <NA>  <NA>      20     6     0     4
    ##  4 Con7  #1/5/3/83/3-3/2 <NA>  <NA>      20     9     0     9
    ##  5 Con8  #3/83/3-3       <NA>  <NA>      20     9     1     8
    ##  6 Con8  #2/95/3         <NA>  <NA>      20     8     0     8
    ##  7 Con8  #3/5/2/2/95     28.5  <NA>      20     8     0     8
    ##  8 Con8  #5/4/3/83/3     28    <NA>      19     9     0     8
    ##  9 Con8  #1/6/2/2/95-2   <NA>  <NA>      20     7     0     6
    ## 10 Con8  #3/5/3/83/3-3-2 <NA>  <NA>      20     8     0     8
    ## # ℹ 36 more rows

skimming

``` r
skimr::skim(pups_df)
```

|                                                  |         |
|:-------------------------------------------------|:--------|
| Name                                             | pups_df |
| Number of rows                                   | 313     |
| Number of columns                                | 6       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |         |
| Column type frequency:                           |         |
| character                                        | 1       |
| numeric                                          | 5       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |         |
| Group variables                                  | None    |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| Litter Number |         0 |             1 |   3 |  15 |     0 |       49 |          0 |

**Variable type: numeric**

| skim_variable | n_missing | complete_rate |  mean |   sd |  p0 | p25 | p50 | p75 | p100 | hist  |
|:--------------|----------:|--------------:|------:|-----:|----:|----:|----:|----:|-----:|:------|
| Sex           |         0 |          1.00 |  1.50 | 0.50 |   1 |   1 |   2 |   2 |    2 | ▇▁▁▁▇ |
| PD ears       |        18 |          0.94 |  3.68 | 0.59 |   2 |   3 |   4 |   4 |    5 | ▁▅▁▇▁ |
| PD eyes       |        13 |          0.96 | 12.99 | 0.62 |  12 |  13 |  13 |  13 |   15 | ▂▇▁▂▁ |
| PD pivot      |        13 |          0.96 |  7.09 | 1.51 |   4 |   6 |   7 |   8 |   12 | ▂▇▂▂▁ |
| PD walk       |         0 |          1.00 |  9.50 | 1.34 |   7 |   9 |   9 |  10 |   14 | ▆▇▇▂▁ |

## excel

``` r
mlb_df = read_excel("data/mlb11.xlsx")
```

look at data

``` r
mlb_df
```

    ## # A tibble: 30 × 12
    ##    team        runs at_bats  hits homeruns bat_avg strikeouts stolen_bases  wins
    ##    <chr>      <dbl>   <dbl> <dbl>    <dbl>   <dbl>      <dbl>        <dbl> <dbl>
    ##  1 Texas Ran…   855    5659  1599      210   0.283        930          143    96
    ##  2 Boston Re…   875    5710  1600      203   0.28        1108          102    90
    ##  3 Detroit T…   787    5563  1540      169   0.277       1143           49    95
    ##  4 Kansas Ci…   730    5672  1560      129   0.275       1006          153    71
    ##  5 St. Louis…   762    5532  1513      162   0.273        978           57    90
    ##  6 New York …   718    5600  1477      108   0.264       1085          130    77
    ##  7 New York …   867    5518  1452      222   0.263       1138          147    97
    ##  8 Milwaukee…   721    5447  1422      185   0.261       1083           94    96
    ##  9 Colorado …   735    5544  1429      163   0.258       1201          118    73
    ## 10 Houston A…   615    5598  1442       95   0.258       1164          118    56
    ## # ℹ 20 more rows
    ## # ℹ 3 more variables: new_onbase <dbl>, new_slug <dbl>, new_obs <dbl>

import FOTR words

``` r
fotr_df = 
  read_excel(
    "data/LotR_Words.xlsx",
    range = "B3:D6"
  )

fotr_df
```

    ## # A tibble: 3 × 3
    ##   Race   Female  Male
    ##   <chr>   <dbl> <dbl>
    ## 1 Elf      1229   971
    ## 2 Hobbit     14  3644
    ## 3 Man         0  1995

## import SAS

read in the PULSE dataset

``` r
pulse_df =
  read_sas("data/public_pulse_data.sas7bdat")

pulse_df = janitor::clean_names(pulse_df)
```
