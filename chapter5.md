---
title       : Einheit 2 (homework)
description : Tidyverse - Aufbereitung von Datensätzen

--- type:NormalExercise lang:r xp:100 skills:1 key:567d7068ae
## 1. Basis Funktionen dplyr
Gegeben ist ein Datensatz `kurse`. Schauen Sie sich den Datensatz in der Konsole an. Der Datensatz ist nicht mehr aktuell und soll nun von Ihnen aktualisiert werden. Das benötigte Paket "dplyr" ist bereits für Sie eingebunden.

Tipp: 

Das Datum ist als Typ "Date" gespeichert und kann durch ganz normale Vergleichsoperatoren verglichen werden. 

Bsp: `Datum < "2017-05-01"`.


*** =instructions
Verkleinern und aktualisieren Sie den Datensatz nach folgenden Vorgaben und mit den in Termin 2 diskutierten Funktionen:

- Erstellen Sie einen Datensatz `aktuell` mit allen Klausurterminen, die vor "2017-05-01" stattgefunden haben. 
- Ordnen Sie den Datensatz nach den Klausurterminen, welche noch im Datensatz vorhanden sind.


*** =hint
- `filter()` wählt bestimmte Zeilen nach angegebenen Bedingung aus. 
- `select()` wählt bestimmte Spalten aus.
- `arrange()` sortiert den Datensatz.

*** =pre_exercise_code
```{r}
library(dplyr)
# Erstellen des Datensatzes
kurse <- data.frame(kurs = c("BWL", "VWL", "Statistik", "Geldpolitik", "Personalmanagement"), klausurtermin_2016 = c("2016-04-18", "2016-05-14", "2016-05-08",  "2016-05-30", "2016-05-21"), klausurtermin_2017 = c("2017-05-03", "2017-04-28", "2017-05-04",  "2017-05-30", "2017-05-23"), kursnummer = c(201, 101, 302, 111, 206))
# Für arrange()
kurse$klausurtermin_2017 <- as.Date(kurse$klausurtermin_2017)
kurse$klausurtermin_2016 <- as.Date(kurse$klausurtermin_2016)
```

*** =sample_code
```{r}
# Entferne alle Spalten und Zeilen mit Klausurterminen die vor dem 01.05.17 stattgefunden haben. 
aktuell <-
# Sortieren Sie den neuen Datensatz nach den aktuellen Klausurterminen.

```

*** =solution
```{r}
# Entferne alle Spalten und Zeilen mit Klausurterminen die vor dem 01.05.17 stattgefunden haben. 
# Sortieren Sie den neuen Datensatz nach den aktuellen Klausurterminen.

aktuell <- filter(kurse, klausurtermin_2017 < "2017-05-01") %>% 
    select(kurs, klausurtermin_2017, kursnummer) %>% 
    arrange(klausurtermin_2017)

```

*** =sct
```{r}
test_function("select")
test_function("filter")
test_function("arrange")
test_object("aktuell")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:7a690271fe
## 2. Basis Funktionen dplyr
Der Datensatz liegt in `evaluation`. Es wurden verschiedene Studiengänge evaluiert. Nun soll von Ihnen der Durchschnitt errechnet werden.
Das Paket "dplyr" wurde bereits eingebunden.


*** =instructions
Erstellen Sie mit `mutate()` eine neue Spalte, in welcher die Durchschnittsnote des jeweiligen Studienganges steht. 

*** =hint
Da Sie hier Zeilenweise und nicht Spaltenweise den Schnitt berechnen, können Sie nicht `mean()` benutzen, da diese Funktion einen Vektor als Eingabe erwartet.

*** =pre_exercise_code
```{r}
library(dplyr)
# Erstellung der Daten
studiengang <- c("lehramt", "mathe", "physik", "medizin", "wirtschaft", "jura", "chemie")
note_1 <- c(32, 40, 25, 33, 144, 54, 22)
note_2 <- c(201, 89, 67, 166, 244, 98, 167)
note_3 <- c(102, 23, 89, 31, 129, 77, 33)
note_4 <- c(12, 3, 33, 12, 29, 54, 19)
evaluation <- data.frame(studiengang, note_1, note_2, note_3, note_4)

```

*** =sample_code
```{r}
# Erstellen Sie den neuen Datensatz mit der neuen Spalte "durchschnitt"
evaluation1 <- 

```

*** =solution
```{r}
# Lösung
evaluation1 <- evaluation %>%
    mutate(durchschnitt = (note_1 + 2*note_2 + 3*note_3 + 4*note_4)/(note_1 + note_2 + note_3 + note_4)) %>%
    arrange(durchschnitt)

```

*** =sct
```{r}
test_function("mutate")
test_function("arrange")
test_object("evaluation1")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:c95c4d616c
## 3. Pipes
Gegeben ist der ihnen schon bekannte Datensatz `evaluation`. Das Paket "dplyr" wurde eingelesen.

*** =instructions
- Verkleinern Sie den Datensatz, sodass nur noch die der Studiengang und die Durchschnittsnote ethalten sind. 
- Nennen Sie die Spalte "durchschnitt" zu "Bewertung" um.
- Bei dieser Aufgabe sollen Sie pipes `%>%` benutzen. Zur Funktionsweise schauen Sie bitte in die Folien.

*** =hint
- um bestimmte Spalten auszuwählen können Sie `select(df, Spalte)` nutzen.
- Zum Umbenennen können Sie `rename(df, Name = alter_Name)` nutzen.


*** =pre_exercise_code
```{r}
library(dplyr)
# Erstellung der Daten
studiengang <- c("lehramt", "mathe", "physik", "medizin", "wirtschaft", "jura", "chemie")
note_1 <- c(32, 40, 25, 33, 144, 54, 22)
note_2 <- c(201, 89, 67, 166, 244, 98, 167)
note_3 <- c(102, 23, 89, 31, 129, 77, 33)
note_4 <- c(12, 3, 33, 12, 29, 54, 19)
evaluation <- data.frame(studiengang, note_1, note_2, note_3, note_4)
evaluation <- evaluation %>%
    mutate(durchschnitt = (note_1 + 2*note_2 + 3*note_3 + 4*note_4)/(note_1 + note_2 + note_3 + note_4)) %>%
    arrange(durchschnitt)

```

*** =sample_code
```{r}
# nutzen Sie zuerst select() und dann rename()
evaluation1 <- evaluation %>%  

```

*** =solution
```{r}
evaluation1 <- evaluation %>% 
    select(studiengang, durchschnitt) %>% 
    rename(Bewertung = durchschnitt)

```

*** =sct
```{r}
test_object("evaluation1")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:545c855428
## 4. tidyr 
Gegeben ist ein Datensatz `firma`. Sie sehen im Datensatz, dass die Spalte Mitarbeiter_Abteilung aus zwei verschiedenen Variablen besteht. Dies soll nun geändert werden.

Das notwendige Paket aus tidyverse "tidyr" wurde für Sie bereits geladen, ebenso wie "dplyr".

 
*** =instructions
- Erstellen Sie für jede der zwei Variablen eine eigene Spalte. 
- Fügen Sie eine Spalte zum Datensatz hinzu, der das Alter der Mitarbeiter anzeigt. 


*** =hint
- `separate(df, into = c("spalte1", "spalte2"), sep = "_")`
- bei `sep = ` geben Sie das jeweilige Trennsymbol ein.
- `mutate()` erstellt eine neue Variable im Datensatz.
- `unite(df, name, spalte1, spalte2, sep = " ")`

*** =pre_exercise_code
```{r}
library(tidyr)
library(dplyr)
# Erstellen der Daten
Mitarbeiter_id <- c(3462, 9305, 3894, 4539, 3205, 4995, 3202, 1847, 5566)
Vorname <- c("Luisa", "Christina", "Heinrich", "Xenia", "Kim", "Franco", "Simon", "Larissa", "Joseph")
Mitarbeiter_Abteilung <- c("Kamm_IT", "Donner_IT", "Lohrer_EDV", "Warm_IT", "Bose_IT", "Gustavo_HR", "Mueller_EDV", "Schnabel_EDV", "Hust_HR") 
Geburtsjahr <- c(1986, 1990, 1974, 1977, 1964, 1981, 1960, 1959, 1974)
Geschlecht <- c("W", "W", "M", "W", "M",  "M",  "M", "W", "M")
firma <- data.frame(Mitarbeiter_id, Vorname, Mitarbeiter_Abteilung, Geschlecht, Geburtsjahr)


```

*** =sample_code
```{r}
# Erstellen Sie die neuen Spalten und errechnen Sie das Alter der Personen ausgehend vom Jahr 2017 (Tage/Monate sind hierbei zu vernachlässigen)
firma <- 

```

*** =solution
```{r}
# auseinander ziehen
firma <- firma %>% 
    separate(Mitarbeiter_Abteilung, into = c("Mitarbeiter", "Abteilung"), sep = "_") %>%
    mutate(Alter = 2017 - Geburtsjahr)

```

*** =sct
```{r}
test_object("firma")
test_error()

```

--- type:NormalExercise lang:r xp:100 skills:1 key:b24f8a3cc7
## 5. tidyr - gather( )
Ihnen liegt der schon bekannte Datensatz `evaluation` vor. Die Pakete "tidyr" und "dplyr" sind bereits geladen. 

Der Datensatz soll so verändert werden, dass man möglichst schnell sehen kann, welche Note am seltensten und welche am häufigsten vergeben wurde.

*** =instructions
- Verändern Sie den Datensatz so, dass statt der 4 Spalten für die Noten nur noch 2 Spalten nötig sind.
- in der einen Spalte sollte der Notenwert stehen (Bsp. note_2) und in der anderen die Anzahl an Stimmen für diese Note.
- sortieren Sie den Datensatz mit `arrange()`

*** =hint
- `gather(df, spalte1, spalte2, spalte3, ..., key = "___", value = "___")`
- Aus welchem Paket ist `arrange()`?

*** =pre_exercise_code
```{r}
library(tidyr)
# Paket für arrange einbinden
library(dplyr)
studiengang <- c("lehramt", "mathe", "physik", "medizin", "wirtschaft", "jura", "chemie")
note_1 <- c(32, 40, 25, 33, 144, 54, 22)
note_2 <- c(201, 89, 67, 166, 244, 98, 167)
note_3 <- c(102, 23, 89, 31, 129, 77, 33)
note_4 <- c(12, 3, 33, 12, 29, 54, 19)
evaluation <- data.frame(studiengang, note_1, note_2, note_3, note_4)

```

*** =sample_code
```{r}
# Nutzen Sie gather um 2 Spalten zu erhalten. Schreiben Sie ihr Ergebnis in ev.
ev <- 

# Sortieren Sie ev nach der Anzahl (kleinste Anzahl oben)


```

*** =solution
```{r}
# Umsortieren
ev <- gather(evaluation, note_1, note_2, note_3, note_4, key = "Note", value = "Anzahl")
# nach Anzahl sortieren
ev <- arrange(ev, Anzahl)
```

*** =sct
```{r}
test_object("ev")
test_function("gather")
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:cf9655bc74
## 6. tidyr - spread( )
Ihr Ergebnis von der vorherigen Aufgabe liegt nun in `evaluation`. Der Anfangsdatensatz wurde unglücklicherweise überschrieben. 


dplyr wurde bereits geladen.


*** =instructions
-  Machen Sie die Aktion rückgängig, indem Sie `spread()` benutzen.

*** =hint
- `spread(df, Spalte1, Spalte2)`

*** =pre_exercise_code
```{r}
library(tidyr)
library(dplyr)
studiengang <- c("lehramt", "mathe", "physik", "medizin", "wirtschaft", "jura", "chemie")
note_1 <- c(32, 40, 25, 33, 144, 54, 22)
note_2 <- c(201, 89, 67, 166, 244, 98, 167)
note_3 <- c(102, 23, 89, 31, 129, 77, 33)
note_4 <- c(12, 3, 33, 12, 29, 54, 19)
evaluation <- data.frame(studiengang, note_1, note_2, note_3, note_4)
# Umsortieren
evaluation <- gather(evaluation, note_1, note_2, note_3, note_4, key = "Note", value = "Anzahl")
evaluation <- arrange(evaluation, Anzahl)

```

*** =sample_code
```{r}
# Nutzen Sie spread um jeder Note wieder ihre eigene Spalte zu geben.
ev <- 

```

*** =solution
```{r}
ev <- spread(evaluation, Note, Anzahl)
```

*** =sct
```{r}
test_function("spread")
test_object("ev")
test_error()

```



--- type:NormalExercise lang:r xp:100 skills:1 key:60a2a30685
## 7. joins
Ihnen Sind 2 Datensätze einer Firma gegeben, `kunden` und `kreditkarten`. Schauen Sie sich die beiden Datensätze in der Konsole an.

`tidyr` und `dplyr` sind bereits eingebunden.

*** =instructions
- Vereinigen Sie die beiden Datensätze so, dass man direkt den Namen des Kunden neben seiner Kreditkarte in einem Datensatz sehen kann. 
- Die Variable "Kundennr" im Datensatz `kunden` entspricht der Variable "Kunde" im Datensatz `kreditkarten`.
- Beachten Sie, dass in dem neuen Datensatz nur Kunden stehen sollen, die auch eine Kreditkarte besitzen. Sie können davon ausgehen, dass jeder Kunde, der eine Kreditkarte besitzt, im Datensatz `kreditkarten` enthalten ist.
- Es sollen keine Spalten verschwinden, der Datensatz soll am Ende aus 6 Spaten bestehen. 

*** =hint
- Schauen Sie nochmal auf die Folien mit den join()-Funktionen.
- Der gemeinsame Schlüssel der beiden Datensätze ist hier nicht gleich benannt. Beachten Sie dies bei ihrem join-Befehl.

*** =pre_exercise_code
```{r}
# Einbinden der Pakete
library(dplyr)
library(tidyr)

# Erstellung der Datensätze
# Kunden
Kundennr <- c(1000, 1001, 1003, 1002, 1004, 1005, 1006, 1007, 1008, 1009)
Nachname <- c("Schindler", "Schmidt", "Meier", "Kanda", "Hoven", "Karlsmann", "Bernardt", "Toelkes", "Schubert", "Bach")
Vorname <- c("Marie", "Johann", "Lukas", "Ernst", "Sophie", "Helene","Jan", "Julia", "Sandra", "Anna")
Ort <- c("Muenster", "Hamm", "Bonn", "Duesseldorf", "Berlin", "Bonn", "Bitburg", "Duesseldorf", "Koeln", "Duesseldorf")
kunden <- data.frame(Kundennr, Nachname, Vorname, Ort)

# Kreditkarten
Kartennr <- c(2003, 4635, 3246, 3464, 3455, 9342)
Firma <- c("VISA", "Mastercard", "VISA", "VISA", "American Express", "Mastercard")
Kunde <- c(1003, 1002, 1008, 1006, 1000, 1009)
kreditkarten <- data.frame(Kartennr, Firma, Kunde)

```

*** =sample_code
```{r}
# Nennen Sie den neuen Datensatz kk
kk <- 
```

*** =solution
```{r}
# Vereinigung der Datensätze
kk <- right_join(kunden, kreditkarten, by = c("Kundennr" = "Kunde"))
# Genauso möglich:
# left_join(kreditkarten, kunden, by = c("Kunde" = "Kundennr"))
# oder
# inner_join(kreditkarten, kunden, by = c("Kunde" = "Kundennr"))

```

*** =sct
```{r}
test_object("kk")
test_error()
success_msg("Sehr gut! Sie hätten in diesem bestimmten Fall drei verschiedenen joins nutzen können: right_join, left_join oder inner_join")

```



--- type:NormalExercise lang:r xp:100 skills:1 key:f64a4481af
## 8. joins 
Gegeben sind ihnen die Datensätze einer Universität `professor`, `zuteilung` und `kurse`. Schauen Sie sich die Datensätze in der Konsole an. 

In dieser und der folgenden Aufgabe sollen nun der Datensatz `professor` und `kurse` in einen gemeinsamen Datensatz gebracht werden. Das geht in diesem Zustand noch nicht, da die beiden Datensätze noch keinen gemeinsamen "key" haben.

In dieser Aufgabe sollen Sie nun die Vorarbeit leisten und 2 neue Datensätze schaffen. Denken Sie bei der Auswahl des join-Befehls daran, dass keine Informationen verloren gehen dürfen (d.h. Ihre Lösung wird NAs enthalten). Benutzen Sie die jeweils gemeinsame Variable, um die Datensätze zu vereinigen.

`tidyr` wurde bereits eingebunden.


*** =instructions
- Erstellen Sie den Datensatz "kursinfo" der aus `zuteilung` und `kurse` entstehen soll. Das Ergebnis sollte 5 Spalten haben. Die gemeinsame Variable ist `Kurs_id`.
- Genauso sollen die beiden Datensätze `professor` und `zuteilung` vereinigt werden. Nennen Sie den neuen Datensatz "prof\_kurs". Dass Ergebnis sollte 3 Spalten haben. Die gemeinsame Variable ist `Prof_id`.

*** =hint
- Schauen Sie in die Vorlesung, um zu entscheiden, welchen join Sie benutzen.

*** =pre_exercise_code
```{r}
library(dplyr)
# Professor
Namenskuerzel <- c("HW", "JO", "GD", "FF", "SL", "ER")
Prof_id <- c(903, 923, 932, 987, 900, 911)
professor <- data.frame(Namenskuerzel, Prof_id)

# proffesor_kurs
Prof_id <- c(903, 923, 932, 987, 900, 911, 923, 987, 900)
Kurs_id <- c(100, 106, 102, 103, 103, 104, 105, 106, 109)
zuteilung <- data.frame(Prof_id, Kurs_id)

# Kurs
Studenten <- c(79, 233, 302, 148, 32, 27, 21, 177, 255, 198)
Semester <- c("SoSe", "WiSe", "SoSe", "SoSe", "WiSe", "SoSe", "SoSe", "WiSe", "WiSe", "WiSe")
Kurs_id <- c(100, 101, 102, 103, 104, 105, 106, 107, 108, 109)
Kursname <- c("Geldpolitik", "Marketing", "Statistische Methoden", "Recht_1", "Englisch_1", "Englisch_2", "Franzoesisch", "Recht_2", "Mathe_1", "Mathe_2")
kurse <- data.frame(Kursname, Kurs_id, Studenten, Semester)

```

*** =sample_code
```{r}
# Joinen Sie zuerst die beiden Datensätze "zuteilung" und "kurse"
kursinfo <- 
# Joinen Sie die beiden Datensätze "professor" und "zuteilung"
prof_kurs <- 
```

*** =solution
```{r}
kursinfo <- full_join(zuteilung, kurse, by = "Kurs_id")
prof_kurs <- full_join(professor, zuteilung, by = "Prof_id")

```

*** =sct
```{r}
test_object("kursinfo")
test_object("prof_kurs")
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:8d700a2a96
## 9. joins
Sie haben nun die beiden Datensätze `kursinfo` und `prof_kurs` gegeben, die Sie in der vorherigen Aufgabe erstellt haben. 

Tipp: Nehmen Sie das Matching anhand zweier Variablen vor.

Das "dplyr" Paket wurde bereits eingebunden.


*** =instructions
- Vereinigen Sie die beiden Datensätze ohne Informationsverlust.
- Vereinigen Sie die Datensätze so, dass Kurse ohne zugeteilten Professor nicht im Datensatz vorkommen.
- Benutzen Sie für die Vereinigung der Datensätze die gemeinsame Variable. Beachten Sie, dass beide Ergebnisse am Ende 6 Spalten haben sollten, aber eine unterschiedliche Anzahl von Zeilen.

*** =hint

*** =pre_exercise_code
```{r}
library(dplyr)
# Professor
Namenskuerzel <- c("HW", "JO", "GD", "FF", "SL", "ER")
Prof_id <- c(903, 923, 932, 987, 900, 911)
professor <- data.frame(Namenskuerzel, Prof_id)

# proffesor_kurs
Prof_id <- c(903, 923, 932, 987, 900, 911, 923, 987, 900)
Kurs_id <- c(100, 106, 102, 103, 103, 104, 105, 106, 109)
zuteilung <- data.frame(Prof_id, Kurs_id)

# Kurs
Studenten <- c(79, 233, 302, 148, 32, 27, 21, 177, 255, 198)
Semester <- c("SoSe", "WiSe", "SoSe", "SoSe", "WiSe", "SoSe", "SoSe", "WiSe", "WiSe", "WiSe")
Kurs_id <- c(100, 101, 102, 103, 104, 105, 106, 107, 108, 109)
Kursname <- c("Geldpolitik", "Marketing", "Statistische Methoden", "Recht_1", "Englisch_1", "Englisch_2", "Franzoesisch", "Recht_2", "Mathe_1", "Mathe_2")
kurse <- data.frame(Kursname, Kurs_id, Studenten, Semester)

# gemeinsamen key:
kursinfo <- full_join(zuteilung, kurse, by = "Kurs_id")
prof_kurs <- full_join(professor, zuteilung, by = "Prof_id")

```

*** =sample_code
```{r}
# Vereinigen Sie die beiden Datensätze so, dass keine Informationen verloren gehen.
gesamt1 <-

# Vereinigung in der nur Kurse auftauchen, für die auch ein Professor zugeteilt wurde.
gesamt2 <- 


```

*** =solution
```{r}
# Vereinigung ohne Informationsverlust
gesamt1 <- full_join(prof_kurs, kursinfo, by = c("Prof_id", "Kurs_id"))

# Vereinigung ohne NAs
gesamt2 <- inner_join(prof_kurs, kursinfo, by = c("Prof_id", "Kurs_id"))
```

*** =sct
```{r}
test_object("gesamt1")
test_object("gesamt2")
test_error()

```
