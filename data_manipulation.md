Data Manipulation
================
Ford Holland

## Import data

``` r
# read dataset
litters_data = read_csv("Data/FAS_litters.csv")
```

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

``` r
pups_data = read_csv("Data/FAS_pups.csv")
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
litters_data <- janitor::clean_names(litters_data)
pups_data <- janitor::clean_names(pups_data)


# clean names
litters_data = janitor::clean_names(litters_data)

# view data
glimpse(litters_data)
```

    ## Observations: 49
    ## Variables: 8
    ## $ group           <chr> "Con7", "Con7", "Con7", "Con7", "Con7", "Con7"...
    ## $ litter_number   <chr> "#85", "#1/2/95/2", "#5/5/3/83/3-3", "#5/4/2/9...
    ## $ gd0_weight      <dbl> 19.7, 27.0, 26.0, 28.5, NA, NA, NA, NA, NA, 28...
    ## $ gd18_weight     <dbl> 34.7, 42.0, 41.4, 44.1, NA, NA, NA, NA, NA, NA...
    ## $ gd_of_birth     <dbl> 20, 19, 19, 19, 20, 20, 20, 20, 20, 20, 19, 20...
    ## $ pups_born_alive <dbl> 3, 8, 6, 5, 6, 6, 9, 9, 8, 8, 9, 7, 8, 5, 7, 8...
    ## $ pups_dead_birth <dbl> 4, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0...
    ## $ pups_survive    <dbl> 3, 7, 5, 4, 6, 4, 9, 8, 8, 8, 8, 6, 8, 4, 7, 5...

``` r
# brief summary
skimr::skim(litters_data)
```

    ## Skim summary statistics
    ##  n obs: 49 
    ##  n variables: 8 
    ## 
    ## -- Variable type:character -------------------------------------------------------------
    ##       variable missing complete  n min max empty n_unique
    ##          group       0       49 49   4   4     0        6
    ##  litter_number       0       49 49   3  15     0       49
    ## 
    ## -- Variable type:numeric ---------------------------------------------------------------
    ##         variable missing complete  n  mean   sd   p0   p25   p50   p75
    ##      gd_of_birth       0       49 49 19.65 0.48 19   19    20    20   
    ##       gd0_weight      15       34 49 24.38 3.28 17   22.3  24.1  26.67
    ##      gd18_weight      17       32 49 41.52 4.05 33.4 38.88 42.25 43.8 
    ##  pups_born_alive       0       49 49  7.35 1.76  3    6     8     8   
    ##  pups_dead_birth       0       49 49  0.33 0.75  0    0     0     0   
    ##     pups_survive       0       49 49  6.41 2.05  1    5     7     8   
    ##  p100     hist
    ##  20   <U+2585><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
    ##  33.4 <U+2581><U+2583><U+2587><U+2587><U+2587><U+2586><U+2581><U+2581>
    ##  52.7 <U+2582><U+2583><U+2583><U+2587><U+2586><U+2582><U+2581><U+2581>
    ##  11   <U+2582><U+2582><U+2583><U+2583><U+2587><U+2585><U+2581><U+2581>
    ##   4   <U+2587><U+2582><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
    ##   9   <U+2582><U+2582><U+2583><U+2583><U+2585><U+2587><U+2587><U+2585>

## Selecting

``` r
litters_data %>% 
  select(litter_number, starts_with("pups"))
```

    ## # A tibble: 49 x 4
    ##    litter_number   pups_born_alive pups_dead_birth pups_survive
    ##    <chr>                     <dbl>           <dbl>        <dbl>
    ##  1 #85                           3               4            3
    ##  2 #1/2/95/2                     8               0            7
    ##  3 #5/5/3/83/3-3                 6               0            5
    ##  4 #5/4/2/95/2                   5               1            4
    ##  5 #4/2/95/3-3                   6               0            6
    ##  6 #2/2/95/3-2                   6               0            4
    ##  7 #1/5/3/83/3-3/2               9               0            9
    ##  8 #3/83/3-3                     9               1            8
    ##  9 #2/95/3                       8               0            8
    ## 10 #3/5/2/2/95                   8               0            8
    ## # ... with 39 more rows

``` r
# arange
litters_data %>%
  select(litter_number, everything())
```

    ## # A tibble: 49 x 8
    ##    litter_number group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>         <chr>      <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85           Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2     Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3 Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2   Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3   Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2   Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-~ Con7        NA          NA            20               9
    ##  8 #3/83/3-3     Con8        NA          NA            20               9
    ##  9 #2/95/3       Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95   Con8        28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
litters_data %>% 
  select(litter_number, gd0_weight:pups_born_alive)
```

    ## # A tibble: 49 x 5
    ##    litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85                   19.7        34.7          20               3
    ##  2 #1/2/95/2             27          42            19               8
    ##  3 #5/5/3/83/3-3         26          41.4          19               6
    ##  4 #5/4/2/95/2           28.5        44.1          19               5
    ##  5 #4/2/95/3-3           NA          NA            20               6
    ##  6 #2/2/95/3-2           NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 #3/83/3-3             NA          NA            20               9
    ##  9 #2/95/3               NA          NA            20               8
    ## 10 #3/5/2/2/95           28.5        NA            20               8
    ## # ... with 39 more rows

``` r
litters_data %>% 
  select(-group)
```

    ## # A tibble: 49 x 7
    ##    litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85                 19.7        34.7          20               3
    ##  2 #1/2/95/2           27          42            19               8
    ##  3 #5/5/3/83/3-3       26          41.4          19               6
    ##  4 #5/4/2/95/2         28.5        44.1          19               5
    ##  5 #4/2/95/3-3         NA          NA            20               6
    ##  6 #2/2/95/3-2         NA          NA            20               6
    ##  7 #1/5/3/83/3-~       NA          NA            20               9
    ##  8 #3/83/3-3           NA          NA            20               9
    ##  9 #2/95/3             NA          NA            20               8
    ## 10 #3/5/2/2/95         28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
# rename
litters_data %>% 
  select(GROUP = group)
```

    ## # A tibble: 49 x 1
    ##    GROUP
    ##    <chr>
    ##  1 Con7 
    ##  2 Con7 
    ##  3 Con7 
    ##  4 Con7 
    ##  5 Con7 
    ##  6 Con7 
    ##  7 Con7 
    ##  8 Con8 
    ##  9 Con8 
    ## 10 Con8 
    ## # ... with 39 more rows

## Filtering

``` r
litters_data %>% 
  filter(group == "Con7")
```

    ## # A tibble: 7 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## 4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ## 5 Con7  #4/2/95/3-3         NA          NA            20               6
    ## 6 Con7  #2/2/95/3-2         NA          NA            20               6
    ## 7 Con7  #1/5/3/83/3-~       NA          NA            20               9
    ## # ... with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# can separateconditions by comma
litters_data %>% 
  filter(group == "Con7", 
         pups_born_alive > 2)
```

    ## # A tibble: 7 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## 4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ## 5 Con7  #4/2/95/3-3         NA          NA            20               6
    ## 6 Con7  #2/2/95/3-2         NA          NA            20               6
    ## 7 Con7  #1/5/3/83/3-~       NA          NA            20               9
    ## # ... with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
# dont filter !is.na()
# use drop_na
litters_data %>% 
  drop_na(gd0_weight)
```

    ## # A tibble: 34 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con8  #3/5/2/2/95         28.5        NA            20               8
    ##  6 Con8  #5/4/3/83/3         28          NA            19               9
    ##  7 Mod7  #59                 17          33.4          19               8
    ##  8 Mod7  #103                21.4        42.1          19               9
    ##  9 Mod7  #3/82/3-2           28          45.9          20               5
    ## 10 Mod7  #4/2/95/2           23.5        NA            19               9
    ## # ... with 24 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
# test contains()
# temp <- as.character(1:100)
# 
# contains("5", temp)
```

## Mutate

``` r
litters_data %>% 
  mutate(wt_gain = gd18_weight - gd0_weight,
         group = group %>% str_to_lower())
```

    ## # A tibble: 49 x 9
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 con7  #85                 19.7        34.7          20               3
    ##  2 con7  #1/2/95/2           27          42            19               8
    ##  3 con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 con7  #1/5/3/83/3-~       NA          NA            20               9
    ##  8 con8  #3/83/3-3           NA          NA            20               9
    ##  9 con8  #2/95/3             NA          NA            20               8
    ## 10 con8  #3/5/2/2/95         28.5        NA            20               8
    ## # ... with 39 more rows, and 3 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>, wt_gain <dbl>

## Arrange

``` r
litters_data %>% 
  arrange(desc(pups_born_alive))
```

    ## # A tibble: 49 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Low7  #102                22.6        43.3          20              11
    ##  2 Mod8  #5/93               NA          41.1          20              11
    ##  3 Con7  #1/5/3/83/3-~       NA          NA            20               9
    ##  4 Con8  #3/83/3-3           NA          NA            20               9
    ##  5 Con8  #5/4/3/83/3         28          NA            19               9
    ##  6 Mod7  #103                21.4        42.1          19               9
    ##  7 Mod7  #4/2/95/2           23.5        NA            19               9
    ##  8 Mod7  #8/110/3-2          NA          NA            20               9
    ##  9 Low7  #107                22.6        42.4          20               9
    ## 10 Low7  #98                 23.8        43.8          20               9
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

## Pipe

create a collection of commands

``` r
litters_data = 
  read_csv("./data/FAS_litters.csv", col_types = "ccddiiii") %>%
  janitor::clean_names() %>%
  select(-pups_survive) %>%
  mutate(
    wt_gain = gd18_weight - gd0_weight,
    group = str_to_lower(group)) %>% 
  drop_na(wt_gain)

litters_data
```

    ## # A tibble: 31 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 con7  #85                 19.7        34.7          20               3
    ##  2 con7  #1/2/95/2           27          42            19               8
    ##  3 con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 mod7  #59                 17          33.4          19               8
    ##  6 mod7  #103                21.4        42.1          19               9
    ##  7 mod7  #3/82/3-2           28          45.9          20               5
    ##  8 mod7  #5/3/83/5-2         22.6        37            19               5
    ##  9 mod7  #106                21.7        37.8          20               5
    ## 10 mod7  #94/2               24.4        42.9          19               7
    ## # ... with 21 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   wt_gain <dbl>

``` r
# . is last thing that happened in chain of commands
# this is how you pipe when the fist arg id not data, like grepl
ex = 
  read_csv("./data/FAS_litters.csv", col_types = "ccddiiii") %>%
  janitor::clean_names(dat = .) %>% 
  lm(gd0_weight ~ gd18_weight, data = .)
```
