---
title       : Einheit 5 (homework)
description : Noch nicht verfügbar


--- type:NormalExercise lang:r xp:100 skills:1 key:12f59cf5a0
## Statistische Verteilungen (I)
Sei X normalverteilt mit Mittelwert 10 und Varianz 3.

Betrachten Sie die zwei folgenden Ereignisse:

  - Ereignis A: die Zufallsvariable nimmt werte zwischen 8 und 10 an
  - Ereignis B: die Zufallsvariable nimmt werte zwischen 9 und 11 an


Hinweis für alle folgenden Aufgaben: 

Verwenden Sie stets exakte Werte. Die korrekte Antwort darf keine Rundungsabweichungen erhalten.

*** =instructions
- Berechnen Sie die Wahrscheinlichkeit, dass Ereignis A und B gleichzeitig eintreten und speichern Sie ihre Lösung in `ergebnis`.
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
ergebnis <- ___
```

*** =solution
```{r}
# Pr( A geschnitten B )
ergebnis <- pnorm( 10,mean = 10,sd = sqrt(3)) - pnorm( 9,mean = 10,sd = sqrt(3))
```

*** =sct
```{r}
test_function("pnorm", args = c("q", "mean", "sd"), index = 1)
test_function("pnorm", args = c("q", "mean", "sd"), index = 2)
test_object("ergebnis")
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:318c5c9d44
## Statistische Verteilungen (II)
Eine Zufallsvariable X sei chiquadrat-verteilt mit 3 Freiheitsgraden.

Betrachten Sie den vorgegebenen R Code.

*** =instructions
- Überlegen Sie sich die inhaltliche Bedeutung des angegebenen Integrals.
- Welche R Funktion setzt diese Berechnung automatisch um? 
- Geben Sie den Befehl mit den entsprechenden Werten an. 
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
  f <- function(x){
    out <- dchisq( x, df = 3 )
    return( out )
  }

integrate( f , lower = 0 , upper = 4)  
```

*** =solution
```{r}
pchisq(4,df=3)
```

*** =sct
```{r}
test_function("pchisq", args = c("q", "df"))
test_error()
```



--- type:NormalExercise lang:r xp:100 skills:1 key:41a3ded1c4
## Statistische Verteilungen (III)
Sei X F-verteilt mit den Freiheitsgraden 3 und 5.


*** =instructions
- Berechnen Sie Pr(3 < X < 8).
- Speichern Sie ihre Lösung in `ergebnis`.
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

ergebnis <- ___
```

*** =solution
```{r}
ergebnis <- pf(8, df1=3, df2= 5) - pf(3,  df1=3, df2= 5)
```

*** =sct
```{r}
test_function("pf", args = c("q", "df1", "df2"), index = 1)
test_function("pf", args = c("q", "df1", "df2"), index = 2)
test_object("ergebnis")
test_error()
```


--- type:NormalExercise lang:r xp:100 skills:1 key:4c9158fb1b
## Statistische Verteilungen (IV)

Sei X chiquadrat-verteilt mit 8 Freiheitsgraden.


Berechnen Sie y, sodass gilt:
  
  Pr( 6 < X < y) = 0.4

*** =instructions
- Speichern Sie ihr Ergebnis in y.
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}


y <-  ___
```

*** =solution
```{r}
# Pr(X<0.6)
tmp1 <- pchisq(6, df = 8)
  
# also ist   Pr( 0 < X < y) = (ca.) 0.35 + 0.4
y <- qchisq( tmp1 + 0.4, df = 8)
  
# teste: 
pchisq( y, df = 8 )- pchisq( 6, df = 8) # läuft!
```

*** =sct
```{r}
test_object("y")
test_error()
```


--- type:NormalExercise lang:r xp:100 skills:1 key:95f2f25dca
## Hypothesentest (I)
Für die Mitarbeiter eines Geschäftsbereichs ist ein Gehaltsbudget von 2000 Euro veranschlagt, wobei Abweichungen von dieser Obergrenze in Einzelfällen zulässig sind.

Eine Stichprobe unter 500 Mitarbeitern weist ein Durchschnittsgehalt von 2040 Euro aus. Die Standardabweichung des Gehalts beträgt 120 Euro .

Testen Sie auf einem 5% Signifikanzniveau, ob das Budget zu knapp bemessen ist.

*** =instructions
- Führen Sie einen vollständigen Hypothesentest durch (inkl. Nullhypothese, Teststatistik und Testentscheidung). 
- Rechnen Sie mit exakten Werten.
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# H_0: ___
teststat <- ___

# Testentscheidung: ___
```

*** =solution
```{r}
# H_0 : mu<2000
teststat <-  (2040-2000)/ (120/sqrt(500))
pnorm(-abs(teststat)) 
# Testentscheidung: verwerfe
```

*** =sct
```{r}
test_object("teststat")
test_function("pnorm")
test_error()
```
