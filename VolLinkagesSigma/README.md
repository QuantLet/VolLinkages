
[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="880" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **VolLinkagesSigma** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : VolLinkagesSigma

Published in : Volatility Linkages between Energy and Agricultural Commodity Prices

Description : 'Computes and plots nonparametric estimates of the unconditional variances and
correlations of crude oil, biodiesel and rapeseed using kernel methods. The bandwidth is determined
using a likelihood cross-validation criterion. Furthermore, pointwise confidence intervals are
computed based on 200 bootstrap experiments.'

Keywords : volatility, correlation, nonparametric, optimal bandwidth, cross-validation, bootstrap

See also : VolLinkagesVecmRes, VolLinkagesPricePlot, VolLinkagesStats, VolLinkagesDCC

Author : Franziska Schulz, Brenda López Cabrera

Submitted : 03.02.2016

Datafile : Data.txt, Data_log.txt

Input : 'VolLinkagesVECM.R, VolLinkagesFGLS.R, VolLinkagesBootstrap.R, VolLinkagesFigure7.R,
VolLinkagesNonp.R'

Example : 'Plot of unconditional volatility and correlation estimates together with 90% pointwise
confidence intervals'

```

![Picture1](VolLinkagesSigma.png)


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
              "ccgarch",
              "boot")

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
source("VolLinkagesVECM.R", print.eval = FALSE)
source("VolLinkagesNonp.R", print.eval = FALSE)
source("VolLinkagesFigure7.R")
```
