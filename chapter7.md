---
title       : Termin 3 (homework) - Testdurchlauf
description : Kontrollstrukturen und Funktionen in R

--- type:NormalExercise lang:r xp:100 skills:1 key:d7a4a29850
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

--- type:NormalExercise lang:r xp:100 skills:1 key:86afeaf738
## 6. Funktionen (III)
Schreiben Sie eine Funktion, die für jede Zahl von 1 bis 100 testet, ob sie durch `teiler1` und `teiler2` (Funktionsargumente) teilbar sind. Geben Sie innerhalb der Schleife immer die Zahl selbst aus, wenn sie nicht teilbar ist und "Zahl ist teilbar" wenn die Zahl sowohl durch `teiler1` als auch durch `teiler2` ohne Rest teilbar ist.
Nutzen Sie für die Ausgabe `print("gewünschter Text")`.

Tipp: 

- Benutzen Sie den Modulo-Operator `%%` um zu überprüfen, ob eine Zahl ohne Rest durch eine andere Zahl teilbar ist. Dieser zeigt den Rest einer ganzzahligen Division an.
- Bsp: 7 %% 2 = 1 oder 6 %% 2 = 0
- Die Ausgabe von Text wird durch folgenden Aufbau erreicht: `for(){print("gewünschterText")}`

*** =instructions
- Schreiben Sie die Funktion `teilbar`, welche zwei Argumente (`teiler1` und `teiler2`) als Eingabe erwartet.
- Benutzen Sie eine Schleife, um den Test für alle Zahlen zwischen 1 und 100 durchzuführen.
- Testen Sie in einer if-Abfrage, ob die momentane Zahl sowohl durch `teiler1` als auch durch `teiler2` ganzzahlig teilbar ist.
- Wenn dies der Fall ist, geben Sie "Zahl ist teilbar" mit print() aus. Sonst soll einfach die Zahl ausgegeben werden.
- Die Funktion hat keinen Rückgabewert, da Sie ihr Ergebnis direkt in der Konsole ausgibt.

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}
# Funktion, die ausgibt, welche Zahlen von 1 bis 100 durch zahl1 und zahl2 ganzzahlig teilbar sind
teilbar <- function(teiler1, teiler2){
  for(i in 1:100){
    if(i %% teiler1 == 0 & i %% teiler2 == 0){
      print("Zahl ist teilbar")} else{
        print(i)
      }
  }
}
# Test an 2 und 3
teilbar(2,3)

```

*** =sct
```{r}
test_function("teilbar")
test_error()

```


--- type:NormalExercise lang:r xp:100 skills:1 key:22d885d3af
## 7. Funktionen(IV) 
In einer Firma reicht ein Mitarbeiter seine gewünschten Urlaubstage für das Jahr 2017 ein (diese liegen im Vektor `wunsch_urlaub`). Am 20.07.2017 und die Zeit zwischen dem 28. und dem 30. Dezember 2017 besteht eine Urlaubssperre.

Schreiben Sie eine Funktion, welche mögliche Terminkonflikte erkennt.

Info: 

- Gehen Sie einfachheitshalber von folgender Form aus: "JJJJ-MM-TT", also z.B. "2017-04-03" 

*** =instructions

- Vergleichen Sie innerhalb der Funktion jeden Wert des Arguments mit den "verbotenen" Tagen. 
- Sie kennen dabei die Anzahl der eingereichten Urlaubstage nicht.
- Die Ausgabe beinhaltet den Vektor mit den Daten, die nicht kollidieren und kennzeichnet Terminkonflikte mit "abgelehnt".
- die Eingabe c("2017-10-03", "2017-12-29", "2017-12-30") liefer also c("2017-10-03", "abgelehnt", "abgelehnt")
- Testen Sie die Funktion mit `wunsch_urlaub`.

*** =hint
- Verwenden Sie eine for-Schleife, welche den Vektor durchläuft und eine if-Abfrage, welche die Bedingung überprüft.

*** =pre_exercise_code
```{r}
# Erstellung der Vektoren
wunsch_urlaub <- c("2017-10-03", "2017-10-04", "2017-10-05", "2017-10-06", "2017-07-20", "2017-07-21",  "2017-07-22",  "2017-07-23",  "2017-07-24", "2017-12-23", "2017-12-28", "2017-12-29", "2017-12-30")

# Ergebnis 
xoxo <- c("2017-10-03", "2017-10-04", "2017-10-05", "2017-10-06", "abgelehnt", 
"2017-07-21", "2017-07-22", "2017-07-23", "2017-07-24", "2017-12-23", 
"abgelehnt", "abgelehnt", "abgelehnt")

```

*** =sample_code
```{r}
#  Schreibe Funktion Urlaub
check_urlaub <- function( wunsch_urlaub ){









  return(possible)
}

# Funktion ausführen
check_urlaub( wunsch_urlaub )


```

*** =solution
```{r}
#  Schreibe Funktion Urlaub
check_urlaub <- function(daten){
 # initialisiere output
  output<- length(daten)
 # Gehe den ganzen daten Vektor durch
  for(i in 1:length(daten)){
 # Bedingung - ist es ein Kollisionstag?
    if(daten[i] != "2017-07-20" & (daten[i] < "2017-12-28" | daten[i] > "2017-12-30") ){
    # kein Kollisionstag, also kann Datum in Vektor output geschrieben werden.
      output[i] <- daten[i]
      } else {
      output[i] <- "abgelehnt"
      }
    }
 
# output zurückgeben
  return(output)
}

# Funktion ausführen
check_urlaub(wunsch_urlaub)

```

*** =sct
```{r}
test_function("check_urlaub")
test_output_contains("xoxo")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:6d3abcf16f
## 8. Funktionen(V) 
Aus der Übungen kennen Sie bereits eine Funktion geschrieben, die den gleitenden Durchschnitt für ein beliebiges Fenster berechnet. 

Bisher durften Sie davon ausgehen, dass die eingegebene Länge des Fensters eine ungerade natürliche Zahl ist. 

Diese Annahme soll nun aufgehoben werden: Setzen Sie die Fensterlänge für gerade Eingaben innnerhalb der Funktion auf einen um 1 erhöhten Wert.

*** =instructions
- Schreiben Sie eine Funktion `gleitender_durchschnitt`, die als Argument einen Vektor `zeitreihe` und eine Fensterlänge `x` erwartet.
- Zuerst soll die Funktion prüfen, ob `x`  gerade oder ungerade ist, und x gegebenenfalls um eins erhöhen.
- Orientieren Sie sich weitestgehend an der Funktion aus den Vorlesungsunterlagen.
- Sie gibt am Ende einen Vektor `ergebnis` zurück.
- Testen Sie ihre Funktion an dem gegebenen Vektor `reihe`.

*** =hint
- Die Struktur einer Funktion: 
- `neue_funktion <- function(Eingabeparameter){...working ...return (Ausgabeparameter)}`
- Berechnen Sie zuerst den Abstand nach links und rechts in der Zeitreihe und speichern Sie diesen in einer neuen Variable in der Funktion.
- Bedenken Sie, dass z.B. der gleitende 9-er Durchschnitt für die ersten und letzten 4 Zahlen nicht berechnet werden kann.

*** =pre_exercise_code
```{r}
reihe <- c(1, 33, 45, 33, 4, 66, 78, 98, 98, 99, 102, 103, 45, 304, 255, 32, 6, 78, 12, 3, 4, 56, 7, 1, 0)
xyz <- c(1.00000,  33.00000,  45.00000,  37.14286,  51.00000,  60.28571,  68.00000,  77.85714,  92.00000,  89.00000, 121.28571, 143.71429, 134.28571, 121.00000, 117.57143, 104.57143,  98.57143,  55.71429,  27.28571,  23.71429,  23.00000,  11.85714,   7.00000,   1.00000,  0.00000)



```

*** =sample_code
```{r}
# Funktion Berechnung gleitender Durchschnitt








# Testen Sie ihre Funktion an reihe mit x = 6 und x = 7
gleitender_durchschnitt(reihe, 6)
gleitender_durchschnitt(reihe, 7)


```

*** =solution
```{r}
# Funktion Berechnung gleitender Durchschnitt
gleitender_durchschnitt <- function(zeitreihe, x){
    laenge <- length(zeitreihe)
    ergebnis <- c()
    if(x %% 2 == 0){ x <- x + 1 }
    # Berechnung des Abstandes nach links und rechts
    n <- (x-1)/2
    for(i in 1:laenge){
        # Darf nicht für die ersten n Zahlen berechnet werden
        if( i <= n | i > (laenge-n)){
            ergebnis[i] <- zeitreihe[i]
        }else{
            ergebnis[i] <- mean( zeitreihe [(i - n) : (i + n)])
        }
    }
    return(ergebnis)
}
# Test an reihe mit x = 6 und x = 7
gleitender_durchschnitt(reihe, 6)
gleitender_durchschnitt(reihe, 7)

```

*** =sct
```{r}
test_function("gleitender_durchschnitt")
test_output_contains("xyz")
test_error()
```


--- type:NormalExercise lang:r xp:100 skills:1 key:994a9f6147
## 9. Funktionen (VI)
Gegeben ist die folgende Funktion zur Berechnung des Indizes für das Maximum eines Vektors.

*** =instructions
- Finden Sie den Fehler und korrigieren Sie ihn.
- Testen Sie selbst, ob ihre Funktion korrekt funktioniert. 
- Sie können ihre Funktion am Vektor `v` testen.
*** =hint

*** =pre_exercise_code
```{r}
v <- c(1:10)

```

*** =sample_code
```{r}
find_max_index <- function( vector ){
laenge <- length(vector)
max <- vector[1]
i <- 1
while( i <= laenge ){
    if( vector[i] > laenge ){
        max <- vector[i]
    }
    i <- i + 1
    }
max_index<- which( vector == max)
return( max_index )
}

```

*** =solution
```{r}
# Eine mögliche Lösung
find_max_index <- function( vector ){
laenge <- length(vector)
max <- vector[1]
max_index <- 1
i <- 1
# Gehe den ganzen Vektor durch
while( i <= laenge ){
    # Wenn ein Wert größer ist, aktualisiere max
    if( vector[i] > max ){
        # Setze neues Maximum
        max <- vector[i]
        # Setze neuen Ergbebnisindex
        max_index <- i
    }
    i <- i + 1
    }
return( max_index )
}

```

*** =sct
```{r}

```
