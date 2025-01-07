### **Split-Kriterien in Entscheidungsbäumen**

Ein zentraler Aspekt bei der Konstruktion eines Entscheidungsbaums ist die Auswahl des besten Merkmals (Spalte) und des besten Schwellenwerts, um die Daten an jedem Knoten aufzuteilen. Dieses Verfahren wird durch **Split-Kriterien** gesteuert. Ein gutes Split-Kriterium sorgt dafür, dass die resultierenden Untergruppen möglichst „rein“ sind, also nur wenige Klassenmischungen oder Varianzen aufweisen. Im Folgenden werden die gängigsten Split-Kriterien und ihre Bedeutung erklärt:

---

#### **1. Informationsgewinn (Information Gain)/ Entropieverlust**

Der Informationsgewinn misst, wie viel Unsicherheit (Entropie) durch eine Aufteilung der Daten reduziert wird. Die Entropie beschreibt dabei die Unordnung oder Unsicherheit in einer Menge. Ziel ist es, die Entropie nach einem Split möglichst gering zu halten, also eine maximale Homogenität in den Untergruppen zu erreichen.

**Formel für den Informationsgewinn**:
$$
\text{Informationsgewinn} = \text{Entropie}(D) - \sum_{i=1}^{k} \frac{|D_i|}{|D|} \cdot \text{Entropie}(D_i)
$$

- \( D \): Die Datenmenge vor dem Split.  
- \( D_i \): Die Untergruppen nach dem Split.  
- \( k \): Anzahl der Untergruppen.




**Definition der Entropie**

Die **Entropie** ist ein Maß für die Unordnung oder Unsicherheit in einem Datensatz. Sie stammt aus der Informationstheorie und beschreibt, wie viel Information benötigt wird, um die Klasse eines Elements korrekt vorherzusagen. Ein Datensatz mit hoher Entropie ist stark gemischt, während ein Datensatz mit niedriger Entropie sehr homogen ist.


Die Entropie wird wie folgt berechnet:

$$
H(D) = - \sum_{i=1}^{n} p_i \cdot \log_2(p_i)
$$

- \( H(D) \): Entropie des Datensatzes \( D \)  
- \( n \): Anzahl der Klassen  
- \( p_i \): Wahrscheinlichkeit der Klasse \( i \) im Datensatz (Anteil der Klasse \( i \) an den Gesamtbeispielen)  

Die Entropie erreicht:
- **0**, wenn alle Beispiele zu einer einzigen Klasse gehören (maximale Homogenität).  
- **1**, wenn alle Klassen gleichmäßig verteilt sind (maximale Unordnung).  


#### **Beispiel**
Angenommen, wir haben einen Datensatz mit 10 Einträgen, die auf zwei Klassen verteilt sind:
- Klasse A: 6 Einträge  
- Klasse B: 4 Einträge  

Die Wahrscheinlichkeiten sind:
$$
p_A = \frac{6}{10} = 0.6, \quad p_B = \frac{4}{10} = 0.4
$$

Die Entropie berechnet sich dann wie folgt:
$$
H(D) = - (0.6 \cdot \log_2(0.6) + 0.4 \cdot \log_2(0.4))
$$

Die Logarithmen können näherungsweise berechnet werden:
$$
\log_2(0.6) \approx -0.51, \quad \log_2(0.4) \approx -0.92
$$

Eingesetzt ergibt sich:
$$
H(D) = - (0.6 \cdot -0.51 + 0.4 \cdot -0.92) \approx 0.67
$$

Die Entropie des Datensatzes beträgt also **0.67**, was darauf hinweist, dass die Daten mäßig gemischt sind.

**Beispiel in Python**:
Hier wird demonstriert, wie der Informationsgewinn bei einer binären Aufteilung berechnet werden kann.

```python
from math import log2

# Funktion zur Berechnung der Entropie
def entropy(classes):
    total = sum(classes)
    return -sum((count / total) * log2(count / total) for count in classes if count > 0)

# Beispiel: Vor dem Split
classes_before = [30, 20]  # 30 positive, 20 negative Beispiele
entropy_before = entropy(classes_before)

# Beispiel: Nach dem Split
split_classes = [[20, 10], [10, 10]]  # Zwei Gruppen nach dem Split
entropy_after = sum((sum(group) / sum(classes_before)) * entropy(group) for group in split_classes)

# Informationsgewinn
info_gain = entropy_before - entropy_after
print("Informationsgewinn:", info_gain)
```

---

#### **2. Gini-Index**

Der Gini-Index misst die Wahrscheinlichkeit, dass ein zufällig ausgewähltes Element falsch klassifiziert wird, wenn es entsprechend der Verteilung der Datenpunkte im Knoten klassifiziert wird. Ein niedriger Gini-Index deutet auf eine hohe Reinheit hin.

**Formel für den Gini-Index**:
$$
\text{Gini-Index} = 1 - \sum_{i=1}^{n} (p_i)^2
$$

- \( p_i \): Anteil der Klasse \( i \) an den Daten.  

**Beispiel in Python**:
Berechnung des Gini-Index für eine einzelne Gruppe:

```python
def gini(classes):
    total = sum(classes)
    return 1 - sum((count / total) ** 2 for count in classes)

# Beispiel: Daten vor und nach einem Split
classes_before = [30, 20]
gini_before = gini(classes_before)

split_classes = [[20, 10], [10, 10]]
gini_after = sum((sum(group) / sum(classes_before)) * gini(group) for group in split_classes)

print("Gini vor dem Split:", gini_before)
print("Gini nach dem Split:", gini_after)
```

Der Gini-Index wird in der Praxis häufig verwendet, da er einfacher zu berechnen ist als der Informationsgewinn und in vielen Szenarien ähnliche Ergebnisse liefert.

---

#### **3. Varianzreduktion**

Die Varianzreduktion ist ein Split-Kriterium, das vor allem bei Regressionsbäumen verwendet wird. Es misst, wie stark die Streuung der Zielvariablen durch den Split reduziert wird. Ziel ist es, die Varianz der Zielwerte in den Untergruppen so gering wie möglich zu halten.

**Formel für die Varianzreduktion**:
$$
\text{Varianzreduktion} = \text{Varianz}(D) - \sum_{i=1}^{k} \frac{|D_i|}{|D|} \cdot \text{Varianz}(D_i)
$$

- \( \text{Varianz}(D) \): Streuung der Zielwerte in den ursprünglichen Daten.  

**Beispiel in Python**:
Hier wird demonstriert, wie die Varianzreduktion berechnet werden kann.

```python
import numpy as np

# Funktion zur Berechnung der Varianz
def variance(data):
    return np.var(data)

# Zielwerte vor dem Split
values_before = [2, 3, 4, 5, 6, 7]
variance_before = variance(values_before)

# Zielwerte nach dem Split
split_values = [[2, 3, 4], [5, 6, 7]]
weighted_variance = sum((len(group) / len(values_before)) * variance(group) for group in split_values)

variance_reduction = variance_before - weighted_variance
print("Varianzreduktion:", variance_reduction)
```

---

### **Wann und warum diese Kriterien verwenden?**

Die Wahl des Split-Kriteriums hängt stark von der Art des Problems und der Zielsetzung ab:
- **Informationsgewinn**: Besonders nützlich bei Klassifikationsproblemen mit einer ungleichen Verteilung der Klassen. Es berücksichtigt explizit die Unsicherheit.
- **Gini-Index**: Einfacher zu berechnen als der Informationsgewinn und oft bei großen Datensätzen vorteilhaft.
- **Varianzreduktion**: Wird ausschließlich bei Regressionsproblemen verwendet, da sie auf numerischen Zielvariablen basiert.

In der Praxis verwenden die meisten Algorithmen, wie `DecisionTreeClassifier` in Scikit-learn, den Gini-Index als Standardkriterium für Klassifikationsaufgaben und die Varianzreduktion für Regressionsbäume. 

