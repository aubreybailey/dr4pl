---
output:
  md_document:
    variant: markdown_github
---


#build status:

[![Build Status](https://travis-ci.org/aubreybailey/dr4pl.svg?branch=master)](https://travis-ci.org/aubreybailey/dr4pl)

#license:

[![Licence](https://img.shields.io/badge/licence-GPL--3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0.en.html)

#cran status:

[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/dr4pl)](https://cran.r-project.org/package=dr4pl)

#release version:

[![packageversion](https://img.shields.io/badge/GitHub%20Package%20version-1.0.0-orange.svg?style=flat-square)](commits/master)

##dr4pl

The package dr4pl (Dose Response 4 Parameter Logisitic model) specializes in applying the 4 Parameter Logistic (4PL) model. The 4PL model has been recognized as a major tool to analyze the relationship between a dose and a response in pharmacological experiments. The package dr4pl may be used to model increasing and decreasing curves. The goal of dr4pl is to bring a statistical method which is capable of handeling specific error cases of which other statistical packages produce errors. Examples of Dose Response datasets that will produce errors in other packages may be accessed by name once dr4pl is loaded and these data sets are under the names of drc_error_1, drc_error_2, drc_error_3, and drc_error_4. Along with these error data sets, this package also supplies 13 standard example data sets for the 4PL model under the name sample_data_1, sampel_data_2, etc. The package dr4pl also alows for the user to decide how their theta variable is approximated. The user may choose the default logistic model or use Mead's Method. Additionally, the user may decide between four loss functions to minimize: Squared, Absolute, Huber, or Tukey's biweight. Please attempt each of the loss functions and choose the best fit from plotting the dr4pl object.

## Installation

You can install dr4pl from github with:


```r
# install.packages("devtools")
devtools::install_bitbucket("dittmerlab/dr4pl")
```

## Example

This is a basic example which shows you how to solve a common problem. This example may be used with drc_error_1, drc_error_2, drc_error_3, and drc_error_4:


```r
## basic example code, datasets
## example requires the drc and dr4pl package to be loaded
library(dr4pl)
library(drc)
#> Loading required package: MASS
#> 
#> 'drc' has been loaded.
#> Please cite R and 'drc' if used for a publication,
#> for references type 'citation()' and 'citation('drc')'.
#> 
#> Attaching package: 'drc'
#> The following objects are masked from 'package:stats':
#> 
#>     gaussian, getInitial
a <- drc::drm(drc_error_1$Response~drc_error_1$Dose, fct = LL.4())
#> Error in drmOpt(opfct, opdfct1, startVecSc, optMethod, constrained, warnVal, : Convergence failed
plot(a)
#> Error in plot(a): object 'a' not found
```


```r
## basic example code
## example requires the dr4pl package to be loaded
b <- dr4pl(drc_error_1$Response~drc_error_1$Dose, method.robust = "Tukey") #Tukey's Biweight loss function estimates best for this particular data set
plot(b)
#> Warning: Transformation introduced infinite values in continuous x-axis

#> Warning: Transformation introduced infinite values in continuous x-axis
```

![plot of chunk example_solution](inst/image/example_solution-1.png)

```r
summary(b)
#> Warning in sqrt(diag(vcov.mat)): NaNs produced
#> $call
#> dr4pl.formula(formula = drc_error_1$Response ~ drc_error_1$Dose, 
#>     method.robust = "Tukey")
#> 
#> $coefficients
#>                 Estimate         2.5 %       97.5 %
#> UpperLimit  2.021259e+04  1.772557e+04 22699.614675
#> IC50        6.609737e-02  4.271953e-03     1.022685
#> Slope      -1.915344e+00           NaN          NaN
#> LowerLimit -8.969570e+01 -1.014693e+04  9967.539552
#> 
#> attr(,"class")
#> [1] "summary.dr4pl"
```
