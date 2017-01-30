<!-- README.md is generated from README.Rmd. Please edit that file -->
goggles
=======

[![Travis-CI Build Status](https://travis-ci.org/nacnudus/goggles.svg?branch=master)](https://travis-ci.org/nacnudus/goggles) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/nacnudus/goggles?branch=master&svg=true)](https://ci.appveyor.com/project/nacnudus/goggles) ![Cran Status](http://www.r-pkg.org/badges/version/goggles)

> Spreadsheets are dangerous. Wear goggles.

> `Goggles` help(s) you spot spreadsheet anomalies in the wild.

Spreadsheets are notoriously helpful in converting numbers to dates. Humans are notoriously unhelpful in overwriting formulas with literals. With goggles, you can quickly visualise possible errors.

This is basically a thin wrapper around [`tidyxl`](https://github.com/nacnudus/tidyxl) and [`unpivotr`](https://github.com/nacnudus/unpivotr) that plots cells in their positions and colours them by some property, e.g. number format.

``` r
library(tidyxl)
library(tidyverse)

x <- tidy_xlsx(system.file("extdata/road-policing-driver-offence-data-jan2009-sep2006.xlsx",
                           package = "nzpullover"))

redlight <- x$data[["Red Light"]]
redlight$numFmt <- x$formats$local$numFmt[redlight$local_format_id]

ggplot(redlight, aes(col, row,
           colour = numFmt,
           alpha = is.na(content))) +
geom_point() +
scale_y_reverse() +
scale_alpha_manual(values = c(1, .5))
```

![](README-unnamed-chunk-2-1.png)
