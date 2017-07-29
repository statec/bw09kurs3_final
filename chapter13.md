---
title       : Einheit 6 (homework)
description : Insert the chapter description here


--- type:NormalExercise lang:r xp:100 skills:1 key:5e9b5a9383
## Anova (I)
Untersuchen Sie mittels einer univariaten Anova Analyse, ob sich der Preis in verschiedenen Farbkategorien (Variable color) signifikant von einander unterscheidet.


Nutzen Sie dazu die Funktion aov().

*** =instructions
- Speichern Sie ihr Ergebnis in `res`.
*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
data(diamonds)
```

*** =sample_code
```{r}
res <- ___

summary(res)
```

*** =solution
```{r}
res <- aov( price ~ color, data =  diamonds)
summary(res)
```

*** =sct
```{r}
test_function("aov")
test_object("res")
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:9a1161ab03
## Anova (II)
Untersuchen Sie mittels einer univariaten Anova Analyse, ob sich der Preis in verschiedenen Qualitätskategorien (Variable cut) signifikant von einander unterscheidet.


Verwenden Sie stets exakte Werte. Die korrekte Antwort darf also keine Rundungsabweichungen erhalten.

Hinweis: Verschaffen Sie sich als erstes einen Überblick wie viele Gruppen gebildet werden müssen und selektieren Sie diese mit filter().

*** =instructions
- Berechnen Sie die Teststatistik ohne Benutzung von aov().
- Speichern Sie die Lösung in `ergebnis`.
*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
data(diamonds)
library(tidyr)
library(dplyr)
# res <- aov( price ~ cut , data =  diamonds)
# summary(res) # Fstat: 175.7
```

*** =sample_code
```{r}
library(tidyr)











# Ergebnisberechnung
ergebnis <- ___

```

*** =solution
```{r}
library(tidyr)

anzahl_gruppen <- length( unique(diamonds$cut) )
anzahl_beobachtungen <- nrow( diamonds)
      
g1 <- filter(diamonds, cut=="Ideal")
g2 <- filter(diamonds, cut=="Premium")
g3 <- filter(diamonds, cut=="Good")
g4 <- filter(diamonds, cut=="Very Good")
g5 <- filter(diamonds, cut=="Fair")
      
n1 <- nrow(g1)
n2 <- nrow(g2)
n3 <- nrow(g3)
n4 <- nrow(g4)
n5 <- nrow(g5)
      
m_g1 <- mean( g1$price )
m_g2 <- mean( g2$price )
m_g3 <- mean( g3$price )
m_g4 <- mean( g4$price )
m_g5 <- mean( g5$price )
m_all <- mean( c( g1$price, g2$price, g3$price, g4$price, g5$price ) )
      
zaehler <- 1/(anzahl_gruppen-1) * ( n1* ( m_g1 - m_all )^2 +
                                    n2* ( m_g2 - m_all )^2 +
                                    n3* ( m_g3 - m_all )^2 +
                                    n4* ( m_g4 - m_all )^2 +
                                    n5* ( m_g5 - m_all )^2 )
nenner <- 1/( anzahl_beobachtungen - anzahl_gruppen ) * ( sum( ( g1$price - m_g1 )^2 ) +
                                                          sum( ( g2$price - m_g2 )^2 ) +
                                                          sum( ( g3$price - m_g3 )^2 ) +
                                                          sum( ( g4$price - m_g4 )^2 ) + 
                                                          sum( ( g5$price - m_g5 )^2 ))
ergebnis <- zaehler/ nenner
```

*** =sct
```{r}
test_object("ergebnis")
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:ed7afe50dd
## Lineare Regression
Berechnen Sie mittels lm() einen linearen Trend des Schlusskurses der Apple Aktie (apple.csv).
    
Der Regressionsoutput sollte also die Parameter der folgenden Regressionsgrade enthalten:

*** =instructions
- Berechnen Sie die lineare Regression und speichern Sie diese in `reg`
- Stellen Sie die Grafik nach und überprüfen Sie diese.
*** =hint

*** =pre_exercise_code
```{r}
ap<- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/apple.csv")
ap$Date<- as.Date(ap$Date)
ap$newvar<- length(ap$Date):1
reg <- lm( Close ~ newvar , data=ap)
    
plot( ap$newvar , ap$Close, type = "l" , lwd= 3, xlab="Datum", ylab="Close" , xaxt='n')
curve( coefficients(reg)[1] + coefficients(reg)[2]*x , add=TRUE , col="red", lty= 2 , lwd= 2)

```

*** =sample_code
```{r}
# Einlesen des Datensatzes, Link: http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/apple.csv
apple<- ___


# Speichern Sie die lineare Regressionsgerade vorerst in reg
reg <- lm(___)


# Plot


```

*** =solution
```{r}
# Einlesen des Datensatzes
apple<- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/apple.csv")
# Datum als Typ Date 
apple$Date<- as.Date(apple$Date)
apple$newvar<- length(apple$Date):1
# Speichern Sie die lineare Regressionsgerade vorerst in reg
reg <- lm(Close ~ newvar, data=apple)
# Uebersicht
summary(reg)
# Plot
plot(apple$newvar, apple$Close, type = "l", lwd= 3, xlab="Datum", ylab="Close" , xaxt='n')
curve(coefficients(reg)[1] + coefficients(reg)[2]*x , add=TRUE , col="red", lty= 2 , lwd= 2)

```

*** =sct
```{r}
test_object("reg")
test_error()
```
