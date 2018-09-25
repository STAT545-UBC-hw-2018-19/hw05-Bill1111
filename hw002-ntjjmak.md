hw02-ntjjmak
================
Nicole Mak
24/09/2018

## Let’s load the data.

``` r
library(gapminder)
library(tidyverse)
```

    ## -- Attaching packages --------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.0.0     v purrr   0.2.5
    ## v tibble  1.4.2     v dplyr   0.7.6
    ## v tidyr   0.8.1     v stringr 1.3.1
    ## v readr   1.1.1     v forcats 0.3.0

    ## -- Conflicts ------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

**What kind of data is this? Print it out.**

``` r
typeof(gapminder)
```

    ## [1] "list"

``` r
class(gapminder)
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

``` r
gapminder
```

    ## # A tibble: 1,704 x 6
    ##    country     continent  year lifeExp      pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779.
    ##  2 Afghanistan Asia       1957    30.3  9240934      821.
    ##  3 Afghanistan Asia       1962    32.0 10267083      853.
    ##  4 Afghanistan Asia       1967    34.0 11537966      836.
    ##  5 Afghanistan Asia       1972    36.1 13079460      740.
    ##  6 Afghanistan Asia       1977    38.4 14880372      786.
    ##  7 Afghanistan Asia       1982    39.9 12881816      978.
    ##  8 Afghanistan Asia       1987    40.8 13867957      852.
    ##  9 Afghanistan Asia       1992    41.7 16317921      649.
    ## 10 Afghanistan Asia       1997    41.8 22227415      635.
    ## # ... with 1,694 more rows

``` r
str(gapminder)
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    1704 obs. of  6 variables:
    ##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
    ##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
    ##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
    ##  $ gdpPercap: num  779 821 853 836 740 ...

``` r
ncol(gapminder)
```

    ## [1] 6

``` r
nrow(gapminder)
```

    ## [1] 1704

**Let’s examine life expectancy and gdp Per capita. What are the values,
ranges, distribution to be expected by continent? Here are some summary
tables:**

``` r
gapminder %>% 
  select(continent)%>% 
  summary()
```

    ##     continent  
    ##  Africa  :624  
    ##  Americas:300  
    ##  Asia    :396  
    ##  Europe  :360  
    ##  Oceania : 24

``` r
gapminder %>% 
  select(lifeExp) %>% 
  summary()
```

    ##     lifeExp     
    ##  Min.   :23.60  
    ##  1st Qu.:48.20  
    ##  Median :60.71  
    ##  Mean   :59.47  
    ##  3rd Qu.:70.85  
    ##  Max.   :82.60

**Values, ranges, distribution can also be explored visually using
graphs. Let’s also use a figure to examine the distribution and
frequency of values for the variable “Life Expectancy”.**

``` r
gapminder %>% 
  ggplot(aes(lifeExp)) +
  geom_histogram(binwidth = 1)
```

![](hw002-ntjjmak_files/figure-gfm/basic%20univariable%20histogram-1.png)<!-- -->

**Let’s try a density plot.**

``` r
gapminder %>% 
  ggplot(aes(lifeExp)) +
  geom_density(kernel = "gaussian")
```

![](hw002-ntjjmak_files/figure-gfm/basic%20univariable%20density%20plot-1.png)<!-- -->

**Let’s do a further exploration of life Expectancy and gdpPercap by
continent.**

First, we can explore by boxplot.

``` r
gapminder %>% 
  ggplot(aes(continent, lifeExp)) + 
  geom_boxplot()
```

![](hw002-ntjjmak_files/figure-gfm/experiment%20with%202%20variables-1.png)<!-- -->

``` r
gapminder %>% 
  ggplot(aes(continent, gdpPercap)) + 
  geom_boxplot()
```

![](hw002-ntjjmak_files/figure-gfm/experiment%20with%202%20variables-2.png)<!-- -->

**The boxplot exploring gdpPercap by continent is a bit difficult to
interpret. Let us transform it to a log scale.**

``` r
gapminder %>% 
  ggplot(aes(continent, log(gdpPercap))) + 
  geom_boxplot()
```

![](hw002-ntjjmak_files/figure-gfm/log%20transformation%20trial-1.png)<!-- -->

**To get an idea of which values are typical, we can alternatively use a
scatter plot so that all data points are seen. Transparency is added to
give an idea of which values are most frequent in the data set.**

``` r
gapminder %>% 
  ggplot(aes(continent, log(gdpPercap))) + 
  geom_point(alpha = 0.05)
```

![](hw002-ntjjmak_files/figure-gfm/experimenting%20with%20transparency-1.png)<!-- -->

**Here is some practice filtering to single countries, Canada and
China.Let’s see whether these countries see a rise in life expectancy
over the years.**

``` r
gapminder %>% 
  filter(country == "Canada") %>% 
  ggplot(aes(year, lifeExp)) +
  geom_point()
```

![](hw002-ntjjmak_files/figure-gfm/applying%20filtering%20and%20piping%20trial%201-1.png)<!-- -->

``` r
gapminder %>% 
  filter(country == "China") %>% 
  ggplot(aes(year, lifeExp)) +
  geom_point()
```

![](hw002-ntjjmak_files/figure-gfm/applying%20filtering%20and%20piping%20trial%201-2.png)<!-- -->

**Here is some more practice piping.**

``` r
gapminder %>% 
  filter(continent == "Oceania") %>% 
  filter(year > "1990") %>% 
  ggplot(aes(country, log(gdpPercap))) +
  geom_point()
```

![](hw002-ntjjmak_files/figure-gfm/building%20more%20piping%20and%20incorporating%20log%20transformation-1.png)<!-- -->

``` r
gapminder %>% 
  select(continent, lifeExp, gdpPercap) %>% 
  filter(lifeExp >= "75") %>% 
  ggplot(aes(continent, log(gdpPercap))) +
  geom_violin(fill = "black")
```

![](hw002-ntjjmak_files/figure-gfm/again%20experimenting%20with%20piping-1.png)<!-- -->

**Let’s play with colour.**

``` r
gapminder %>% 
  filter(year > "1970") %>%
  ggplot(aes(continent, mean(pop), fill = continent)) +
  geom_col()
```

![](hw002-ntjjmak_files/figure-gfm/more%20visualisation%20but%20with%20colour-1.png)<!-- -->

**Let’s try flipping it around.**

``` r
gapminder %>% 
  filter(year > "1970") %>%
  ggplot(aes(continent, mean(pop), fill = continent)) +
  geom_col() + 
  coord_flip()
```

![](hw002-ntjjmak_files/figure-gfm/flipping%20x%20and%20y-1.png)<!-- -->

**Lastly, let’s experiment a couple more `dplyr` functions.**

``` r
select(gapminder, -continent, - gdpPercap) %>% 
  filter(year == "2007") %>%
  arrange(lifeExp)
```

    ## # A tibble: 142 x 4
    ##    country                   year lifeExp      pop
    ##    <fct>                    <int>   <dbl>    <int>
    ##  1 Swaziland                 2007    39.6  1133066
    ##  2 Mozambique                2007    42.1 19951656
    ##  3 Zambia                    2007    42.4 11746035
    ##  4 Sierra Leone              2007    42.6  6144562
    ##  5 Lesotho                   2007    42.6  2012649
    ##  6 Angola                    2007    42.7 12420476
    ##  7 Zimbabwe                  2007    43.5 12311143
    ##  8 Afghanistan               2007    43.8 31889923
    ##  9 Central African Republic  2007    44.7  4369038
    ## 10 Liberia                   2007    45.7  3193942
    ## # ... with 132 more rows

## All done.
