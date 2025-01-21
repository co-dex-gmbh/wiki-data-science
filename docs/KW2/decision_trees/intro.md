**Entscheidungsbäume – Eine Einführung**

Entscheidungsbäume sind ein Werkzeug im Bereich des überwachten maschinellen Lernens. Sie dienen dazu, Entscheidungsprozesse in einer baumartigen Struktur abzubilden. Dabei können Entscheidungsbäume sowohl für Klassifikationsaufgaben, bei denen Kategorien vorhergesagt werden, als auch für Regressionsaufgaben, bei denen kontinuierliche Werte vorhergesagt werden, eingesetzt werden.

Das Besondere an Entscheidungsbäumen ist ihre einfache und intuitive Struktur. Sie bestehen aus einem Stammknoten, mehreren inneren Knoten (Entscheidungsknoten) und Blattknoten (Endknoten). Jeder Knoten repräsentiert dabei eine Frage oder Bedingung zu einem bestimmten Merkmal des Datensatzes, und die Verzweigungen geben die möglichen Antworten auf diese Frage an. Die Blattknoten stehen schließlich für die Ergebnisse oder Vorhersagen.

![Entscheidungsbaum](https://www.ibm.com/content/dam/connectedassets-adobe-cms/worldwide-content/cdp/cf/ul/g/10/3c/Decision-Tree-Example.component.complex-narrative-xl-retina.ts=1665767756305.png/content/adobe-cms/de/de/topics/decision-trees/jcr:content/root/table_of_contents/body/content_section_styled/content-section-body/complex_narrative/items/content_group_1441304462/image)


## Motivation
Entscheidungsbäume bieten eine Möglichkeit, komplexe Entscheidungsprozesse auf eine klare und interpretierbare Weise abzubilden. Ihre visuelle Baumstruktur ermöglicht es, Entscheidungslogiken leicht zu verstehen und bietet Einblicke in die Daten, ohne komplexe mathematische Modelle zu fordern. Diese Flexibilität macht Entscheidungsbäume zu einem beliebten Werkzeug in verschiedenen Anwendungsbereichen, von der Klassifikation bis zur Regression. Mit ihrer Fähigkeit, sowohl numerische als auch kategoriale Daten zu handhaben, erfordern sie weniger Datenvorbereitungsaufwand und bieten gleichzeitig Robustheit gegenüber unterschiedlichen Skalierungen der Merkmale. Die Leichtigkeit ihrer Anpassung an nichtlineare Zusammenhänge und ihre Effizienz bei großen Datensätzen machen sie zu einer motivierenden Wahl für datengetriebene Entscheidungsfindung.

## Begriffe

**Wurzelknoten**: Der oberste Knoten im Baum, der die gesamte Bevölkerung darstellt, die in Untergruppen aufgeteilt werden soll.

**Zweige**: Ein Zweig repräsentiert eine mögliche Antwort auf eine Funktion.

**Blattknoten**: Ein Blattknoten repräsentiert eine Entscheidung oder ein Ergebnis. Es gibt keine untergeordneten Knoten.

**Interne Knoten**: Ein interner Knoten repräsentiert eine Funktion, die eine Entscheidung trifft, wo der nächste Knoten zu finden ist.

**Tiefe des Baumes**: Die Länge des längsten Pfades von der Wurzel bis zu einem Blatt.

## Lernprozess
Der Lernprozess von Entscheidungsbäumen basiert auf einer "Teile-und-Herrsche-Strategie", die durch eine "gierige" Suche optimale Teilungspunkte innerhalb des Baums ermittelt. Diese Aufteilung erfolgt rekursiv von oben nach unten, bis die meisten Datenpunkte bestimmten Klassen zugeordnet sind. Die Komplexität des Baums beeinflusst, ob alle Datenpunkte homogene Mengen oder gemischte Klassen repräsentieren. Kleine Bäume neigen dazu, reine Blattknoten zu erreichen, während größere Bäume zur Fragmentierung und möglicher Überanpassung neigen. Entsprechend dem Prinzip der Sparsamkeit in Occams Razor sollten Entscheidungsbäume die Komplexität nur dann erhöhen, wenn nötig, da die einfachste Erklärung oft die beste ist.

Um Überanpassung zu vermeiden, wird üblicherweise "Zurechtschneiden" (Pruning) angewendet, indem unwichtige Zweige entfernt werden. Die Modellbewertung erfolgt oft durch Kreuzvalidierung. Ein weiterer Ansatz zur Erhaltung der Genauigkeit ist die Verwendung von Ensemble-Methoden wie dem Random-Forest-Algorithmus, der präzisere Vorhersagen ermöglicht, insbesondere wenn die einzelnen Bäume unkorreliert sind. Dieser Ansatz unterstreicht die Vielseitigkeit und Anpassungsfähigkeit von Entscheidungsbäumen in datengetriebenen Entscheidungsfindungsprozessen.


### **Wie funktionieren Entscheidungsbäume?**

Entscheidungsbäume nutzen das Prinzip „Teile und herrsche“. Sie zerlegen die Daten schrittweise in immer kleinere Teilmengen, bis diese möglichst homogen sind. Die grundlegende Idee ist es, bei jedem Schritt das Merkmal auszuwählen, das die Daten am besten in Klassen oder Wertebereiche trennt. Diese Trennung erfolgt durch sogenannte **Split-Kriterien**, wie etwa:

- **Gini-Index**: Misst die „Unreinheit“ eines Knotens.
- **Informationsgewinn**: Bewertet, wie viel Unsicherheit durch den Split reduziert wird.
- **Varianzreduktion**: Wird bei Regressionsbäumen verwendet, um die Streuung der Zielvariablen zu minimieren.

Ein Entscheidungsbaum startet immer beim Stammknoten, der alle Daten enthält, und spaltet diese rekursiv auf. Der Algorithmus stoppt, wenn entweder alle Knoten homogen sind oder eine festgelegte Bedingung erreicht ist, wie die maximale Tiefe des Baums oder eine minimale Anzahl von Datenpunkten pro Knoten.

#### **Ein kleines Beispiel**

Angenommen, wir haben einen Datensatz, der die folgenden Merkmale enthält:
- Wetter (sonnig, bewölkt, regnerisch)
- Temperatur (hoch, mittel, niedrig)
- Luftfeuchtigkeit (hoch, niedrig)
- Wind (stark, schwach)

Die Zielvariable ist, ob wir Fußball spielen („ja“ oder „nein“). Ein Entscheidungsbaum könnte wie folgt aufgebaut sein:

1. Der Stammknoten entscheidet zuerst, ob das Wetter „sonnig“, „bewölkt“ oder „regnerisch“ ist.
2. Wenn es „sonnig“ ist, wird der nächste Knoten nach der Luftfeuchtigkeit gefragt.
3. Wenn es „regnerisch“ ist, entscheidet der Baum anhand der Windstärke.
4. Die Blätter repräsentieren die Entscheidungen: „ja“ oder „nein“.

Das Entscheidungsverfahren könnte dann etwa lauten:  
„Wenn das Wetter regnerisch und der Wind stark ist, spielen wir nicht. Wenn es bewölkt ist, spielen wir immer.“

---

### **Vorteile und Nachteile von Entscheidungsbäumen**

#### Vorteile:
- **Einfach und intuitiv**: Die Struktur eines Entscheidungsbaums ist leicht verständlich, auch für Personen ohne tiefes technisches Wissen.
- **Transparenz**: Entscheidungsprozesse können klar nachvollzogen werden, da jede Entscheidung im Baum logisch dargestellt ist.
- **Flexibilität**: Entscheidungsbäume können sowohl für Klassifikations- als auch für Regressionsprobleme verwendet werden.

#### Nachteile:
- **Überanpassung (Overfitting)**: Entscheidungsbäume neigen dazu, sich stark an die Trainingsdaten anzupassen, insbesondere wenn sie sehr tief werden.
- **Instabilität**: Kleine Änderungen in den Daten können große Auswirkungen auf die Baumstruktur haben.
- **Begrenzte Genauigkeit**: Einzelne Entscheidungsbäume können im Vergleich zu anderen Modellen, wie z. B. Random Forests, weniger genau sein.

---

### **Anwendungsbeispiel in Python**

Hier ein Beispiel, wie ein Entscheidungsbaum mit dem Iris-Datensatz trainiert und visualisiert werden kann:

```python
from sklearn.datasets import load_iris
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
import matplotlib.pyplot as plt

# Datensatz laden
iris = load_iris()
X, y = iris.data, iris.target

# Entscheidungsbaum-Klassifikator erstellen
clf = DecisionTreeClassifier(max_depth=3, random_state=42)
clf.fit(X, y)

# Entscheidungsbaum visualisieren
plt.figure(figsize=(12, 8))
tree.plot_tree(clf, feature_names=iris.feature_names, class_names=iris.target_names, filled=True)
plt.show()
```

In diesem Beispiel wird ein Entscheidungsbaum erstellt, der die Blumenarten des Iris-Datensatzes klassifiziert. Die Visualisierung zeigt, welche Merkmale (z. B. „petal length“) und Schwellenwerte für die Entscheidungen im Baum herangezogen werden.

#### **Interpretation der Visualisierung**
- Jeder Knoten zeigt das Merkmal und den Schwellenwert, der für den Split verwendet wurde.
- Unterhalb der Entscheidung stehen die Anzahl der Datenpunkte in diesem Knoten und die Verteilung auf die Klassen.
- Die Blätter stellen die Vorhersage dar (z. B. „Setosa“).

---

### **Optimierung eines Entscheidungsbaums**

Um die Performance eines Entscheidungsbaums zu verbessern und Überanpassung zu vermeiden, gibt es mehrere Strategien:

- **Pruning (Beschneiden)**: Reduziert die Baumtiefe, indem unwichtige Äste entfernt werden.
- **Maximale Tiefe begrenzen**: Setzt eine Obergrenze für die Anzahl der Schichten im Baum.
- **Minimale Anzahl an Datenpunkten pro Knoten**: Verhindert, dass der Baum zu stark spezialisiert wird.

Hier ein Beispiel für das Beschneiden durch Begrenzung der maximalen Tiefe:

```python
clf_pruned = DecisionTreeClassifier(max_depth=2, random_state=42)
clf_pruned.fit(X, y)

plt.figure(figsize=(12, 8))
tree.plot_tree(clf_pruned, feature_names=iris.feature_names, class_names=iris.target_names, filled=True)
plt.show()
```

In diesem Fall ist der Baum weniger tief, was ihn weniger anfällig für Überanpassung macht.

