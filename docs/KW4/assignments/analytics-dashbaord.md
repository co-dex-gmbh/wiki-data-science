# Aufgabe

Erstellt ein Dashboard, auf wir verschiedene Algorithmen, Preprocessoren und Metriken für Klassifikationsprobleme vergleichen können.

Für die Erstellung sind sowohl Dash, als auch Stramlit zulässig.

Folgende Kernfunktion sollte das Dashboard beinhalten:

- Datensatz auswählen
- Visualisierung auswählen
- Modelle Auswählen
- Vorverabeitungsmodell auswählen


## Wie kann man starten

1. Erstelle den Dropdown, welcher verschiedene Datensätze auswählen lässt. Wir beschränken uns hier mal auf Klassifikation.
    - Mögliche Datensätzen findest du beispielsweise hier: https://github.com/mwaskom/seaborn-data
    - Erstelle einen Multiselect, um die Spalten des Datensatzes auszuwählen.
    - Erstelle ein Barplot mit der verteilung der Klassen anzeigt
    - Ermögliche über einen Dropdown das einsetzen von SMOTE 
    - Zeige, wie sich dadurch Verteilung und Größe der Klassen verändert
    - Erstelle ein Scatterplot, welches die ersten beiden Dimensionen des Datensatzes anzeigt. Die Punkte sollen nach Klassen gefärbt sein.
    - Erstelle einen Dropdown, um eine Klassifikationsmodell auszuwählen. Mögliche Wahlen sind:
        - KNN
        - Decision Tree
        - SVM
    - Je nach Modell kannst du weitere Parameter anpassbar machen
    - Gib evaluationsmetriken aus