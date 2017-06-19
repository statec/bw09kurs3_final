---
title       : Einheit 5 (inclass)
description :  Wahrscheinlichkeitsrechnung und statistische Methoden (I)

 

--- type:NormalExercise lang:r xp:100 skills:1 key:18badc89d0
## Statistische Verteilungen (I)
Sei X eine normalverteilte Zufallsvariable mit Mittelwert 10 und Varianz 2. 
 


*** =instructions
- a) Berechne den Wert Wahrscheinlichkeitsdichte an der Stelle x = 9.
- b) Wie groß ist die Wahrscheinlichkeit, dass X einen Wert kleiner als 8 annimmt?
- c) Für welches x gilt: Pr( X < x ) = 40% ?
- d) Erstellen Sie einen Vektor aus 10 zufälligen Ziehungen dieser Verteilung.

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}
# Wahrscheinlichkeitsverteiling an der Stelle x = 9
dnorm(x = 9, mean = 10, sd = sqrt(2) ) 

# Verteilungsfunktion an der Stelle x = 8
pnorm(q = 8, mean = 10, sd = sqrt(2) )

# kleiner gleich welcher Wert ist X zu 40%
qnorm(p = 0.4 , mean = 10, sd = sqrt(2) )

# 10 zufälligen Ziehungen
rnorm(n = 10, mean = 10, sd = sqrt(2) )


```

*** =sct
```{r}
test_function("dnorm", args = c("x", "mean", "sd"))
test_function("pnorm", args = c("q", "mean", "sd"))
test_function("qnorm", args = c("p", "mean", "sd"))
test_function("rnorm", args = c("n", "mean", "sd"))
test_error()
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:bd5b2e2444
## Statistische Verteilungen (II)
Versuchen Sie die folgende Frage ohne Berechnung zu beantworten.

Welches Ergebnis liefert `qnorm(0.5, mean = 40, sd = 5)`

*** =instructions
- Einen zufälligen Wert zwischen 35 und 45
- 40
- 20
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad))
```



--- type:NormalExercise lang:r xp:100 skills:1 key:51172fb546
## Statistische Verteilungen (III)

Sei X eine chiquadrat verteilte Zufallsvariable mit vier Freiheitsgraden. 
 
Tipp: Um nachzuvollziehen um welche Wahrscheinlichkeiten es geht, ist eine grafische Veranschaulichung immer hilfreich. Führen Sie im vorliegenden Fall z.B. `curve( dchisq(x, df =  4), from = -1, to = 10)` aus. 


*** =instructions
- Berechnen Sie: Pr( 6 < X < 8 )
- Verwenden Sie exakte Werte. Die korrekte Antwort darf also keine Rundungsabweichungen erhalten.
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}




# Speichern Sie Ihr Ergebnis unter dem folgendem Objekt
p <- _____
```

*** =solution
```{r}
p <- pchisq( q = 8 , df= 4 ) - pchisq( q = 6 , df= 4 )
```

*** =sct
```{r}
test_object("p") 
test_error()
success_msg("Sehr gut!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:2182f33994
## Statistische Verteilungen (IV)

Sei X eine binomialverteilte Zufallsvariable mit n=50 und p= 0.1.

*** =instructions
- Wie hoch ist die Wahrscheinlichkeit, dass X die Werte 3, 6 oder 10 annimmt.
- Verwenden Sie exakte Werte. Die korrekte Antwort darf also keine Rundungsabweichungen erhalten.
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}



# Speichern Sie Ihr Ergebnis unter dem folgendem Objekt
p <- _____
```


*** =solution
```{r}
# Speichern Sie das Ergebnis unter folgendem Objekt
p <- dbinom( x = 3 , size = 50, prob = 0.1) +     dbinom( x = 6 , size = 50, prob = 0.1) + dbinom( x = 10 , size = 50, prob = 0.1)
```


*** =sct
```{r}
test_object("p") 
test_error()
success_msg("Sehr gut!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:ab30f0abfa
## ZGS (I)
Das mittlere Jahreseinkommen von Haushalten einer Großstadt beträgt 33000€ mit einer Standardabweichung von 6500€.
Man entnimmt eine Zufallsstichprobe mit 500 Haushalten.



*** =instructions
- Wie hoch ist die Wahrscheinlichkeit in der Stichprobe ein mittleres Jahreseinkommen von über 32800€ zu finden?
- Gehen Sie von der Gültigkeit des ZGS aus und machen Sie sich dessen inhaltliche Bedeutung klar.
- Verwenden Sie exakte Werte. Die korrekte Antwort darf also keine Rundungsabweichungen erhalten.

*** =hint


*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}



# Ergebnis
p <- ___
```

*** =solution
```{r}
Zn  <- sqrt(500)* (32800-33000) /6500 
gegen_p <- pnorm(Zn)
p <- 1 - gegen_p
```

*** =sct
```{r}
test_object("p")
test_error()
success_msg("Sehr gut!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:635ecf6689
## ZGS (II)
Das mittlere Jahreseinkommen von Haushalten einer Großstadt beträgt 33000€ mit einer Standardabweichung von 6500€.
Man entnimmt eine Zufallsstichprobe mit 500 Haushalten.
  

*** =instructions
- Berechnen Sie die Wahrscheinlichkeit dafür, dass der Stichprobenmittelwert zwischen 32750 und 33250 liegt. 
- Gehen Sie von der Gültigkeit des ZGS aus und machen Sie sich dessen inhaltliche Bedeutung klar.
- Verwenden Sie exakte Werte. Die korrekte Antwort darf also keine Rundungsabweichungen erhalten.
*** =hint

*** =pre_exercise_code
```{r}
 

```

*** =sample_code
```{r}



# Ergebnis
p <- ___
```

*** =solution
```{r}
upperbound <- pnorm( sqrt(500)*(33250-33000) /6500 ) 
lowerbound <- pnorm( sqrt(500)*(32750-33000) /6500 ) 
p <- upperbound - lowerbound

```

*** =sct
```{r}
test_object("p")
test_error()
success_msg("Sehr gut!")
```







--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:0d18979882
## Hypothesentests (I)
Das wahre mittlere Jahreseinkommen einer Großstadt sei nun unbekannt. Rechnen Sie weiterhin mit einer Standardabweichung von 6500€.
Sie entnehmen eine Zufallsstichprobe mit 500 Haushalten und beobachten ein Jahreseinkommen von 32000€. 

Überprüfen Sie in einem zweiseitigen Hypothesentest die Nullhypothese, dass das mittlere Jahreseinkommen 32500€ beträgt.

Gehen Sie von der Gültigkeit des ZGS aus.

*** =instructions
- Keine Ablehnung auf den gegeben Signifikanzniveaus
- Ablehnung der Hypothese auf Signifikanzniveau 1%
- Ablehnung der Hypothese auf Signifikanzniveau 5%
- Ablehnung der Hypothese auf Signifikanzniveau 10%
*** =hint
pwert <- 2* pnorm( -abs( (32000 - 35000) / 
                        ( 6500/ sqrt(500) ) 
                        ) )  

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig!"
test_mc(correct = 4, feedback_msgs = c(msg_bad, msg_bad, msg_bad, msg_success))
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:fcb503360c
## Hypothesentests (II)
Die Annahmeprüfung für eine Produktion von Sicherungen wird auf Stichprobenbasis durchgeführt.

Der Hersteller behauptet, der Anteil der nicht funktionsfähigen Sicherungen höchstens 10% beträgt. Eine Stichprobe von 400 zufällig ausgewählten Sicherungen ergab, dass 355 funktionsfähig waren.

Führen Sie basierend auf der Behauptung des Herstellers einen einseitigen Hypothesentest durch.

*** =instructions
- Keine Ablehnung auf den gegeben Signifikanzniveaus
- Ablehnung der Hypothese auf Signifikanzniveau 1%
- Ablehnung der Hypothese auf Signifikanzniveau 5%
- Ablehnung der Hypothese auf Signifikanzniveau 10%

*** =hint
- pwert <- pbinom(q = 355, size = 400, prob = 0.90)
 
*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig!"
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad, msg_bad, msg_bad))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:a015e94bb1
##  Monte Carlo Analyse (I)

Gegeben sei eine Stichprobe der Größe 100 von chiquadratverteilten Zufallsvariablen mit zwei Freiheitsgraden.

Wie hoch ist die asymptotische Varianz des Mittelwertes dieser Stichprobe? 



*** =instructions
- 1/5
- 1/25
- 1/100

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig! Hier gilt stets: Varianz = 2*freiheitsgrade."
test_mc(correct = 2, feedback_msgs = c(msg_success, msg_bad, msg_bad))
```




--- type:NormalExercise lang:r xp:100 skills:1 key:20e949d5dc
## Monte Carlo Analyse (II)

Kehren Sie auf die Folien 18 und 19 in den Unterlagen zurück.

Replizieren Sie die Grafik für n=30 und n=1000. Gehen Sie von 1 Freiheitsgrad aus.

Hinweis: Ihre Lösung kann in diesem Fall ausnahmsweise nicht automatisiert überprüft werden. Sie sind fertig, wenn Ihre Grafiken (nahezu) identisch zu Folie 18 und 19 ist.
*** =instructions
- Setze die korrekte Standardabweichung für der ChiQuadrat verteilung. 
- Überprüfen Sie selbst, ob die von Ihnen erstellte Grafik den entsprechenden Grafiken im Skript entsprechen.
*** =hint

*** =pre_exercise_code
```{r}


```

*** =sample_code
```{r}
# Sie können folgende Hilfestellung verwenden:
 stichproben_groesse <- _____
 varianz_zv <- _____
 varianz_mittelwert<- _____ 
 
 
 check_zgs <- function(groesse, freiheitsgrade){ ____ }
 
 # Generierung der Stichprobenmittelwerte
 mw <- check_zgs( _____ )
 
 # Plotting von mw
 plot(density(mw))
 
 # Asymptotische Verteilung lt. ZGS
 curve( ____ )
```

*** =solution
```{r}
check_zgs <- function(groesse, freiheitsgrade){
  mittelwerte <- c()
  for(i in 1:10000){
    stichprobe_i <- rchisq(n = groesse, df = freiheitsgrade)
    mittelwerte[i] <- mean(stichprobe_i)
  }
  return(mittelwerte)
}

# Anwenden der Funktion für n = 30
groesse = 30
freiheitsgrade = 1
# Varianz = 2*df
varianz = 2
mw <- check_zgs(groesse, freiheitsgrade)
plot(density(mw))
# Setzen Sie die korrekte Standardabweichung
sd_test <- sqrt(varianz/groesse)
# vergleich zur asymptotischen Verteilung laut ZGS (norm)
curve(dnorm(x, mean = 1, sd = sd_test), from = -5, to = 5, col = "red", lwd = 2, add = TRUE)
legend("topright", c("check_zgs", "ZGS"), col=c("black", "red"))

# Anwenden der Funktion für n = 100
groesse = 100
mw <- check_zgs(groesse, freiheitsgrade)
plot(density(mw))
# Setzen Sie die korrekte Standardabweichung
sd_test <- sqrt(varianz/groesse)
# vergleich zur asymptotischen Verteilung laut ZGS (norm)
curve(dnorm(x, mean = 1, sd = sd_test), from = -5, to = 5, col = "red", lwd = 2, add = TRUE)
legend("topright", c("check_zgs", "ZGS"), col=c("black", "red"))
```

*** =sct
```{r}

```