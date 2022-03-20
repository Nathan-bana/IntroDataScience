Report 3
================
Nathan Bana
(20 March, 2022)

We will be using the `gapminder` data set from the `dslabs` package.

``` r
library(dslabs)
library(dplyr)
library(knitr)
```

Let’s filter by country and year; we are only going to look at the
Switzerland and France observations starting from 1980 on:

``` r
gapminder2 <- gapminder %>%
  filter(country %in% c("Switzerland","France"), year>=1980)
```

Now, let’s select a subset of the columns; we are only going to look at
country, year and fertility:

``` r
gapminder2 <- gapminder2 %>% 
  select(country, year, fertility)
head(gapminder2)
```

    ##       country year fertility
    ## 1      France 1980      1.83
    ## 2 Switzerland 1980      1.51
    ## 3      France 1981      1.84
    ## 4 Switzerland 1981      1.51
    ## 5      France 1982      1.84
    ## 6 Switzerland 1982      1.52

``` r
tail(gapminder2)
```

    ##        country year fertility
    ## 69      France 2014      1.98
    ## 70 Switzerland 2014      1.54
    ## 71      France 2015      1.98
    ## 72 Switzerland 2015      1.55
    ## 73      France 2016        NA
    ## 74 Switzerland 2016        NA

``` r
str(gapminder2)
```

    ## 'data.frame':    74 obs. of  3 variables:
    ##  $ country  : Factor w/ 185 levels "Albania","Algeria",..: 58 160 58 160 58 160 58 160 58 160 ...
    ##  $ year     : int  1980 1980 1981 1981 1982 1982 1983 1983 1984 1984 ...
    ##  $ fertility: num  1.83 1.51 1.84 1.51 1.84 1.52 1.85 1.53 1.85 1.54 ...

Now let’s arrange the data by country, highest-to-lowest fertility, and
year:

``` r
gapminder2 <- gapminder2 %>% 
  arrange(country, desc(fertility), year)
print(gapminder2)
```

    ##        country year fertility
    ## 1       France 2009      1.98
    ## 2       France 2010      1.98
    ## 3       France 2011      1.98
    ## 4       France 2012      1.98
    ## 5       France 2013      1.98
    ## 6       France 2014      1.98
    ## 7       France 2015      1.98
    ## 8       France 2008      1.97
    ## 9       France 2007      1.96
    ## 10      France 2006      1.95
    ## 11      France 2005      1.94
    ## 12      France 2004      1.92
    ## 13      France 2003      1.89
    ## 14      France 2002      1.87
    ## 15      France 1983      1.85
    ## 16      France 1984      1.85
    ## 17      France 1981      1.84
    ## 18      France 1982      1.84
    ## 19      France 1985      1.84
    ## 20      France 2001      1.84
    ## 21      France 1980      1.83
    ## 22      France 1986      1.83
    ## 23      France 2000      1.82
    ## 24      France 1987      1.81
    ## 25      France 1999      1.80
    ## 26      France 1988      1.79
    ## 27      France 1989      1.77
    ## 28      France 1998      1.77
    ## 29      France 1990      1.75
    ## 30      France 1997      1.75
    ## 31      France 1991      1.74
    ## 32      France 1996      1.74
    ## 33      France 1992      1.72
    ## 34      France 1993      1.72
    ## 35      France 1994      1.72
    ## 36      France 1995      1.72
    ## 37      France 2016        NA
    ## 38 Switzerland 1987      1.55
    ## 39 Switzerland 1988      1.55
    ## 40 Switzerland 1989      1.55
    ## 41 Switzerland 1990      1.55
    ## 42 Switzerland 2015      1.55
    ## 43 Switzerland 1984      1.54
    ## 44 Switzerland 1985      1.54
    ## 45 Switzerland 1986      1.54
    ## 46 Switzerland 1991      1.54
    ## 47 Switzerland 1992      1.54
    ## 48 Switzerland 2014      1.54
    ## 49 Switzerland 1983      1.53
    ## 50 Switzerland 1993      1.53
    ## 51 Switzerland 1994      1.53
    ## 52 Switzerland 2013      1.53
    ## 53 Switzerland 1982      1.52
    ## 54 Switzerland 1995      1.52
    ## 55 Switzerland 2012      1.52
    ## 56 Switzerland 1980      1.51
    ## 57 Switzerland 1981      1.51
    ## 58 Switzerland 2011      1.51
    ## 59 Switzerland 1996      1.50
    ## 60 Switzerland 2010      1.50
    ## 61 Switzerland 1997      1.49
    ## 62 Switzerland 2009      1.49
    ## 63 Switzerland 1998      1.47
    ## 64 Switzerland 2008      1.47
    ## 65 Switzerland 2007      1.46
    ## 66 Switzerland 1999      1.45
    ## 67 Switzerland 2000      1.44
    ## 68 Switzerland 2006      1.44
    ## 69 Switzerland 2001      1.43
    ## 70 Switzerland 2005      1.43
    ## 71 Switzerland 2002      1.42
    ## 72 Switzerland 2003      1.42
    ## 73 Switzerland 2004      1.42
    ## 74 Switzerland 2016        NA

We can see that in France, over the 1980 to 2015 period, fertility
peaked in 2009 and has remained stable ever since. In Switzerland, over
the same period, fertility has been considerably lower. We can also see
that fertility has been going up, and it reached its peak in 2015.
Lastly, fertility has been less variable in Switzerland than in France.

Next, let’s calculate the mean fertility rate for each country. Let’s
also calculate the standard deviation:

``` r
gapminder3 <- gapminder2 %>% 
  group_by(country) %>% 
  summarize(average_fertility=mean(fertility, na.rm=T), sd_fertility=sd(fertility, na.rm = T)) %>% 
  arrange(average_fertility)
print(gapminder3)
```

    ## # A tibble: 2 x 3
    ##   country     average_fertility sd_fertility
    ##   <fct>                   <dbl>        <dbl>
    ## 1 Switzerland              1.50       0.0446
    ## 2 France                   1.85       0.0932

Now it is clear that over the 1980 to 2015 period, fertility has been
lower on average and less variable in Switzerland than in France.

Next, let’s create a variation of `gapminder2` in which we remove all
the observations in which there is at least one NA value:

``` r
gapminder4 <- na.omit(gapminder2)
str(gapminder4)
```

    ## 'data.frame':    72 obs. of  3 variables:
    ##  $ country  : Factor w/ 185 levels "Albania","Algeria",..: 58 58 58 58 58 58 58 58 58 58 ...
    ##  $ year     : int  2009 2010 2011 2012 2013 2014 2015 2008 2007 2006 ...
    ##  $ fertility: num  1.98 1.98 1.98 1.98 1.98 1.98 1.98 1.97 1.96 1.95 ...
    ##  - attr(*, "na.action")= 'omit' Named int [1:2] 37 74
    ##   ..- attr(*, "names")= chr [1:2] "37" "74"

We can see that 2 observations were removed.

Finally, let’s join 2 datasets from the `dslabs` package,
`results_us_election_2016` and `murders`:

``` r
full_join(results_us_election_2016, murders)
```

    ## Joining, by = "state"

    ##                   state electoral_votes clinton trump others abb        region
    ## 1            California              55    61.7  31.6    6.7  CA          West
    ## 2                 Texas              38    43.2  52.2    4.5  TX         South
    ## 3               Florida              29    47.8  49.0    3.2  FL         South
    ## 4              New York              29    59.0  36.5    4.5  NY     Northeast
    ## 5              Illinois              20    55.8  38.8    5.4  IL North Central
    ## 6          Pennsylvania              20    47.9  48.6    3.6  PA     Northeast
    ## 7                  Ohio              18    43.5  51.7    4.8  OH North Central
    ## 8               Georgia              16    45.9  51.0    3.1  GA         South
    ## 9              Michigan              16    47.3  47.5    5.2  MI North Central
    ## 10       North Carolina              15    46.2  49.8    4.0  NC         South
    ## 11           New Jersey              14    55.5  41.4    3.2  NJ     Northeast
    ## 12             Virginia              13    49.8  44.4    5.8  VA         South
    ## 13           Washington              12    54.3  38.1    7.6  WA          West
    ## 14              Arizona              11    45.1  48.7    6.2  AZ          West
    ## 15              Indiana              11    37.8  56.9    5.3  IN North Central
    ## 16        Massachusetts              11    60.0  32.8    7.2  MA     Northeast
    ## 17            Tennessee              11    34.7  60.7    4.6  TN         South
    ## 18             Maryland              10    60.3  33.9    5.8  MD         South
    ## 19            Minnesota              10    46.4  44.9    8.6  MN North Central
    ## 20             Missouri              10    38.1  56.8    5.1  MO North Central
    ## 21            Wisconsin              10    46.5  47.2    6.3  WI North Central
    ## 22              Alabama               9    34.4  62.1    3.6  AL         South
    ## 23             Colorado               9    48.2  43.3    8.6  CO          West
    ## 24       South Carolina               9    40.7  54.9    4.4  SC         South
    ## 25             Kentucky               8    32.7  62.5    4.8  KY         South
    ## 26            Louisiana               8    38.4  58.1    3.5  LA         South
    ## 27          Connecticut               7    54.6  40.9    4.5  CT     Northeast
    ## 28             Oklahoma               7    28.9  65.3    5.7  OK         South
    ## 29               Oregon               7    50.1  39.1   10.8  OR          West
    ## 30             Arkansas               6    33.7  60.6    5.8  AR         South
    ## 31                 Iowa               6    41.7  51.1    7.1  IA North Central
    ## 32               Kansas               6    36.1  56.7    7.3  KS North Central
    ## 33          Mississippi               6    40.1  57.9    1.9  MS         South
    ## 34               Nevada               6    47.9  45.5    6.6  NV          West
    ## 35                 Utah               6    27.5  45.5   27.0  UT          West
    ## 36             Nebraska               5    34.3  59.9    5.8  NE North Central
    ## 37           New Mexico               5    48.3  40.0   11.7  NM          West
    ## 38        West Virginia               5    26.5  68.6    4.9  WV         South
    ## 39               Hawaii               4    62.2  30.0    7.7  HI          West
    ## 40                Idaho               4    27.5  59.3   13.2  ID          West
    ## 41                Maine               4    48.0  45.0    7.0  ME     Northeast
    ## 42        New Hampshire               4    46.8  46.5    6.7  NH     Northeast
    ## 43         Rhode Island               4    54.4  38.9    6.7  RI     Northeast
    ## 44               Alaska               3    36.6  51.3   12.2  AK          West
    ## 45             Delaware               3    53.4  41.9    4.7  DE         South
    ## 46              Montana               3    35.9  56.5    7.6  MT          West
    ## 47         North Dakota               3    27.2  63.0    9.8  ND North Central
    ## 48         South Dakota               3    31.7  61.5    6.7  SD North Central
    ## 49              Vermont               3    56.7  30.3   13.1  VT     Northeast
    ## 50              Wyoming               3    21.9  68.2   10.0  WY          West
    ## 51 District of Columbia               3    90.9   4.1    5.0  DC         South
    ##    population total
    ## 1    37253956  1257
    ## 2    25145561   805
    ## 3    19687653   669
    ## 4    19378102   517
    ## 5    12830632   364
    ## 6    12702379   457
    ## 7    11536504   310
    ## 8     9920000   376
    ## 9     9883640   413
    ## 10    9535483   286
    ## 11    8791894   246
    ## 12    8001024   250
    ## 13    6724540    93
    ## 14    6392017   232
    ## 15    6483802   142
    ## 16    6547629   118
    ## 17    6346105   219
    ## 18    5773552   293
    ## 19    5303925    53
    ## 20    5988927   321
    ## 21    5686986    97
    ## 22    4779736   135
    ## 23    5029196    65
    ## 24    4625364   207
    ## 25    4339367   116
    ## 26    4533372   351
    ## 27    3574097    97
    ## 28    3751351   111
    ## 29    3831074    36
    ## 30    2915918    93
    ## 31    3046355    21
    ## 32    2853118    63
    ## 33    2967297   120
    ## 34    2700551    84
    ## 35    2763885    22
    ## 36    1826341    32
    ## 37    2059179    67
    ## 38    1852994    27
    ## 39    1360301     7
    ## 40    1567582    12
    ## 41    1328361    11
    ## 42    1316470     5
    ## 43    1052567    16
    ## 44     710231    19
    ## 45     897934    38
    ## 46     989415    12
    ## 47     672591     4
    ## 48     814180     8
    ## 49     625741     2
    ## 50     563626     5
    ## 51     601723    99

We could explore the relationship between the population of a state and
the tendency of its citizens to vote either for Trump or Clinton.
