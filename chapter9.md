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