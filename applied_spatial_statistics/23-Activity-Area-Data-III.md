---
title: "Activity 11: Area Data III"
output: html_notebook
---

# Activity 11: Area Data III

Remember, you can download the source file for this activity from [here](https://github.com/paezha/Spatial-Statistics-Course).

## Practice questions

Answer the following questions:

1. What does the 45 degree line in the scatterplot of spatial moving averages indicate?
2. What is the effect of centering a variable around the mean?
3. In your own words, describe the phenomenon of spatial autocorrelation.
4. What is the null hypothesis in the test of autocorrelation based on Moran's I?

## Learning objectives

In this activity, you will:

1. Calculate Moran's I coefficient of autocorrelation for area data.
2. Create Moran's scatterplots.
2. Examine the results of the tests/scatterplots for further insights.
3. Think about ways to decide whether a landscape is random when working with area data.

## Suggested reading

O'Sullivan D and Unwin D (2010) Geographic Information Analysis, 2nd Edition, Chapter 7. John Wiley & Sons: New Jersey.

## Preliminaries

For this activity you will need the following:

* An R markdown notebook version of this document (the source file).

* A package called `geog4ga3`.

It is good practice to clear the working space to make sure that you do not have extraneous items there when you begin your work. The command in R to clear the workspace is `rm` (for "remove"), followed by a list of items to be removed. To clear the workspace from _all_ objects, do the following:

```r
rm(list = ls())
```

Note that `ls()` lists all objects currently on the worspace.

Load the libraries you will use in this activity. 

In addition to `tidyverse`, you will need `sf`, a package that implements simple features in R (you can learn about `sf` [here](https://cran.r-project.org/web/packages/sf/vignettes/sf1.html)) and `spdep`, a package that implements several spatial statistical methods (you can learn more about it [here](https://cran.r-project.org/web/packages/spdep/index.html)):

```r
library(tidyverse)
library(sf)
library(spdep)
library(geog4ga3)
```

Begin by loading the data that you will use in this activity:

```r
data(Hamilton_CT)
```

This is a `sf` object with census tracts and selected demographic variables for the Hamilton CMA in Canada.

You can obtain new (calculated) variables as follows. For instance, to obtain the proportion of residents who are between 20 and 34 years old, and between 35 and 49:

```r
Hamilton_CT <- mutate(Hamilton_CT, Prop20to34 = (AGE_20_TO_24 + AGE_25_TO_29 + AGE_30_TO_34)/POPULATION, Prop35to49 = (AGE_35_TO_39 + AGE_40_TO_44 + AGE_45_TO_49)/POPULATION)
```

You can also convert the `sf` object into a `SpatialPolygonsDataFrame` object for use with the `spdedp` package:

```r
Hamilton_CT.sp <- as(Hamilton_CT, "Spatial")
```

You are now ready for the next activity.

## Activity

1. Create a spatial weights matrix for the census tracts in the Hamilton CMA.

2. Use `moran.test` to test the following variables for autocorrelation: proportion of the population who are 20 to 34 years old, 35 to 49 years old, 50 to 65 years old, and 65 and older. How confident are you deciding whether these variables are not spatially random? What can you say regarding the relative strength of these variables' spatial patterns?

3. Use `moran.plot` to create Moran's scatterplots to complement your tests of spatial autocorrelation. Discuss the patterns that you observe.

4. The scatterplots created using `moran.plot` include some observations that are labeled with their id and a different symbol. Why do you think these observations are highlighted in such a way?
