---
title       : Develping Data Products Course Project 
subtitle    : Shiny App Explanation
author      : Hyunsik Shim
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---


## Welcome to mtcars database explorer

This application is based on the `Motor Trend Car Road Tests` database.

The data was extracted from the 1974 Motor Trend US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973~74 models).

Source code is available on the [GitHub](https://github.com/icshs1/Developing_Data_Products).

You can adjust and select date variables of mtcars on the left side and can show plot result according selected vairables ont the right side. 

--- .class #id 


## mtcars dataset - Description

### Source

> Henderson and Velleman (1981), Building multiple regression models interactively. Biometrics, 37, 391~411.


```r
library(datasets)
head(mtcars, 3)
```

```
##                mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4     21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag 21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710    22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
```

--- .class #id 

## mtcars dataset - Format

**A data frame with 32 observations on 11 variables.**

| Index | Field | Detail |
------- | ----- | ------ |
| [, 1] | mpg | Miles/(US) gallon |
| [, 2]  | cyl | Number of cylinders |
| [, 3]  | disp | Displacement (cu.in.) |
| [, 4]  | hp | Gross horsepower |
| [, 5]	| drat | Rear axle ratio |
| [, 6]	| wt | Weight (lb/1000) |
| [, 7]	| qsec | 1/4 mile time |
| [, 8]	| vs | V/S |
| [, 9]	| am | Transmission (0 = automatic, 1 = manual) |
| [,10]	| gear | Number of forward gears |
| [,11]	| carb | Number of carburetors |

---  .class #id 

## Funtions of Shiny App

### The following functions are supported.

1. Histogram
  - You can select one variable of `mtcars` and show histogram.
2. Correlation
  - You can check several variable of `mtcars` and show correlations of selected variables
3. Download
  - You can check several variable of `mtcars` for saving data that you want.
4. Modeling
  - You can select one variable of `mtcars` for modeling of linear regression.
5. About
  - You can know about this App.

--- 

## Moldeing 

### Source code for linear regression modeling


```r
  # linear model training 
  # predictor am and selected variable (hp, dist, qsec, wt) 
  ## fit<- lm(mpg ~ x1 + am + x1 * am, mtcars) 
  fit<- reactive({ 
    fit<-lm(mpg ~ mtcars[ , predictor()] + am + mtcars[ , predictor()]* am, mtcars) 
    return(fit) 
  }) 
  # predict resutl with input predict value. 
  predict_result<- reactive({ 
    predict<-c(fit()$coef[1] + predict_value() * fit()$coef[2], 
       fit()$coef[1] + fit()$coef[3] + predict_value() * (fit()$coef[2] + fit()$coef[4])) 
    return(predict) 
  }) 
```



