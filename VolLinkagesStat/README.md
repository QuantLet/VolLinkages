
[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="880" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **VolLinkagesStat** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : VolLinkagesStat

Published in : Volatility Linkages between Energy and Agricultural Commodity Prices

Description : 'Computes summary statistics, normality tests and tests for autocorrelation and GARCH
effects of the price data'

Keywords : volatility, linkage, price, time-series, autocorrelation

See also : VolLinkagesVECM, VolLinkagesPricePlot

Author : Franziska Schulz, Brenda López Cabrera

Submitted : 06.01.2016

Datafile : CrudeOil.txt, Biodiesel.txt, Rapeseed.txt

Input : VolLinkagesData.R

Example : Summary statistics and tests results for the price data

```


```r
# Clear memory
rm(list = ls())
graphics.off()
# Set working directory
#setwd("...")

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

source("VolLinkagesData.R")

print("Mean")
print(colMeans(Data[, -1]))
print("St.D.")
print(sqrt(var(Data[, -1])))
print("Corr.")
print(cor(Data[, -1]))

r = diff(as.matrix(lp))[-1, ]  # differenced deseasonalized logs
print("Skewness")
print(c(skewness(r[, 1]),
        skewness(r[, 2]),
        skewness(r[, 3])))

print("Kurtosis")
print(c(kurtosis(r[, 1]),
        kurtosis(r[, 2]),
        kurtosis(r[, 3])))

print("Box Ljung (residuals)")
print(c(Box.test(r[, 1], lag = 20, type = "Ljung")$p.value, 
        Box.test(r[, 2], lag = 20, type = "Ljung")$p.value, 
        Box.test(r[, 3], lag = 20, type = "Ljung")$p.value))

print("Box-Ljung (squared residuals)")
print(c(Box.test(r[, 1]^2, lag = 20, type = "Ljung")$p.value, 
        Box.test(r[, 2]^2, lag = 20, type = "Ljung")$p.value, 
        Box.test(r[, 3]^2, lag = 20, type = "Ljung")$p.value))

print("ARCH")
print(c(ArchTest(r[, 1], lags = 5)$p.value,
        ArchTest(r[, 2], lags = 5)$p.value,
        ArchTest(r[, 3], lags = 5)$p.value))

print("Shapiro-Wilk")
print(c(shapiro.test(r[, 1])$p.value,
        shapiro.test(r[, 2])$p.value,
        shapiro.test(r[, 3])$p.value))


```
