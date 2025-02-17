---
title: "HW08: Collecting and analyzing data from the web"
date: 2022-11-02T13:30:00-06:00  # Schedule page publish date
publishdate: 2019-04-01

draft: false
type: post
aliases: ["/hw08-webdata.html"]

summary: "Collect data from the web and analyze it."
---



# Overview

Due by 11:59pm on July 14th.

We learned three ways of collecting data from the internet:

* Accessing data using packages that wrap APIs
* Running (basic) API queries "by hand"
* Web scraping

For the homework, you will

* Combine two existing datasets in a novel (and reproducible!) way
* Create a new dataset by using an API or web scraping

# Accessing the `hw08` repository

Go [here](https://github.coecis.cornell.edu/cis-fa22) and find your copy of the `hw08` repository. It follows the naming convention `hw08-<USERNAME>`. Clone the repository to your computer.

# Part 1: Exploring the `gapminder` data (even more)

We've examined the `gapminder` data quite a bit. One relationship we've looked at (or are about to) is the relationship between population and life expectancy.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />

For the assignment, I want you to replace **population** with **population density** and evaluate its relationship with average life expectancy. To do this:

1. Get the country information using [geonames](http://www.geonames.org/) - remember there is a [R package for this](https://cran.r-project.org/web/packages/geonames/index.html) (see the lecture notes)
1. Merge `gapminder` and the country information from `geonames`
    * Use `left_join` from `dplyr` to [merge the tables](http://r4ds.had.co.nz/relational-data.html)
    * Note that you cannot directly do this - `gapminder` writes the name of countries differently from `geonames`. To complete the merge, you need a unique *key* to match observations between the data frames
    * There is neat little package for R called [`countrycode`](https://github.com/vincentarelbundock/countrycode) that helps solve this problem. `countrycode()` takes as an input a country's name in a specific format and outputs it using whatever format you specify.
        * `gapminder` stores them using the `country.name` format
        * `geonames` stores them under the `countryCode` column using the `iso2c` format
        * I leave it to you to make the joining operation work
1. Calculate the population density for each observation
1. Produce an updated graph using population density
    * If you want to be real fancy, estimate a statistical model or compare the relationship across continents

# Part 2: More complicated data collection

For the second part of the assignment, I want you to **create a new dataset and analyze it**. You can do so using any of the following methods:

* Install and play
* Write an API query function
* Scrape a website

If you go either of the last two routes, you need to write your own code or function to query the server and obtain the results. If you decide to skip the API entirely, you will need to use [`rvest`](https://github.com/hadley/rvest) to scrape the content of a web page and extract the relevant information.

**If you use the install and play option, I expect immaculate and thorough analysis since you are choosing a much easier method to obtain your data.** Consider yourself warned.

The end result must be a tidy data frame stored in the repository with some analytical component. This can be exploratory description and visualization or some method of statistical learning. I should be able to run your code and reproduce your data and analysis.[^repro] [^key]

{{% callout note %}}

Some suggested APIs you could write your own code for in R:

* [An API of Ice and Fire](https://anapioficeandfire.com/)
* [balldontlie API (NBA stats)](http://www.balldontlie.io/#introduction)
* [NASA APIs](https://api.nasa.gov/index.html)
* [The New York Times Developer Network](https://developer.nytimes.com/)
* [SWAPI - the Star Wars API](https://swapi.dev/)
* [USASpending.gov](https://api.usaspending.gov/)
* [USGS Earthquake Catalog](https://earthquake.usgs.gov/fdsnws/event/1/)
* [xkcd](https://xkcd.com/json.html)

{{% /callout %}}

# Submit the assignment

Your assignment should be submitted as a set of two Quarto documents using the `github_document` format. Whatever is necessary to show your code and present your results. Follow instructions on [homework workflow](/faq/homework-guidelines/#homework-workflow).

# Rubric

Needs improvement: Cannot get code to run. Fail to accurately create the population density variable. Generated data set is not tidy. No documentation explaining how to use your API function or web scraping script.

Satisfactory: Solid effort. Hits all the elements. No clear mistakes. Easy to follow (both the code and the output). Nothing spectacular, either bad or good.

Excellent: Estimate a statistical model for the `gapminder` question, or do something beyond producing a graph. Implement an advanced statistical learning model or extensive exploratory analysis. Write an API function that uses authentication.

## Acknowledgments


* This page is derived in part from ["UBC STAT 545A and 547M"](http://stat545.com), licensed under the [CC BY-NC 3.0 Creative Commons License](https://creativecommons.org/licenses/by-nc/3.0/).

[^repro]: Obviously if you are scraping from a web page that frequently updates its content, I may not perfectly reproduce your results. That's fine - just make sure you've saved a copy of the data frame in the repo.
[^key]: Also if you [write your own API function for a site that requires authentication](https://cran.r-project.org/web/packages/httr/vignettes/api-packages.html#authentication), make sure to include instructions about where to store my API key so I can run your code **without sharing your private key**.
