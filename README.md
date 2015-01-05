metricsgraphics is an 'htmlwidget' interface to the MetricsGraphics.js D3 chart library.

The current `htmlwidget` wrapper for it is minimaly functional and does not provide support for metricsgraphics histograms and also does not really take advantage of metricsgraphics' best feature - time series charts. Both will be added in the next release and support for legends will appear shortly thereafter.

Charts look best in a Boostrap page (unless you customize your own CSS).

You can see what the output below produces [on RPubs](http://rpubs.com/hrbrmstr/metricsgraphics0-1).

The following functions are implemented:

-   `mjs_plot`: Create a new metricsgraphics.js plot
-   `mjs_line`: metricsgraphics.js linechart "geom"
-   `mjs_point`: metricsgraphics.js scatterplot "geom"
-   `mjs_bar`: metricsgraphics.js bar chart "geom"
-   `mjs_axis_x`: Configure x axis ticks & limits
-   `mjs_axis_y`: Configure y axis ticks & limits
-   `mjs_labs`: Configure axis labels & plot description
-   `mjs_add_baseline`: Sets a baseline line/label
-   `mjs_add_marker`: Sets a marker line/label

### News

-   Version 0.1 released
-   Version 0.2 released - added support for markers & baselines + minimal support for time-series

### Installation

``` r
devtools::install_github("hrbrmstr/metricsgraphics")
```

### Usage

``` r
library(metricsgraphics)

tmp <- data.frame(year=seq(1790, 1970, 10), uspop=as.numeric(uspop))

tmp %>%
  mjs_plot(x=year, y=uspop) %>%
  mjs_line() %>%
  mjs_add_marker(1850, "Something Wonderful") %>%
  mjs_add_baseline(150, "Something Awful")


tmp %>%
  mjs_plot(x=year, y=uspop, width=600) %>%
  mjs_line(area=TRUE)

tmp %>% 
  mjs_plot(x=uspop, y=year, width=500, height=400) %>%
  mjs_bar() %>%
  mjs_axis_x(xax_format = 'plain')

mtcars %>% 
  mjs_plot(x=wt, y=mpg, width=400, height=300) %>%
  mjs_point(color_accessor=carb, size_accessor=carb) %>%
  mjs_labs(x="Weight of Car", y="Miles per Gallon")


mtcars %>% 
  mjs_plot(x=wt, y=mpg, width=400, height=300) %>%
  mjs_point(least_squares=TRUE) %>%
  mjs_labs(x="Weight of Car", y="Miles per Gallon")


set.seed(1492)
dat <- data.frame(date=seq(as.Date("2014-01-01"), 
                           as.Date("2014-01-31"), 
                           by="1 day"),
                  value=rnorm(n=31, mean=0, sd=2))

dat %>%
  mjs_plot(x=date, y=value) %>%
  mjs_line() %>%
  mjs_axis_x(xax_format = "date")
```
