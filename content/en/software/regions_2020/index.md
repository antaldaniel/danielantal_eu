+++
title = "regions R package"
date = 2020-06-03T17:00:00
lastmod = 2021-06-21T12:00:00
draft = false

authors = ["Daniel Antal"]

# Publication type.
# Legend:

publication_types = ["0"]

# Abstract and optional shortened version.
abstract = "An open source R package for validating sub-national statistical typologies, re-coding across standard typologies of sub-national statistics, and making valid aggregate level imputation, re-aggregation, re-weighting and projection down to lower hierarchical levels to create meaningful data panels and time series."

abstract_short = "Validating sub-national statistical typologies, re-coding across standard typologies of sub-national statistics, and making valid aggregate level imputation, re-aggregation, re-weighting and projection down to lower hierarchical levels to create meaningful data panels and time series."

# Is this a featured publication? (true/false)
featured = true

# Projects (optional).
projects = ["R", "opendata"]

categories = ["R"]

tags = ["r-bloggers", "regions", "geography"]

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references 
#   `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides = ""

# Links (optional).
url_pdf = ""
url_preprint = ""
url_code = ""
url_dataset = ""
url_project = "regions.dataobservatory.eu"
url_slides = ""
url_video = ""
url_poster = ""
url_source = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
url_custom = [{name = "Github repo", url = "https://github.com/rOpenGov/regions/"}, {name = "regions on CRAN", url = "https://cran.r-project.org/web/packages/regions/index.html"}]

# Digital Object Identifier (DOI)
doi = "10.5281/zenodo.5006056"

# Does this page contain LaTeX math? (true/false)
math = false

# Featured image
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "TopLeft"
+++


## Installation

You can install the development version from
[GitHub](https://github.com/) with:

``` r
devtools::install_github("rOpenGov/regions")
```

or the released version from CRAN:

``` r
install.packages("regions")
```

You can review the complete package documentation on
[regions.dataobservaotry.eu](https://regions.dataobservatory.eu/). If
you find any problems with the code, please raise an issue on
[Github](https://github.com/rOpenGov/regions). Pull requests are welcome
if you agree with the [Contributor Code of
Conduct](https://contributor-covenant.org/version/2/0/CODE_OF_CONDUCT.html)

If you use `regions` in your work, please [cite the
package](https://doi.org/10.5281/zenodo.5006056).

## Working with Sub-national Statistics

In international comparison, using nationally aggregated indicators
often have many disadvantages, which result from the very different
levels of homogeneity, but also from the often very limited observation
numbers in a cross-sectional analysis. When comparing European
countries, a few missing cases can limit the cross-section of countries
to around 20 cases which disallows the use of many analytical methods.
Working with sub-national statistics has many advantages: the similarity
of the aggregation level and high number of observations can allow more
precise control of model parameters and errors, and the number of
observations grows from 20 to 200-300.

<div class="figure" style="text-align: center">

<img src="https://regions.dataobservatory.eu/articles/indicator_with_map.png" alt="The change from national to sub-national level comes with a huge data processing price: internal administrative boundaries, their names, codes codes change very frequently." width="80%" />
<p class="caption">
The change from national to sub-national level comes with a huge data
processing price: internal administrative boundaries, their names, codes
codes change very frequently.
</p>

</div>

Yet the change from national to sub-national level comes with a huge
data processing price. While national boundaries are relatively stable,
with only a handful of changes in each recent decade. The change of
national boundaries requires a more-or-less global consensus. But states
are free to change their internal administrative boundaries, and they do
it with large frequency. This means that the names, identification codes
and boundary definitions of sub-national regions change very frequently.
Joining data from different sources and different years can be very
difficult.

<div class="figure" style="text-align: center">

<img src="https://regions.dataobservatory.eu/articles/recoded_indicator_with_map.png" alt="Our regions R package helps the data processing, validation and imputation of sub-national, regional datasets and their coding." width="80%" />
<p class="caption">
Our regions R package helps the data processing, validation and
imputation of sub-national, regional datasets and their coding.
</p>

</div>

There are numerous advantages of switching from a national level of the
analysis to a sub-national level comes with a huge price in data
processing, validation and imputation. The
[regions](https://regions.dataobservatory.eu/) package aims to help this
process.

This package is an offspring of the
[eurostat](https://ropengov.github.io/eurostat/) package on
[rOpenGov](https://ropengov.github.io/). It started as a tool to
validate and re-code regional Eurostat statistics, but it aims to be a
general solution for all sub-national statistics. It will be developed
parallel with other rOpenGov packages.

## Sub-national Statistics Have Many Challenges

**Frequent boundary changes**: as opposed to national boundaries, the
territorial units, typologies are often change, and this makes the
validation and recoding of observation necessary across time. For
example, in the European Union, sub-national typologies change about
every three years and you have to make sure that you compare the right
French region in time, or, if you can make the time-wise comparison at
all.

``` r
library(regions)
library(dplyr)
#> 
#> Attaching package: 'dplyr'
#> The following objects are masked from 'package:stats':
#> 
#>     filter, lag
#> The following objects are masked from 'package:base':
#> 
#>     intersect, setdiff, setequal, union
example_df <- data.frame ( 
  geo  =  c("FR", "DEE32", "UKI3" ,
            "HU12", "DED", 
            "FRK"), 
  values = runif(6, 0, 100 ),
  stringsAsFactors = FALSE )

recode_nuts(dat = example_df, 
            nuts_year = 2013) %>%
  select ( .data$geo, .data$values, .data$code_2013) %>%
  knitr::kable()
```

| geo   |   values | code\_2013 |
|:------|---------:|:-----------|
| FR    | 79.70385 | FR         |
| UKI3  | 53.50594 | UKI3       |
| DED   | 84.45034 | DED        |
| FRK   | 63.54153 | FR7        |
| HU12  | 23.97015 | NA         |
| DEE32 | 26.95203 | NA         |

**Hierarchical aggregation and special imputation**: missingness is very
frequent in sub-national statistics, because they are created with a
serious time-lag compared to national ones, and because they are often
not back-casted after boundary changes. You cannot use standard
imputation algorithms because the observations are not similarly
aggregated or averaged. Often, the information is seemingly missing, and
it is present with an obsolete typology code. This is a basic example
which shows you how to impute data from a larger territorial unit, such
as a national statistic, to lower territorial units:

``` r
library(regions)

upstream <- data.frame ( 
   country_code =  rep("AU", 2),
   year         = c(2019:2020),
   my_var       = c(10,12)
   )

downstream <- australia_states

imputed <- impute_down ( 
   upstream_data  = upstream,
   downstream_data = downstream,
   country_var = "country_code",
   regional_code = "geo_code",
   values_var = "my_var",
   time_var = "year" )

knitr::kable(imputed)
```

| geo\_code | year | geo\_name                              | country\_code | my\_var | method                 |
|:----------|-----:|:---------------------------------------|:--------------|--------:|:-----------------------|
| AU-NSW    | 2019 | New South Wales state                  | AU            |      10 | imputed from AU actual |
| AU-QLD    | 2019 | Queensland state                       | AU            |      10 | imputed from AU actual |
| AU-SA     | 2019 | South Australia state                  | AU            |      10 | imputed from AU actual |
| AU-TAS    | 2019 | Tasmania state                         | AU            |      10 | imputed from AU actual |
| AU-VIC    | 2019 | Victoria state                         | AU            |      10 | imputed from AU actual |
| AU-WA     | 2019 | Western Australia state                | AU            |      10 | imputed from AU actual |
| AU-ACT    | 2019 | Australian Capital Territory territory | AU            |      10 | imputed from AU actual |
| AU-NT     | 2019 | Northern Territory territory           | AU            |      10 | imputed from AU actual |
| AU-NSW    | 2020 | New South Wales state                  | AU            |      12 | imputed from AU actual |
| AU-QLD    | 2020 | Queensland state                       | AU            |      12 | imputed from AU actual |
| AU-SA     | 2020 | South Australia state                  | AU            |      12 | imputed from AU actual |
| AU-TAS    | 2020 | Tasmania state                         | AU            |      12 | imputed from AU actual |
| AU-VIC    | 2020 | Victoria state                         | AU            |      12 | imputed from AU actual |
| AU-WA     | 2020 | Western Australia state                | AU            |      12 | imputed from AU actual |
| AU-ACT    | 2020 | Australian Capital Territory territory | AU            |      12 | imputed from AU actual |
| AU-NT     | 2020 | Northern Territory territory           | AU            |      12 | imputed from AU actual |

## Package functionality

-   Generic vocabulary translation and joining functions for
    geographically coded data
-   Keeping track of the boundary changes within the European Union
    between 1999-2024
-   Vocabulary translation and joining functions for standardized
    European Union statistics
-   Vocabulary translation for the `ISO-3166-2` based Google data and
    the European Union
-   Imputation functions from higher aggregation hierarchy levels to
    lower ones, for example from `NUTS1` to `NUTS2` or from `ISO-3166-1`
    to `ISO-3166-2` (impute down)
-   Imputation functions from lower hierarchy levels to higher ones
    (impute up)
-   Aggregation function from lower hierarchy levels to higher ones, for
    example from NUTS3 to `NUTS1` or from `ISO-3166-2` to `ISO-3166-1`
    (aggregate; under development)
-   Disaggregation functions from higher hierarchy levels to lower ones,
    again, for example from `NUTS1` to `NUTS2` or from `ISO-3166-1` to
    `ISO-3166-2` (disaggregate; under development)

We started building an experimental APIs data is running regions
regularly and improving known statistical data sources. See: [Digital
Music Observatory](https://music.dataobservatory.eu/), [Green Deal Data
Observatory](https://greendeal.dataobservatory.eu/), [Economy Data
Observatory](https://economy.dataobservatory.eu/).

## Vignettes / Articles

-   [Mapping Regional Data, Mapping Metadata
    Problem](https://regions.dataobservatory.eu/articles/mapping.html)
-   [Working With Regional, Sub-National Statistical
    Products](https://regions.dataobservatory.eu/articles/Regional_stats.html)
-   [Validating Your
    Typology](https://regions.dataobservatory.eu/articles/validation.html)
-   [Recoding And
    Relabelling](https://regions.dataobservatory.eu/articles/recode.html)

## Contributors

Thanks for [@KKulma](https://github.com/KKulma) for the improved
continous integration on Github.

## Code of Conduct

Please note that the regions project is released with a [Contributor Code of Conduct](https://contributor-covenant.org/version/2/0/CODE_OF_CONDUCT.html).
By contributing to this project, you agree to abide by its terms.
## Feedback?

Raise and [issue](https://github.com/rOpenGov/regions/issues) on Github or [get in touch](https://danielantal.eu/#contact). Downloaders from CRAN: 
[![metacran downloads](https://cranlogs.r-pkg.org/badges/regions)](https://cran.r-project.org/package=regions)
