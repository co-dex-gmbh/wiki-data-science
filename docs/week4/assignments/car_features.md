# Car Features and MSRP


Auf der Seite https://www.kaggle.com/datasets/CooperUnion/cardataset/data befindet sich ein Dataset über verschiedene Automodelle und deren Eigenschaften. Wir werden diesen Datensatz nutzen, um die Themen Klassifikation, Regression und Clustering zu behandeln. Wir gehen davon aus, dass die Preise in $ vorliegen.

## Aufgabe 1 - Daten verarbeiten und EDA:
1. Lade den Datensatz in Python und führe eine erste EDA durch. Welche Features gibt es? Welche Datentypen haben die Features? Gibt es fehlende Werte? Wie ist die Verteilung der Merkmale?
2. Beantworte die nachfolgenden Fragen:
   > 1. Wie viele verschiedene Automarken gibt es in dem Datensatz?
   > 2. Wie hat sich die Popularität der Marke BMW im Laufe der Zeit verändert?
   > 3. Wie hat sich der Durchschnittspreis von Fahrzeugen über die Jahre entwickelt?
   > 4. Bei welchen Marktklassen sind die Preise am stärksten gestiegen?
   > 5. Gibt es einen Zusammenhang zwischen Preis und Population?
   > 6. Definiere 3 weitere Fragen, welche du beantwortest. Bereite diese so vor, dass du sie vorstellen kannst.

## Aufgabe 2 - Klassifikation:
Ziel dieser Aufgabe ist es, die Marke eines Fahrzeuges vorherzusagen. 

1. Führe bei bedarf ein Feature Engineering und Data Cleaning durch.
2. Identifiziere Relevante Spalten für deine spätere Vorhersage.
3. Führe einen Test-Train Split durch. Verwende den randon_state 73 und ein Test-Train-Verhältnis von 80/20.
4. Verwende einen Entscheidungsbaum, um die Marke eines Fahrzeuges vorherzusagen
5. Bewerte dein Modell.
6. Entferne die Spalte "Model" und alle davon abgeleiteten Spalten. Vergleiche die Performance deiner Modelle.
   
## Aufgabe 3 - Regression:
Ziel dieser Aufgabe ist es, die UVP (MRSP) eines Fahrzeuges vorherzusagen.

1. Führe bei bedarf ein Feature Engineering und Data Cleaning durch.
2. Identifiziere Relevante Spalten für deine spätere Vorhersage.
3. Führe einen Test-Train Split durch. Verwende den randon_state 73 und ein Test-Train-Verhältnis von 80/20.
4. Verwende eine Lineare Regression, um die Marke eines Fahrzeuges vorherzusagen
5. Bewerte dein Modell.
<!-- 
## Aufgabe 4 - Clustering:
Ziel dieser Aufgabe ist es, die  -->