---
title       : Termin 1 (inclass)
description : Übungen zu grundlegenden Funktionen mit R


--- type:NormalExercise lang:r xp:100 skills:1 key:641f650cf3
## Einlesen von Datensätzen in R

Ihnen wurde der Preisverlauf der Deutschen Bank Aktie eines Jahres als `CSV-Datei` unter der angegebenen URL zur Verfügung gestellt.

(Quelle: de.finance.yahoo.com)


*** =instructions

- Lesen Sie die Daten ein und speichern Sie diese im Objekt `deutschebank`.
- Schauen Sie sich die Daten in der Konsole an.

*** =hint
- Nutzen Sie die `read.csv()` Funktion.
- Setzen Sie den Pfad als Argument der Funktion `read.csv()` in "Anführungszeichen".

*** =pre_exercise_code
```{r}
```

*** =sample_code
```{r}

# die Datei liegt in https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv
deutschebank <-


```

*** =solution
```{r}
# der Pfad der Datei ist 
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")


```

*** =sct
```{r}
test_function("read.csv", args = c("file"))
test_object("deutschebank")
#test_output_contains("deutschebank")
test_error()
success_msg("Sehr gut!")

```


--- type:NormalExercise lang:r xp:100 skills:1 key:5db7fe4b29
## Missing Values (I)

Gegeben ist der Datensatz `aktien` (bereits eingelesen). Er besteht aus den Kursdaten der Deutschen Bank (gehandelt an einer inländischen Börse) und facebook (gehandelt an einer US Börse). 
Durch die unterschiedlichen Feiertage in Deutschland und den USA fehlen einige Werte im Datensatz. Diese Felder sind mit `NA` gekennzeichnet und sind Gegenstand der vorliegenden Aufgabe.

(Quelle der Daten: de.finance.yahoo.com)


*** =instructions
Ersetzen Sie die NA Felder in dem Datensatz durch:

- den Durchschnitt der gesamten Zeitreihe. Hierfür können Sie die `mean()`-Funktion nutzen.
- in den [ ]-Klammern hinter der Variable stehen die Auswahlbedingungen. Beispielsweise: `spalte[is.na(spalte)]` gibt nur die Felder aus `spalte` zurück, in denen NA steht.

Ergänzen Sie die fehlenden Werte direkt im Datensatz `aktien`.

*** =hint

- `na.rm = TRUE` entfernt die NA Felder, zur Berechnung des Durchschnitts.
- `is.na(daten)` findet die NAs in den daten.

*** =pre_exercise_code
```{r}
# Einlesen der Daten
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
facebook <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie2NA.csv")

# Zusammenführung der Daten
library(dplyr)

# Merging der Datensätze
aktienjoin <- full_join(facebook, deutschebank, by = "Date")

# Verkleinerung der Datensätze
aktien <- select(aktienjoin, Date, fb = Open.x, db = Open.y )
remove(aktienjoin)
remove(facebook)
remove(deutschebank)

# Nach Datum sortieren
aktien <- aktien[order(aktien$Date),]

# class Datum setzen
aktien$Date <- as.Date(aktien$Date)

```

*** =sample_code
```{r}
# Schaue, an welchen Tagen sich NAs befinden
aktien$Date[is.na(aktien$db)] # entspricht Zeile 7 und 145 im Datensatz
aktien$Date[is.na(aktien$fb)] # entspricht Zeile 197 und 222 im Datensatz

# Ersetzen Sie NAs in der Spalte 'db' durch den Durchschnitt der Spalte

mittelwert_db <- ___(___, na.rm = TRUE)

aktien$___[ 7 ] <- mittelwert_db
aktien$___[___] <- ___

# Ersetzen Sie NAs in der Spalte 'fb' durch den Durchschnitt der Spalte



```

*** =solution
```{r}
# Schaue, an welchen Tagen sich NAs befinden
aktien$Date[is.na(aktien$fb)]
aktien$Date[is.na(aktien$db)]

# Ersetzen Sie NAs in der Spalte 'db' durch den Durchschnitt der Spalte
aktien$db[is.na(aktien$db)] <- mean(aktien$db, na.rm = TRUE)

# Ersetzen Sie NAs in der Spalte 'fb' durch den Durchschnitt der Spalte
aktien$fb[is.na(aktien$fb)] <- mean(aktien$fb, na.rm = TRUE)


```

*** =sct
```{r}

test_function("mean", index = 1, args = c("x", "na.rm"))
test_function("mean", index = 2, args = c("x", "na.rm"))

test_object("aktien")
test_error()
success_msg("Sehr gut!")
```

--- type:NormalExercise lang:r xp:300 skills:1 key:df9a88a1a0
## Missing Values (II)

Gegeben ist wieder der Datensatz `aktien` (bereits eingelesen). Ersetzen Sie nun die NAs im Datensatz durch den gleitenden Durchschnitt über 10 Tage. Nehmen Sie hierfür den Durchschnitt von den 5 vorherigen und 5 folgenden Werten. 

Nützliche R Funktionen:

- `c(1,2,3,4,9)` bildet einen Vektor mit dem Inhalt 1,2,3,4,9.
- `c(1:4,9)` bildet den gleichen Vektor.
- `which(9 == c(1:4,9) )` gibt an, an welcher Stelle der Vektor dem Wert 9 entspricht (also = 5).

*** =instructions

Ersetzen Sie die NAs in beiden Spalten db und fb durch den gleitenden 10er-Durchschnitt der jeweiligen Spalte.

Die NA-Stellen finden Sie über: 
`aktien$Date[is.na(aktien$db)]`

Für Facebook analog.

*** =hint



*** =pre_exercise_code
```{r}
# Einlesen der Daten
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
facebook <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie2NA.csv")

# Zusammenführung der Daten
library(dplyr)

# Merging der Datensätze
aktienjoin <- full_join(facebook, deutschebank, by = "Date")

# Verkleinerung der Datensätze
aktien <- select(aktienjoin, Date, fb = Open.x, db = Open.y )
remove(aktienjoin)
remove(facebook)
remove(deutschebank)

# class Datum setzen
aktien$Date <- as.Date(aktien$Date)

# Nach Datum sortieren
aktien <- aktien[order(aktien$Date),]

```

*** =sample_code
```{r}

### deutschebank  (db)
# Finde die Zeile mit dem ersten Feiertag "2016-04-14" und speichere die Zeilennummer in index1
index1 <- which(___ == "___")
# durch Durchschnitt ersetzen
aktien$db[___] <- ___( aktien$db[c((index1-___):(index1-___),(index1+___):(index1+___))] )
# Überprüfe neuen Wert
aktien$db[___]




### facebook (fb)
# Finde die Zeile mit dem ersten Feiertag "2017-01-16" und speichere die Zeilennummer in index2

# durch Durchschnitt ersetzen

# Überprüfe neuen Wert





```

*** =solution
```{r}
# Deutschebank
# Finde den Index 1
index1 <- which(aktien$Date == "2016-04-14")
# durch Durchschnitt ersetzen
aktien$db[index1] <- mean(c(aktien$db[c((index1-5):(index1-1),(index1+1):(index1+5))]))
# Neuer Wert
aktien$db[index1]


# Facebook 
# Finde den Index 3
index2 <- which(aktien$Date == "2017-01-16")
# durch Durchschnitt ersetzen
aktien$fb[index2] <- mean(c(aktien$fb[c((index2-5):(index2-1),(index2+1):(index2+5))]))
# Neuer Wert
aktien$fb[index2]



```

*** =sct
```{r}
test_function("which", args = "x", index = 1)
test_function("which", args = "x", index = 2)
test_object("index1")
test_object("index2")
test_function("mean", index = 1, args = c("x"))
test_function("mean", index = 2, args = c("x"))
test_output_contains("aktien$db[index1]")
test_output_contains("aktien$fb[index2]")

test_error()
success_msg("Sehr gut!")
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:09dde5f88b
## Missing Values (III)

Ihre Ergebnisse aus der letzten Aufgabe wurden geplotted. Sie sehen rechts den Plot für die facebook Aktie. Beim ersten Plot wurden die fehlenden Werte durch den gesamten Durchschnitt ersetzt, beim zweiten Plot wurden die fehlenden Werte durch den gleitenden 10er-Durchschnitt ersetzt.

Schauen Sie sich beide Plots an und vergleichen Sie die ersetzten Stellen (Feiertage am 16.01.17 und 20.02.17). 

Welche Methode eignet sich besser zur Ersetzung?
*** =instructions


- Gleitender 10er-Durchschnitt
- Durchschnitt gesamte Spalte

*** =hint


*** =pre_exercise_code
```{r}
# Einlesen der Daten
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
facebook <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie2NA.csv")

# Zusammenführung der Daten
library(dplyr)

# Merging der Datensätze
aktienjoin <- full_join(facebook, deutschebank, by = "Date")

# Verkleinerung der Datensätze
aktien <- select(aktienjoin, Date, fb = Open.x, db = Open.y )

# class Datum setzen
aktien$Date <- as.Date(aktien$Date)

# Nach Datum sortieren
aktien <- aktien[order(aktien$Date),]
aktien2 <- aktien

# Gesamten durchschnitt setzen
aktien2$fb[is.na(aktien2$fb)] <- mean(aktien2$fb, na.rm = TRUE)

# Gleitender Durchschnitt setzen
index3 <- which(aktien$Date == "2017-01-16")
aktien$fb[index3] <- mean(c(aktien$fb[c((index3-5):(index3-1),(index3+1):(index3+5))]))
index4 <- which(aktien$Date == "2017-02-20")
aktien$fb[index4] <- mean(c(aktien$fb[c((index4-5):(index4-1),(index4+1):(index4+5))]))

# Plot von facebook Aktien mit NA durch gleitenden 10er Durchschnitt ersetzt
plot(aktien$Date, aktien$fb, type = "l", main = "Facebook Aktie 2016-2017 mit gleitendem 10er-Durchschnitt", xlab = "Datum", ylab = "Eroeffnungspreis ($)")
# Plot von facebook Aktien mit NA durch gesamten Durchschnitt ersetzt
plot(aktien2$Date, aktien2$fb, type = "l", main = "Facebook Aktie 2016-2017 mit gesamt Durchschnitt", xlab = "Datum", ylab = "Eröffnungspreis ($)")

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig!"
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad))

```

--- type:NormalExercise lang:r xp:100 skills:1 key:860b4a4e28
## Berechnungen in R: Rendite (I)

Gegeben ist wieder der Datensatz `aktien` (bereits eingelesen). Nun sollen die diskreten Renditen für jeden Tag der Zeitreihe berechnet werden. 

Vektoren können in R einfach elementweise voneinander subtrahiert werden, solange sie die gleiche Dimension haben. 

Tipp: Durch `vektor[5:length(vektor)]` entsteht ein Vektor, der alle Elemente von `vektor` ab dem 5. Element enthält.

Die Formel zur Berechnung der Rendite finden Sie im Skript.


*** =instructions

Berechnen Sie die Rendite für die Deutsche Bank für jeden Tag des gegebenen Datensatzes. `aktien$db` gibt Ihnen den Vektor mit den benötigten Daten.

*** =hint

- Achten Sie darauf, dass die beiden Vektoren die gleiche Länge haben müssen.
- Die Länge eines Vektors bekommen Sie durch `length(vektor)` und ergibt 254.

*** =pre_exercise_code
```{r}
# Einlesen der Daten
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
facebook <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie2NA.csv")

# Zusammenführung der Daten
library(dplyr)
# Merging der Datensätze
aktienjoin <- full_join(facebook, deutschebank, by = "Date")

# Verkleinerung der Datensätze
aktien <- select(aktienjoin, Date, fb = Open.x, db = Open.y )
remove(aktienjoin)

# class Datum setzen
aktien$Date <- as.Date(aktien$Date)

# Nach Datum sortieren
aktien <- aktien[order(aktien$Date),]

# Nehme Gletenden Durchschnitt um NAs zu füllen
index1 <- which(aktien$Date == "2016-04-14")
aktien$db[index1] <- mean(c(aktien$db[c((index1-5):(index1-1),(index1+1):(index1+5))]))
index2 <- which(aktien$Date == "2016-10-31")
aktien$db[index2] <- mean(c(aktien$db[c((index2-5):(index2-1),(index2+1):(index2+5))]))

```

*** =sample_code
```{r}
# Bedenken Sie, dass sich für den ersten Tag keine Rendite berechnen lässt.

# Erstelle einen Vektor mit den Einträgen aus aktien$db, OHNE den letzten Wert
x_tminus1 <- 
# Lasse ersten Eintrag weg, da Rendite erst ab 2. Tag berechenbar
x_t <- 
# Berechnung der Rendite
renditeDB <- 


```

*** =solution
```{r}
# Erstelle einen vektor mit den Einträgen aus aktien$db. Lasse den letzten Eintrag weg.
x_tminus1 <- aktien$db[1:(length(aktien$db)-1)]

# Lasse ersten Eintrag weg, da Rendite erst ab 2. Tag berechenbar
x_t <- aktien$db[2:length(aktien$db)]

# Berechnung der Rendite
renditeDB <- (x_t - x_tminus1) / x_tminus1



```

*** =sct
```{r}
test_object("x_tminus1")
test_object("x_t")
test_object("renditeDB")
test_error()
success_msg("Sehr gut!")

```

--- type:NormalExercise lang:r xp:100 skills:1 key:ce73d9c96b
## Berechnungen in R: Rendite (II)

Der Datensatz liegt in `aktien`. Nun sollen die stetigen (logarithmischen) Renditen für jeden Tag berechnet werden.

Tipps:

Vektoren können in R einfach elementweise voneinander subtrahiert werden, solange sie die gleiche Dimension haben. Durch `vektor[5:length(vektor)]` entsteht ein Vektor, der alle Elemente von `vektor` ab dem 5. Element enthält.

Den natürlichen Logarithmus können Sie in R einfach mit `log(x)` bestimmen. Hierbei kann `x` auch ein Vektor sein, der Logarithmus wird in dem Fall elementeweise ausgeführt.

Die Formel zur Berechnung der log-Rendite finden Sie im Skript.


*** =instructions

Berechnen Sie die log-Rendite für die Deutsche Bank für jeden Tag des gegebenen Datensatzes. `aktien$db` gibt Ihnen den Vektor mit den benötigten Daten.


*** =hint

- Achten Sie darauf, dass die beiden Vektoren die gleiche Länge haben müssen.
- Die Länge eines Vektors bekommen Sie durch `length(vektor)` und ergibt 254.


*** =pre_exercise_code
```{r}
# Einlesen der Daten
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
facebook <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie2NA.csv")

# Zusammenführung der Daten
library(dplyr)
# Merging der Datensätze
aktienjoin <- full_join(facebook, deutschebank, by = "Date")

# Verkleinerung der Datensätze
aktien <- select(aktienjoin, Date, fb = Open.x, db = Open.y )
remove(aktienjoin)

# class Datum setzen
aktien$Date <- as.Date(aktien$Date)

# Nach Datum sortieren
aktien <- aktien[order(aktien$Date),]

# Nehme Gletenden Durchschnitt um NAs zu füllen
index1 <- which(aktien$Date == "2016-04-14")
aktien$db[index1] <- mean(c(aktien$db[c((index1-5):(index1-1),(index1+1):(index1+5))]))
index2 <- which(aktien$Date == "2016-10-31")
aktien$db[index2] <- mean(c(aktien$db[c((index2-5):(index2-1),(index2+1):(index2+5))]))


```

*** =sample_code
```{r}
# Erstellung Vektor mit Einträgen aus aktien$db. Entferne den letzten Eintrag.
x_tminus1 <- 
# Lasse ersten Eintrag weg, da Rendite erst ab 2. Tag berechenbar
x_t <- 
# Berechnung der Rendite
logRenditeDB <- 


```

*** =solution
```{r}
# Erstellung Vektor mit Einträgen aus aktien$db. Entferne den letzten Eintrag.
x_tminus1 <- aktien$db[1:(length(aktien$db)-1)]
# Lasse ersten Eintrag weg, da Rendite erst ab 2. Tag berechenbar
x_t <- aktien$db[2:length(aktien$db)]
# Berechnung der Rendite
logRenditeDB <- log(x_t) - log(x_tminus1)


```

*** =sct
```{r}
test_object("x_tminus1")
test_object("x_t")
test_object("logRenditeDB")

test_error()
success_msg("Sehr gut!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:5efd106c9f
## Grafische Darstellung

In R gibt es viele Möglichkeiten, Daten grafisch darzustellen. In früheren Aufgaben haben Sie bereits einige Plots gesehen. Solche Plots sollen in dieser Aufgabe nun von Ihnen erstellt werden.

Verwenden Sie `plot(x,y, ...)` um die Zeitreihe der Facebook-Aktie zu plotten. Verwenden Sie den Eröffnungspreis (Open) im Datensatz `aktien`. 
Hilfe zum `plot` Befehl und den Eingabemöglichkeiten finden Sie, indem Sie `?plot()` in der Konsole eingeben. 

*** =instructions

Der Plot sollte folgende Anforderungen erfüllen:

- Die Datenpunkte sollten durch Linien miteinander verbunden sein.
- Der Plot sollte einen sinnvollen Titel erhalten.
- Die x-Achse und y-Achse sollten mit "Datum" und "Eroeffnungspreis ($)" beschriftet werden.


*** =hint

Im Plot Befehl müssen Sie type, main, xlab und ylab füllen. Das tuen Sie durch plot(x,y,type = "l", main = ...)

*** =pre_exercise_code
```{r}
# Plotten der Zeitreihe aus 1
# Einlesen der Daten (Daten sind bereits eingelesen)
aktien <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie.csv")

# Datum als class Date initialisieren
aktien$Date <- as.Date(aktien$Date)

# sortieren Datensatz nach Datum
aktien <- aktien[order(aktien$Date),]

```

*** =sample_code
```{r}
plot( __ , __ , type = __ , main = __ , xlab = "Datum", ylab = __ )

```

*** =solution
```{r}
# Plot erstellen 
plot(aktien$Date, aktien$Open, type = "l", main = "Facebook Aktie 2016-2017", xlab = "Datum", ylab = "Eroeffnungspreis ($)")

```

*** =sct
```{r}
test_function("plot", args = c("x", "y", "type", "xlab", "ylab") )
test_error()
success_msg("Sehr gut!")

```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:de382d695d
##  Analyse der Daten

Im Datensatz `aktien` haben wir den Eröffnungspreis und die jeweilige Tagesrendite der Facebook Aktie von einem Jahr. Wir betrachten nun die Volatilität der Zeitreihe. Bei dem Plot der Eröffnungspreise (Plot 1) kann man nur grob schätzen wo die Volatilität am stärksten ist. Im Plot 2 sehen Sie die Rendite der Zeitreihe geplottet. Hier kann man das Ergebnis schon etwas besser heraus lesen.

Wo ist die Volatilität am höchsten? 

Sollte die Lösung nicht eindeutig sein, können Sie auch die Ergebnisse des `var()` Befehls für die angegebenen Zeiträume vergleichen.


*** =instructions

- Anfang November
- Ende April
- Anfang Januar
- Mitte August



*** =hint

*** =pre_exercise_code
```{r}
library(dplyr)
# Einlesen der Daten 
aktien <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie.csv")

# Datum als class Date initialisieren
aktien$Date <- as.Date(aktien$Date)

# sortieren Datensatz nach Datum
aktien <- aktien[order(aktien$Date),]

# Verkleinerung der Datensätze
aktien <- select(aktien, Date, Open)
plot(aktien$Date, aktien$Open, type = "l", main = "Facebook Aktie 2016-2017", xlab = "Datum", ylab = "Eröffnungspreis ($)")

# Funktion zur Berechnung der Rendite
rendite <- function(zeitreihe){ 
  r <- zeitreihe[1:(length(zeitreihe)-1)];  
  ren <- zeitreihe[2:length(zeitreihe)];
  ren <- (ren - r) / r;
  return(ren)     
}

# Rendite für Eröffnungspreise berechnen
fbRendite <- rendite(aktien$Open) 

# Rendite zum Datensatz hizufügen, vorne 0
fbRen <- c(0,fbRendite)
aktien[ , "Rendite"] <- fbRen

plot(aktien$Date, aktien$Rendite, type = "l", main = "Facebook Aktie 2016-2017", xlab = "Datum", ylab = "Rendite")

```

*** =sct
```{r}
msg_bad <- "Falsch!"
msg_success <- "Richtig!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))

```

--- type:NormalExercise lang:r xp:100 skills:1 key:5e209754d2
## Histogramm
Der Datensatz `aktien` mit den berechneten Renditen für die Deutsche Bank Aktie ist bereits eingelesen. Erstellen Sie ein Histogramm über die Verteilung der Renditen. 

Nutzen Sie die Funktion zum Erstellen eines Histogramms ist `hist(x,...)`.


*** =instructions
Nutzen Sie `?hist()` um mehr über die Anwendung der Funktion zu erfahren.
Das Histogramm sollte enthalten: 

- `breaks` um die Dicke der Balken anzupassen.
- eine Überschrift "Verteilung der Renditen".
- `xlab` und `ylab` zur Beschriftung der Achsen, mit "Renditen" und "Haeufigkeit".


*** =hint

- Auf die x-Werte können Sie über `aktien$Rendite` zugreifen
- Denken Sie daran, die Beschriftungen in Anführungszeichen zu setzen.


*** =pre_exercise_code
```{r}
# Einlesen der Daten
aktien <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie.csv")

# Datum als class Date initialisieren
aktien$Date <- as.Date(aktien$Date)

# sortieren Datensatz nach Datum
aktien <- aktien[order(aktien$Date),]

# Funktion zur Berechnung der Rendite
rendite <- function(zeitreihe){ 
  r <- zeitreihe[1:(length(zeitreihe)-1)];  
  ren <- zeitreihe[2:length(zeitreihe)];
  ren <- (ren - r) / r;
  return(ren)     
}

# Rendite von DB Aktien
rDbAktien <- rendite(aktien$Open)

# Rendite zum Datensatz hinzufügen
rDbAktien <- c(0,rDbAktien)
aktien[ , "Rendite"] <- rDbAktien

```

*** =sample_code
```{r}
# Erstellen Sie ein Histogramm und setzen Sie breaks = 20.

# Erstellen Sie das Histogramm mit breaks = 40.

```

*** =solution
```{r}
# Erstellen Sie ein Histogramm und setzen Sie breaks = 20.
hist(aktien$Rendite, breaks = 20, main = "Verteilung der Renditen", xlab = "Renditen", ylab = "Haeufigkeit")

# Erstellen Sie das Histogramm mit breaks = 40.
hist(aktien$Rendite, breaks = 40, main = "Verteilung der Renditen", xlab = "Renditen", ylab = "Haeufigkeit")

```

*** =sct
```{r}
test_function("hist", args = c("x", "breaks", "main", "xlab", "ylab"), index = 1) 
test_function("hist", args = c("x", "breaks", "main", "xlab", "ylab"), index = 2) 
test_error()
success_msg("Gratulation! Sie haben die letzte Aufgabe gemeistert.")
```
