# K-Nearest Neighbors (KNN) - Grundlagen und Implementierung

## 1. Grundprinzip
KNN ist ein instanzbasierter Lernalgorithmus, der sowohl für Klassifikation als auch Regression verwendet werden kann. Er basiert auf dem einfachen Prinzip: "Sage mir, wer deine Nachbarn sind, und ich sage dir, wer du bist."

## 2. Funktionsweise

### 2.1 Für Klassifikation:
- Bestimme die k nächsten Nachbarn eines neuen Datenpunkts
- Führe eine Mehrheitsabstimmung durch
- Weise dem neuen Punkt die häufigste Klasse unter den Nachbarn zu

### 2.2 Für Regression:
- Bestimme die k nächsten Nachbarn eines neuen Datenpunkts
- Berechne den Durchschnitt (oder gewichteten Durchschnitt) der Zielwerte
- Weise dem neuen Punkt diesen Durchschnittswert zu

## 3. Der Algorithmus im Detail

### 3.1 Pseudocode für KNN-Klassifikation:
```
INPUT:
    D: Trainingsdata (x_i, y_i)
    k: Anzahl der Nachbarn
    x_new: Neuer Datenpunkt für Klassifikation

ALGORITHMUS:
1. FÜR ALLE Punkte x_i in D:
    - Berechne Distanz d(x_new, x_i)
    - Speichere (d(x_new, x_i), y_i) in Liste distances

2. Sortiere distances nach aufsteigender Distanz

3. Wähle die ersten k Einträge aus distances
   Speichere deren Labels in neighbors

4. Zähle Häufigkeit jeder Klasse in neighbors
   y_pred = Klasse mit höchster Häufigkeit

RETURN: y_pred
```

### 3.2 Distanzmetriken
Die häufigsten Distanzmetriken sind:

1. Euklidische Distanz:
   d(x,y) = √(Σ(xᵢ - yᵢ)²)

2. Manhattan-Distanz:
   d(x,y) = Σ|xᵢ - yᵢ|

3. Minkowski-Distanz:
   d(x,y) = (Σ|xᵢ - yᵢ|ᵖ)^(1/p)

## 4. Wichtige Überlegungen und Parameter

### 4.1 Wahl von k
- Kleines k: Hohe Varianz, niedriger Bias
- Großes k: Niedrige Varianz, hoher Bias
- k sollte ungerade sein (bei Binärklassifikation)
- Typische Werte: 3, 5, 7, 11

### 4.2 Distanzgewichtung
Die Stimmen der Nachbarn können gewichtet werden:
- Uniform: Alle Nachbarn haben gleiches Gewicht
- Nach Distanz: w = 1/d oder w = 1/d²

### 4.3 Skalierung
- Feature-Skalierung ist KRITISCH
- Standardisierung (z-score) oder 
- Min-Max-Skalierung sind üblich

## 5. Implementierungsbeispiel in Python

```python
import numpy as np
from collections import Counter

class SimpleKNN:
    def __init__(self, k=3):
        self.k = k
        
    def fit(self, X, y):
        self.X_train = X
        self.y_train = y
        
    def euclidean_distance(self, x1, x2):
        return np.sqrt(np.sum((x1 - x2) ** 2))
    
    def predict(self, X):
        predictions = []
        
        for x in X:
            # Distanzen berechnen
            distances = []
            for idx, x_train in enumerate(self.X_train):
                dist = self.euclidean_distance(x, x_train)
                distances.append((dist, self.y_train[idx]))
            
            # Sortieren nach Distanz
            distances.sort(key=lambda x: x[0])
            
            # k nächste Nachbarn finden
            k_nearest = distances[:self.k]
            
            # Labels der k nächsten Nachbarn
            k_nearest_labels = [label for _, label in k_nearest]
            
            # Mehrheitsentscheidung
            most_common = Counter(k_nearest_labels).most_common(1)
            predictions.append(most_common[0][0])
            
        return np.array(predictions)
```

## 6. Vor- und Nachteile

### 6.1 Vorteile
- Einfach zu verstehen und zu implementieren
- Keine Trainingsphase notwendig
- Nicht-parametrisch (keine Annahmen über Datenverteilung)
- Gut für multimodale Klassen
- Natürliche Behandlung von Multi-Class-Problemen

### 6.2 Nachteile
- Berechnungsaufwand bei der Vorhersage
- Speicherintensiv (alle Trainingsdaten müssen gespeichert werden)
- Sensibel gegenüber irrelevanten Features
- "Fluch der Dimensionalität"
- Skalierung der Features ist kritisch
