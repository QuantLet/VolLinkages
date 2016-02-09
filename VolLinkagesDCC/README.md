
[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="880" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **VolLinkagesDCC** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : VolLinkagesDCC

Published in : Volatility Linkages between Energy and Agricultural Commodity Prices

Description : 'Computes and plots estimates of the conditional variances and correlations of crude
oil, biodiesel and rapeseed. Estimates are obtained using a dynamic conditional correlation (DCC)
model, where the conditional variances follow an EGARCH(1,1) process.'

Keywords : volatility, correlation, garch, dcc, dynamic, time varying

See also : VolLinkagesSigma, VolLinkagesPricePlot, VolLinkagesStats, VolLinkagesVecmRes

Author : Franziska Schulz, Brenda López Cabrera

Submitted : 03.02.2016

Datafile : Data.txt, Data_log.txt

Input : VolLinkagesVECM.R, VolLinkagesFGLS.R, VolLinkagesVARPlot.R,

Example : Plot of conditional variance and correlation estimates.

```

![Picture1](VolLinkagesDCC.png)


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
source("VolLinkagesVARPlot.R")
```
