## Generalisierung

Generalisierung beschreibt, wie gut sich ein Modell an die Daten anpassunt und wie gut es auf ungesehenen, neuen Daten zurechtkommt

## Test/ Train Split

Wir benutzen ein Splitting zwischen Test- und Trainingsdaten, um unsere Modelle auf ungesehenen Daten zu validieren. Diesen können wir beispielsweise durch die Verwendung der funktion `train_test_split` aus `sklearn.model_selection` erstellen.

```
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

## Overfitting

Overfitting tritt auf, wenn ein Modell zu stark an die Trainingsdaten angepasst ist und dadurch auf neuen, bisher ungesehenen Daten schlecht generalisiert. Overfitting hat daher direkte Auswirkungen auf die Leistungsfähigkeit und die Vorhersagegenauigkeit von Modellen.

Grund für das OVerfitting ist, dass ein Modell die Trainingsdaten zu genau erfasst, einschließlich ihrer Rauschen und Ausreißer. Das Modell passt sich den Daten so stark an, dass es spezifische Muster und Details lernt, die nicht notwendigerweise auf neuen Daten vorhanden sind. Im Gegensatz dazu steht Underfitting, bei dem das Modell zu einfach ist und selbst die Trainingsdaten nicht gut erklären kann.

### Ursachen von Overfitting:

1. **Komplexität des Modells:** Modelle mit zu vielen Parametern oder zu hoher Komplexität neigen dazu, die Trainingsdaten zu genau zu erfassen und übermäßig auf Muster zu reagieren, die nicht repräsentativ sind.

2. **Mangel an Trainingsdaten:** Wenn die Menge an Trainingsdaten begrenzt ist, besteht die Gefahr, dass das Modell nicht genügend Vielfalt lernt und stattdessen spezifische Beispiele auswendig lernt.

3. **Rauschen in den Daten:** Wenn die Trainingsdaten Rauschen oder zufällige Schwankungen enthalten, kann das Modell versuchen, auch dieses Rauschen zu modellieren, was zu Overfitting führt.

### Anzeichen von Overfitting:

1. **Hohe Genauigkeit auf Trainingsdaten, niedrige Genauigkeit auf Testdaten:** Ein überangepasstes Modell wird auf den Trainingsdaten sehr genau sein, aber auf neuen Daten schlecht abschneiden.

2. **Instabile Modellparameter:** Kleine Änderungen in den Trainingsdaten können zu erheblichen Veränderungen in den Modellparametern führen.

3. **Overly Complex Decision Boundaries:** Visualisierungen von Entscheidungsgrenzen zeigen, dass überangepasste Modelle dazu neigen, zu komplexe Formen zu erzeugen, um alle Trainingsdaten zu berücksichtigen.

### Methoden zur Vermeidung von Overfitting:

1. **Kreuzvalidierung:** Verwenden Sie Kreuzvalidierungstechniken, um die Leistung des Modells auf unabhängigen Testdaten zu bewerten.

2. **Regulierungsmethoden:** Fügen Sie Regularisierungsterme zu den Verlustfunktionen hinzu, um die Größe der Modellparameter zu begrenzen.

3. **Mehr Trainingsdaten:** Erhöhen Sie die Menge an verfügbaren Trainingsdaten, um das Modell mit einer breiteren Vielfalt an Beispielen zu versorgen.

4. **Feature Selection:** Reduzieren Sie die Anzahl der Merkmale oder verwenden Sie Techniken zur Auswahl der wichtigsten Merkmale.


**Underfitting**

Underfitting tritt auf, wenn ein Modell zu einfach ist, um die zugrunde liegenden Strukturen in den Trainingsdaten zu erfassen. Im Gegensatz zum Overfitting, bei dem das Modell zu komplex ist und die Trainingsdaten zu genau erfasst, versagt ein unterangepasstes Modell darin, selbst auf den Trainingsdaten angemessene Vorhersagen zu treffen.

Auslöser für Underfitting ist ein Modell, dass nicht in der Lage ist, die Komplexität der zugrunde liegenden Datenstrukturen zu erfassen. Es entsteht, wenn das Modell zu einfach ist, um die Muster in den Trainingsdaten korrekt zu lernen. Ein unterangepasstes Modell generalisiert schlecht auf neue, bisher ungesehene Daten, da es nicht in der Lage ist, die inhärenten Muster und Zusammenhänge zu verstehen.

### Ursachen von Underfitting:

1. **Zu einfaches Modell:** Modelle mit zu wenigen Parametern oder zu geringer Komplexität können nicht alle relevanten Muster in den Daten erfassen.

2. **Mangel an relevanten Merkmalen:** Wenn wichtige Merkmale in den Daten fehlen oder nicht berücksichtigt werden, kann das Modell nicht angemessen generalisieren.

3. **Fehlerhafte Modellwahl:** Die Auswahl eines Modells, das nicht zur Struktur der Daten passt, kann zu Underfitting führen.

### Anzeichen von Underfitting:

1. **Schlechte Leistung auf Trainingsdaten:** Das Modell erzielt eine niedrige Genauigkeit oder hohe Fehler auf den Trainingsdaten.

2. **Schlechte Generalisierung:** Die Vorhersagen des Modells sind auch auf neuen Daten ungenau und wenig zuverlässig.

3. **Einfache Entscheidungsgrenzen:** Visualisierungen zeigen, dass das Modell zu einfache Entscheidungsgrenzen erzeugt, die nicht den realen Datenverteilungen entsprechen.

### Methoden zur Vermeidung von Underfitting:

1. **Erhöhen der Modellkomplexität:** Verwenden Sie Modelle mit mehr Parametern oder höherer Komplexität, um die Daten besser zu erfassen.

2. **Hinzufügen relevanter Merkmale:** Stellen Sie sicher, dass alle relevanten Merkmale in den Daten berücksichtigt werden.

3. **Anpassung des Modells:** Wählen Sie ein Modell, das besser zur Struktur der Daten passt.

4. **Optimierung von Hyperparametern:** Experimentieren Sie mit verschiedenen Hyperparameterwerten, um die Modellleistung zu verbessern.


## Exkurs: Regularisierung

Regularisierung ist ein Konzept im maschinellen Lernen, das dazu dient, Overfitting in Modellen zu verhindern oder zu verringern, indem zusätzliche Informationen in den Optimierungsprozess einbezogen werden. Overfitting tritt auf, wenn ein Modell zu gut an die Trainingsdaten angepasst ist und sich dadurch auf neuen, bisher ungesehenen Daten schlecht verallgemeinert.

Es gibt zwei Haupttypen der Regularisierung, die in der Praxis häufig verwendet werden:

1. **L1-Regularisierung (Lasso-Regularisierung):**
Bei der L1-Regularisierung wird der Regularisierungsterm zur Loss-Funktion hinzugefügt, der proportional zur absoluten Summe der Modellparameter ist. Dies führt dazu, dass einige der Gewichtungen im Modell auf genau null gesetzt werden können, was zu einer automatischen Feature-Auswahl führt. Die L1-Regularisierung trägt somit dazu bei, das Modell zu vereinfachen und irrelevante Features zu eliminieren.

1. **L2-Regularisierung (Ridge-Regularisierung):**
Im Gegensatz dazu fügt die L2-Regularisierung der Loss-Funktion einen Term hinzu, der proportional zum Quadrat der L2-Norm der Modellparameter ist. Dies verhindert, dass einzelne Gewichtungen dominieren, indem sie dazu neigen, große Gewichtungen zu reduzieren. Die L2-Regularisierung trägt dazu bei, das Modell zu stabilisieren und Overfitting zu verhindern, indem sie die Gewichtungen gleichmäßig verteilt.

Die Regularisierung wird oft in Verbindung mit linearen Regressionen, logistischen Regressionen und neuronalen Netzwerken verwendet, kann aber auch in anderen Modelltypen angewendet werden.

### Warum ist Regularisierung wichtig?

- **Overfitting-Prävention:** Das Hinzufügen von Regularisierungstermen zur Loss-Funktion hilft, Overfitting zu minimieren, indem es das Modell dazu zwingt, nicht zu stark auf die Trainingsdaten zu reagieren.

- **Bessere Verallgemeinerung:** Regularisierung verbessert die Fähigkeit eines Modells, auf neuen Daten, die es nicht während des Trainings gesehen hat, korrekte Vorhersagen zu treffen.

- **Feature-Auswahl:** Insbesondere L1-Regularisierung kann dazu beitragen, irrelevante oder redundante Features zu eliminieren, was die Effizienz des Modells verbessert.

Die Stärke der Regularisierung wird durch einen sogenannten Hyperparameter gesteuert, der während des Trainingsprozesses optimiert wird. Die Wahl des geeigneten Regularisierungsterms hängt von der spezifischen Problemstellung und den Eigenschaften der Daten ab.