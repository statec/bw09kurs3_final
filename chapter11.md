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

--- type:NormalExercise lang:r xp:100 skills:1 key:80da065f16
## Hypothesentest (II)
Die Annahmeprüfung für eine Produktion von Sicherungen wird auf Stichprobenbasis durchgeführt. 
Der Hersteller behauptet, der Anteil der nicht funktionsfähigen Sicherungen beträgt höchstens 5%. 
Es wird eine Stichprobe von 500 Stück geprüft.
  
Wie viele Lampen müssen funktionstüchtig sein, um auf einem Signifikanzniveau von 7% anzunehmen, dass die Hypothese des Herstellers korrekt ist?

*** =instructions
- Wie viele Lampen müssen funktionstüchtig sein, um auf einem Signifikanzniveau von 7% anzunehmen, dass die Hypothese des Herstellers korrekt ist?
- Speichern Sie die Lösung in `ergebnis`
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
# Berechnung durch inverse Verteilungsfunktion... 7% im linken rand der Verteilung
ergebnis <- qbinom(p =0.07 , size = 500, prob = 0.95 )
```

*** =sct
```{r}
test_object("ergebnis")
test_function("qbinom", args = c("p", "size", "prob"))
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:b01dd2d16f
## Wiederholung Grafiken
Die folgende Grafik stellt die Wahrscheinlichkeit Pr( X > 1 ) einer standardnormalverteilten Zufallsvariable dar. 


Hinweis: Sie müssen die Grafik nicht exakt nachbilden. Ihre Lösung muss jedoch den gekennzeichneten Bereich der Wahrscheinlichkeitsmasse enthalten. 
Sie müssen außerdem nicht ggplot verwenden. (Es gibt hier keinen automatisierten Test)

*** =instructions
- Replizieren Sie die Grafik. 
- Überprüfen Sie ihre Lösung eigenständig.
*** =hint

*** =pre_exercise_code
```{r}

library(tidyr)
library(ggplot2)
funcShaded <- function(x) {
  y <- dnorm(x)
  y[x < 1] <- NA
  return(y)
}


ggplot(data.frame(x = c(-4, 4)), aes(x = x)) +
  stat_function(fun = dnorm)+
  stat_function(fun = funcShaded, geom="area", fill="blue", alpha=0.2)
```

*** =sample_code
```{r}

```

*** =solution
```{r}
library(tidyr)
library(ggplot2)
funcShaded <- function(x) {
  y <- dnorm(x)
  y[x < 1] <- NA
  return(y)
}


ggplot(data.frame(x = c(-4, 4)), aes(x = x)) +
  stat_function(fun = dnorm)+
  stat_function(fun = funcShaded, geom="area", fill="blue", alpha=0.2)
```

*** =sct
```{r}
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:6e691cab67
## Wiederholung Funktionen
Erstellen Sie eine Funktion, die Ihnen in Abhängigkeit einer übergebenen Verteilung (inkl. eventueller Parameter) die Quantile der Verteilung liefert.

Die Funktion soll mit drei Verteilungen umgehen können: 

- Normalverteilung (mit Paramtern: mean, sd)
- Chiquadrat Vereteilung (mit Parametern: df)
- F Verteilung (mit Paramtern: df1 , df2 )
  
Dokumentieren Sie Ihre Funktion.

*** =instructions
- Erstellen Sie `testfunc()` nach den bereits genannten Bedingungen.
- Testen Sie die bereits vorgegebenen Beispiele.
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
testfunc <- ___


# Test Chiquadrat
chi <- testfunc( typ = "chiquadrat", p = 0.6 , df1 = 3 ) 

# Test Normal
n <- testfunc( typ = "normal" , p = 0.6 ,  mean = 3 , sd = 5) 

# Test F-Verteilung
f <- testfunc( typ = "f", p = 0.6 , df1 = 3, df2=5 ) 

```

*** =solution
```{r}
 testfunc <- function( typ , p,  mean, sd, df1, df2 ){
    if( typ == "normal" ){
      out <- qnorm( p , mean = mean, sd = sd)        
    }
    if( typ == "chiquadrat" ){
      out <- qchisq( p , df = df1 )       
    }
    if( typ == "f" ){
      out <- qf( p , df1 = df1, df2 = df2)        
    }
  return( out )
  }
# Test Chiquadrat
chi <- testfunc( typ = "chiquadrat", p = 0.6 , df1 = 3 ) 

# Test Normal
n <- testfunc( typ = "normal" , p = 0.6 ,  mean = 3 , sd = 5) 

# Test F-Verteilung
f <- testfunc( typ = "f", p = 0.6 , df1 = 3, df2=5 ) 
```

*** =sct
```{r}
test_function("testfunc")
test_object("chi")
test_object("n")
test_object("f")
test_error()
```
