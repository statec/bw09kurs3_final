---
title       : Termin 3 (homework) - Noch nicht verfügbar
description : Kontrollstrukturen und Funktionen in R

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:a89b75f3c5
## Wuerfelwurf
In `wurf` ist das Ergebnis eines Würfelwurfes gespeichert. Bei einer Zahl, die echt größer als eins und echt kleiner als fünf ist, gewinnt man. 


*** =instructions
- Schreiben Sie eine if Abfrage, die die Variable `gewonnen` im Fall eines Sieges auf TRUE und sonst auf FALSE setzt. 
*** =hint
- if(Bedingung1 & Bedingung2){do something}else{do something else}

*** =pre_exercise_code
```{r}
wurf <- 3

```

*** =sample_code
```{r}
# Nutzen Sie if else um abzufragen, ob der wurf gewonnen oder verloren hat und setzen Sie "gewonnen" dementsprechend


```

*** =solution
```{r}
# Nutzen Sie if else um abzufragen, ob der wurf gewonnen oder verloren hat und setzen Sie "gewonnen" dementsprechend
if(wurf > 1 & wurf <5){
    gewonnen <- TRUE}else {
    gewonnen <- FALSE
    }


```

*** =sct
```{r}
test_object("gewonnen")
test_error()

```


--- type:NormalExercise lang:r xp:100 skills:1 key:1bc800d9fd
## Schleife (I)
Gegeben ist ein Vektor `v`. Sie sollen mit Hilfe einer Schleife einen Vektor `r` erstellen, der die Elemente von `v` in umgekehrter Reihenfolge enthält. 


*** =instructions
- Erstellen Sie in einer Schleife einen Vektor `r`, welcher die Elemente von `v` in umgekehrter Reihenfolge enthält.
- Denken Sie daran, dass sie die Funktion `length(vector)` benutzen können, um die Länge eines Vektors zu erhalten.


*** =hint
- Mit `vektor[i]`greift man auf den i-ten Wert des Vektors zu.
- Lassen Sie innerhalb der Schleife eine Variable runter zählen.

*** =pre_exercise_code
```{r}
v <- c(2,4,6,8,9,11,23,33,45,46,47,48)


```

*** =sample_code
```{r}
# Gebe v aus
v
# Initialisiere r
r <- c()
# Erstellen Sie Zählvariable j und setzen Sie sie auf die Länge von v

# for Schleife 

  
```

*** =solution
```{r}
# Gebe v aus
v
# Initialisiere r
r <- c()
# Erstellen Sie Zählvariable j und setzen Sie sie auf die Länge von v
j <- length(v)
# for Schleife die r erstellt
for(i in 1:length(v)){
  r[i] <- v[j]
  j <- j-1}

```

*** =sct
```{r}
test_object("r")
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:bda88050f2
## Schleife (II)


*** =instructions

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```
