### **Modell-Evaluation: Grundlagen und Methoden**

Die Evaluation eines Modells ist ein entscheidender Schritt im Machine Learning-Prozess. Sie hilft uns zu beurteilen, wie gut ein Modell funktioniert, und sicherzustellen, dass es auf neuen, unbekannten Daten gute Vorhersagen treffen kann. Eine fundierte Evaluation ist wichtig, um Überanpassung (Overfitting) oder Unteranpassung (Underfitting) zu vermeiden und die richtige Modellwahl zu treffen.


#### **Ziele der Modell-Evaluation**

Die Hauptziele der Modell-Evaluation sind:
- **Überprüfung der Genauigkeit:** Wie genau sagt das Modell die Zielvariable vorher?  
- **Bewertung der Generalisierungsfähigkeit:** Wie gut performt das Modell auf neuen Daten, die nicht im Training enthalten waren?  
- **Identifikation von Schwächen:** Wo liegen die Stärken und Schwächen des Modells, und wie können sie verbessert werden?


#### **Wichtige Metriken zur Modellbewertung**

Die Wahl der Bewertungsmetrik hängt davon ab, ob es sich um ein Regressions- oder Klassifikationsproblem handelt.



### **1. Klassifikationsmetriken**

#### **Genauigkeit (Accuracy)**  
Die Genauigkeit misst den Anteil der korrekten Vorhersagen an allen Vorhersagen. Sie eignet sich besonders für ausgeglichene Datensätze, bei denen die Klassenverteilung gleichmäßig ist.

**Formel:**  
$$
\text{Accuracy} = \frac{\text{Anzahl der korrekten Vorhersagen}}{\text{Gesamtanzahl der Datenpunkte}}
$$

Beispiel in Python:
```python
from sklearn.metrics import accuracy_score

y_true = [1, 0, 1, 1, 0]  # Wahre Klassen
y_pred = [1, 0, 1, 0, 0]  # Vorhergesagte Klassen

accuracy = accuracy_score(y_true, y_pred)
print("Accuracy:", accuracy)
```



#### **Precision (Präzision)**  
Die Präzision misst den Anteil der korrekt vorhergesagten positiven Klassen an allen als positiv vorhergesagten Klassen. Sie ist wichtig, wenn falsch-positive Vorhersagen (False Positives) minimiert werden sollen.

**Formel:**  
$$
\text{Precision} = \frac{\text{True Positives (TP)}}{\text{True Positives (TP)} + \text{False Positives (FP)}}
$$

Beispiel in Python:
```python
from sklearn.metrics import precision_score

precision = precision_score(y_true, y_pred)
print("Precision:", precision)
```


#### **Recall (Empfindlichkeit/Sensitivität)**  
Der Recall gibt an, wie viele der tatsächlich positiven Klassen korrekt erkannt wurden. Diese Metrik ist relevant, wenn falsch-negative Vorhersagen (False Negatives) vermieden werden sollen.

**Formel:**  
$$
\text{Recall} = \frac{\text{True Positives (TP)}}{\text{True Positives (TP)} + \text{False Negatives (FN)}}
$$

Beispiel in Python:
```python
from sklearn.metrics import recall_score

recall = recall_score(y_true, y_pred)
print("Recall:", recall)
```


#### **F1-Score**  
Der F1-Score ist das harmonische Mittel von Precision und Recall. Er ist nützlich, wenn ein Gleichgewicht zwischen Precision und Recall wichtig ist, z. B. bei unausgeglichenen Datensätzen.

**Formel:**  
$$
F_1 = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}
$$

Beispiel in Python:
```python
from sklearn.metrics import f1_score

f1 = f1_score(y_true, y_pred)
print("F1-Score:", f1)
```


#### **ROC-AUC-Wert (Receiver Operating Characteristic - Area Under Curve)**  
Der ROC-AUC-Wert misst die Trennfähigkeit eines Klassifikationsmodells. Ein Wert von 1 zeigt perfekte Trennung, während ein Wert von 0,5 auf reines Raten hinweist.

**Formel für die AUC:**  
Die Berechnung erfolgt basierend auf der Fläche unter der ROC-Kurve. Die ROC-Kurve selbst zeigt die True Positive Rate (Recall) gegen die False Positive Rate:
$$
\text{False Positive Rate (FPR)} = \frac{\text{False Positives (FP)}}{\text{False Positives (FP)} + \text{True Negatives (TN)}}
$$

Beispiel in Python:
```python
from sklearn.metrics import roc_auc_score

# Wahrscheinlichkeiten für die Klasse 1
y_prob = [0.9, 0.8, 0.3, 0.4, 0.2]

roc_auc = roc_auc_score(y_true, y_prob)
print("ROC-AUC-Wert:", roc_auc)
```

### **2. Regressionsmetriken**

#### **Mittlerer Absoluter Fehler (Mean Absolute Error, MAE)**  
MAE misst den durchschnittlichen absoluten Unterschied zwischen vorhergesagten und tatsächlichen Werten. Diese Metrik ist leicht interpretierbar und eignet sich, wenn alle Fehler gleich gewichtet werden sollen.

**Formel:**  
$$
\text{MAE} = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|
$$

Beispiel in Python:
```python
from sklearn.metrics import mean_absolute_error

y_true = [3.5, 2.8, 4.0, 5.2]
y_pred = [3.6, 2.7, 3.9, 5.1]

mae = mean_absolute_error(y_true, y_pred)
print("MAE:", mae)
```


#### **Mittlerer quadratischer Fehler (Mean Squared Error, MSE)**  
MSE berechnet den durchschnittlichen quadrierten Unterschied zwischen den Vorhersagen und den tatsächlichen Werten. Größere Fehler werden stärker gewichtet, was diese Metrik empfindlich gegenüber Ausreißern macht.

**Formel:**  
$$
\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
$$

Beispiel in Python:
```python
from sklearn.metrics import mean_squared_error

mse = mean_squared_error(y_true, y_pred)
print("MSE:", mse)
```


#### **Wurzel des Mittleren Quadratischen Fehlers (Root Mean Squared Error, RMSE)**  
Die RMSE ist die Quadratwurzel des MSE und hat dieselbe Einheit wie die Zielvariable. Sie ist besonders nützlich, um die Größe der Fehler direkt zu interpretieren.

**Formel:**  
$$
\text{RMSE} = \sqrt{\text{MSE}}
$$

Beispiel in Python:
```python
import numpy as np

rmse = np.sqrt(mse)
print("RMSE:", rmse)
```


#### **Bestimmtheitsmaß (R²-Score)**  
Der R²-Score misst, wie gut das Modell die Varianz der Zielvariable erklärt. Ein Wert von 1 bedeutet perfekte Vorhersagen, ein Wert von 0 deutet darauf hin, dass das Modell nicht besser als der Mittelwert ist.

**Formel:**  

$$
R^2 = 1 - \frac{\sum_{i=1}^{n} (y_i - \hat{y}_i)^2}{\sum_{i=1}^{n} (y_i - \bar{y})^2}
$$

Beispiel in Python:
```python
from sklearn.metrics import r2_score

r2 = r2_score(y_true, y_pred)
print("R²-Wert:", r2)
```


#### **Kreuzvalidierung (Cross-Validation)**

Die Kreuzvalidierung ist eine Methode, um die Modellleistung stabiler zu bewerten. Dabei wird der Datensatz in k-Folds aufgeteilt, und das Modell wird k-mal trainiert und getestet. Dies reduziert die Abhängigkeit von einer einzelnen Datenaufteilung.

Beispiel in Python:
```python
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import LinearRegression

model = LinearRegression()
scores = cross_val_score(model, X, y, cv=5, scoring='r2')

print("R²-Scores aus der Kreuzvalidierung:", scores)
print("Durchschnittlicher R²-Wert:", scores.mean())
```


<!-- #### **Bias-Variance Tradeoff**

Ein zentrales Konzept in der Modell-Evaluation ist der **Bias-Variance Tradeoff**:
- **Bias (Verzerrung):** Wie gut das Modell die zugrunde liegende Beziehung erfasst. Ein Modell mit hohem Bias (z. B. eine zu einfache Annahme) führt zu Underfitting.
- **Variance (Varianz):** Wie stark das Modell auf Trainingsdaten spezialisiert ist. Ein Modell mit hoher Varianz führt zu Overfitting.

Die richtige Balance zwischen Bias und Varianz ist entscheidend für die Generalisierungsfähigkeit eines Modells. -->
