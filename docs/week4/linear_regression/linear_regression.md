### **Lineare Regression: Einführung und Funktionsweise**

Die **lineare Regression** ist ein grundlegendes statistisches Verfahren, das zur Modellierung der Beziehung zwischen einer abhängigen Variablen (Zielvariable) und einer oder mehreren unabhängigen Variablen (Prädiktoren) verwendet wird. Sie ist ein essenzielles Werkzeug in der Data Science und wird häufig für Vorhersagen und Analyseaufgaben eingesetzt.


#### **Grundidee der linearen Regression**

Die lineare Regression versucht, eine Gerade zu finden, die den Zusammenhang zwischen den Variablen möglichst gut beschreibt. Die Gerade wird durch die folgende Gleichung definiert:

$$
y = \beta_0 + \beta_1 \cdot x_1 + \beta_2 \cdot x_2 + \dots + \beta_n \cdot x_n + \epsilon
$$

- \( y \): Abhängige Variable (Zielvariable)  
- \( \beta_0 \): Achsenabschnitt (Intercept)  
- \( \beta_1, \beta_2, \dots, \beta_n \): Koeffizienten der unabhängigen Variablen  
- \( x_1, x_2, \dots, x_n \): Unabhängige Variablen (Prädiktoren)  
- \( \epsilon \): Fehlerterm  

Die Koeffizienten \( \beta \) geben die Stärke und Richtung des Einflusses jeder unabhängigen Variable auf die Zielvariable an.


#### **Wann verwendet man die lineare Regression?**

Die lineare Regression ist geeignet, wenn:
- Es einen linearen Zusammenhang zwischen den Variablen gibt.  
- Die Zielvariable kontinuierlich ist (z. B. Preis, Temperatur, Umsatz).  
- Das Ziel darin besteht, die Beziehung zwischen Variablen zu quantifizieren oder Vorhersagen zu treffen.

Beispielanwendungen:
- Vorhersage des Hauspreises basierend auf Fläche und Lage.  
- Analyse der Verkaufszahlen im Zusammenhang mit Werbeausgaben.  



#### **Beispiel: Einfache lineare Regression in Python**

Angenommen, wir haben Daten über den Flächeninhalt eines Hauses (\( x \)) und dessen Preis (\( y \)) und möchten eine Vorhersage treffen:

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression

# Beispiel-Daten
x = np.array([50, 60, 70, 80, 90]).reshape(-1, 1)  # Fläche in Quadratmetern
y = np.array([150000, 180000, 210000, 240000, 270000])  # Preis in Euro

# Lineares Regressionsmodell
model = LinearRegression()
model.fit(x, y)

# Vorhersage
y_pred = model.predict(x)

# Visualisierung
plt.scatter(x, y, color="blue", label="Datenpunkte")
plt.plot(x, y_pred, color="red", label="Regressionslinie")
plt.xlabel("Fläche (m²)")
plt.ylabel("Preis (€)")
plt.title("Lineare Regression: Fläche vs. Preis")
plt.legend()
plt.show()

# Ausgeben der Koeffizienten
print("Steigung (β1):", model.coef_[0])
print("Achsenabschnitt (β0):", model.intercept_)
```



#### **Erweiterung: Multiple lineare Regression**

Wenn es mehrere unabhängige Variablen gibt (z. B. Fläche, Anzahl der Zimmer, Baujahr), spricht man von **multipler linearer Regression**. Die Grundidee bleibt gleich, aber die Berechnung umfasst mehrere Prädiktoren:

$$
y = \beta_0 + \beta_1 \cdot x_1 + \beta_2 \cdot x_2 + \dots + \beta_n \cdot x_n
$$

Beispiel in Python:
```python
# Beispiel-Daten für multiple Regression
X = np.array([[50, 2], [60, 3], [70, 3], [80, 4], [90, 4]])  # Fläche, Zimmeranzahl
y = np.array([150000, 180000, 210000, 240000, 270000])       # Preis

# Modell trainieren
model = LinearRegression()
model.fit(X, y)

# Ausgeben der Koeffizienten
print("Koeffizienten:", model.coef_)
print("Achsenabschnitt (β0):", model.intercept_)
```

**Ergebnis:**
Die Koeffizienten geben an, wie stark sich der Preis verändert, wenn z. B. die Fläche um einen Quadratmeter oder die Zimmeranzahl um eins steigt.


#### **Evaluierung des Modells**

Um die Güte der linearen Regression zu bewerten, wird häufig der **R²-Wert** (Bestimmtheitsmaß) verwendet. Er gibt an, wie gut die unabhängigen Variablen die Zielvariable erklären können. Ein Wert von 1 bedeutet eine perfekte Anpassung, ein Wert von 0 bedeutet, dass die unabhängigen Variablen keinen Einfluss haben.

Beispiel:
```python
print("R²-Wert:", model.score(X, y))
```