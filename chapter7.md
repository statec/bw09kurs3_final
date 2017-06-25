---
title       : Termin 3 (homework) - Noch nicht verfügbar
description : Kontrollstrukturen und Funktionen in R

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:a89b75f3c5
## 1. Wuerfelwurf
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
## 2. Schleife (I)
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
## 3. Schleife (II)
Sie sollen nun mit Hilfe einer Schleife berechnen, wie oft die Zahl fünf eine andere gegebene Zahl `zahl` teilt (es darf ein Rest übrig bleiben). Sie dürfen bei `zahl` von natürlichen Zahlen (0 inklusive) ausgehen.


Tipp:

- Sei 'zahl' = 13. Die Berechnung von 13 - 5 - 5 liefert einen Rest von 3 und die
Information, dass 5 'zahl' zweimal teilt.

*** =instructions
- Ziehen Sie innerhalb der Schleife immer 5 von der Zahl ab.
- Erhöhen Sie anschließend den Zähler `x` um eins.
- Überlegen Sie, bis wohin die Schleife sinnvollerweise gehen sollte, damit `zahl` niemals negativ wird. 
- In Zahl soll am Ende der Rest stehen, der aus der ganzzahligen Division übrig geblieben ist.

*** =hint


*** =pre_exercise_code
```{r}
# zahl setzen
zahl <- 63
```

*** =sample_code
```{r}
# Zähler auf Null setzen
x <- 0
# Schleife 

# Ausgabe von x und zahl
x


```

*** =solution
```{r}
# Zähler setzen
x <- 0
# Schleife
while(zahl >= 5){
  zahl <- zahl - 5
  x <- x + 1
}
# Ausgabe
x


```

*** =sct
```{r}
test_object("x")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:6e737169fe
## 4. Funktionen (I)
Schreiben Sie eine Funktion, welche zwei Zahlen `a` und `b` als Eingabe erhält. Die Funktion soll als Ausgabe das Produkt der beiden Zahlen ausgeben. Sie sollen innerhalb der Funktion das Produkt berechnen, ohne den Multiplikationsoperator `*` zu benutzen. 

Benutzen Sie stattdessen Schleifen und Addition.

Tipp: 

Die Multiplikation 3 * 4 kann genauso als Addition gesehen werden - man addiert 3 mal die 4 aufeinander (4 + 4 + 4).

*** =instructions
- Schreiben Sie die Funktion `multiply` 
- Sie soll als Argument zwei Zahlen `a` und `b` erhalten.
- Benutzen Sie statt eine Multiplikation eine Addition (siehe Tipp).
- Die Funktion soll das Produkt der beiden Zahlen zurück geben.

*** =hint

*** =pre_exercise_code
```{r}
x = 12*14

```

*** =sample_code
```{r}
# Funktion erstellen





# Testen Sie ihre Funktion für a = 12 und b = 14


```

*** =solution
```{r}
# Funktion erstellen
multiply <- function(a,b){
  product <- 0
  while(a>0){
    product <- product + b
    a <- a - 1}
  return(product)
}
# Testen Sie ihre Funktion für a = 12 und b = 14
multiply(12,14)

```

*** =sct
```{r}
test_function("multiply")
test_output_contains("x")
test_error()
```

*** =sct
```{r}

```

--- type:NormalExercise lang:r xp:100 skills:1 key:2dd5d51085
## 5. Funktionen (II)
Schreiben Sie eine Funktion, welche die Wurzel einer Zahl ausgibt. Wenn die Eingabe negativ ist, soll die Wurzel aus dem Absolutwert der Zahl gezogen werden.

*** =instructions
- die Funktion `abswurzel()` erhält eine Zahl als Argument.
- Falls die eingegebene Zahl negativ ist, soll der Absolutwert der Zahl berechnet werden, andernfalls wird die Wurzel der Zahl berechnet.

*** =hint
- mit `sqrt()` kann man die Wurzel einer Zahl ziehen. 

*** =pre_exercise_code
```{r}
n <- 2
```

*** =sample_code
```{r}

```

*** =solution
```{r}
# Funktion
abswurzel <- function(zahl){
  if(zahl < 0 ){ ergebnis <- sqrt(-zahl)}
  else {ergebnis <- sqrt(zahl)}
  return(ergebnis)
}
# Ausgabe Test für 4 und -4
abswurzel(4)
abswurzel(-4)

```

*** =sct
```{r}
test_function("abswurzel")
test_output_contains("n")
test_error()

```
