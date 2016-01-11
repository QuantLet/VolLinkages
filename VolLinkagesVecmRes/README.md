
[<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **VolLinkagesVecmRes** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : VolLinkagesVecmRes

Published in : Volatility Linkages between Energy and Agricultural Commodity Prices

Description : Estimates a VECM of the prices using a FGLS estimator and plots the residuals

Keywords : volatility, linkage, garch, least-squares, price, time-series

See also : VolLinkagesStat, VolLinkagesPricePlot

Author : Franziska Schulz, Brenda López Cabrera

Submitted : 06.01.2016

Datafile : CrudeOil.txt, Biodiesel.txt, Rapeseed.txt

Input : VolLinkagesData.R, VolLinkagesFGLS, VolLinkagesVECM

Example : VECM estimates, plot of VECM residuals

```

![Picture1](VolLinkagesVecmRes.png)


```r
# Clear memory
rm(list = ls())
# Set working directory
#setwd("C:...")

# install and load libraries
libraries = c("car",
              "abind",
              "quantmod",
              "zoo", 
              "Epi",
              "tseries",
              "urca",
              "vars",
              "tsDyn",
              "stats", 
              "fGarch",
              "np",
              "corpcor",
              "FinTS",
              "rugarch", 
              "rmgarch",
              "Rcpp",
              "truncnorm",
              "Kendall",
              "sm",
              "ccgarch")

lapply(libraries, function(x) if (!(x %in% installed.packages())) {
    install.packages(x)
})

lapply(libraries,require,quietly=TRUE,character.only=TRUE)

#install archived package uroot
pkgfile = "uroot_1.4.tar.gz"

download.file(url      = "http://cran.r-project.org/src/contrib/Archive/uroot/uroot_1.4.tar.gz",
              destfile = pkgfile)

install.packages(pkgs  = pkgfile,
                 type  = "source",
                 repos = NULL)

source("VolLinkagesData.R")
source("VolLinkagesVECM.R")

par(mfrow = c(1, 3))

plot(u.final[, 1],
     type = "h",
     ylab = "",
     xlab = "", 
     main = "Crude Oil")

plot(u.final[, 2],
     type = "h",
     ylab = "",
     xlab = "", 
     main = "Rapeseed")

plot(u.final[, 3],
     type = "h",
     ylab = "",
     xlab = "", 
     main = "Biodiesel")

```
