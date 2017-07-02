--- 
title       : Einheit 4 (homework) - Noch nicht verfügbar
description : Grafische Analysen mit ggplot 

--- type:NormalExercise lang:r xp:100 skills:1 key:b369dec2de
## 1. ggplot (I)
Die folgende Grafik basiert auf dem Datensatz `cars`.

*** =instructions
- Reproduzieren Sie die angezeigte Grafik.
*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
data("cars")
cars <- as.data.frame(cars)
# Plot
ggplot(data = cars, mapping = aes(x = dist, y = speed))+
    geom_point(color = "red")+
    xlab("Distanz")+
    ylab("Geschwindigkeit")+
    ggtitle("cars")

```

*** =sample_code
```{r}
library(ggplot2)
# Plot



    
```

*** =solution
```{r}
# Plot
ggplot(data = cars, mapping = aes(x = dist, y = speed))+
    geom_point(color = "red")+
    xlab("Distanz")+
    ylab("Geschwindigkeit")+
    ggtitle("cars")

```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"))
test_function("geom_point", args = c("color"))
test_function("xlab")
test_function("ylab")
test_function("ggtitle")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:47a20d3e73
## ggplot(II)
Die folgende Grafik basiert auf dem Datensatz `cars`.

Folgende Variablen benötigen Sie aus dem Datensatz:
- mpg: Miles/(US) gallon
- wt: Weight (1000 lbs)
- qsec: 1/4 mile time

*** =instructions
- Reproduzieren Sie die angezeigte Grafik.
- Die Variation im Aussehen der Datenpunkte soll sich anhand der Geschwindigkeit auf eine viertel Meile unterscheiden. Gehen Sie auf die Suche nach dem passenden
Argument im 'aes ()' Teil.
- die Darstellung der Punktform kontrollieren Sie über das Argument 'shape'.
*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
data("cars")
cars <- as.data.frame(cars)

ggplot(data = mtcars, mapping = aes(x = wt, y = mpg, size = qsec))+
  geom_point(shape = 15)

```

*** =sample_code
```{r}
library(ggplot2)
# Plot


```

*** =solution
```{r}
ggplot(data = mtcars, mapping = aes(x = wt, y = mpg, size = qsec))+
  geom_point(shape = 15)

```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"))
test_function("geom_point", args = c("shape"))
test_error()

```


--- type:NormalExercise lang:r xp:100 skills:1 key:58a2dac0b3
## 3. Boxplot
Erstellen sie einen kategorialen Boxplot der Variable "mpg" aus dem Datensatz der Voraufgabe `cars`. 

*** =instructions
- Erstellen Sie den Boxplot.
- Unterteilen Sie die Grafik anhand von "am" (automatik/manuell) in zwei Teile.
- Beschriften Sie die Grafik sinnvoll.
*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
data("cars")
cars <- as.data.frame(cars)
```

*** =sample_code
```{r}
library(ggplot2)
# Boxplot




```

*** =solution
```{r}
ggplot(data = mtcars)+
  geom_boxplot(mapping = aes(x = am, y= mpg, group = am))+
  ylab("Miles per Gallon")
```

*** =sct
```{r}
test_function("ggplot", args = c("data"))
test_function("geom_boxplot", args = c("mapping"))
test_error()

```


--- type:NormalExercise lang:r xp:100 skills:1 key:5e13eeefd0
## 4. ggplot (III)
Die folgende Grafik basiert auf dem Datensatz cars.


Tipp: Folgende Variablen benötigen Sie aus dem Datensatz:


- mpg: Miles/(US) gallon
- wt: Weight (1000 lbs)
*** =instructions
Reproduzieren Sie die angezeigte Grafik.
*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
data("cars")
cars <- as.data.frame(cars)
# lineare Regression
ggplot(data = mtcars, mapping = aes(x = wt, y = mpg)) +
    geom_point() + 
    geom_smooth(method = 'lm')
```

*** =sample_code
```{r}
library(ggplot2)
# lineare Regression


```

*** =solution
```{r}
# lineare Regression
ggplot(data = mtcars, mapping = aes(x = wt, y = mpg)) +
    geom_point() + 
    geom_smooth(method = 'lm')

```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"))
test_function("geom_point")
test_function("geom_smooth", args = c("method"))
test_error()
```


--- type:NormalExercise lang:r xp:100 skills:1 key:2a836c5d1d
## 5. ggplot (IV)
Erweitern Sie die grafische Darstellung aus der vorherigen Aufgabe (Siehe Plot) um einen nicht linearen Zusammenhang. Orientieren Sie sich dabei am Vorgehen in Termin 4.

Folgende Variablen benötigen Sie aus dem Datensatz:


- mpg: Miles/(US) gallon
- wt: Weight (1000 lbs)

*** =instructions
- der gewählte Ansatz soll Nachbarpunkten bei der Approximation ein hohes Gewicht beimessen
*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
data("cars")
cars <- as.data.frame(cars)
# lineare Regression
ggplot(data = mtcars, mapping = aes(x = wt, y = mpg)) +
    geom_point() + 
    geom_smooth(method = 'lm')
```

*** =sample_code
```{r}
library(ggplot2)
# Regressionsplot

```

*** =solution
```{r}
# Beispiel für 0.4
ggplot(data = mtcars, mapping = aes(x = wt, y = mpg))+
  geom_point()+
  geom_smooth(span = 0.4)

```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"))
test_function("geom_point")
test_function("geom_smooth")
test_error()
```


--- type:NormalExercise lang:r xp:100 skills:1 key:7ebaeb9afb
## 6. ggplot (V)
Die folgende Grafik basiert auf dem Datensatz `cars`.


*** =instructions
- Reproduzieren Sie die angezeigte Grafik.
- um den Fülleffekt zu erhalten benötigen Sie das Argument 'fill' im aes Teil.
- das geom 'geom_density' eignet sich zur Darstellung einer Dichte.
- setzen Sie das Argument 'alpha' in 'geom_density' auf 0.4.
- achten Sie auch auf Beschriftungen und Gruppenunterteilungen.
*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
data("mtcars")
mtcars <- as.data.frame(mtcars)
ggplot(mtcars, mapping = aes(x = mpg))+
    geom_density(aes(group = cyl, color = cyl, fill = cyl), alpha = 0.4)+
    ggtitle("Haeufigkeitsverteilung")+
    xlab("Miles per gallon")

```

*** =sample_code
```{r}
library(ggplot2)
# Density Plot




```

*** =solution
```{r}
# Density Plot
ggplot(data = mtcars, mapping = aes(x = mpg))+
    geom_density(aes(group = cyl, color = cyl, fill = cyl), alpha = 0.4)+
    ggtitle("Haeufigkeitsverteilung")+
    xlab("Miles per gallon")
```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"))
test_function("geom_density", args = c("mapping", "alpha"))
test_function("ggtitle")
test_function("xlab")
test_error()
```


--- type:NormalExercise lang:r xp:100 skills:1 key:1827cd70e9
## 7. ggplot (VI)
Lesen Sie die drei Datensätze in R ein und erstellen Sie mit ggplot eine Grafik in der alle Zeitreihen dargestellt werden, wie auf dem dargestellten Plot.


Tipp: Sie benötigen Funktionen, die in Termin 2 besprochen wurden.
*** =instructions
- Stellen Sie die Schlusskurse grafisch dar.
- Verwenden Sie nur Zeitpunkte, die in allen drei Zeitreihen vorhanden sind.
- Überprüfen Sie selbst, ob ihre Grafik korrekt ist.
*** =hint
-Denken Sie daran, das Datum mit `as.Date` auf den richtigen Typ zu bringen.
*** =pre_exercise_code
```{r}
apple <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/apple.csv")
fb <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/fb_aktie.csv")
db <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/db_aktie.csv")

library(dplyr)
apple <- select(apple, appleClose = Close, Date = Date)
fb <- select(fb, fbClose = Close, Date = Date)
db <- select(db, dbClose = Close, Date = Date)

dataset <- inner_join(apple, fb, by = "Date")
dataset <- inner_join(dataset, db, by = "Date")
dataset$Date <- as.Date(dataset$Date)
  
library(ggplot2)

ggplot(data = dataset)+
  geom_line(mapping = aes(x = Date, y = appleClose), color = "blue")+
  geom_line(mapping = aes(x = Date, y = fbClose), color = "red")+
  geom_line(mapping = aes(x = Date, y = dbClose))
rm(apple)
rm(fb)
rm(db)
rm(dataset)
```

*** =sample_code
```{r}
# Apple Daten in http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/apple.csv
apple <- ___
# Facebook Daten in http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/fb_aktie.csv
fb <- ___
# Deutsche Bank Daten in http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/db_aktie.csv
db <- ___

library(dplyr)



  
library(ggplot2)

  
  


```

*** =solution
```{r}
apple <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/apple.csv")
fb <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/fb_aktie.csv")
db <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/db_aktie.csv")

library(dplyr)
apple <- select(apple, appleClose = Close, Date = Date)
fb <- select(fb, fbClose = Close, Date = Date)
db <- select(db, dbClose = Close, Date = Date)

dataset <- inner_join(apple, fb, by = "Date")
dataset <- inner_join(dataset, db, by = "Date")
dataset$Date <- as.Date(dataset$Date)
  
library(ggplot2)

ggplot(data = dataset)+
  geom_line(mapping = aes(x = Date, y = appleClose), color = "blue")+
  geom_line(mapping = aes(x = Date, y = fbClose), color = "red")+
  geom_line(mapping = aes(x = Date, y = dbClose))
```

*** =sct
```{r}
test_error()
```



--- type:NormalExercise lang:r xp:100 skills:1 key:bec1d15e21
## 8. ggplot (VII)
Rechts wird Ihnen eine Grafik angezeigt.

*** =instructions
- Replizieren Sie die angezeigte Grafik.
- Überprüfen Sie selbst, ob ihre Lösung mit der angezeigten Grafik übereinstimmt.
*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
daten <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/exxon.csv")
daten$Date <- as.Date(daten$Date)

ggplot(data = daten)+
    geom_line(mapping = aes(x = Date, y = Close))+
    xlab("Datum")+
    ylab("Schlusskurs")+
    ggtitle("Kursentwicklung der Exxon Aktie")
    
```

*** =sample_code
```{r}
# Daten in http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/exxon.csv

    
```

*** =solution
```{r}


```

*** =sct
```{r}

```
