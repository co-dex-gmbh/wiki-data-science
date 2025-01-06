# Deskriptive Datenanalyse

## Einführung in die Explorative Datenanalyse (EDA)

In der explorativen Datenanalyse (EDA) werfen wir einen ersten Blick auf unsere Daten, um die wichtigsten Merkmale des Datensatzes zu erfassen und zu visualisieren. Diese Schritte helfen uns, die Daten besser zu verstehen, Hypothesen zu formulieren, und schließlich die Voraussetzungen für eine fundierte Analyse oder ein Modell zu schaffen. Im Folgenden führen wir dich Schritt für Schritt durch die fünf wesentlichen Schritte einer EDA.


### Schritt 1: Verstehen der Datenstruktur

#### 1.1 Datentypen und Strukturen
- Daten werden meist in numerische, kategorische und Zeitreihen-Daten unterteilt, und jeder Typ braucht besondere Techniken und Darstellungen.
- Nutze Datenstrukturen wie DataFrames (Pandas in Python) und Arrays (NumPy), um Daten zu laden und effizient zu verarbeiten.

#### 1.2 Kontext und Quelle der Daten
- Woher kommen die Daten? Wann wurden sie gesammelt? Notiere den Kontext, um den Zweck der Daten zu verstehen und mögliche Verzerrungen zu erkennen.

#### 1.3 Metadaten und Dokumentation
- Wenn verfügbar, überprüfe die Metadaten und die Dokumentation zum Datensatz. Das liefert oft wichtige Hinweise zu den Variablen und der Datenqualität.


### Schritt 2: Datenbereinigung und Vorverarbeitung

#### 2.1 Fehlende Werte behandeln
- **Optionen**: Zeilen oder Spalten entfernen, fehlende Werte mit Durchschnitt oder Median auffüllen, oder Vorhersagemodelle nutzen, um die Werte zu schätzen.

#### 2.2 Duplikate entfernen
- Doppelte Einträge in deinem Datensatz verfälschen Ergebnisse. Entferne sie, um die Integrität deiner Daten zu sichern.

#### 2.3 Transformation der Daten
- **Normalisierung**: Skalierung der Daten für eine einheitliche Verteilung.
- **Kodierung**: Umwandlung von Kategorien in numerische Werte (z.B. One-Hot-Codierung).
- **Zeitreihen**: Konvertiere Datumsangaben für eine korrekte Analyse von Zeitdaten.

#### 2.4 Ausreißer identifizieren und behandeln
- Verwende Diagramme wie Boxplots oder statistische Tests (z.B. Z-Scores), um Ausreißer zu finden. Entschließe, ob du diese entfernst oder transformierst.


### Schritt 3: Univariate Analyse (Einzelne Variablen)

#### 3.1 Deskriptive Statistik
- Führe grundlegende statistische Berechnungen durch (Mittelwert, Median, Modus), um zentrale Tendenzen und Streuung der Variablen zu verstehen.

#### 3.2 Visualisierungen (Univariate)
- **Histogramme**: Zum Veranschaulichen der Verteilung.
- **Boxplots**: Zeigen Verteilung und Ausreißer.
- **Balkendiagramme**: Für die Häufigkeit von Kategorien.


### Schritt 4: Bivariate und multivariate Analyse (Zusammenhänge)

#### 4.1 Bivariate Analyse
- **Scatterplots**: Visualisiert die Beziehung zwischen zwei numerischen Variablen.
- **Korrelationsmatrix**: Berechnet Korrelationen zwischen Variablen.

#### 4.2 Multivariate Analyse
- **Paarplots** und **Heatmaps**: Zeigen Beziehungen mehrerer Variablen.
- **PCA** (Principal Component Analysis): Reduziert die Komplexität der Daten.
- **Clustering**: Zum Gruppieren von Datenpunkten basierend auf Ähnlichkeiten.

#### 4.3 Wechselwirkungen erkennen
- Achte auf Wechselwirkungen zwischen Variablen, die möglicherweise auf komplexe Abhängigkeiten oder Multikollinearität hinweisen.


### Schritt 5: Einblicke und Schlussfolgerungen ziehen

#### 5.1 Wichtige Erkenntnisse zusammenfassen
- Notiere die wichtigsten Muster und Ausreißer. Welche Einblicke bieten deine Analysen?

#### 5.2 Visuelles Storytelling
- Nutze ansprechende Diagramme, um deine Ergebnisse zu kommunizieren. Erstelle klare Visualisierungen, die die Daten einfach und verständlich zusammenfassen.

#### 5.3 Entscheidungen treffen
- Verwende die Erkenntnisse der EDA, um Hypothesen zu formulieren, strategische Entscheidungen zu treffen oder nächste Schritte für Modellierungen festzulegen.

#### 5.4 Dokumentation
- Dokumentiere die EDA-Schritte, Methoden und Ergebnisse vollständig, damit der Prozess nachvollziehbar und wiederholbar bleibt.

