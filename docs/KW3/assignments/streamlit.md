# Aufgaben Streamlit

## Aufgabe 1

### Aufgabe 1.1

Erstelle eine mehrseitiges Streamlit-Web-App, welche als Nachschlagewertr für die Grundlagen des Machine Learnings dient. Die App soll folgende Seiten enthalten:

1. Startseite: Begrüßung und kurze Einleitung
   1. - Was ist Machine Learning?
   2. - Welche Arten von Algorithmen gibt es?
   3. - Wie funktioniert ein Machine Learning Modell?
   4. - Was sind Traingins- und Testdaten?
   
2. Modelle: Hier sollen die wichtigsten Machine Learning Modelle vorgestellt werden. Jedes der bisher behandelten Modelle erhält eine Unterseite
   1. - Lineare Regression
   2. - SVM (Support Vector Machine)
   3. - Decision Trees



Hinweis: Aufgabe 2 kann in Gruppen bearbeitet werden. Jede Person erhält ein Modell zugewiesen, welches sie vorstellen soll.

### Aufgabe 1.2

Füge zu jedem Modell ein Beispiel hinzu, welches die Funktionsweise des Modells verdeutlicht. Als Datensaätze können die Beispiele aus den bisherigen Aufgaben oder Beispieldatensätze aus scikit-learn verwendet werden.

### Aufgabe 1.3

Füge der Streamlit App eine Authentifikation hinzu. Der Nutzer soll sich mit einem Passwort anmelden können, um die App zu nutzen. Das Passwort soll in einer Umgebungsvariable gespeichert werden.


# Aufgabe 2

Sieh dir den Datensatz zu täglichen Einsätzen der Berliner Feuerwehr an [https://github.com/Berliner-Feuerwehr/BF-Open-Data/blob/main/Datasets/Daily_Data/BFw_mission_data_daily.csv](https://github.com/Berliner-Feuerwehr/BF-Open-Data/blob/main/Datasets/Daily_Data/BFw_mission_data_daily.csv). 

Hier findest du eine Beschreibung der Spalten:

| **Spalte**                                         | **Erklärung**                                                                          |
| -------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **mission_created_date**                           | Datum, an dem die Mission erstellt wurde.                                              |
| **mission_count_all**                              | Gesamtzahl der Einsätze.                                                               |
| **mission_count_ems**                              | Anzahl der medizinischen Notfalleinsätze (EMS).                                        |
| **mission_count_ems_critical**                     | Anzahl der kritischen medizinischen Notfalleinsätze (EMS).                             |
| **mission_count_ems_critical_cpr**                 | Anzahl der kritischen EMS-Einsätze, bei denen CPR erforderlich war.                    |
| **mission_count_fire**                             | Anzahl der Brandeinsätze.                                                              |
| **mission_count_technical_rescue**                 | Anzahl der technischen Rettungseinsätze.                                               |
| **response_time_ems_critical_mean**                | Durchschnittliche Reaktionszeit für kritische EMS-Einsätze.                            |
| **response_time_ems_critical_median**              | Median der Reaktionszeit für kritische EMS-Einsätze.                                   |
| **response_time_ems_critical_std**                 | Standardabweichung der Reaktionszeit für kritische EMS-Einsätze.                       |
| **response_time_ems_critical_cpr_mean**            | Durchschnittliche Reaktionszeit für kritische EMS-Einsätze mit CPR.                    |
| **response_time_ems_critical_cpr_median**          | Median der Reaktionszeit für kritische EMS-Einsätze mit CPR.                           |
| **response_time_ems_critical_cpr_std**             | Standardabweichung der Reaktionszeit für kritische EMS-Einsätze mit CPR.               |
| **response_time_fire_time_to_first_pump_mean**     | Durchschnittliche Zeit bis zum ersten Pumpeneinsatz bei Brandeinsätzen.                |
| **response_time_fire_time_to_first_pump_median**   | Median der Zeit bis zum ersten Pumpeneinsatz bei Brandeinsätzen.                       |
| **response_time_fire_time_to_first_pump_std**      | Standardabweichung der Zeit bis zum ersten Pumpeneinsatz bei Brandeinsätzen.           |
| **response_time_fire_time_to_first_ladder_mean**   | Durchschnittliche Zeit bis zur ersten Leiter bei Brandeinsätzen.                       |
| **response_time_fire_time_to_first_ladder_median** | Median der Zeit bis zur ersten Leiter bei Brandeinsätzen.                              |
| **response_time_fire_time_to_first_ladder_std**    | Standardabweichung der Zeit bis zur ersten Leiter bei Brandeinsätzen.                  |
| **response_time_fire_time_to_full_crew_mean**      | Durchschnittliche Zeit bis zum Einsatz der vollständigen Crew bei Brandeinsätzen.      |
| **response_time_fire_time_to_full_crew_median**    | Median der Zeit bis zum Einsatz der vollständigen Crew bei Brandeinsätzen.             |
| **response_time_fire_time_to_full_crew_std**       | Standardabweichung der Zeit bis zum Einsatz der vollständigen Crew bei Brandeinsätzen. |
| **response_time_technical_rescue_mean**            | Durchschnittliche Reaktionszeit für technische Rettungseinsätze.                       |
| **response_time_technical_rescue_median**          | Median der Reaktionszeit für technische Rettungseinsätze.                              |
| **response_time_technical_rescue_std**             | Standardabweichung der Reaktionszeit für technische Rettungseinsätze.                  |


### 2.1 Erstellen Sie ein interaktives Dashboard zur Visualisierung der täglichen Einsatzzahlen
  1. Filtern Sie nach Datum und Einsatzarten (z. B. `mission_count_fire`, `mission_count_ems`), um die Daten nach verschiedenen Kriterien anzuzeigen.
  2. Visualisieren Sie die Anzahl der Einsätze pro Tag/ Woche/ Monat.
  3. Zeigen Sie die durchschnittlichen Reaktionszeiten für alle Einsatzarten (z. B. `response_time_fire_time_to_first_pump_mean`) in einem Liniendiagramm an.
  4. Erstellen Sie interaktive Widgets, mit denen die Benutzer den Zeitraum und die Einsatzarten nach Bedarf anpassen können.

### 2.2 Erstellen Sie ein Modell zur Vorhersage der Reaktionszeit für Brandeinsätze
  1. Verwenden Sie `mission_count_fire` und `mission_count_ems_critical` als Eingabefunktionen für Ihr Modell.
  2. Bauen Sie ein lineares Regressionsmodell, das die durchschnittliche Reaktionszeit für Brandeinsätze (`response_time_fire_time_to_first_pump_mean`) vorhersagt.
  3. Bewerten Sie das Modell anhand der mittleren quadratischen Abweichung (MSE), um die Genauigkeit Ihrer Vorhersagen zu prüfen.

### Zusatz: 2.3 ALT Kategorisieren Sie Einsätze als "kritisch" oder "nicht-kritisch"
  1. Trainieren Sie ein Klassifikationsmodell (z. B. SVM oder Entscheidungsbaum), das auf `mission_count_ems_critical` und `response_time_ems_critical_mean` basiert. Gibt es einen zusammenhang?
  2. Evaluieren Sie das Modell (mit den Metriken Präzision, Recall und F1-Score), um die Leistung der Klassifikation zu bewerten.

### Zusatz: 2.3 Kategorisieren Sie Einsätze
  1. Trainieren Sie ein Klassifikationsmodell (z. B. SVM oder Entscheidungsbaum), das auf den Datensatz [https://github.com/Berliner-Feuerwehr/BF-Open-Data/blob/main/Datasets/Mission_Data/mission_data_set_open_data_2024.csv](https://github.com/Berliner-Feuerwehr/BF-Open-Data/blob/main/Datasets/Mission_Data/mission_data_set_open_data_2024.csv) zurückgreift. Das Modell soll die Klasse `dispatchcode_criticality` vorhersagen
  2. Evaluieren Sie das Modell (mit den Metriken Präzision, Recall und F1-Score), um die Leistung der Klassifikation zu bewerten.
  3. Erstellen Sie ein Regressionsmodell, um die `response_time`in diesem 

### 2.4 Erstellen Sie ein Tool zur Analyse der Reaktionszeiten für kritische und nicht-kritische Einsätze
  1. Visualisieren Sie die durchschnittliche Reaktionszeit für kritische EMS-Einsätze (`response_time_ems_critical_mean`) und für Brandeinsätze (`response_time_fire_time_to_first_pump_mean`).
  2. Implementieren Sie interaktive Widgets, mit denen die Benutzer verschiedene Zeiträume auswählen und die Reaktionszeiten vergleichen können.

### 2.5 Erstellen Sie ein Kreisdiagramm zur Darstellung der Verteilung der Einsatzarten
  1. Wie verteilen sich die verschiedenen Arten von Einsätzen (Brände, EMS, technische Rettung) über den gesamten Zeitraum?
  2. Welche Kategorie stellt den größten Anteil an den Einsätzen dar, und wie hoch ist dieser Anteil im Vergleich zu den anderen Kategorien?

### 2.6 Erstellen Sie ein Liniendiagramm zur Darstellung der Entwicklung der Einsatzzahlen im Zeitverlauf
  1. Wie haben sich die Gesamtzahlen der Einsätze über die Zeit verändert?
  2. Lassen sich saisonale Schwankungen oder langfristige Trends in den Einsatzzahlen erkennen?

### 2.7 Erstellen Sie ein Boxplot zur Darstellung der Reaktionszeiten (`response_time...`) für verschiedene Einsatzarten
  1. Gibt es signifikante Unterschiede in den Reaktionszeiten für die verschiedenen Einsatzarten (EMS, Brände, technische Rettung)?
  2. Welche Einsatzarten zeigen die längsten oder kürzesten Reaktionszeiten?

### 2.8 Erstellen Sie ein Streudiagramm, um die Korrelation zwischen der Anzahl der Einsätze und den Reaktionszeiten zu visualisieren
  1. Gibt es eine erkennbare Korrelation zwischen der Anzahl der Einsätze und den Reaktionszeiten?
  2. Wie verändert sich die Reaktionszeit, wenn die Zahl der Einsätze steigt oder sinkt?

### 2.9 Erstellen Sie ein Balkendiagramm zur Darstellung der durchschnittlichen Reaktionszeiten für verschiedene Einsatzarten
  1. Welche Einsatzart weist die längste durchschnittliche Reaktionszeit auf?
  2. Welche Trends oder Veränderungen in den Reaktionszeiten sind im Zeitverlauf zu beobachten?

### 2.10 Erstellen Sie ein Histogramm zur Darstellung der Häufigkeit der kritischen Einsätze (`mission_count_..._critical`)
  1. Wie häufig treten kritische Einsätze auf, und wie hoch ist deren Anteil an den Gesamteinsätzen?
  2. Gibt es spezifische Zeiträume oder Tage, an denen besonders viele oder wenige kritische Einsätze auftraten?
