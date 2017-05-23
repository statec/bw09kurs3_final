---
title       : Termin 3 (inclass)
description : Kontrollstrukturen und Funktionen in R

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:a89b75f3c5
## if-Abfrage(I)
Gegeben ist der folgende R-Code:

`a <- 1`

`if(FALSE) {a <- sqrt(-4)} else {a <- 3}`

*** =instructions
- a ist 1
- a ist 3
- a ist nicht definiert

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig! Die if Bedingung wird nicht erfüllt, somit wird der else-Teil ausgeführt."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad))

```

--- type:NormalExercise lang:r xp:100 skills:1 key:a545b07906
## if-Abfrage(II)
Im Beispielcode ist eine if-Abfrage gegeben. Führen Sie diese aus und überlegen Sie, was passiert ist.

Tipp: Wenn Sie bestimmte Codeabschnitte, also mehrere Zeilen auf einmal, in der Konsole ausführen möchten, markieren Sie den gewünschten Codeabschnitt und drücken Sie gleichzeitig `Strg` und `Enter`.


*** =instructions
- Führen Sie die if-Abfrage aus und geben Sie `a` in der Konsole aus.
- Ändern Sie anschließend die Bedingung von "FALSE" auf "TRUE" und führen Sie die Abfrage erneut aus. 
- Schauen Sie sich wieder `a` in der Konsole an.


*** =hint

*** =pre_exercise_code
```{r}
text_if <- "ich bin in der if-Abfrage enstanden"
text_else <- "ich bin in dem else-Teil entstanden"

```

*** =sample_code
```{r}
# text_if und text_else sind bereits existierende Variablennamen

# Führe die Abfrage durch und gebe a in der Konsole aus.
if( FALSE ){
  a <- text_if
} else { a<- text_else }
# Ausgabe
a

# Ändere Bedingung so, dass text_if ausgegeben wird
if(___){
    a <- text_if} else { a<- text_else }
# Ausgabe
a
```

*** =solution
```{r}
# Führe if-Abfrage aus und gebe a aus.
if(FALSE){
    a <- text_if} else { a<- text_else }
print(a)

# Ändere Bedingung zu TRUE und geben erneut a aus.
if(TRUE){
    a <- text_if} else { a<- text_else }
print(a)


```

*** =sct
```{r}
test_output_contains("text_if")
test_output_contains("text_else")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:fe02cb131f
## if-Abfrage(III)
Ihnen ist wieder eine if-Abfrage gegeben, nur die Bedingung fehlt. 

Je nachdem ob die Variable `note` kleiner oder gleich 4 ist, soll die Variable `ergebnis` den Wert "bestanden" oder "nicht bestanden" beinhalten.

*** =instructions
- setzen Sie die Bedingung für die if-Abfrage.
*** =hint
- Für die Vergleichsoperatoren nehmen Sie die Vorlesungsunterlagen zur Hilfe.

*** =pre_exercise_code
```{r}
note = 3
ergebnis = "bestanden"
```

*** =sample_code
```{r}
# Abfrage der Note
if(note ____ ){
  ergebnis <- ____ }else{ }

# Ausgabe von Note (bereits eingelesen) und Ergebnis
note
ergebnis
```

*** =solution
```{r}
# Abfrage
if(note <= 4){
    ergebnis <- "bestanden" }else{ ergebnis <- "nicht bestanden"}

```

*** =sct
```{r}
test_object("ergebnis")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:9dcf2f1327
## if-Abfrage(IV)
Nun sollen Sie Ihre erste eigene if-Abfrage schreiben. Gegeben sind die Variablen a und b. 

Die Variable c ist die Differenz von a und b und soll in unserem Beispiel nur positive Werte annehmen. Es muss daher vor der Berechnung getestet werden, ob a oder b größer ist.

Schauen Sie in die Vorlesung oder in den "Hint" um zu sehen, wie das Gerüst aufgebaut ist.


*** =instructions
- Schreiben Sie eine if-Abfrage, die abfragt ob `a` kleiner gleich `b` ist.
- Wenn das der Fall ist, setzen Sie `c` auf `b-a`.
- Falls nicht, greift der else-Teil: dann soll c = a-b sein.

*** =hint
- `if(Bedingung){c <- ___ }else{c <- ___ }`

*** =pre_exercise_code
```{r}
a = 2
b = 5
```

*** =sample_code
```{r}
# a und b sind bereits eingelesen
# schreiben Sie eine if-Abfrage

    
# Geben Sie das Ergebnis c aus.
c
```

*** =solution
```{r}
# schreiben Sie eine if-Abfrage
if(a <= b){
    c <- b-a} else{ c <- a-b }
    
# Geben Sie das Ergebnis c aus.
c
```

*** =sct
```{r}
test_object("c")
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:4cc9a15a6f
## if-Abfrage(V)
Gegeben ist Ihnen die Variablen `a` und `b`. Wenn `a` ungleich null ist, dann soll `b` durch `a` geteilt werden. 


*** =instructions
- Schreiben Sie eine if-Abfrage die TRUE ist, wenn `a` ungleich Null ist.
- Wenn das der Fall ist, soll `b` durch `a` geteilt werden.

*** =hint
- `if(Bedingung){___}`
*** =pre_exercise_code
```{r}
a <- 2
b <- 10
c <- b/a

```

*** =sample_code
```{r}
# Falls a nicht gleich 0, soll b durch a gerechnet werden.


```

*** =solution
```{r}
# Falls a ungleich 0, soll b/a gerechnet werden.
if(a != 0){
    b/a} 

```

*** =sct
```{r}
test_output_contains("c")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:4ed9623928
## for-Schleife
Die Fibonaccifolge ist eine Zahlenfolge von natürlichen Zahlen, die mit zwei Einsen beginnt. Die weiteren Zahlen der Folge sind immer die Summe der beiden vorangegangenen Zahlen, 


also 1, 1, 2, 3, ...

*** =instructions
- Berechnen Sie in einer for-Schleife die 3. bis 10. Fibonaccizahl.
- Speichern Sie die Zahlen im Verktor `fib`.

*** =hint
- `for(Bedingung){Ausführung}`

*** =pre_exercise_code
```{r}
```

*** =sample_code
```{r}
# Vektor "fib" initialisieren
fib <- c()
# Erste beiden Werte Setzen
fib[1]<- 
fib[2]<- 
# Berechnen Sie den Verktor "fib" bis zur 10. Stelle in einer for-Schleife


# Geben Sie "fib" in der Konsole aus.
fib

```

*** =solution
```{r}
# Vektor "fib" initialisieren
fib <- c()
# Erste beiden Werte Setzen
fib[1]<- 1
fib[2]<- 1
# Berechnen Sie den Verktor "fib" bis zur 10. Stelle in einer for-Schleife
for(i in 3:10){
  fib[i] <- fib[i-1] + fib[i-2]}
# Geben Sie "fib" in der Konsole aus.
fib


```

*** =sct
```{r}
test_object("fib")
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:6e2eab47f2
## while-Schleife
Hier sehen Sie eine while-Schleife, die die Fakultät von `zahl` berechnet. Füllen Sie die Lücken im vorgegebenen Code.

Tipp:

- Denken Sie daran - um einen Teil des Codes auszuprobieren, können Sie diesen Teil markieren und gleichzeitig `Strg` und `Enter` betätigen.
- Denken Sie dran, dass keine Endlosschleifen entstehen dürfen.

*** =instructions
- Ergänzen Sie den Code so, dass in der while-Schleife die Fakultät der `zahl` berechnet wird und in `fak` gespeichert wird.

*** =hint
- Die Fakultät berechnet sich bsp. für 4! = 1\*2\*3*4 
- Um die while-Schleife auf jeden Fall terminieren zu lassen, muss sichergestellt werden, dass die Zählvariable `i` in der while-Schleife um eins erhöht wird.

*** =pre_exercise_code
```{r}
ergebnis <- 120

```

*** =sample_code
```{r}
# Testen Sie ihre Schleife mit der Zahl 5
i <- 1
zahl <- 5
fak <- 1
# while Schleife zur Fakultätsberechnung
while(i <= ___){
  fak <- ___*i
  i <- ___
}

# Ergebnis Ausgabe
fak


```

*** =solution
```{r}
# Initialisierung der Werte
i <- 1
zahl <- 5
fak <- 1
# Fakultätsberechnung
while(i <= zahl){
  fak <- fak * i
  i <- i+1
}
# Ausgabe des Ergebnisses
print(fak)

```

*** =sct
```{r}
test_output_contains("ergebnis")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:bc6c49a486
## Funktionen (I)
In den Folien haben Sie gesehen, wie man den Absolutwert einer Zahl berechnen kann. Um eine solche Abfrage immer wieder nutzen zu können, ist es sinnvoll, Sie in eine Funktion einzubetten.

Funktionen haben Eingabeparameter und Ausgabeparameter. Als Eingabe soll ein beliebiger `wert` gelesen werden, die Ausgabe soll den Absolutbetrag `absolut_wert` zurück geben.


*** =instructions
- Erstellen Sie eine Funktion `absolut()` mit Eingabeparameter `wert`.
- Die Funktion fragt über eine if-Abfrage ab, ob der Wert negativ ist oder nicht und wandelt ihn zu einer positiven Zahl um (dieser Teil kann vollständig aus den Folien übernommen werden).
- Sie gibt den berechneten `absolut_wert` zurück.
- Testen Sie ihre Funktion an mehreren Beispielen.

*** =hint
- Die Struktur einer Funktion: 
- `neue_funktion <- function(Eingabeparameter){...working ...return (Ausgabeparameter)}`

*** =pre_exercise_code
```{r}
wert1 <- -10
ergebnis1 <- 10
wert2 <- 5
ergebnis2 <- 5
```

*** =sample_code
```{r}
# Erstellung der Funktion
absolut <- function(wert){
    if(wert___){
        
    }else {
        
    }
    return(___)
}

# Testen Sie ihre Funktion für "wert1" (bereits eingelesen)
absolut(wert1)
# Testen Sie ihre Funktion für "wert2" (bereits eingelesen)
absolut(wert2)

```

*** =solution
```{r}
# Erstellung der Funktion
absolut <- function(wert){
    if(wert<0){
        absolut_wert <- -wert
    }else {
        absolut_wert <- wert
    }
    return(absolut_wert)
}
# Testen Sie ihre Funktion aus, in dem Sie z.B. absolut(-4) testen.
absolut(-4)
# Testen Sie ihre Funktion für "wert1"
absolut(wert1)
# Testen Sie ihre Funktion für "wert2"
absolut(wert2)

```

*** =sct
```{r}
test_output_contains("ergebnis1")
test_output_contains("ergebnis2")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:be80e0c720
## Funktionen (II)
In der 4. Aufgabe haben Sie die positive Differenz zweier Zahlen gebildet. Betten Sie diese Abfrage nun in eine Funktion ein.

Eine Funktion bekommt die Zahlen `a` und `b` als Eingabeparameter und soll nun die positive Differenz der beiden berechnen. 


*** =instructions
- Schreiben Sie die Funktion "pos_differenz()", welche die Eingabeparameter `a` und `b` bekommt.
- Testen Sie, welches der beiden größer ist und bilden Sie die positive Differenz.
- Speichern Sie diese als `c` ab.
- `c` ist der Rückgabewert der Funktion

*** =hint
- `neue_funktion <- function(Eingabeparameter){...working ...return (Ausgabeparameter)}`

*** =pre_exercise_code
```{r}
ergebnis1 = 8
ergebnis2 = 6
```

*** =sample_code
```{r}
# Schreiben Sie die Funktion
pos_differenz <- function(___){
    
    
    
    return(___)
}
# Testen Sie die Funktion an a=2, b=10
pos_differenz(2,10)
# Testen Sie die Funktion an a=10, b=4
pos_differenz(10,4)
```

*** =solution
```{r}
# Funktion
pos_differenz <- function(a,b){
    if(a <= b){
    c <- b-a} else{ 
    c <- a-b }
    return(c)
}
# Testen Sie die Funktion an a=2, b=10
pos_differenz(2,10)
# Testen Sie die Funktion an a=10, b=4
pos_differenz(10,4)
```

*** =sct
```{r}
test_output_contains("ergebnis1")
test_output_contains("ergebnis2")
test_error()
```


--- type:NormalExercise lang:r xp:100 skills:1 key:c45d01f88e
## Funktionen (III)
In den Folien haben Sie gesehen, wie eine Funktion für den gleitenden 5-er Durchschnitt aussieht. In dieser Aufgabe sollen Sie eine Funktion schreiben, die den gleitenden Durchschnitt für eine beliebige ungerade Fensterlänge berechnet und zurück gibt. 

Als Eingabe soll diese Funktion einen vektor `zahlenreihe` und einen Wert `x` erhalten. Es soll davon ausgegangen werden, dass x ein natürliche ungerade Zahl ist (muss nicht extra geprüft werden). 


*** =instructions
- Schreiben Sie eine Funktion `gleitender_durchschnitt`, die als Eingabe einen Vektor `zeitreihe` und einen ungeraden Wert `x` erwartet.
- Die Funktion soll den gleitenden x-er Durchschnitt berechnet. Sie können sich hier weitestgehend an der Funktion aus der Vorlesung orientieren.
- Sie gibt am Ende ein `ergebnis` zurück.
- Testen Sie ihre Funktion an dem gegebenen Vektor `reihe`.

*** =hint
- Die Struktur einer Funktion: 
- `neue_funktion <- function(Eingabeparameter){...working ...return (Ausgabeparameter)}`
- Berechnen Sie zuerst den Abstand nach links und rechts in der Zeitreihe und speichern Sie diesen in einer neuen Variable in der Funktion.
- Bedenken Sie, dass z.B. der gleitende 9-er Durchschnitt für die ersten und letzten 4 Zahlen nicht berechnet werden kann.

*** =pre_exercise_code
```{r}
reihe <- c(11, 12, 13, 16, 18, 20, 33, 66, 54, 67, 89, 102, 133, 150, 120, 110, 60, 78, 90, 101, 50, 37, 21, 2)
yqw <- c( 11, 12, 13, 17.57143,  25.42857,  31.42857 , 39.14286 , 49.57143,  61.57143 , 77.71429  ,94.42857 ,102.14286 ,110.14286 ,109.14286, 107.57143,  105.85714, 101.28571, 87.00000, 75.14286, 62.42857, 50.00000, 37.00000, 21.00000, 2.00000)

```

*** =sample_code
```{r}
# Funktion Berechnung gleitender Durchschnitt
gleitender_durchschnitt <- function(___){
    laenge <- ___
    ergebnis <- ___
    
    for(i in ___){
        if( i <= ___ | i >= ___){
            ergebnis[i] <- ___
        }else{
            ergebnis[i] <- ___
        }
    }
    return(___)
}
# Testen Sie ihre Funktion an der Zeitreihe "reihe" für x=7
gleitender_durchschnitt(reihe, 7)

```

*** =solution
```{r}
# Funktion Berechnung gleitender Durchschnitt
gleitender_durchschnitt <- function(zeitreihe, x){
    laenge <- length(zeitreihe)
    ergebnis <- c()
    # Berechnung des Abstandes nach links und rechts
    n <- (x-1)/2
    for(i in 1:laenge){
        # Darf nicht für die ersten n Zahlen berechnet werden
        if( i <= n | i >= (laenge-n)){
            ergebnis[i] <- zeitreihe[i]
        }else{
            ergebnis[i] <- mean( zeitreihe [(i - n) : (i + n)])
        }
    }
    return(ergebnis)
}
# Test an reihe mit x=7
gleitender_durchschnitt(reihe, 7)


```

*** =sct
```{r}
test_output_contains("yqw")
test_error()

```
