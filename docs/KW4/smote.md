# SMOTE: Theoretischer Hintergrund und mathematische Grundlagen

## Motivation

SMOTE ist aus mehreren wichtigen Gründen für das maschinelle Lernen bedeutsam:

- Problem der Modellverzerrung
   Ein klassisches Beispiel: Stell dir vor, du hast einen Datensatz mit 1000 gesunden und nur 10 kranken Patienten. Ein naives Modell könnte einfach IMMER "gesund" vorhersagen und hätte damit 99% Genauigkeit - wäre aber völlig nutzlos für den eigentlichen Zweck.


- Reale Anwendungsfälle sind oft unbalanciert
   
    - Betrugserkennung: Nur etwa 0.1% aller Transaktionen sind betrügerisch
    - Medizinische Diagnosen: Seltene Krankheiten betreffen oft weniger als 1% der Patienten
    - Maschinenwartung: Kritische Ausfälle sind selten, aber sehr wichtig zu erkennen
    - Spam-Erkennung: Normalerweise sind deutlich weniger als 50% der E-Mails Spam

- Auswirkungen auf die Modellleistung ohne SMOTE:
```python
# Beispiel mit stark unbalancierten Daten
from sklearn.metrics import classification_report

# Angenommen: 990 negative, 10 positive Fälle
y_true = [0]*990 + [1]*10
y_pred = [0]*1000  # Modell sagt immer 0 vorher

print(classification_report(y_true, y_pred))
# Ergebnis:
# Klasse 0: Precision=0.99, Recall=1.00
# Klasse 1: Precision=0.00, Recall=0.00
```


- Verbesserungen durch SMOTE:
    
    - Balanced Accuracy steigt (oft um 20-30%)
    - Recall für die Minderheitsklasse verbessert sich deutlich
    <!-- - ROC-AUC und PR-AUC Metriken werden realistischer -->
    - Das Modell lernt tatsächlich die relevanten Merkmale der Minderheitsklasse
  
- Praktische Bedeutung:
    
    - Ein Beispiel aus der Kreditkartenbetrugsbekämpfung:
        - Ohne SMOTE: Modell erkennt 30% der Betrugsfälle
        - Mit SMOTE: Modell erkennt 80% der Betrugsfälle
        - Resultat: Millionen € weniger Schaden durch Betrug

- Warum nicht einfach Oversampling?

    - Einfaches Oversampling (Kopieren der Minderheitsklasse) führt zu:
        - Overfitting auf die wenigen echten Beispiele
        - Keine neuen Informationen für das Modell
        - Schlechter Generalisierung
    
    - SMOTE ist besonders wichtig in kritischen Anwendungen:
        - Medizinische Diagnostik (seltene Krankheiten)
        - Sicherheitssysteme (Eindringlingsversuche)
        - Qualitätskontrolle (seltene Produktfehler)
        - Finanzwesen (Betrugsversuche)
    
    - Ein konkretes Beispiel aus der Praxis bei der Erkennung von Brustkrebs in Mammographien:
        - Ursprüngliche Daten: 98% negativ, 2% positiv
        - Modell ohne SMOTE: 99% Accuracy, aber nur 20% der Krebsfälle erkannt
        - Modell mit SMOTE: 95% Accuracy, aber 90% der Krebsfälle erkannt
        → Der leichte Rückgang in der Gesamtgenauigkeit ist hier ein kleiner Preis für die deutlich verbesserte Erkennung der wichtigen positiven Fälle.
    


## 2. Grundlegendes Problem: Imbalanced Learning

Das fundamentale Problem, das SMOTE (Synthetic Minority Over-sampling Technique) adressiert, liegt in der Natur unausgewogener Datensätze. In vielen realen Anwendungsfällen ist die Klassenverteilung stark ungleich verteilt, was zu verschiedenen Herausforderungen führt:

### 2.1 Mathematische Probleme bei Imbalanced Data
- Die Likelihood-Funktion wird von der Mehrheitsklasse dominiert
- Die Prior-Wahrscheinlichkeit der Minderheitsklasse ist sehr klein
- Klassische Verlustfunktionen wie Cross-Entropy optimieren hauptsächlich auf die Mehrheitsklasse

### 2.2 Auswirkungen auf das Machine Learning
- Klassifikatoren tendieren zur Mehrheitsklasse
- Die Decision Boundary wird zugunsten der Mehrheitsklasse verschoben
- Feature-Importance-Metriken werden verzerrt

## 3. Mathematische Grundlagen von SMOTE

### 3.1 Grundprinzip
SMOTE basiert auf dem Konzept der Interpolation im Feature-Raum. Für jeden Punkt x₁ der Minderheitsklasse wird ein synthetischer Punkt x_new wie folgt erzeugt:

x_new = x₁ + λ(x₂ - x₁)

wobei:
   - x₁ ist der Ausgangspunkt in der Minderheitsklasse
   - x₂ ist einer der k nächsten Nachbarn von x₁
   - λ ist ein zufälliger Wert zwischen 0 und 1

### 3.2 K-Nearest Neighbors im SMOTE-Kontext
Die Auswahl der k nächsten Nachbarn erfolgt typischerweise im euklidischen Raum:

d(x₁, x₂) = √(Σ(x₁ᵢ - x₂ᵢ)²)

Die Wahl von k beeinflusst dabei:
   - Die Varianz der synthetischen Beispiele
   - Die Dichte der generierten Punkte
   - Die Gefahr von Overfitting oder Underfitting

## 4. Theoretische Eigenschaften und Garantien

### 4.1 Topologische Eigenschaften
SMOTE erhält wichtige topologische Eigenschaften des ursprünglichen Datenraums:

   - Die konvexe Hülle der Minderheitsklasse bleibt erhalten
   - Die Dichte-Verteilung wird lokal approximiert
   - Cluster-Strukturen bleiben weitgehend erhalten

### 4.2 Statistische Eigenschaften
Die generierten Datenpunkte haben folgende statistische Eigenschaften:

   - Der Erwartungswert liegt auf der Verbindungslinie zwischen zwei realen Punkten
   - Die Varianz wird durch die lokale Nachbarschaft bestimmt
   - Die Kovarianzstruktur der originalen Daten bleibt approximativ erhalten

## 5. Theoretische Limitationen

### 5.1 Grundlegende Einschränkungen
 - Die Methode ist anfällig für Rauschen in den Originaldaten
 - Bei hochdimensionalen Daten kann der Fluch der Dimensionalität problematisch werden

### 5.2 Statistische Limitationen
 - Die wahre Verteilung der Minderheitsklasse wird nur approximiert
 - Extreme Werte (Outlier) können zu verzerrten synthetischen Beispielen führen
 - Die Unabhängigkeitsannahme zwischen den Features wird implizit vorausgesetzt
<!-- 
## 5. Erweiterungen des Basis-SMOTE-Algorithmus

### 5.1 Borderline-SMOTE
Fokussiert auf die Generierung von Beispielen nahe der Entscheidungsgrenze durch:
- Identifikation von Borderline-Beispielen
- Gewichtete Synthese basierend auf der Nähe zur Entscheidungsgrenze

### 5.2 Adaptive Synthetic Sampling (ADASYN)
Erweitert SMOTE durch:
- Adaptive Gewichtung der Syntheserate
- Berücksichtigung lokaler Dichteverhältnisse
- Dynamische Anpassung der Syntheseparameter

### 5.3 Safe-Level-SMOTE
Verbessert die Robustheit durch:
- Evaluation der "Sicherheit" einer Region
- Vermeidung der Synthese in unsicheren Regionen
- Adaptive Anpassung der Interpolationsparameter -->

## 6. Theoretische Verbindungen zu anderen Konzepten

### 6.1 Verbindung zur Manifold-Hypothese
SMOTE basiert implizit auf der Annahme, dass:
- Die Daten auf einem niedrigdimensionalen Manifold liegen
- Lineare Interpolation auf diesem Manifold sinnvoll ist
- Lokale Strukturen global relevant sind

### 6.2 Beziehung zu anderen Sampling-Methoden
- Random Oversampling: Spezialfall mit λ = 0
- Tomek Links: Komplementäre Methode zur Grenzbereinigung
- Condensed Nearest Neighbor: Alternative für Unterabtastung