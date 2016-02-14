---
title       : Titanic
subtitle    : Prediction of Survival
author      : EffZeh
job         : Coursera Data Science - 09 Developing Data Products
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
logo        : 
---

## Content & Agenda

This is the corresponding documentation for the shiny app:
https://effzeh.shinyapps.io/Course_Project/

The code (server.R, ui.R) for this app can be found in:
https://github.com/christianwerres/09-Developing-Data-Products

The app "Titanic - Prediction of Survival" predicts the likeliyhood of survival based on gender (femal or male), age (child or adult) and ticket purchased for the Titanic (1st class, 2nd, 3rd or crew).

The next slides outline
* the underlying data
* the prediction model


--- .class #id 

## Underlying Data

The data used for the prediction has been pulled from the R library 'datasets'


```r
library('datasets')
summary(Titanic)
```

```
## Number of cases in table: 2201 
## Number of factors: 4 
## Test for independence of all factors:
## 	Chisq = 1637.4, df = 25, p-value = 0
## 	Chi-squared approximation may be incorrect
```

```r
head(as.data.frame(Titanic),3)
```

```
##   Class  Sex   Age Survived Freq
## 1   1st Male Child       No    0
## 2   2nd Male Child       No    0
## 3   3rd Male Child       No   35
```



--- .class #id 

## Prediction Model (1)

The variables gender ('sex'), 'age' and 'class' (input) has been used to predict the variable 'survived' (outcome).

First a data frame containing a row for each of the 2201 passenger has been created. 
Then the input variables have been converted to n-dimensional vectors:
* gender -> 2-dimensional vector, e.g.: male = (1,0), female = (0,1)
* age -> 2-dimensional vector
* class -> 4-dimensional vector



```r
# Example:
x <- data.frame(0,1,0,1,0,0,0,1,1)
names(x) <- c("gender_male", "gender_female","age_child", "age_adult"
              , "class_1st", "class_2nd", "class_3rd", "class_crew","survived")
```


--- .class #id 

## Prediction Model (2)

Based on the transformed data a training, cross validation and testing dataset have been calculated randomly.

The training data has been used to initally train a neural net. The cross validation dataset has then been used to enhance the settings of the neural net.

The trained neural net work achived a accuracy of ~ 82 % for the testing dataset. This trained neural net is used by the shiny app to predict the survival on the Titanic.



```r
## packages used for neural net:
# install.packages('neuralnet')
# library("neuralnet")
```
