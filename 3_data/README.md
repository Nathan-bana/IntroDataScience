Report 2
================
Nathan Bana
(12 March, 2022)

-   [Dataset 1](#dataset-1)
-   [Dataset 2](#dataset-2)
-   [Dataset 3](#dataset-3)

# Dataset 1

For our first dataset, let’s use R’s pre-loaded `cars`:

``` r
library(knitr)
kable(head(cars))
```

| speed | dist |
|------:|-----:|
|     4 |    2 |
|     4 |   10 |
|     7 |    4 |
|     7 |   22 |
|     8 |   16 |
|     9 |   10 |

Next, let’s use the `str()` function to see what R data types these 2
variables are:

``` r
str(cars)
```

    ## 'data.frame':    50 obs. of  2 variables:
    ##  $ speed: num  4 4 7 7 8 9 10 10 10 11 ...
    ##  $ dist : num  2 10 4 22 16 10 18 26 34 17 ...

We can see that both variables are numeric vectors. Now, let’s take a
look at the R Documentation about `cars` to figure out what kind of
statistical variables there is. Here is what the description says:

> > > “The data give the speed of cars and the distances taken to stop.”

This means that both variables are quantitative continuous.

# Dataset 2

The second dataset we will be exploring is made available on
<https://www.kaggle.com/>. It contains information on the colors of
every official LEGO set. First, let’s import the data and display it in
a nice table:

``` r
colors <- read.csv("colors.csv")
kable(head(colors))
```

|  id | name           | rgb    | is_trans |
|----:|:---------------|:-------|:---------|
|  -1 | Unknown        | 0033B2 | f        |
|   0 | Black          | 05131D | f        |
|   1 | Blue           | 0055BF | f        |
|   2 | Green          | 237841 | f        |
|   3 | Dark Turquoise | 008F9B | f        |
|   4 | Red            | C91A09 | f        |

The meaning of the first 2 variables is pretty straightforward,
hopefully. As for the last one, it indicates whether or not the given
color is transparent. It is clear that all these variables are
qualitative nominal, statistically speaking. What about the R data
types? Let’s call the `str()` function and take a look:

``` r
str(colors)
```

    ## 'data.frame':    135 obs. of  4 variables:
    ##  $ id      : int  -1 0 1 2 3 4 5 6 7 8 ...
    ##  $ name    : chr  "Unknown" "Black" "Blue" "Green" ...
    ##  $ rgb     : chr  "0033B2" "05131D" "0055BF" "237841" ...
    ##  $ is_trans: chr  "f" "f" "f" "f" ...

By default, R has set the first column to integer, and the next 3 to
character. While this choice makes sense for columns 2 and 3, I don’t
think it does for the first and last column. The id is really just a
label, so it would make more sense to set it to string. As for the last
column, it only contains “true” and “false” values, so it’s better to
set it to logical. Let’s do the changes:

``` r
colors$is_trans <- as.logical(toupper(colors$is_trans))
colors$id <- as.character(colors$id)
str(colors)
```

    ## 'data.frame':    135 obs. of  4 variables:
    ##  $ id      : chr  "-1" "0" "1" "2" ...
    ##  $ name    : chr  "Unknown" "Black" "Blue" "Green" ...
    ##  $ rgb     : chr  "0033B2" "05131D" "0055BF" "237841" ...
    ##  $ is_trans: logi  FALSE FALSE FALSE FALSE FALSE FALSE ...

Much better.

# Dataset 3

Our final dataset also comes from <https://www.kaggle.com/>. It contains
information on 5000 metal bands. The data was scraped from the website
<http://metalstorm.net/> in 2017. Once again, let’s import the data and
display it in a nice table:

``` r
metal <- read.csv("metal_bands_2017.csv")
kable(head(metal))
```

|   X | band_name   | fans | formed | origin         | split | style                                            |
|----:|:------------|-----:|:-------|:---------------|:------|:-------------------------------------------------|
|   0 | Iron Maiden | 4195 | 1975   | United Kingdom | \-    | New wave of british heavy,Heavy                  |
|   1 | Opeth       | 4147 | 1990   | Sweden         | 1990  | Extreme progressive,Progressive rock,Progressive |
|   2 | Metallica   | 3712 | 1981   | USA            | \-    | Heavy,Bay area thrash                            |
|   3 | Megadeth    | 3105 | 1983   | USA            | 1983  | Thrash,Heavy,Hard rock                           |
|   4 | Amon Amarth | 3054 | 1988   | Sweden         | \-    | Melodic death                                    |
|   5 | Slayer      | 2955 | 1981   | USA            | 1981  | Thrash                                           |

Here is the list of the variables:

1.  the name of the band
2.  how many fans the band has on metalstorm.net
3.  when the band formed
4.  the country of origin of the band
5.  when the band split
6.  the styles of the band

Number 1, 4 and 6 are qualitative nominal, whereas 2, 3 and 5 are
quantitative discrete variables, statistically speaking. What about the
R data types? Let’s call the `str()` function and take a look:

``` r
str(metal)
```

    ## 'data.frame':    5000 obs. of  7 variables:
    ##  $ X        : int  0 1 2 3 4 5 6 7 8 9 ...
    ##  $ band_name: chr  "Iron Maiden" "Opeth" "Metallica" "Megadeth" ...
    ##  $ fans     : int  4195 4147 3712 3105 3054 2955 2690 2329 2307 2183 ...
    ##  $ formed   : chr  "1975" "1990" "1981" "1983" ...
    ##  $ origin   : chr  "United Kingdom" "Sweden" "USA" "USA" ...
    ##  $ split    : chr  "-" "1990" "-" "1983" ...
    ##  $ style    : chr  "New wave of british heavy,Heavy" "Extreme progressive,Progressive rock,Progressive" "Heavy,Bay area thrash" "Thrash,Heavy,Hard rock" ...

Here again, I’m going to set the id to string. I also want to set
`metal$origin` to factor, as the number of unique values is limited.
Let’s do the changes:

``` r
metal$origin <- as.factor(metal$origin)
metal$X <- as.character(metal$X)
str(metal)
```

    ## 'data.frame':    5000 obs. of  7 variables:
    ##  $ X        : chr  "0" "1" "2" "3" ...
    ##  $ band_name: chr  "Iron Maiden" "Opeth" "Metallica" "Megadeth" ...
    ##  $ fans     : int  4195 4147 3712 3105 3054 2955 2690 2329 2307 2183 ...
    ##  $ formed   : chr  "1975" "1990" "1981" "1983" ...
    ##  $ origin   : Factor w/ 114 levels "","Albania","Andorra",..: 109 98 112 112 98 112 112 112 109 35 ...
    ##  $ split    : chr  "-" "1990" "-" "1983" ...
    ##  $ style    : chr  "New wave of british heavy,Heavy" "Extreme progressive,Progressive rock,Progressive" "Heavy,Bay area thrash" "Thrash,Heavy,Hard rock" ...

And just like that, we’re done.
