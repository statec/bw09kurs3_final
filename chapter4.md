---
title       : Termin 2 (inclass)
description : Tidyverse - Aufbereitung von Datensätzen

--- type:NormalExercise lang:r xp:50 skills:1 key:4e6279614f
## dplyr - SELECT
Der Datensatz der Deutschen Bank wurde bereits geladen und in dem Objekt `db` gespeichert. Alle benötigten Funktionen aus dem Paket `dplyr` sind in der gesamten Übung bereits eingebunden und verfügbar. 

Sie sollen nun durch zwei verschiedene Varianten auf eine bestimmte Spalte des Datensatzes zugreifen. Nutzen Sie dafür `select()`. Schauen Sie zur Funktionsweise der Funktion in den Folien nach, oder führen Sie `?select()` in der Konsole aus.


Tipp: 
Wenn Sie eine Zeile des R-Codes aus dem Skript in der Konsole ausführen möchten, nutzen Sie den Shortcut `Strg`+`Enter`, während sich der Cursor in der entsprechenden Zeile befindet. Testen Sie es! Geben Sie `db` im Skript (oben) ein und drücken Sie die beiden Tasten. Schauen Sie, was passiert.


(Quelle: yahoo/finance)
*** =instructions
Um auf die `Open` Spalte des Datensatzes zuzugreifen, haben Sie im letzten Termin schon eine Möglichkeit kennen gelernt. Nutzen Sie diese, um die `Open` Spalte des Datensatzes in `spalte1` zu speichern.
Nutzen Sie außerdem die Funktion `select()`, um das gleiche Ergebnis zu erzielen.



*** =hint
- nutzen Sie `daten$spalte`
- `select(daten, spaltenname)`

*** =pre_exercise_code
```{r}
library(dplyr)

db <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3722/datasets/db_aktie.csv")

```

*** =sample_code
```{r}
# shortcut Test

# schon bekannte Variante
spalte1 <-

# select Variante
spalte2 <-

```

*** =solution
```{r}
# shortcut Test
db

# schon bekannte Variante
spalte1 <- db$Open

# select Variante
spalte2 <- select(db, Open)

```

*** =sct
```{r}
test_object("spalte1")
test_object("spalte2")
test_function("select", args = c(".data"))
test_error()
success_msg("Sehr gut! Einen kleinen Unterschied gab es dann doch zwischen select() und $. Achten Sie bei der nächsten Aufgabe besonders darauf!")

```


--- type:NormalExercise lang:r xp:100 skills:1 key:8fb5e293ad
## dplyr - SELECT & FILTER
Der Datensatz liegt wieder in `db` für Sie bereit.
Den bereits bekannten Zugriff auf eine Spalte, welche eine bestimmte Bedingung erfüllt mit `daten$spalte[bedingung]` kennen Sie bereits. Experimentieren Sie ein wenig damit, um sich deren Funktion wieder ins Gedächnis zu rufen. 


Genauso funktionieren `select()` + `filter()`. Informationen zu den Funktionen finden Sie im Vorlesungsskript oder wie sonst auch mit `?function()` in der Konsole.


Denken Sie an den Shortcut `Strg` + `Enter` für angenehmeres Arbeiten. 


(Quelle: yahoo/finance)
*** =instructions
Wie hoch ist der Eröffnungskurs einer Deutschen Bank Aktie am 17.03.2017?
Nutzen Sie einmal die altbekannte Variante und einmal `select()` und `filter()`.

Denken Sie bei letzterem über die richtige Reihenfolge nach und speichern Sie ihr Ergebnis in den vorgegebenen Variablen.

*** =hint
- Wenden Sie zuerst `filter()` und dann `select()` an.
- Geben Sie das Datum in der Form "YYYY-MM-DD" an.


*** =pre_exercise_code
```{r}
library(dplyr)

db <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3722/datasets/db_aktie.csv")

```

*** =sample_code
```{r}
# Format des gesuchten Tages: "2017-03-17"
# mit $ und []
day1 <-

# mit select() und filter()
day2 <-

```

*** =solution
```{r}
# In den Lösungen werden Pipes benutzt. Pipes können gerne benutzt werden, sind aber nicht notwendig.

# mit $ und []
day1 <- db$Open[db$Date == "2017-03-17"]

# mit select() und filter() 
day2 <- db %>%
    filter(Date == "2017-03-17") %>% 
    select(Open)


```

*** =sct
```{r}
test_object("day1")
test_object("day2")
test_function("select")
test_function("filter")
test_error()
success_msg("Sehr schön! Ist Ihnen der Unterschied aufgefallen? filter() belässt das Erbegnis bei dem Typ data.frame, [ ] jedoch erstellt einen Vektor. Genau so bei select() und $.")

```

--- type:NormalExercise lang:r xp:300 skills:1 key:cafc5b7402
## dplyr - verschiedene Funktionen
In dieser Aufgabe geht es um die Anwendung verschiedener Funktionen aus dem `dplyr` Packet (bereits geladen). Die Daten der Deutschen Bank Aktie liegen im Objekt `db`. Alle benötigten Funktionen finden Sie in den Vorlesungsunterlagen.

Das Ziel dieser Aufgabe ist es, die Rendite als neue Variable des Datensatzes `db` zu erstellen.

Tipp: 

- x\_t und x\_tminus1 sind bereits Bestandteil des Datensatzes
- Durch `select()` können Sie auf bestimmte Spalten, durch `filter()` auf bestimmte Zeilen zugreifen. 
- Orientieren Sie sich an Beispielen in den Vorlesungsfolien.


(Quelle: yahoo/finance)

*** =instructions
- Verkleinern Sie den Datensatz mittels `select()`, sodass er nur noch Date, Open, x\_t und x\_tminus1 enthält.
- Sortieren Sie den Datensatz nach dem Datum.
- Benennen Sie die Spalte "Open" zu "Kurs" um.
- Erstellen Sie eine neue Variable "Rendite" in der die jeweilige Tagesrendite steht. (Diese muss aus dem Datensatz errechnet werden).

*** =hint
- ordnen: `arrange(daten, spalte)`.
- das erste bzw. letzte Datum in des sortierten Datensatzes bekommen Sie durch `head(db)` bzw. `tail(db)`.

*** =pre_exercise_code
```{r}
library(dplyr)

# Einlesen der Daten
db <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_3722/datasets/db_aktie.csv")
db$Date <- as.Date(db$Date)

# Erstellung der 2 Vektoren, die für Renditenberechnung notwendig sind
x_t <- db$Open[db$Date != "2016-04-06"]
x_tminus1 <- db$Open[db$Date != "2017-04-05"]

# Wir brauchen die Daten ohne die Erste Zeile (Keine Rendite berechenbar). Nutzen Sie filter().
db <- filter(db, Date != "2016-04-06")

# Fügen die zwei Hilfsvektoren zum Datensatz hinzu
db$x_t <- x_t
db$x_tminus1 <- x_tminus1

```

*** =sample_code
```{r}
# Verkleinerung des Datensatzes mit den Variablen Open, Date, x_t, x_tminus1
db <- 

# Sortieren aufsteigend nach Date (Tipp: arrange() )
db <-

# Umbenennung des Wertes (Tipp: rename() )
db <-

# Berechnen Sie die Rendite und erstellen Sie eine neue Variable "Rendite" im Datensatz. Dieser sollte nur noch die Spalten Date, Kurs und Rendite enthalten.
daten <- 


```

*** =solution
```{r}
# Verkleinerung des Datensatzes
db <- select(db, Date, Open, x_t, x_tminus1)

# Sortieren nach Date
db <- arrange(db, Date)

# Umbenennung des Wertes
db <- rename(db, Kurs = Open)

# Berechnen Sie die Rendite und erstellen Sie eine neue Variable "Rendite" im Datensatz.
daten <- db %>% mutate(Rendite = (x_t-x_tminus1)/x_tminus1) %>% select(Date, Kurs, Rendite)

head(daten)

```

*** =sct
```{r}
test_object("daten")
success_msg("Geschafft!")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:3923d161a1
## tidyr - SEPARATE 
Gegeben ist ein Datensatz `daten`. Wenn Sie ihn in der Konsole ausgeben, werden Sie merken, dass die zwei Variablen Kontinent und Land gemeinsam in eine Variable geschrieben wurden. Dies sollen Sie nun durch `separate()` ändern.
Das notwendige Paket aus tidyverse `(tidyr)` wurde für Sie bereits geladen.

(Quelle: Wikipedia)
 
*** =instructions
Erstellen Sie einen neuen Datensatz `tidyTable`, in welchem Sie die Spalte ort auf zwei Spalten "land" und "kontinent" aufteilen.

*** =hint
- `separate(df, into = c("spalte1", "spalte2"), sep = "_")`
- bei `sep = ` geben Sie das jeweilige Trennsymbol ein.

*** =pre_exercise_code
```{r}
library(tidyr)
library(dplyr)
# Erstellen der Daten
unternehmen <- c("BMW", "Sony", "AXA", "IBM", "Toyota", "Lenovo")
# Hauptsitz
ort <- c("Europa_Deutschland", "Asien_Japan", "Europa_Frankreich", "Amerika_USA", "Asien_Japan", "Asien_China")
stadt <- c("Muenchen", "Tokio", "Paris", "Armonk", "Toyota", "Peking")
daten <- data.frame(unternehmen, ort, stadt)


```

*** =sample_code
```{r}
# Schauen Sie sich die Ausgangsdaten in der Konsole an
print(daten)

# Erstellen Sie die neuen Spalten und speichern Sie ihr Ergebnis unter "tidyTable"
tidyTable<- 

# Schauen Sie sich das Ergebnis in der Konsole an
print(tidyTable)

```

*** =solution
```{r}
# auseinander ziehen
tidyTable <- daten %>% separate(ort, into = c("kontinent", "land"), sep = "_")
# Ausgabe
print(tidyTable)

```

*** =sct
```{r}
test_object("tidyTable")
test_error()
success_msg("Sehr gut, Sie können nun Spalten auseinander ziehen.")

```

--- type:NormalExercise lang:r xp:100 skills:1 key:b29966e91c
## tidyr - UNITE
Der von Ihnen soeben geänderte Datensatz ist in `daten` gegeben. Nun soll ihre Aktion mittels `unite()` wieder rückgängig gemacht werden.
Das notwendige Paket aus tidyverse `(tidyr)` wurde für Sie bereits geladen.

(Quelle: Wikipedia)
 
*** =instructions
Erstellen Sie einen neuen Datensatz "untidyTable", in welchem Sie die zwei Spalten "kontinent" und "land" (in dieser Reihenfolge) zu einer Spalte "ort" vereinen. Benutzen Sie als Trennsymbol das Leerzeichen.

*** =hint
- `unite(df, name, spalte1, spalte2, sep = " ")`
- bei `sep = ` geben Sie das jeweilige Trennsymbol ein.

*** =pre_exercise_code
```{r}
library(tidyr)
library(dplyr)
# Erstellen der Daten
unternehmen <- c("BMW", "Sony", "AXA", "IBM", "Toyota", "Lenovo")
# Hauptsitz
ort <- c("Europa_Deutschland", "Asien_Japan", "Europa_Frankreich", "Amerika_USA", "Asien_Japan", "Asien_China")
stadt <- c("Muenchen", "Tokio", "Paris", "Armonk", "Toyota", "Peking")
# Erstellen dataframe
daten <- data.frame(unternehmen, ort, stadt)
# auseinander ziehen
daten <- daten %>% separate(ort, into = c("kontinent", "land"), sep = "_")

```

*** =sample_code
```{r}
# Vereinigen Sie die beiden Spalten zu einer neuen Spalte "ort"
untidyTable <-

```

*** =solution
```{r}
# Vereinigen Sie die beiden Spalten zu einer neuen Spalte "ort"
untidyTable <- daten %>% unite(ort, kontinent, land, sep = " ")
# Ausgabe
print(untidyTable)

```

*** =sct
```{r}
test_object("untidyTable")
test_error()

```


--- type:NormalExercise lang:r xp:100 skills:1 key:eb9e1eebd4
## tidyr - GATHER
Die Daten liegen in `df`. Ein Datensatz in der Form wie er hier betrachtet wird, nennt man in R "data.frame". Bei dem gegebenen Datensatz sind die Spaltennamen keine Variablenbezeichnungen, sondern Werte einer Variablen. Nutzen Sie die in der Vorlesung vorgestellte Funktion, um den Datensatz zu ordnen. 


*** =instructions
- Räumen Sie den Datensatz auf (vgl. Vorlesungsunterlagen)
- Entfernen Sie unnötige Informationen durch die Funktionen, die Sie in den vorherigen Aufgaben bereits gelernt haben.
- Schauen Sie sich zur Überprüfung den Datensatz durch `print(dfTidy)` in der Konsole an.

*** =hint
- `gather(df, Wert1, Wert2, key = "___", value = "___" )`.
- Hilfe bei Funktionen bekommen Sie mit `?function()` in der Konsole.

*** =pre_exercise_code
```{r}
library(tidyr)
library(dplyr)
# Erstellen des Datensatzes
aktie <- c("Firma1", "Firma2", "Firma3")
mitarbeiter_2016 <- c(983, 1301, 457)
mitarbeiter_2017 <- c(1003, 1223, 461)
df <- data.frame(aktie, mitarbeiter_2016, mitarbeiter_2017)

```

*** =sample_code
```{r}
# Aufräumen des Datensatzes unter Benutzung von gather() 
dfTidy <-
# Benutzen Sie separate() um die betrefffende Spalte aufzuteilen in "uninteressant" und "jahr"
dfTidy <-
# Entfernen Sie die betrefffende Spalte durch select()
dfTidy <-

```

*** =solution
```{r}
# Hinweis: Die Lösung benutzt Pipes, es kann aber genauso in mehr Schritten ohne Pipes gemacht werden.
# Speichern Sie ihr Ergebnis in dfTidy
dfTidy <- df %>% 
    gather(mitarbeiter_2016, mitarbeiter_2017, key = "jahr", value = "mitarbeiter")

# Benutzen Sie separate() um die Spalte aufzuteilen in "uninteressant" und "jahr"
# Entfernen Sie die Spalte durch select()
dfTidy <- dfTidy %>% 
    separate(jahr, into = c("uninteressant", "jahr"), sep = "_") %>% 
    select(aktie, jahr, mitarbeiter)

```

*** =sct
```{r}
test_object("dfTidy")
test_function("gather")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:154576692b
## tidyr - SPREAD
Der Datensatz liegt im objekt `df`. Nutzen Sie die spread Funktion um die Zeilenanzahl zu reduzieren, sodass jedes Jahr seine eigene Spalte mit Renditen im Datensatz bekommt.


*** =instructions
- Nutzen Sie die Funktion `spread()` und speichern Sie das Ergebnis im Objekt `dfNew`.
- Vergleichen Sie den alten und neuen Datensatz durch Ausgabe in der Konsole mit `print(df)` bzw. `print(dfNew)`.

*** =hint
- `spread(df, spalte1, spalte2)`

*** =pre_exercise_code
```{r}
library(dplyr)
library(tidyr)
# Erstellung des Datensatzes
wertpapiere <- c("Aktie1", "Aktie2", "Aktie3", "Aktie1", "Aktie2", "Aktie3", "Aktie1", "Aktie2", "Aktie3")
jahr <- c("Rendite_2015", "Rendite_2015", "Rendite_2015", "Rendite_2016", "Rendite_2016", "Rendite_2016", "Rendite_2017", "Rendite_2017", "Rendite_2017")
rendite <- c(0.01, 0.03, 0.5, 0.2, 0.06, 0.31, 0.2, 0.08, 0.12)
df <-  data.frame(wertpapiere, jahr, rendite)

```

*** =sample_code
```{r}
# Reduzieren Sie die Zeilenanzahl und speichern Sie ihr Ergebnis in "dfNew".

# Schauen Sie sich beide Datensätze zum Vergleich in der Konsole an.

```

*** =solution
```{r}
# Reduzieren Sie die Zeilenanzahl und speichern Sie ihr Ergebnis in "dfNew".
dfNew <- df %>% spread(jahr, rendite)
# Schauen Sie sich beide Datensätze zum Vergleich in der Konsole an.
print(df)
print(dfNew)

```

*** =sct
```{r}
test_object("dfNew")
test_error()
success_msg("Sehr gut! kommen wir nun zu relationalen Datensätzen.")

```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:916e13138e
## Mehrere Datensätze: Keys
Schauen Sie sich die beiden Datensätze einer Firma an. Die Datensätze sind in `firma` und `abteilungen` gespeichert. Geben Sie `print(datensatz)` in der Konsole ein, um den Datensatz zu begutachten.

Welche Aussage ist korrekt, wenn wir `firma` als den eigenen Datensatz und `abteilungen` als Fremddatensatz betrachten?

*** =instructions
- Der "name" ist der primary key
- Der primary key ist die "mitarbeiter_id".
- Der foreign key des zweiten Datensatzes (abteilungen) ist "abteilung".

*** =hint

*** =pre_exercise_code
```{r}
# Erstellung des Datensatzes
mitarbeiter_id <- c(123, 134, 122, 167)
name <- c("Meier", "Kunze", "Schmitz", "Meier")
gehalt <- c(2580, 3600, 3450, 2900)
firma <- data.frame(mitarbeiter_id, name, gehalt)

abteilung <- c("marketing", "it", "finance", "it")
abteilungen <- data.frame(mitarbeiter_id, abteilung)

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:ea430943f2
## Mehrere Datensätze: Joins
Ihnen sind 3 Datensätze gegeben. `table1` und `table2` wurden mit einem bestimmten join Befehl vereinigt. Das Ergebnis können Sie in `mixed` sehen. Für die verschiedenen join Befehle, können Sie einen Blick in die Vorlesungsfolien werfen. 

Sollte Ihnen das Prinzip noch nicht ganz klar sein, probieren Sie selbst die verschiedenen join Befehle in der Konsole aus.

Welcher join Befehl wurde hier ausgeführt?


*** =instructions
- full_join
- right_join
- left_join
- inner_join

*** =hint
- führen Sie `print(datensatz)` in der Konsole aus, um die Datensätze anzuschauen.
- `____join(table1, table1, by = "___")`.

*** =pre_exercise_code
```{r}
library(dplyr)
# Erstellung der Daten
key <- c(1,2,3)
val <- c("x1", "y1", "z1")
table1 <- data.frame(key, val)

key <- c(1,3,4)
val <- c("x2", "y2", "z2")
table2 <- data.frame(key, val)

# Vereinigung der Datensätze
mixed <- inner_join(table1, table2, by = "key")

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig!"
test_mc(correct = 4, feedback_msgs = c(msg_bad, msg_bad, msg_bad, msg_success))

```

--- type:NormalExercise lang:r xp:100 skills:1 key:8d206b5035
##  Mehrere Datensätze: Full & inner join
Gegeben sind zwei Datensätze `table1` und `table2`. Diese Datensätze sollen nun von Ihnen auf zwei unterschiedliche Arten zu einem Datensatz vereinigt werden.


Tipp: Wenn bei einem join `NAs` entstehen, bekommen Sie in rot eine "warning message" in der Konsole. Diese können Sie aber einfach ignorieren. 
*** =instructions
- Nutzen Sie den `inner_join()` und speichern Sie ihr Ergebnis in "inner".
- Nutzen Sie den `full_join()` und speichern Sie ihr Ergebnis in "full".
- Vergleichen Sie die Ergebnisse indem Sie sich beide Datensätze in der Konsole ausgeben lassen.

*** =hint
- `inner_join(table1, table2, by = "___")`

*** =pre_exercise_code
```{r}
library(dplyr)
# Erstellung der Daten
aktie <- c("aktie1", "aktie2", "aktie3")
kurs_Open <- c(19.5, 20.2, 7.6)
table1 <- data.frame(aktie, kurs_Open)

aktie <- c("aktie2", "aktie3", "aktie4")
kurs_Close <- c(19.9, 7.7, 12.3)
table2 <- data.frame(aktie, kurs_Close)

```

*** =sample_code
```{r}
# inner_join()
inner <- 
# full_join()
full <-

```

*** =solution
```{r}
# inner_join()
inner <- inner_join(table1, table2, by = "aktie")
# full_join()
full <- full_join(table1, table2, by = "aktie")
# Ausgabe in der Konsole
inner
full

```

*** =sct
```{r}
test_object("full")
test_object("inner")
test_function("inner_join", args = c("x", "y", "by"))
test_function("full_join", args = c("x", "y", "by"))
test_error()
success_msg("Sehr schön! Wir kommen nun zur letzten Aufgabe!")

```


--- type:NormalExercise lang:r xp:100 skills:1 key:3ce8e31499
## Mehrere Datensätze: Right & left join
Gegeben sind zwei Datensätze `table1` und `table2`. Diese Datensätze sollen nun von Ihnen auf zwei unterschiedliche Arten zu einem Datensatz vereinigt werden.


Tipp: Wenn bei einem join `NAs` entstehen, bekommen Sie in rot eine "warning message" in der Konsole. Diese können Sie aber einfach ignorieren. 
*** =instructions
- Nutzen Sie den `right_join()` und speichern Sie ihr Ergebnis in "right".
- Nutzen Sie den `left_join()` und speichern Sie ihr Ergebnis in "left".
- Vergleichen Sie die Ergebnisse indem Sie sich beide Datensätze in der Konsole ausgeben lassen.

*** =hint
- Schauen Sie sich die Datensätze in der Konsole an, indem Sie `print(datensatz)` eingeben und auf Enter drücken.

*** =pre_exercise_code
```{r}
library(dplyr)
# Erstellung der Daten
aktie <- c("aktie1", "aktie2", "aktie3")
kurs_Open <- c(19.5, 20.2, 7.6)
table1 <- data.frame(aktie, kurs_Open)

aktie <- c("aktie2", "aktie3", "aktie4")
kurs_Close <- c(19.9, 7.7, 12.3)
table2 <- data.frame(aktie, kurs_Close)

```

*** =sample_code
```{r}
# right_join()
right <-
# left_join()
left <-

```

*** =solution
```{r}
# right_join()
right <- right_join(table1, table2, by = "aktie")
# left_join()
left <- left_join(table1, table2, by = "aktie")
# Ausgabe in der Konsole
right
left

```

*** =sct
```{r}
test_object("right")
test_object("left")
test_function("right_join", args = c("x", "y", "by"))
test_function("left_join", args = c("x", "y", "by"))
test_error()
success_msg("Glückwunsch! Sie haben es geschafft!")

```