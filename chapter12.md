---
title       : Einheit 6 (inclass)
description : Varianzanalyse und Modellierung


--- type:NormalExercise lang:r xp:100 skills:1 key:82ad91f31b
## ANOVA (I)
Ihnen ist ein `datensatz` gegeben. 

Untersuchen Sie mittels einer univariaten Anova Analyse, ob sich die Gruppenmittelwerte von `werte` signifikant voneinander unterscheiden.

*** =instructions
- Benutzen Sie `aov()` um eine Varianzanalyse durchzuführen.
- Speichern Sie das Ergebnis in `res`.
- Geben sie das Summary des Ergebnisses aus. 
*** =hint

*** =pre_exercise_code
```{r}
n <- 100
set.seed(2)
# Erstellt Zufallszahlen
gruppe1 <- rnorm(n, mean = 0, sd = 5)
gruppe2 <- rnorm(n, mean = 1, sd = 5)
gruppe3 <- rnorm(n, mean = 2, sd = 5)
gruppe4 <- rnorm(n, mean = 3, sd = 5)
# Liste der Gruppen
werte <- c(gruppe1, gruppe2, gruppe3, gruppe4)
gruppenname <- c(rep("g1", n), rep("g2", n), rep("g3",n), rep("g4", n))
datensatz <- data.frame(werte, gruppenname)

```

*** =sample_code
```{r}
# ANOVA Analyse
res <- _____

# Summary
summary(res)

```

*** =solution
```{r}
# ANOVA Analyse
res <- aov(werte ~ gruppenname, data = datensatz)

# Summary
summary(res)
```

*** =sct
```{r}
test_function("aov", args = c("data"))
test_object("res")
test_error()
success_msg("Sehr gut!")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:920fd7379a
## ANOVA (II)
Wenden Sie nun die Formel zur Berechnung der Teststatistik an. Berechnen Sie zunächst den Zähler (Abweichung im Gruppenmittelwert). 

Die Daten liegen in `datensatz`.


Tipp: Die Daten sind in 4 Gruppen aufgeteilt, welche in `gruppe_i` für 1<=i<=4 enthalten sind.

*** =instructions
- Berechnen Sie die Abweichung im Gruppenmittelwert.
- Speichern Sie das Ergebnis in `zaehler`.
*** =hint

*** =pre_exercise_code
```{r}
n <- 100
set.seed(2)
# Erstellt Zufallszahlen
gruppe_1 <- rnorm(n, mean = 0, sd = 5)
gruppe_2 <- rnorm(n, mean = 1, sd = 5)
gruppe_3 <- rnorm(n, mean = 2, sd = 5)
gruppe_4 <- rnorm(n, mean = 3, sd = 5)
# Liste der Gruppen
werte <- c(gruppe_1, gruppe_2, gruppe_3, gruppe_4)
gruppenname <- c(rep("g1", n), rep("g2", n), rep("g3",n), rep("g4",n))
datensatz <- data.frame(werte, gruppenname)


```

*** =sample_code
```{r}






zaehler <- ___


```

*** =solution
```{r}
# Anzahl der Gruppen
l <- 4
# Anzahl der Beobachtungen pro Gruppe
n_i <- 100
# means berechnen
m_g1 <- mean(gruppe_1)
m_g2 <- mean(gruppe_2)
m_g3 <- mean(gruppe_3)
m_g4 <- mean(gruppe_4)
m_all <- mean(c(gruppe_1, gruppe_2, gruppe_3, gruppe_4))
# Abweichung im Gruppenmittelwert
zaehler <- 1/(l-1) * (  n_i* ( m_g1 - m_all )^2 +
                        n_i* ( m_g2 - m_all )^2 +
                        n_i* ( m_g3 - m_all )^2 +
                        n_i* ( m_g4 - m_all )^2 )
```

*** =sct
```{r}
test_object("zaehler")
test_error()
success_msg("Sehr gut!")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:b3ecb8c0b2
## ANOVA (III)
Berechnen Sie als nächstes den Nenner der Teststatistik (berücksichtigt die Varianz innerhalb der Gruppen).

Die Daten liegen in `datensatz`. Das Ergebnis der vorherigen Aufgabe steht in `zaehler`.

Tipp: Um die Summen über die korrekten vektoren zu bilden, müssen Sie den Datensatz erst anhand der Gruppen aufteilen. 

*** =instructions
- Berechnen Sie die Varianz innerhalb der Gruppen.
- Speichern Sie das Ergebnis in `nenner`.
- Benutzen Sie `filter()` um die Gruppen aufzuteilen.
- Berechnen Sie F.
*** =hint

*** =pre_exercise_code
```{r}
n <- 100
set.seed(2)
# Erstellt Zufallszahlen
gruppe_1 <- rnorm(n, mean = 0, sd = 5)
gruppe_2 <- rnorm(n, mean = 1, sd = 5)
gruppe_3 <- rnorm(n, mean = 2, sd = 5)
gruppe_4 <- rnorm(n, mean = 3, sd = 5)
# Liste der Gruppen
werte <- c(gruppe_1, gruppe_2, gruppe_3, gruppe_4)
gruppenname <- c(rep("g1", n), rep("g2", n), rep("g3",n), rep("g4",n))
datensatz <- data.frame(werte, gruppenname)

# Anzahl der Gruppen
l <- 4
# Anzahl der Beobachtungen pro Gruppe
n_i <- 100
# means berechnen
m_g1 <- mean(gruppe_1)
m_g2 <- mean(gruppe_2)
m_g3 <- mean(gruppe_3)
m_g4 <- mean(gruppe_4)
m_all <- mean(c(gruppe_1, gruppe_2, gruppe_3, gruppe_4))
# Abweichung im Gruppenmittelwert
zaehler <- 1/(l-1) * (  n_i* ( m_g1 - m_all )^2 +
                        n_i* ( m_g2 - m_all )^2 +
                        n_i* ( m_g3 - m_all )^2 +
                        n_i* ( m_g4 - m_all )^2 )
```

*** =sample_code
```{r}
library(dplyr)







# Varianz innerhalb der Gruppen
nenner <- _____




# Ergebnis
F_wert <- zaehler/nenner
# Vergleich mit aov()
summary( aov( werte ~ gruppenname, data = datensatz ) )
```

*** =solution
```{r}
library(dplyr)
# Anzahl der Gruppen
l <- 4
# Anzahl Beobachtungen von allen Gruppen
n <- 400
# Gruppentrennung
g1 <- filter(datensatz, gruppenname == "g1")
g2 <- filter(datensatz, gruppenname == "g2")
g3 <- filter(datensatz, gruppenname == "g3")
g4 <- filter(datensatz, gruppenname == "g4")
# means berechnen
m_g1 <- mean(g1$werte)
m_g2 <- mean(g2$werte)
m_g3 <- mean(g3$werte)
m_g4 <- mean(g4$werte)
# Varianz innerhalb der Gruppen
nenner <- 1/( n - l ) * ( sum( ( g1$werte - m_g1 )^2 ) +
                            sum( ( g2$werte - m_g2 )^2 ) +
                            sum( ( g3$werte - m_g3 )^2 ) +
                            sum( ( g4$werte - m_g4 )^2 ) )
# Ergebnis
F_wert = zaehler/nenner
# Vergleich mit aov()
summary(aov(werte ~ gruppenname, data = datensatz))
```

*** =sct
```{r}
test_object("nenner")
test_object("F_wert")
test_function("aov", args = c("data"))
test_error()
success_msg("Sehr gut!")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:4ce94c7b53
## ANOVA(IV)

Die Gültigkeit der F-Verteilung gilt nur für normalverteilte Variablen mit gleicher Varianz innerhalb der Gruppen.

Überprüfen Sie mittels grafischer Analyse die Annahme der Normalverteilung. 

Extrahieren Sie dazu die Werte einer bestimmten Gruppe (z.B. in `gruppe_xy`) und verwenden Sie `hist( gruppe_xy )` oder `plot( density( gruppe_xy ) )`.

Ein Beispiel `datensatz2` ist bereits eingelesen.
*** =instructions

- Die Normalverteilungsannahme trifft zu.
- Die Normalverteilungsannahme trifft nicht zu.

*** =hint

*** =pre_exercise_code
```{r}
n <- 100
set.seed(2)
# Erstellt Zufallszahlen
gruppe_1 <- rnorm(n, mean = 0, sd = 5)
gruppe_2 <- rnorm(n, mean = 1, sd = 25)
gruppe_3 <- rnorm(n, mean = 2, sd = 5)
gruppe_4 <- rnorm(n, mean = 3, sd = 100)
# Liste der Gruppen
werte <- c(gruppe_1, gruppe_2, gruppe_3, gruppe_4)
gruppenname <- c(rep("g1", n), rep("g2", n), rep("g3",n), rep("g4",n))
datensatz2 <- data.frame(werte, gruppenname)

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig!"
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad))
```





--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:92a85b0c7c
## ANOVA(V)

Die Gültigkeit der F-Verteilung gilt nur für normalverteilte Variablen mit gleicher Varianz innerhalb der Gruppen.

Überprüfen Sie mittels grafischer Analyse die Annahme identischer Varianzen. 

Extrahieren Sie dazu die Werte einer bestimmten Gruppe (z.B. in `gruppe_xy`) und verwenden Sie `hist( gruppe_xy )` oder `plot( density( gruppe_xy ) )`.

Ein Beispiel `datensatz2` ist bereits eingelesen.
*** =instructions

- Es liegt Varianzhomogenität vor.
- Es liegt keine Varianzhomogenität vor.

*** =hint

*** =pre_exercise_code
```{r}
n <- 100
set.seed(2)
# Erstellt Zufallszahlen
gruppe_1 <- rnorm(n, mean = 0, sd = 5)
gruppe_2 <- rnorm(n, mean = 1, sd = 25)
gruppe_3 <- rnorm(n, mean = 2, sd = 5)
gruppe_4 <- rnorm(n, mean = 3, sd = 100)
# Liste der Gruppen
werte <- c(gruppe_1, gruppe_2, gruppe_3, gruppe_4)
gruppenname <- c(rep("g1", n), rep("g2", n), rep("g3",n), rep("g4",n))
datensatz2 <- data.frame(werte, gruppenname)

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success))
```











--- type:NormalExercise lang:r xp:100 skills:1 key:9a4690dabe
## Lineare Regression
Berechnen Sie mittels `lm()` den Zusammenhang zwischen den Eröffnungskursen von Google und Apple. Diese liegen in `daten_google` und `daten_apple`.

Tipp: Sie können per `coefficients( linreg )[i]` auf den i-ten Koeffizienten zugreifen.


*** =instructions
- Regressieren Sie die Eröffnungskurse von Google auf die von Apple.
- Speichern Sie die lineare Regressionsgerade in `linreg`.
- Plotten Sie Ihr Ergebnis, sodass der Plot wie der vorgegebene aussieht.

*** =hint

*** =pre_exercise_code
```{r}



apple_data <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/AAPL.csv")
google_data <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/GOOG.csv")

open_apple <- apple_data$Open
open_google <- google_data$Open

linreg <- lm( open_google ~ open_apple )


plot( open_apple , open_google , type = "p" , lwd= 2, xlab="Apple", ylab="Google" )
curve( coefficients(linreg)[1] + coefficients(linreg)[2]*x , add=TRUE , col="red", lty= 2 , lwd= 4)

```

*** =sample_code
```{r}



linreg <- _____
plot( _____ , _____ , type = "p" , lwd= 2, xlab="Apple", ylab="Google" )
curve( _____ , add=TRUE , _____, lty= 2 , lwd= 4)
```

*** =solution
```{r}
linreg <- lm( open_google ~ open_apple )
plot( open_apple , open_google , type = "p" , lwd= 2, xlab="Apple", ylab="Google" )
curve( coefficients(linreg)[1] + coefficients(linreg)[2]*x , add=TRUE , col="red", lty= 2 , lwd= 4)
```

*** =sct
```{r}
test_object("linreg")
test_function("curve")
test_function("plot")
test_error()
success_msg("Sehr gut!")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:3c4f6d0b92
## Logistische Regression (I)
Ihnen ist der Datensatz `titanic` gegeben, der Daten von Passagieren auf der Titanic enthält.

Untersuchen Sie den Zusammenhang zwischen dem Überleben der Passagiere und dem Alter.
    

*** =instructions
- Führen Sie eine nicht lineare Schätzung mit dem logistischen Regressionsmodell durch.
*** =hint

*** =pre_exercise_code
```{r}

titanic <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3874/datasets/Titanic.csv")

```

*** =sample_code
```{r}
# lineare Schaetzung
reg2 <- ____
# summary()


# Plot
plot( titanic$Age , titanic$Survived, 
      type = "p", xlab="Alter", ylab="Überlebend" )
curve( 1/ ( 1 + exp( - (coefficients(reg2)[1] + coefficients(reg2)[2]*x ) ) ), 
       add = TRUE, col="red")

```

*** =solution
```{r}
reg2 <- glm(Survived ~ Age, data = titanic, family=binomial(link='logit'))
summary(reg2)


```

*** =sct
```{r}
test_object("reg2")
test_error()
success_msg("Sehr gut!")
```

