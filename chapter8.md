---
title       : Einheit 4 (inclass)
description : Grafische Analysen mit ggplot 

--- type:NormalExercise lang:r xp:100 skills:1 key:04384eb4ed
## plot und ggplot (I)
Vergleichen Sie die bereits bekannte Funktion `plot()` mit der Funktionalität des ggplot Packets.

Gegeben ist der Datensatz "diamonds", der Informationen wie die Karatzahl, Preis und Qualität von Diamanten enthält. Verschaffen Sie sich einen Überblich und erstellen Sie zwei Plots gemäß der Vorgaben.

Hilfe zum `plot` Befehl und den verschiedene Eingabeparametern finden Sie, indem Sie `?plot()` in der Konsole eingeben. 


*** =instructions
- Erstellen Sie einen Punkte-Plot der die Karatzahl und den Preis aus dem dataframe "diamonds" enthält. Benutzen Sie `plot()`.
- Erstellen Sie den gleichen Plot mit der ggplot-Funktion. Benutzen Sie `geom_point()`.
- Die Karatzahl soll jeweils auf der x-Achse und der Preis auf der y-Achse dargestellt werden.

*** =hint
- Schauen Sie für die ggplot-Funktion ins Skript oder benutzen Sie `?ggplot()` um mehr zu erfahren.

*** =pre_exercise_code
```{r}
library(ggplot2) 
data("diamonds")
diamonds <- as.data.frame(diamonds)
```

*** =sample_code
```{r}
library(ggplot2) 

# Plot mit plot(), type = "p" erstellt einen Punkteplot.
plot(___, ___, type = "p", main = "diamonds", xlab = "carat", ylab = "price")
# Plot mit ggplot() mit geom_point()
ggplot(data = ___, mapping = ___) +
  

```

*** =solution
```{r}
# Plot mit plot() 
plot(diamonds$carat, diamonds$price, type = "p", main = "diamonds", xlab = "carat", ylab = "price")
# Plot mit ggplot() mit geom_point()
ggplot(data = diamonds, mapping = aes(x = carat, y = price))+
  geom_point()

```

*** =sct
```{r}
test_function("plot", args = c("x", "y", "type", "main", "xlab", "ylab") )
test_function("ggplot", args = c("data", "mapping"))
test_function("geom_point")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:f9dcd5853c
## plot und ggplot (II)

Arbeiten Sie ab jetzt nur noch mit ggplot. 

Ihnen ist wieder der "diamonds" Datensatz gegeben. Bei großen Datensätze wie diesem, kann man sehr schön mit dem Transparenzparameter `alpha` arbeiten. Testen Sie verschiedene Werte. 


*** =instructions
- Erstellen Sie drei Plots und variieren Sie jeweils den Wert der Transparenz (`alpha`).
- Benutzen Sie für `alpha` jeweils 1/10, 1/20 und 1/100.
- Schauen Sie sich die Unterschiede in den drei Plots an.

*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
data("diamonds")
diamonds <- as.data.frame(diamonds)

```

*** =sample_code
```{r}
library(ggplot2)
# Plot mit alpha = 1/10


# Plot mit alpha = 1/20

  
# Plot mit alpha = 1/100


```

*** =solution
```{r}
# Plot mit alpha = 1/10
ggplot(data = diamonds, mapping = aes(x = carat, y = price) )+
  geom_point(alpha = 1/10)

# Plot mit alpha = 1/20
ggplot(data = diamonds, mapping = aes(x = carat, y = price) )+
  geom_point(alpha = 1/20)
  
# Plot mit alpha = 1/100
ggplot(data = diamonds, mapping = aes(x = carat, y = price) )+
  geom_point(alpha = 1/100)

```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"), index = 1)
test_function("geom_point", args = c("alpha"), index = 1)
test_function("ggplot", args = c("data", "mapping"), index = 2)
test_function("geom_point", args = c("alpha"), index = 2)
test_function("ggplot", args = c("data", "mapping"), index = 3)
test_function("geom_point", args = c("alpha"), index = 3)
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:e53d6f01e4
## geoms (I)

Probieren Sie nun das geom `geom_line` aus.

*** =instructions
- Erstellen Sie einen Plot über die Karatzahl auf der x-Achse und dem Preis auf der y-Achse.
- Fügen Sie ein "geom_line" hinzu, färben Sie diese blau (mit color).
- Betiteln Sie die x-Achse mit "Karat" und die y-Achse mit "Preis".

*** =hint
- Die Achsen können durch eigene geoms betitelt werden.

*** =pre_exercise_code
```{r}
library(ggplot2)
data("diamonds")
diamonds <- as.data.frame(diamonds)
```

*** =sample_code
```{r}
library(ggplot2)

# Plotten Sie mit ggplot()





```

*** =solution
```{r}
# Plotten Sie mit ggplot()
ggplot(data = diamonds, mapping = aes(x = carat, y = price) )+
  geom_line(color = "blue")+
  xlab("Karat")+
  ylab("Preis")

```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"))
test_function("geom_line", args = c("color"))
test_function("xlab")
test_function("ylab")
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:d84eccfab0
## geoms (II)

Die Qualität der Diamanten ist in der Variable "cut" gespeichert. 

Erstellen Sie eine Häufigkeitsverteilung mit `geom_bar()`.

*** =instructions
- Erstellen Sie ein Balkendiagramm, welches die Häufigkeit der verschiedenen Qualitäten der Edelsteine zeigt.

*** =hint
- Benutzen Sie `geom_bar`

*** =pre_exercise_code
```{r}
library(ggplot2)
data("diamonds")
diamonds <- as.data.frame(diamonds)
```

*** =sample_code
```{r}
library(ggplot2)

# Erstellen Sie ein Balkendiagramm über cut

```

*** =solution
```{r}
# Plotten Sie mit ggplot()
ggplot(data = diamonds, mapping = aes(x = cut))+
    geom_bar( )
```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"))
test_function("geom_bar")
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:182b668adc
## geoms (III)

Erstellen Sie eine Grafik, welche die jeweiligen Datenpunkte (Karat zu Preis) darstellt. 

Erweitern Sie die Grafik durch einen linearen Trend um einen Eindruck über die Abhängigkeit zwischen den beiden Variablen zu erhalten.

Um mehr über die Eingabeparameter von geom\_smooth zu erfahren, geben Sie `?geom_smooth()` in der Konsole ein.

*** =instructions
- Erstellen Sie einen Punkte-Plot mit der Karat Zahl auf der x-Achse und de Preis auf der y-Achse.
- Fügen Sie das geom hinzu, was für eine Glättung der Funktion sorgt.
- Um eine lineare Regression zu bekommen, müssen Sie als Methode "lm" wählen.

*** =hint
- `geom_smooth(method = "lm")`

*** =pre_exercise_code
```{r}
library(ggplot2)
data("diamonds")
diamonds <- as.data.frame(diamonds)
```

*** =sample_code
```{r}
library(ggplot2)

# Fügen Sie einen linearen Trend ein




```

*** =solution
```{r}
# Erstellen Sie eine lineare Regression
ggplot(data = diamonds, aes(x = carat, y = price))+
  geom_point()+
  geom_smooth(method = "lm")
```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"))
test_function("geom_point")
test_function("geom_smooth", args = c("method"))
test_error()
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:0a648e1e7d
## geoms (IV)
Was bewirkt ein hoher Wert für den span-Parameter bei der `geom_smooth` Funktion?

Nehmen Sie die Beispielplots zur Hilfe.

*** =instructions

- Die Funktion wird glatter.
- Punkte in der direkten Nachbarschaft werden stärker berücksichtigt.

*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
library(dplyr)
data("diamonds")
diamonds <- as.data.frame(diamonds)
diamonds <- filter(diamonds, diamonds$table < 54)
# Span auf 0.8
ggplot(data = diamonds, mapping = aes(x = carat, y = price))+
  geom_point()+
  geom_smooth(span = 0.8)+
  ggtitle("Span = 0.8", subtitle = NULL)
# Span auf 0.1 (Warnungen ignorieren)
ggplot(data = diamonds, mapping = aes(x = carat, y = price))+
  geom_point()+
  geom_smooth(span = 0.1)+
  ggtitle("Span = 0.1", subtitle = NULL)

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig!"
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad))
```



--- type:NormalExercise lang:r xp:100 skills:1 key:9039fe0643
## geoms (V)

Nutzen Sie eine Glättungsfunktion für eine Teilstichprobe von `diamonds` .  

Info: Bei der span Eingabe von span = 0.1 werden Warnungen in der Konsole ausgegeben. Diese können Sie ignorieren.

*** =instructions
- Erstellen Sie einen Plot mit `geom_point`.
- Glätten Sie die Funktion mit `geom_smooth`.
- Setzen Sie das span Argument einmal auf 0.8 und einmal auf 0.1 (Warnungen ignorieren)
- Vergleichen Sie die Ergebnisplots und achten Sie besonders auf die Wirkung der verschiedenen Eingaben für den "span"-Parameter.

*** =hint

*** =pre_exercise_code
```{r}
library(ggplot2)
library(dplyr)
data("diamonds")
diamonds <- as.data.frame(diamonds)
diamonds <- filter(diamonds, diamonds$table < 54)
```

*** =sample_code
```{r}
library(ggplot2)

# Span auf 0.8



# Span auf 0.1 (Warnungen ignorieren)


```

*** =solution
```{r}
# Span auf 0.8
ggplot(data = diamonds, mapping = aes(x = carat, y = price))+
  geom_point()+
  geom_smooth(span = 0.8)
# Span auf 0.1 (Warnungen ignorieren)
ggplot(data = diamonds, mapping = aes(x = carat, y = price))+
  geom_point()+
  geom_smooth(span = 0.1)
```

*** =sct
```{r}

test_function("ggplot", args = c("data", "mapping"), index = 1)
test_function("geom_point", index = 1)
test_function("geom_smooth", args = c("span"), index = 1)
test_function("ggplot", args = c("data", "mapping"), index = 2)
test_function("geom_point", index = 2)
test_function("geom_smooth", args = c("span"), index = 2)
test_error()
```





--- type:NormalExercise lang:r xp:100 skills:1 key:cf02c17c22
## Grafiken mit mehreren Variablen (I)

Bisher haben Sie Grafiken mit zwei Variablen erstellt. 

Ein Beispiel für eine Grafik mit drei Variablen finden Sie in Ihren Unterlagen - orientieren Sie sich bei der Bearbeitung des  `diamonds` Datensatzen an diesem Beispiel.

*** =instructions
- Erstellen Sie ein Punktediagramm mit `carat` auf der x-Achse und `price` auf der y-Achse.
- Die Punkte sollen die Datenpunkte farblich nach ihrer Qualität (`cut`) trennen.
*** =hint
- setzen Sie im mapping: `group = VARIABLE` und `color = VARIABLE`

*** =pre_exercise_code
```{r}
library(ggplot2)
data("diamonds")
diamonds <- as.data.frame(diamonds)

```

*** =sample_code
```{r}
library(ggplot2)

# Erstellen Sie einen Plot mit den Variablen carat, price und cut.


```

*** =solution
```{r}
# Erstellen Sie einen Plot mit den Variablen carat, price und cut.
ggplot(data = diamonds, mapping = aes(x = carat, y = price, group = cut, color = cut))+
  geom_point()


 
```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"))
test_function("aes")
test_function("geom_point")
test_error()
```
--- type:NormalExercise lang:r xp:100 skills:1 key:b9786438e0
## Grafiken mit mehreren Variablen (II)

Erstellen Sie ein Boxplot über das Gewicht. Je nach Farbkategorie soll ein eigenes Boxplot erstellt werden. 

Zur Erinnerung: Ein Boxplot ist ein Diagramm, welches die Verteilung einer oder mehrerer Merkmale grafisch darstellt. Man sieht so z.B. auf einen Blick Median, Quartile und Ausreißer.

*** =instructions
- Erstellen Sie mit ggplot einen Boxplot, welcher die Verteilung der Gewichte (y-Achse) pro Farbe (x-Achse) erstellt.
- Finden Sie eigenständig das geom, welches einen Boxplot erstellt
- Färben Sie die Ausreißer rot (`outlier.color = "red"`).

*** =hint
- `geom_boxplot(mapping = aes(x  = ___, y = ___), outlier.color = "red")`

*** =pre_exercise_code
```{r}
library(ggplot2)
data("diamonds")
diamonds <- as.data.frame(diamonds)
```

*** =sample_code
```{r}
library(ggplot2)

# Boxplot erstellen



```

*** =solution
```{r}
# Boxplot erstellen

ggplot(data = diamonds, mapping = aes(x = color, y= carat) )+
  geom_boxplot( outlier.color = "red" )

```

*** =sct
```{r}
test_function("ggplot", args = c("data","mapping"))
test_function("geom_boxplot", args = c("outlier.color"))
test_function("aes")
test_error()

```
--- type:NormalExercise lang:r xp:100 skills:1 key:8d133ae583
## ggplot und dplyr

Erstellen Sie aus dem bereits eingelesen Datensatz `daten` zunächst eine "aufgeräumte" Form. 

Stellen Sie anschließend mit `ggplot` drei Zeitreihen in einer Grafik dar.

*** =instructions
- verschaffen Sie sich zunächst einen Überblick über den Datensatz `daten`
- räumen Sie den Datensatz auf
- nutzen Sie das `group` Argument in  ggplot und `geom_line`

*** =hint


*** =pre_exercise_code
```{r}
library(ggplot2)
library(tidyr)
library(dplyr)
 
daten <- read.csv(file="http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/daten.csv", sep=";")
``` 

*** =sample_code
```{r}
library(ggplot2)
library(tidyr)
library(dplyr)

## Aufräumen des Datensatzes
daten_tidy <- 

## Darstellung mit ggplot


```

*** =solution
```{r}

daten_tidy <- gather( daten , Close_google, Close_fb, Close_apple, key="titel", value="Schlusskurs")

ggplot( data = daten_tidy, mapping = aes( x = Datum, y = Schlusskurs, group = titel )) +
  geom_line()

```

*** =sct
```{r}
test_function("gather")
test_function("ggplot", args=("data"))
test_function("geom_line")
```
