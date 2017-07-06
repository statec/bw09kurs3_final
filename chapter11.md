---
title       : Einheit 5 (homework)
description : Noch nicht verfügbar


--- type:NormalExercise lang:r xp:100 skills:1 key:12f59cf5a0
## Statistische Verteilungen (I)
Sei X normalverteilt mit Mittelwert 10 und Varianz 3.

Betrachten Sie die zwei folgenden Ereignisse:

  - Ereignis A: die Zufallsvariable nimmt werte zwischen 8 und 10 an
  - Ereignis B: die Zufallsvariable nimmt werte zwischen 9 und 11 an


Hinweis: Verwenden Sie stets exakte Werte. Die korrekte Antwort darf keine Rundungsabweichungen erhalten.

*** =instructions
- Berechnen Sie die Wahrscheinlichkeit, dass Ereignis A und B gleichzeitig eintreten und speichern Sie ihre Lösung in `ergebnis`.
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

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
