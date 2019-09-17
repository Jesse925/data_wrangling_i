Data Import
================
Junxian Chen (jc5314)
9/17/2019

## Load in the dataset

``` r
# read in a dataset
litters_data = read_csv(file = "./FAS_litters.csv")
## Parsed with column specification:
## cols(
##   Group = col_character(),
##   `Litter Number` = col_character(),
##   `GD0 weight` = col_double(),
##   `GD18 weight` = col_double(),
##   `GD of Birth` = col_double(),
##   `Pups born alive` = col_double(),
##   `Pups dead @ birth` = col_double(),
##   `Pups survive` = col_double()
## )

names(litters_data)
## [1] "Group"             "Litter Number"     "GD0 weight"       
## [4] "GD18 weight"       "GD of Birth"       "Pups born alive"  
## [7] "Pups dead @ birth" "Pups survive"

litters_data = janitor::clean_names(litters_data)
names(litters_data)
## [1] "group"           "litter_number"   "gd0_weight"      "gd18_weight"    
## [5] "gd_of_birth"     "pups_born_alive" "pups_dead_birth" "pups_survive"

skimr::skim(litters_data)
## Skim summary statistics
##  n obs: 49 
##  n variables: 8 
## 
## ── Variable type:character ──────────────────────────
##       variable missing complete  n min max empty n_unique
##          group       0       49 49   4   4     0        6
##  litter_number       0       49 49   3  15     0       49
## 
## ── Variable type:numeric ────────────────────────────
##         variable missing complete  n  mean   sd   p0   p25   p50   p75
##      gd_of_birth       0       49 49 19.65 0.48 19   19    20    20   
##       gd0_weight      15       34 49 24.38 3.28 17   22.3  24.1  26.67
##      gd18_weight      17       32 49 41.52 4.05 33.4 38.88 42.25 43.8 
##  pups_born_alive       0       49 49  7.35 1.76  3    6     8     8   
##  pups_dead_birth       0       49 49  0.33 0.75  0    0     0     0   
##     pups_survive       0       49 49  6.41 2.05  1    5     7     8   
##  p100     hist
##  20   ▅▁▁▁▁▁▁▇
##  33.4 ▁▃▇▇▇▆▁▁
##  52.7 ▂▃▃▇▆▂▁▁
##  11   ▂▂▃▃▇▅▁▁
##   4   ▇▂▁▁▁▁▁▁
##   9   ▂▂▃▃▅▇▇▅
```

## Load in another dataset

``` r
pups_data = read_csv(file = "./FAS_pups.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   `Litter Number` = col_character(),
    ##   Sex = col_double(),
    ##   `PD ears` = col_double(),
    ##   `PD eyes` = col_double(),
    ##   `PD pivot` = col_double(),
    ##   `PD walk` = col_double()
    ## )

``` r
names(pups_data)
```

    ## [1] "Litter Number" "Sex"           "PD ears"       "PD eyes"      
    ## [5] "PD pivot"      "PD walk"

``` r
pups_data = janitor::clean_names(pups_data)
names(pups_data)
```

    ## [1] "litter_number" "sex"           "pd_ears"       "pd_eyes"      
    ## [5] "pd_pivot"      "pd_walk"

``` r
litters_data = read_csv(file = "./FAS_litters.csv",
  skip = 10, col_names = FALSE)
```

    ## Parsed with column specification:
    ## cols(
    ##   X1 = col_character(),
    ##   X2 = col_character(),
    ##   X3 = col_double(),
    ##   X4 = col_double(),
    ##   X5 = col_double(),
    ##   X6 = col_double(),
    ##   X7 = col_double(),
    ##   X8 = col_double()
    ## )

## Column parsinh

``` r
litters_data = read_csv(
  file = "./FAS_litters.csv",
  col_types = cols(
    Group = col_character(),
    `Litter Number` = col_character(),
    `GD0 weight` = col_double(),
    `GD18 weight` = col_double(),
    `GD of Birth` = col_integer(),
    `Pups born alive` = col_integer(),
    `Pups dead @ birth` = col_integer(),
    `Pups survive` = col_integer()
  )
)

tail(litters_data)
```

    ## # A tibble: 6 x 8
    ##   Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##   <chr> <chr>                  <dbl>         <dbl>         <int>
    ## 1 Low8  #79                     25.4          43.8            19
    ## 2 Low8  #100                    20            39.2            20
    ## 3 Low8  #4/84                   21.8          35.2            20
    ## 4 Low8  #108                    25.6          47.5            20
    ## 5 Low8  #99                     23.5          39              20
    ## 6 Low8  #110                    25.5          42.7            20
    ## # … with 3 more variables: `Pups born alive` <int>, `Pups dead @
    ## #   birth` <int>, `Pups survive` <int>

## Read in an excel file

``` r
library(readxl)

mlb11_data = read_excel("./mlb11.xlsx", n_max = 20)
#mlb11_data = read_excel(
#  path = "./mlb11.xlsx",
#  sheet = xxx,
#  range = "A1:B7")

head(mlb11_data, 5)
```

    ## # A tibble: 5 x 12
    ##   team   runs at_bats  hits homeruns bat_avg strikeouts stolen_bases  wins
    ##   <chr> <dbl>   <dbl> <dbl>    <dbl>   <dbl>      <dbl>        <dbl> <dbl>
    ## 1 Texa…   855    5659  1599      210   0.283        930          143    96
    ## 2 Bost…   875    5710  1600      203   0.28        1108          102    90
    ## 3 Detr…   787    5563  1540      169   0.277       1143           49    95
    ## 4 Kans…   730    5672  1560      129   0.275       1006          153    71
    ## 5 St. …   762    5532  1513      162   0.273        978           57    90
    ## # … with 3 more variables: new_onbase <dbl>, new_slug <dbl>, new_obs <dbl>

## Read in SAS

``` r
library(haven)

pulse_data = read_sas("./public_pulse_data.sas7bdat")

head(pulse_data, 5)
```

    ## # A tibble: 5 x 7
    ##      ID   age Sex   BDIScore_BL BDIScore_01m BDIScore_06m BDIScore_12m
    ##   <dbl> <dbl> <chr>       <dbl>        <dbl>        <dbl>        <dbl>
    ## 1 10003  48.0 male            7            1            2            0
    ## 2 10015  72.5 male            6           NA           NA           NA
    ## 3 10022  58.5 male           14            3            8           NA
    ## 4 10026  72.7 male           20            6           18           16
    ## 5 10035  60.4 male            4            0            1            2
