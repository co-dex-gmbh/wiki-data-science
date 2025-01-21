# Feature Scaling: Methoden und ihre Bedeutung

## 1. Warum ist Skalierung wichtig?

### 1.1 Grundlegende Probleme ohne Skalierung
- Features in unterschiedlichen Größenordnungen (z.B. Alter [0-100] vs. Einkommen [0-1.000.000])
- Algorithmen, die auf Distanzen basieren (KNN, k-Means, SVM), werden von großen Werten dominiert
- Gradient Descent konvergiert langsamer
- L1/L2 Regularisierung funktioniert nicht optimal

### 1.2 Beispiel ohne Skalierung:
```python
import numpy as np
from sklearn.datasets import make_blobs

# Beispieldaten
X, y = make_blobs(n_samples=1000, centers=2, random_state=42)
# Zweite Feature künstlich vergrößern
X[:, 1] = X[:, 1] * 1000

# Ohne Skalierung: Distanzberechnung wird von Feature 2 dominiert
point1 = X[0]
point2 = X[1]
distance = np.sqrt(np.sum((point1 - point2) ** 2))
print(f"Dominierte Distanz: {distance}")  # Wird von großen Werten dominiert
```

## 2. Wichtigste Skalierungsmethoden

### 2.1 StandardScaler (Standardisierung)
Transformiert Features auf Mittelwert=0 und Standardabweichung=1.

```python
from sklearn.preprocessing import StandardScaler
import pandas as pd

# Beispieldaten
data = pd.DataFrame({
    'Alter': [25, 35, 45, 55],
    'Einkommen': [30000, 45000, 70000, 90000]
})

scaler = StandardScaler()
scaled_data = scaler.fit_transform(data)

print("Original:\n", data)
print("\nSkaliert:\n", pd.DataFrame(scaled_data, columns=data.columns))
```

**Formel:** z = (x - μ) / σ
- Vorteile:
  - Robust gegen Ausreißer
  - Erhält die Form der Verteilung
  - Ideal für Normalverteilte Daten
- Nachteile:
  - Keine garantierten Min/Max Grenzen
  - Schwerer interpretierbar

### 2.2 MinMaxScaler
Skaliert Features in einen festen Bereich [0,1] oder beliebigen anderen.

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
scaled_data = scaler.fit_transform(data)

print("MinMax Skaliert:\n", pd.DataFrame(scaled_data, columns=data.columns))
```

**Formel:** x_scaled = (x - x_min) / (x_max - x_min)
- Vorteile:
  - Fester Wertebereich
  - Erhält Null-Einträge
  - Gut interpretierbar
- Nachteile:
  - Empfindlich gegen Ausreißer
  - Verändert die Verteilungsform

### 2.3 RobustScaler
Verwendet Statistiken, die robust gegen Ausreißer sind (Median und IQR).

```python
from sklearn.preprocessing import RobustScaler

scaler = RobustScaler()
scaled_data = scaler.fit_transform(data)

print("Robust Skaliert:\n", pd.DataFrame(scaled_data, columns=data.columns))
```

**Formel:** x_scaled = (x - median) / IQR
- Vorteile:
  - Sehr robust gegen Ausreißer
  - Gut für schiefe Verteilungen
- Nachteile:
  - Keine garantierten Grenzen
  - Weniger effizient bei normalverteilten Daten

### 2.4 Vergleich der Methoden

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.preprocessing import StandardScaler, MinMaxScaler, RobustScaler

# Daten mit Ausreißer
data = np.array([1, 2, 3, 4, 100]).reshape(-1, 1)

scalers = {
    'Standard': StandardScaler(),
    'MinMax': MinMaxScaler(),
    'Robust': RobustScaler()
}

# Skalierung vergleichen
for name, scaler in scalers.items():
    scaled = scaler.fit_transform(data)
    print(f"\n{name} Scaler:")
    print(f"Skalierte Werte: {scaled.flatten()}")
```

## 3. Anwendungsgebiete

### 3.1 Wann welche Skalierung?

| Szenario             | Empfohlene Skalierung | Grund                             |
| -------------------- | --------------------- | --------------------------------- |
| Neural Networks      | StandardScaler        | Schnellere Konvergenz             |
| KNN, K-Means         | MinMaxScaler          | Gleiche Gewichtung aller Features |
| Daten mit Ausreißern | RobustScaler          | Minimaler Einfluss von Ausreißern |
| SVM                  | StandardScaler        | Optimale Hyperebenen-Berechnung   |

### 3.2 Praktisches Beispiel: Vergleich der Auswirkungen

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score

# Daten laden
iris = load_iris()
X_train, X_test, y_train, y_test = train_test_split(
    iris.data, iris.target, random_state=42)

# Verschiedene Skalierungen testen
results = {}
for name, scaler in scalers.items():
    # Daten skalieren
    X_train_scaled = scaler.fit_transform(X_train)
    X_test_scaled = scaler.transform(X_test)
    
    # Model trainieren
    knn = KNeighborsClassifier(n_neighbors=3)
    knn.fit(X_train_scaled, y_train)
    
    # Vorhersagen
    y_pred = knn.predict(X_test_scaled)
    accuracy = accuracy_score(y_test, y_pred)
    results[name] = accuracy

print("\nKNN Accuracy mit verschiedenen Skalierungen:")
for name, acc in results.items():
    print(f"{name}: {acc:.3f}")
```

## 4. Best Practices

### 4.1 Wichtige Regeln:
1. Skalierung immer nur auf Trainingsdaten fitten
2. Gleiche Skalierung auf Test-/Validierungsdaten anwenden
3. Skalierung vor Feature Selection/Engineering
4. Bei Updates: Alte Skalierungsparameter verwenden

### 4.2 Pipeline-Integration:
```python
from sklearn.pipeline import Pipeline

# Korrekte Integration in Pipeline
pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', KNeighborsClassifier())
])

# Falsch wäre:
X_scaled = scaler.fit_transform(X)  # Data Leakage!
```