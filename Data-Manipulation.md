Data Manipulation with dplyr
================
Junxian Chen (jc5314)
9/19/2019

## Selecting

``` r
select(litters_data, group, litter_number, starts_with("pups"))
```

    ## # A tibble: 49 x 5
    ##   group litter_number pups_born_alive pups_dead_birth pups_survive
    ##   <chr> <chr>                   <int>           <int>        <int>
    ## 1 Con7  #85                         3               4            3
    ## 2 Con7  #1/2/95/2                   8               0            7
    ## 3 Con7  #5/5/3/83/3-3               6               0            5
    ## # … with 46 more rows

``` r
select(litters_data, litter_number, group, everything())
```

    ## # A tibble: 49 x 8
    ##   litter_number group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr>         <chr>      <dbl>       <dbl>       <int>           <int>
    ## 1 #85           Con7        19.7        34.7          20               3
    ## 2 #1/2/95/2     Con7        27          42            19               8
    ## 3 #5/5/3/83/3-3 Con7        26          41.4          19               6
    ## # … with 46 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
# remove variable
select(litters_data, -group)
```

    ## # A tibble: 49 x 7
    ##   litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 #85                 19.7        34.7          20               3
    ## 2 #1/2/95/2           27          42            19               8
    ## 3 #5/5/3/83/3-3       26          41.4          19               6
    ## # … with 46 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
select(litters_data, litter_number, gd0_weight:pups_born_alive)
```

    ## # A tibble: 49 x 5
    ##   litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 #85                 19.7        34.7          20               3
    ## 2 #1/2/95/2           27          42            19               8
    ## 3 #5/5/3/83/3-3       26          41.4          19               6
    ## # … with 46 more rows

``` r
# renmae the variable
select(litters_data, GROUP = group, litter_number)
```

    ## # A tibble: 49 x 2
    ##   GROUP litter_number
    ##   <chr> <chr>        
    ## 1 Con7  #85          
    ## 2 Con7  #1/2/95/2    
    ## 3 Con7  #5/5/3/83/3-3
    ## # … with 46 more rows

``` r
# just rename the variable but no selection
rename(litters_data, GROUP = group)
```

    ## # A tibble: 49 x 8
    ##   GROUP litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # … with 46 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

## Filtering

``` r
filter(litters_data, group == 'Con7')
```

    ## # A tibble: 7 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## 4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ## 5 Con7  #4/2/95/3-3         NA          NA            20               6
    ## 6 Con7  #2/2/95/3-2         NA          NA            20               6
    ## 7 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ## # … with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
filter(litters_data, pups_born_alive < 6)
```

    ## # A tibble: 8 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ## 3 Con8  #2/2/95/2           NA          NA            19               5
    ## 4 Mod7  #3/82/3-2           28          45.9          20               5
    ## 5 Mod7  #5/3/83/5-2         22.6        37            19               5
    ## 6 Mod7  #106                21.7        37.8          20               5
    ## 7 Low7  #111                25.5        44.6          20               3
    ## 8 Low8  #4/84               21.8        35.2          20               4
    ## # … with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
# group == con7 and/or con8
filter(litters_data, group %in% c("Con7", "Con8"))
```

    ## # A tibble: 15 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  8 Con8  #3/83/3-3           NA          NA            20               9
    ##  9 Con8  #2/95/3             NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95         28.5        NA            20               8
    ## 11 Con8  #5/4/3/83/3         28          NA            19               9
    ## 12 Con8  #1/6/2/2/95-2       NA          NA            20               7
    ## 13 Con8  #3/5/3/83/3-…       NA          NA            20               8
    ## 14 Con8  #2/2/95/2           NA          NA            19               5
    ## 15 Con8  #3/6/2/2/95-3       NA          NA            20               7
    ## # … with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
filter(litters_data, group == 'Con7' | group == 'Con8')
```

    ## # A tibble: 15 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  8 Con8  #3/83/3-3           NA          NA            20               9
    ##  9 Con8  #2/95/3             NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95         28.5        NA            20               8
    ## 11 Con8  #5/4/3/83/3         28          NA            19               9
    ## 12 Con8  #1/6/2/2/95-2       NA          NA            20               7
    ## 13 Con8  #3/5/3/83/3-…       NA          NA            20               8
    ## 14 Con8  #2/2/95/2           NA          NA            19               5
    ## 15 Con8  #3/6/2/2/95-3       NA          NA            20               7
    ## # … with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
filter(litters_data, gd0_weight < gd18_weight)
```

    ## # A tibble: 31 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # … with 28 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
# don't do this:
filter(litters_data, !is.na(gd0_weight))
```

    ## # A tibble: 34 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # … with 31 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
# recommend:
drop_na(litters_data, gd0_weight)
```

    ## # A tibble: 34 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # … with 31 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

## Mutate the data

``` r
mutate(
  litters_data, 
  wt_gain = gd18_weight - gd0_weight,
  group = str_to_lower(group),
  group = str_to_upper(group))
```

    ## # A tibble: 49 x 9
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 CON7  #85                 19.7        34.7          20               3
    ## 2 CON7  #1/2/95/2           27          42            19               8
    ## 3 CON7  #5/5/3/83/3-3       26          41.4          19               6
    ## # … with 46 more rows, and 3 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>, wt_gain <dbl>

## Arrange

``` r
arrange(litters_data, pups_born_alive)
```

    ## # A tibble: 49 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Low7  #111                25.5        44.6          20               3
    ## 3 Low8  #4/84               21.8        35.2          20               4
    ## # … with 46 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
arrange(litters_data, pups_born_alive, gd0_weight)
```

    ## # A tibble: 49 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Low7  #111                25.5        44.6          20               3
    ## 3 Low8  #4/84               21.8        35.2          20               4
    ## # … with 46 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

## Example

### First option

``` r
litters_data = 
  read_csv("./FAS_litters.csv", col_types = "ccddiiii") %>%
  janitor::clean_names() %>%
  select(-pups_survive) %>%
  mutate(
    wt_gain = gd18_weight - gd0_weight,
    group = str_to_lower(group)) %>% 
  drop_na(wt_gain)

litters_data
```

    ## # A tibble: 31 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 con7  #85                 19.7        34.7          20               3
    ## 2 con7  #1/2/95/2           27          42            19               8
    ## 3 con7  #5/5/3/83/3-3       26          41.4          19               6
    ## # … with 28 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   wt_gain <dbl>
