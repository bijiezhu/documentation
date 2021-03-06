---
title: geom_histogram | Examples | Plotly
name: geom_histogram
permalink: ggplot2/geom_histogram/
description: How to make a histogram in ggplot2. Examples and tutorials for plotting histograms with geom_histogram, geom_density and stat_density.
layout: base
thumbnail: thumbnail/histogram.jpg
language: ggplot2
page_type: example_index
has_thumbnail: true
display_as: statistical
order: 3
redirect_from: ggplot2/line-shapes/
output:
  html_document:
    keep_md: true
---



### New to Plotly?

Plotly's R library is free and open source!<br>
[Get started](https://plot.ly/r/getting-started/) by downloading the client and [reading the primer](https://plot.ly/r/getting-started/).<br>
You can set up Plotly to work in [online](https://plot.ly/r/getting-started/#hosting-graphs-in-your-online-plotly-account) or [offline](https://plot.ly/r/offline/) mode.<br>
We also have a quick-reference [cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf) (new!) to help you get started!

### Version Check

Version 4 of Plotly's R package is now [available](https://plot.ly/r/getting-started/#installation)!<br>
Check out [this post](http://moderndata.plot.ly/upgrading-to-plotly-4-0-and-above/) for more information on breaking changes and new features available in this version.


```r
library(plotly)
packageVersion('plotly')
```

### Basic Histogram


```r
library(plotly)

dat <- data.frame(xx = c(runif(100,20,50),runif(100,40,80),runif(100,0,30)),yy = rep(letters[1:3],each = 100))

p <- ggplot(dat,aes(x=xx)) +
    geom_histogram(data=subset(dat,yy == 'a'),fill = "red", alpha = 0.2) +
    geom_histogram(data=subset(dat,yy == 'b'),fill = "blue", alpha = 0.2) +
    geom_histogram(data=subset(dat,yy == 'c'),fill = "green", alpha = 0.2)

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_histogram/basic")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4094.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Add Lines


```r
library(plotly)

df1 <- data.frame(cond = factor( rep(c("A","B"), each=200) ),
                  rating = c(rnorm(200),rnorm(200, mean=.8)))

df2 <- data.frame(x=c(.5,1),cond=factor(c("A","B")))

p <- ggplot(data=df1, aes(x=rating, fill=cond)) +
    geom_vline(xintercept=c(.5,1)) +
    geom_histogram(binwidth=.5, position="dodge")

p <- ggplotly(p)


# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_histogram/lines")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4096.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Add Facet


```r
library(plotly)

df <- data.frame (type=rep(1:2, each=1000), subtype=rep(c("a","b"), each=500), value=rnorm(4000, 0,1))

library(plyr)
df.text<-ddply(df,.(type,subtype),summarise,mean.value=mean(value))

p <- ggplot(df, aes(x=value, fill=subtype)) +
    geom_histogram(position="identity", alpha=0.4)+
    facet_grid(. ~ type)

p <- ggplotly(p)


# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_histogram/facet")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4098.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Probability & Density


```r
library(plotly)

df <- data.frame(x = rnorm(1000))

p <- ggplot(df, aes(x=x)) +
    geom_histogram(aes(y = ..density..), binwidth=density(df$x)$bw) +
    geom_density(fill="red", alpha = 0.2)

p <- ggplotly(p)


# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_histogram/prob-density")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4100.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
