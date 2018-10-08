STAT545\_hmk4\_WilliamHall
================
William Hall
2018-10-04

Data Reshaping Prompts
----------------------

> Activity \#2

Make a tibble with one row per year and columns for life expectancy for two or more countries.

-   Use knitr::kable() to make this table look pretty in your rendered homework.
-   Take advantage of this new data shape to scatterplot life expectancy for one country against that of another.

The first thing we need to do is install the kable package.

``` r
#install.packages("kableExtra")
library(knitr)
library(kableExtra)
library(gapminder)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(readxl)
```

So let's have a look at the gapminder dataset without any processing with kable()

``` r
(mindthegap <- gapminder[1:10, ])
```

    ## # A tibble: 10 x 6
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

need to get the table displaying inline, and not in the window....
------------------------------------------------------------------

Gross. Now let's kable it.

``` r
mindthegap %>%
  kable() %>%
  kable_styling()
```

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
country
</th>
<th style="text-align:left;">
continent
</th>
<th style="text-align:right;">
year
</th>
<th style="text-align:right;">
lifeExp
</th>
<th style="text-align:right;">
pop
</th>
<th style="text-align:right;">
gdpPercap
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1952
</td>
<td style="text-align:right;">
28.801
</td>
<td style="text-align:right;">
8425333
</td>
<td style="text-align:right;">
779.4453
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1957
</td>
<td style="text-align:right;">
30.332
</td>
<td style="text-align:right;">
9240934
</td>
<td style="text-align:right;">
820.8530
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1962
</td>
<td style="text-align:right;">
31.997
</td>
<td style="text-align:right;">
10267083
</td>
<td style="text-align:right;">
853.1007
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1967
</td>
<td style="text-align:right;">
34.020
</td>
<td style="text-align:right;">
11537966
</td>
<td style="text-align:right;">
836.1971
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1972
</td>
<td style="text-align:right;">
36.088
</td>
<td style="text-align:right;">
13079460
</td>
<td style="text-align:right;">
739.9811
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1977
</td>
<td style="text-align:right;">
38.438
</td>
<td style="text-align:right;">
14880372
</td>
<td style="text-align:right;">
786.1134
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1982
</td>
<td style="text-align:right;">
39.854
</td>
<td style="text-align:right;">
12881816
</td>
<td style="text-align:right;">
978.0114
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1987
</td>
<td style="text-align:right;">
40.822
</td>
<td style="text-align:right;">
13867957
</td>
<td style="text-align:right;">
852.3959
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1992
</td>
<td style="text-align:right;">
41.674
</td>
<td style="text-align:right;">
16317921
</td>
<td style="text-align:right;">
649.3414
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1997
</td>
<td style="text-align:right;">
41.763
</td>
<td style="text-align:right;">
22227415
</td>
<td style="text-align:right;">
635.3414
</td>
</tr>
</tbody>
</table>
Cute. Now let's make different coloured lines.

``` r
kable(mindthegap) %>%
  kable_styling(bootstrap_options = c("striped", "hover"))
```

<table class="table table-striped table-hover" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
country
</th>
<th style="text-align:left;">
continent
</th>
<th style="text-align:right;">
year
</th>
<th style="text-align:right;">
lifeExp
</th>
<th style="text-align:right;">
pop
</th>
<th style="text-align:right;">
gdpPercap
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1952
</td>
<td style="text-align:right;">
28.801
</td>
<td style="text-align:right;">
8425333
</td>
<td style="text-align:right;">
779.4453
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1957
</td>
<td style="text-align:right;">
30.332
</td>
<td style="text-align:right;">
9240934
</td>
<td style="text-align:right;">
820.8530
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1962
</td>
<td style="text-align:right;">
31.997
</td>
<td style="text-align:right;">
10267083
</td>
<td style="text-align:right;">
853.1007
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1967
</td>
<td style="text-align:right;">
34.020
</td>
<td style="text-align:right;">
11537966
</td>
<td style="text-align:right;">
836.1971
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1972
</td>
<td style="text-align:right;">
36.088
</td>
<td style="text-align:right;">
13079460
</td>
<td style="text-align:right;">
739.9811
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1977
</td>
<td style="text-align:right;">
38.438
</td>
<td style="text-align:right;">
14880372
</td>
<td style="text-align:right;">
786.1134
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1982
</td>
<td style="text-align:right;">
39.854
</td>
<td style="text-align:right;">
12881816
</td>
<td style="text-align:right;">
978.0114
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1987
</td>
<td style="text-align:right;">
40.822
</td>
<td style="text-align:right;">
13867957
</td>
<td style="text-align:right;">
852.3959
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1992
</td>
<td style="text-align:right;">
41.674
</td>
<td style="text-align:right;">
16317921
</td>
<td style="text-align:right;">
649.3414
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1997
</td>
<td style="text-align:right;">
41.763
</td>
<td style="text-align:right;">
22227415
</td>
<td style="text-align:right;">
635.3414
</td>
</tr>
</tbody>
</table>
Okkkk. But those rows look a little big. Let's make them smaller

``` r
kable(mindthegap) %>%
  kable_styling(bootstrap_options = c("striped", "hover", "condensed"))
```

<table class="table table-striped table-hover table-condensed" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
country
</th>
<th style="text-align:left;">
continent
</th>
<th style="text-align:right;">
year
</th>
<th style="text-align:right;">
lifeExp
</th>
<th style="text-align:right;">
pop
</th>
<th style="text-align:right;">
gdpPercap
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1952
</td>
<td style="text-align:right;">
28.801
</td>
<td style="text-align:right;">
8425333
</td>
<td style="text-align:right;">
779.4453
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1957
</td>
<td style="text-align:right;">
30.332
</td>
<td style="text-align:right;">
9240934
</td>
<td style="text-align:right;">
820.8530
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1962
</td>
<td style="text-align:right;">
31.997
</td>
<td style="text-align:right;">
10267083
</td>
<td style="text-align:right;">
853.1007
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1967
</td>
<td style="text-align:right;">
34.020
</td>
<td style="text-align:right;">
11537966
</td>
<td style="text-align:right;">
836.1971
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1972
</td>
<td style="text-align:right;">
36.088
</td>
<td style="text-align:right;">
13079460
</td>
<td style="text-align:right;">
739.9811
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1977
</td>
<td style="text-align:right;">
38.438
</td>
<td style="text-align:right;">
14880372
</td>
<td style="text-align:right;">
786.1134
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1982
</td>
<td style="text-align:right;">
39.854
</td>
<td style="text-align:right;">
12881816
</td>
<td style="text-align:right;">
978.0114
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1987
</td>
<td style="text-align:right;">
40.822
</td>
<td style="text-align:right;">
13867957
</td>
<td style="text-align:right;">
852.3959
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1992
</td>
<td style="text-align:right;">
41.674
</td>
<td style="text-align:right;">
16317921
</td>
<td style="text-align:right;">
649.3414
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1997
</td>
<td style="text-align:right;">
41.763
</td>
<td style="text-align:right;">
22227415
</td>
<td style="text-align:right;">
635.3414
</td>
</tr>
</tbody>
</table>
Ok fine. But I want the table on the left.

``` r
kable(mindthegap) %>%
  kable_styling(bootstrap_options = "striped", full_width = F, position = "left")
```

<table class="table table-striped" style="width: auto !important; ">
<thead>
<tr>
<th style="text-align:left;">
country
</th>
<th style="text-align:left;">
continent
</th>
<th style="text-align:right;">
year
</th>
<th style="text-align:right;">
lifeExp
</th>
<th style="text-align:right;">
pop
</th>
<th style="text-align:right;">
gdpPercap
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1952
</td>
<td style="text-align:right;">
28.801
</td>
<td style="text-align:right;">
8425333
</td>
<td style="text-align:right;">
779.4453
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1957
</td>
<td style="text-align:right;">
30.332
</td>
<td style="text-align:right;">
9240934
</td>
<td style="text-align:right;">
820.8530
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1962
</td>
<td style="text-align:right;">
31.997
</td>
<td style="text-align:right;">
10267083
</td>
<td style="text-align:right;">
853.1007
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1967
</td>
<td style="text-align:right;">
34.020
</td>
<td style="text-align:right;">
11537966
</td>
<td style="text-align:right;">
836.1971
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1972
</td>
<td style="text-align:right;">
36.088
</td>
<td style="text-align:right;">
13079460
</td>
<td style="text-align:right;">
739.9811
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1977
</td>
<td style="text-align:right;">
38.438
</td>
<td style="text-align:right;">
14880372
</td>
<td style="text-align:right;">
786.1134
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1982
</td>
<td style="text-align:right;">
39.854
</td>
<td style="text-align:right;">
12881816
</td>
<td style="text-align:right;">
978.0114
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1987
</td>
<td style="text-align:right;">
40.822
</td>
<td style="text-align:right;">
13867957
</td>
<td style="text-align:right;">
852.3959
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1992
</td>
<td style="text-align:right;">
41.674
</td>
<td style="text-align:right;">
16317921
</td>
<td style="text-align:right;">
649.3414
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1997
</td>
<td style="text-align:right;">
41.763
</td>
<td style="text-align:right;">
22227415
</td>
<td style="text-align:right;">
635.3414
</td>
</tr>
</tbody>
</table>
Just joking. I want it on the right - and I want the text beside it.

how do I do this? Here is where I got it from: <https://cran.r-project.org/web/packages/kableExtra/vignettes/awesome_table_in_html.html>
----------------------------------------------------------------------------------------------------------------------------------------

``` r
kable(mindthegap) %>%
  kable_styling(bootstrap_options = "striped", full_width = F, position = "float_right")
```

<table class="table table-striped" style="width: auto !important; float: right; margin-left: 10px;">
<thead>
<tr>
<th style="text-align:left;">
country
</th>
<th style="text-align:left;">
continent
</th>
<th style="text-align:right;">
year
</th>
<th style="text-align:right;">
lifeExp
</th>
<th style="text-align:right;">
pop
</th>
<th style="text-align:right;">
gdpPercap
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1952
</td>
<td style="text-align:right;">
28.801
</td>
<td style="text-align:right;">
8425333
</td>
<td style="text-align:right;">
779.4453
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1957
</td>
<td style="text-align:right;">
30.332
</td>
<td style="text-align:right;">
9240934
</td>
<td style="text-align:right;">
820.8530
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1962
</td>
<td style="text-align:right;">
31.997
</td>
<td style="text-align:right;">
10267083
</td>
<td style="text-align:right;">
853.1007
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1967
</td>
<td style="text-align:right;">
34.020
</td>
<td style="text-align:right;">
11537966
</td>
<td style="text-align:right;">
836.1971
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1972
</td>
<td style="text-align:right;">
36.088
</td>
<td style="text-align:right;">
13079460
</td>
<td style="text-align:right;">
739.9811
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1977
</td>
<td style="text-align:right;">
38.438
</td>
<td style="text-align:right;">
14880372
</td>
<td style="text-align:right;">
786.1134
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1982
</td>
<td style="text-align:right;">
39.854
</td>
<td style="text-align:right;">
12881816
</td>
<td style="text-align:right;">
978.0114
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1987
</td>
<td style="text-align:right;">
40.822
</td>
<td style="text-align:right;">
13867957
</td>
<td style="text-align:right;">
852.3959
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1992
</td>
<td style="text-align:right;">
41.674
</td>
<td style="text-align:right;">
16317921
</td>
<td style="text-align:right;">
649.3414
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1997
</td>
<td style="text-align:right;">
41.763
</td>
<td style="text-align:right;">
22227415
</td>
<td style="text-align:right;">
635.3414
</td>
</tr>
</tbody>
</table>
Ok now what if I want to change font size.

``` r
kable(mindthegap) %>%
  kable_styling(bootstrap_options = "striped", font_size = 14)
```

<table class="table table-striped" style="font-size: 14px; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
country
</th>
<th style="text-align:left;">
continent
</th>
<th style="text-align:right;">
year
</th>
<th style="text-align:right;">
lifeExp
</th>
<th style="text-align:right;">
pop
</th>
<th style="text-align:right;">
gdpPercap
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1952
</td>
<td style="text-align:right;">
28.801
</td>
<td style="text-align:right;">
8425333
</td>
<td style="text-align:right;">
779.4453
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1957
</td>
<td style="text-align:right;">
30.332
</td>
<td style="text-align:right;">
9240934
</td>
<td style="text-align:right;">
820.8530
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1962
</td>
<td style="text-align:right;">
31.997
</td>
<td style="text-align:right;">
10267083
</td>
<td style="text-align:right;">
853.1007
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1967
</td>
<td style="text-align:right;">
34.020
</td>
<td style="text-align:right;">
11537966
</td>
<td style="text-align:right;">
836.1971
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1972
</td>
<td style="text-align:right;">
36.088
</td>
<td style="text-align:right;">
13079460
</td>
<td style="text-align:right;">
739.9811
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1977
</td>
<td style="text-align:right;">
38.438
</td>
<td style="text-align:right;">
14880372
</td>
<td style="text-align:right;">
786.1134
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1982
</td>
<td style="text-align:right;">
39.854
</td>
<td style="text-align:right;">
12881816
</td>
<td style="text-align:right;">
978.0114
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1987
</td>
<td style="text-align:right;">
40.822
</td>
<td style="text-align:right;">
13867957
</td>
<td style="text-align:right;">
852.3959
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1992
</td>
<td style="text-align:right;">
41.674
</td>
<td style="text-align:right;">
16317921
</td>
<td style="text-align:right;">
649.3414
</td>
</tr>
<tr>
<td style="text-align:left;">
Afghanistan
</td>
<td style="text-align:left;">
Asia
</td>
<td style="text-align:right;">
1997
</td>
<td style="text-align:right;">
41.763
</td>
<td style="text-align:right;">
22227415
</td>
<td style="text-align:right;">
635.3414
</td>
</tr>
</tbody>
</table>
Cool. Now what if we want to high year 1972 and 1992.

``` r
kable(mindthegap) %>%
  kable_styling("striped", full_width = F) %>%
  column_spec(1:6, bold = T) %>%
  row_spec(c(5,9), bold = T, color = "white", background = "#D7261E")
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
country
</th>
<th style="text-align:left;">
continent
</th>
<th style="text-align:right;">
year
</th>
<th style="text-align:right;">
lifeExp
</th>
<th style="text-align:right;">
pop
</th>
<th style="text-align:right;">
gdpPercap
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1952
</td>
<td style="text-align:right;font-weight: bold;">
28.801
</td>
<td style="text-align:right;font-weight: bold;">
8425333
</td>
<td style="text-align:right;font-weight: bold;">
779.4453
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1957
</td>
<td style="text-align:right;font-weight: bold;">
30.332
</td>
<td style="text-align:right;font-weight: bold;">
9240934
</td>
<td style="text-align:right;font-weight: bold;">
820.8530
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1962
</td>
<td style="text-align:right;font-weight: bold;">
31.997
</td>
<td style="text-align:right;font-weight: bold;">
10267083
</td>
<td style="text-align:right;font-weight: bold;">
853.1007
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1967
</td>
<td style="text-align:right;font-weight: bold;">
34.020
</td>
<td style="text-align:right;font-weight: bold;">
11537966
</td>
<td style="text-align:right;font-weight: bold;">
836.1971
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
Asia
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
1972
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
36.088
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
13079460
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
739.9811
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1977
</td>
<td style="text-align:right;font-weight: bold;">
38.438
</td>
<td style="text-align:right;font-weight: bold;">
14880372
</td>
<td style="text-align:right;font-weight: bold;">
786.1134
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1982
</td>
<td style="text-align:right;font-weight: bold;">
39.854
</td>
<td style="text-align:right;font-weight: bold;">
12881816
</td>
<td style="text-align:right;font-weight: bold;">
978.0114
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1987
</td>
<td style="text-align:right;font-weight: bold;">
40.822
</td>
<td style="text-align:right;font-weight: bold;">
13867957
</td>
<td style="text-align:right;font-weight: bold;">
852.3959
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
Asia
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
1992
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
41.674
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
16317921
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
649.3414
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1997
</td>
<td style="text-align:right;font-weight: bold;">
41.763
</td>
<td style="text-align:right;font-weight: bold;">
22227415
</td>
<td style="text-align:right;font-weight: bold;">
635.3414
</td>
</tr>
</tbody>
</table>
Sweet. So now lets put some headers above our columns.

``` r
kable(mindthegap) %>%
  kable_styling(c("striped", "bordered"), full_width = F) %>%
  column_spec(1:6, bold = T) %>%
  row_spec(c(5,9), bold = T, color = "white", background = "#D7261E") %>% 
  add_header_above(c("Place" = 2, " " = 4))
```

<table class="table table-striped table-bordered" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2">
Place

</th>
<th style="border-bottom:hidden" colspan="4">
</th>
</tr>
<tr>
<th style="text-align:left;">
country
</th>
<th style="text-align:left;">
continent
</th>
<th style="text-align:right;">
year
</th>
<th style="text-align:right;">
lifeExp
</th>
<th style="text-align:right;">
pop
</th>
<th style="text-align:right;">
gdpPercap
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1952
</td>
<td style="text-align:right;font-weight: bold;">
28.801
</td>
<td style="text-align:right;font-weight: bold;">
8425333
</td>
<td style="text-align:right;font-weight: bold;">
779.4453
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1957
</td>
<td style="text-align:right;font-weight: bold;">
30.332
</td>
<td style="text-align:right;font-weight: bold;">
9240934
</td>
<td style="text-align:right;font-weight: bold;">
820.8530
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1962
</td>
<td style="text-align:right;font-weight: bold;">
31.997
</td>
<td style="text-align:right;font-weight: bold;">
10267083
</td>
<td style="text-align:right;font-weight: bold;">
853.1007
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1967
</td>
<td style="text-align:right;font-weight: bold;">
34.020
</td>
<td style="text-align:right;font-weight: bold;">
11537966
</td>
<td style="text-align:right;font-weight: bold;">
836.1971
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
Asia
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
1972
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
36.088
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
13079460
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
739.9811
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1977
</td>
<td style="text-align:right;font-weight: bold;">
38.438
</td>
<td style="text-align:right;font-weight: bold;">
14880372
</td>
<td style="text-align:right;font-weight: bold;">
786.1134
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1982
</td>
<td style="text-align:right;font-weight: bold;">
39.854
</td>
<td style="text-align:right;font-weight: bold;">
12881816
</td>
<td style="text-align:right;font-weight: bold;">
978.0114
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1987
</td>
<td style="text-align:right;font-weight: bold;">
40.822
</td>
<td style="text-align:right;font-weight: bold;">
13867957
</td>
<td style="text-align:right;font-weight: bold;">
852.3959
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
Asia
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
1992
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
41.674
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
16317921
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white;background-color: #D7261E;">
649.3414
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;">
Afghanistan
</td>
<td style="text-align:left;font-weight: bold;">
Asia
</td>
<td style="text-align:right;font-weight: bold;">
1997
</td>
<td style="text-align:right;font-weight: bold;">
41.763
</td>
<td style="text-align:right;font-weight: bold;">
22227415
</td>
<td style="text-align:right;font-weight: bold;">
635.3414
</td>
</tr>
</tbody>
</table>
> Activity \#3

Compute some measure of life expectancy (mean? median? min? max?) for all possible combinations of continent and year. Reshape that to have one row per year and one variable for each continent. Or the other way around: one row per continent and one variable per year.

-   Use knitr::kable() to make these tables look pretty in your rendered homework.
-   Is there a plot that is easier to make with the data in this shape versis the usual form? If so (or you think so), try it! Reflect.

So what we are trying to do here is calculate the mean life expectancy for every combination of continent and year. Then reduce down to a table with just the year, continent, and mean. So let's use the group\_by and summarise function.

``` r
gapminder %>% 
  group_by(continent,year) %>%
  summarise(meanLife = mean(lifeExp))
```

    ## # A tibble: 60 x 3
    ## # Groups:   continent [?]
    ##    continent  year meanLife
    ##    <fct>     <int>    <dbl>
    ##  1 Africa     1952     39.1
    ##  2 Africa     1957     41.3
    ##  3 Africa     1962     43.3
    ##  4 Africa     1967     45.3
    ##  5 Africa     1972     47.5
    ##  6 Africa     1977     49.6
    ##  7 Africa     1982     51.6
    ##  8 Africa     1987     53.3
    ##  9 Africa     1992     53.6
    ## 10 Africa     1997     53.6
    ## # ... with 50 more rows

Join Prompts
------------

> Activity \#1

Create a second data frame, complementary to Gapminder. Join this with (part of) Gapminder using a dplyr join function and make some observations about the process and result. Explore the different types of joins. Examples of a second data frame you could build:

-   One row per country, a country variable and one or more variables with extra info, such as language spoken, NATO membership, national animal, or capitol city.
-   One row per continent, a continent variable and one or more variables with extra info, such as northern versus southern hemisphere.

So let's start with the countries, and their languages. We will begin by uploading a dataset with all the countries and their languages. Then remove all the NA's, then rename the columns (remember that the column name that you want to use to join must be identical in both datasets).

``` r
LanguageCountry <- read_excel("LanguageCountry.xlsx")

LangCountry <- LanguageCountry %>%
                        na.omit() 
colnames(LangCountry) <- c("country", "language")
LangCountry
```

    ## # A tibble: 241 x 2
    ##    country          language                                              
    ##    <chr>            <chr>                                                 
    ##  1 Afghanistan      Afghan Persian or Dari (official) 80% (Dari functions…
    ##  2 Akrotiri         English, Greek                                        
    ##  3 Albania          Albanian 98.8% (official - derived from Tosk dialect)…
    ##  4 Algeria          Arabic (official), French (lingua franca), Berber or …
    ##  5 American Samoa   Samoan 88.6% (closely related to Hawaiian and other P…
    ##  6 Andorra          Catalan (official), French, Castilian, Portuguese     
    ##  7 Angola           Portuguese 71.2% (official), Umbundu 23%, Kikongo 8.2…
    ##  8 Anguilla         English (official)                                    
    ##  9 Antigua and Bar… English (official), Antiguan creole                   
    ## 10 Argentina        Spanish (official), Italian, English, German, French,…
    ## # ... with 231 more rows

Now lets join it with the population of the gap minder dataset. Let's create the reduced gapminder dataset with only the population and country.

``` r
reducedGap <- gapminder %>%
                group_by(country) %>%
                summarise(meanpop = mean(pop)) %>%
                mutate_if(is.factor, as.character)
```

Join the two together with full join.

``` r
LangPopCountry <- full_join(LangCountry, reducedGap, by = "country")
LangPopCountry
```

    ## # A tibble: 254 x 3
    ##    country         language                                        meanpop
    ##    <chr>           <chr>                                             <dbl>
    ##  1 Afghanistan     Afghan Persian or Dari (official) 80% (Dari f…   1.58e7
    ##  2 Akrotiri        English, Greek                                  NA     
    ##  3 Albania         Albanian 98.8% (official - derived from Tosk …   2.58e6
    ##  4 Algeria         Arabic (official), French (lingua franca), Be…   1.99e7
    ##  5 American Samoa  Samoan 88.6% (closely related to Hawaiian and…  NA     
    ##  6 Andorra         Catalan (official), French, Castilian, Portug…  NA     
    ##  7 Angola          Portuguese 71.2% (official), Umbundu 23%, Kik…   7.31e6
    ##  8 Anguilla        English (official)                              NA     
    ##  9 Antigua and Ba… English (official), Antiguan creole             NA     
    ## 10 Argentina       Spanish (official), Italian, English, German,…   2.86e7
    ## # ... with 244 more rows

Reflection
----------

Had some problems with the group\_by function because I hadn't loaded the dplyr library. Spent way too much time trying to fiddle with the code. Learned that you should clear your workspace, and start new everytime so as to not make mistakes like that.
