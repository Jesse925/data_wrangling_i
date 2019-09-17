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
## ── Variable type:character ───────────────────────────────
##       variable missing complete  n min max empty n_unique
##          group       0       49 49   4   4     0        6
##  litter_number       0       49 49   3  15     0       49
## 
## ── Variable type:numeric ─────────────────────────────────
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
