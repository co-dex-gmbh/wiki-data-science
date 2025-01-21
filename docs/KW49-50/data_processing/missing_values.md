# Missing Values

Unsere Datensätze sind in den wengisten Fällen perfekt vollständig. Beispielsweise kann es bei der Erfassung von Personaldaten vorkommen, dass nicht alle Felder ausgefüllt wurden. Diese fehlenden Werte können die Analyse und Modellierung beeinträchtigen. Daher ist es wichtig, diese Lücken zu identifizeren und zu behandeln.

## Umgang mit fehlenden Werten

Es gibt verschiedene Strategien, um fehlende Werte zu behandeln. Die Wahl der Methode hängt von der Art der Daten und dem Kontext ab. Hier sind einige gängige Ansätze:

### 1. **Entfernen von fehlenden Werten**

Eine einfache Methode besteht darin, alle Zeilen oder Spalten zu entfernen, die fehlende Werte enthalten. Dies kann jedoch zu einem Informationsverlust führen, insbesondere wenn viele Daten fehlen. Generell sollten wir beim Entfernen der Daten uns vorher ansehen, ob die Daten zufällig fehlen oder ob es ein Muster gibt. Machmal kann es auch vorkommen, dass unser Datensatz durch das Entfernen von Daten verzerrt oder zu klein wird.

### 2. **Imputation von fehlenden Werten**

Eine häufigere Methode ist die Imputation, bei der fehlende Werte durch Schätzungen basierend auf den verbleibenden Daten ersetzt werden. Dies kann durch den Durchschnitt, den Median oder durch Vorhersagemodelle erfolgen. Die Wahl der Methode hängt von der Art der Daten und dem Kontext ab. Vor der Wahl einer der Methoden für die Imputation müssen wir auch hier ein Grundverständnis von unseren Daten haben. 

Beobachte wir beispielsweise Wetterdaten und es Fehlt die Temperatur an einem Tag, dann könnten wir die Temperatur des Vortages als Schätzung verwenden. Auch die Verwendung eines Mittelweertes der anliegenden Tage könnte eine Möglichkeit sein. Haben wir jedoch ungeordnete Daten, wie beispielsweise Namen, dann macht es keinen Sinn, den Durchschnitt für die Spalte Alter als Ersatz für Missing Values zu berechnen.

Je nach Art der Daten und des Problems ist bei der Imputation Kreativität und Fachwissen gefragt.

### 3. **Vorhersagemodelle für die Imputation**

In einigen Fällen kann es sinnvoll sein, Vorhersagemodelle zu verwenden, um fehlende Werte zu schätzen. Dies kann insbesondere dann nützlich sein, wenn die fehlenden Werte nicht zufällig sind und ein Muster aufweisen. Beispielsweise könnten wir ein Regressionsmodell trainieren, um fehlende Werte zu schätzen, basierend auf anderen verfügbaren Variablen.

### 4. **Kategorisierung von fehlenden Werten**

Manchmal kann es sinnvoll sein, fehlende Werte als separate Kategorie zu behandeln, anstatt sie zu schätzen oder zu entfernen. Dies kann insbesondere dann nützlich sein, wenn das Fehlen von Werten eine Bedeutung hat und Informationen enthält. Beispielsweise kann das fehlen eines Wertes bei der Anwesenheit eines Patienten in einem Krankenhaus darauf hinweisen, dass der Patient nicht anwesend war.

