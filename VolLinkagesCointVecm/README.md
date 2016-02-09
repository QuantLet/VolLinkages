
[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="880" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **VolLinkagesCointVecm** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : VolLinkagesCointVecm

Published in : Volatility Linkages between Energy and Agricultural Commodity Prices

Description : 'Estimates the cointegration relationship between crude oil, biodiesel and rapeseed
using a feasible generalized least square (FGLS) estimator and estimates a vector error correction
model (VECM) of the three price series.'

Keywords : cointegration, fgls, vecm, equilibrium, least-squares, price, time-series, linkage

See also : VolLinkagesSigma, VolLinkagesPricePlot, VolLinkagesStats, VolLinkagesVecmRes

Author : Franziska Schulz, Brenda López Cabrera

Submitted : 03.02.2016

Datafile : Data.txt, Data_log.txt

Input : VolLinkagesVECM.R, VolLinkagesFGLS.R

Example : Estimates of the cointegration relation and the VECM.

```


```r
# Clear memory
rm(list = ls())
graphics.off()

 #Set System from German to English
Sys.setlocale('LC_ALL','C') 

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

require("uroot")
unlink(pkgfile)

#set options and seed
options(digits=3)
set.seed(20)

#read data
Data      <- read.delim("Data.txt")
Data$Date <- as.Date(Data$Date)
lp        <- read.delim("Data_log.txt")

#source dependent files
source("VolLinkagesVECM.R")
```
