# Noch Exkurs: Random Forests

Random Forests sind eine Ensemble-Lernmethode im Bereich des maschinellen Lernens. Sie gehören zur Familie der Entscheidungsbäume und werden für Klassifikationsund Regressionsaufgaben verwendet. Der Hauptgedanke hinter Random Forests ist, mehrere Entscheidungsbäume zu erstellen und ihre Vorhersagen zu kombinieren, um robustere und genaue Modelle zu erhalten. Einen Überblick zu Entscheidungsbäumen findest du [hier](/Algorithmen/decision-trees).

![Random Forest](https://av-eks-blogoptimized.s3.amazonaws.com/33019random-forest-algorithm287548.png)
## Erstellung eines Random Forests

Ein Random Forest besteht aus einer großen Anzahl von Entscheidungsbäumen. Jeder dieser Bäume ist ein Klassifikator, der eine Entschiedung für eine Teilmeng der Ausgangsklassen trifft. Die Vorhersage des Random Forests ist die Klasse, die von den meisten Bäumen vorhergesagt wird. Die Vorhersage eines einzelnen Baumes ist möglicherweise nicht sehr genau, aber wenn wir die Vorhersagen vieler Bäume kombinieren, erhalten wir eine Vorhersage, die genauer ist und weniger anfällig für Rauschen ist. Die Erstellung eines Random Forests kann in mehrere Schritte aufgeteilt werden.


1. **Datensätze auswählen (Bootstrap Aggregating - Bagging):**
   Für jeden Baum aus dem Trainingsdatensatz werden zufällige Stichproben (mit Wiederholung) erstellt. Dies bedeutet, dass einige Datenpunkte mehrfach in einer Stichprobe auftreten können, während andere möglicherweise überhaupt nicht enthalten sind.

2. **Entscheidungsbaum erstellen:**
   Für jede erstellte Stichprobe wird ein Entscheidungsbaum trainiert. Bei jedem Schritt des Baumwachstums wird nur eine zufällige Teilmenge der Features berücksichtigt, um die Unabhängigkeit der Bäume sicherzustellen.

3. **Ensemble bilden:**
   Die erstellten Entscheidungsbäume bilden das Ensemble des Random Forests.

4. **Vorhersage erstellen:**
   Für eine neue Instanz wird die Vorhersage durch Aggregation der Vorhersagen aller Bäume erstellt. Bei Klassifikationsaufgaben erfolgt dies oft durch Mehrheitsabstimmung, und bei Regressionsaufgaben wird der Durchschnitt der Vorhersagen genommen.

5. **Out-of-Bag (OOB) Bewertung:**
   Da verschiedene Bäume verschiedene Teilmengen der Daten sehen, können Datenpunkte, die in einem Baum nicht verwendet wurden, für die Bewertung der Modellgenauigkeit verwendet werden. Diese Technik wird als Out-of-Bag (OOB) Bewertung bezeichnet.

6. **Feature Importance:**
   Random Forests bieten eine Möglichkeit zur Berechnung der Bedeutung einzelner Features. Dies geschieht durch die Analyse, wie sehr sich die Genauigkeit des Modells ändert, wenn die Werte eines Features permutiert werden.

7. **Anzahl der Bäume und Hyperparameter:**
   Die Anzahl der Bäume (Estimators) und andere Hyperparameter des Random Forests können je nach Anwendungsfall angepasst werden, um die Modellleistung zu optimieren.

Der Schlüsselaspekt eines Random Forests ist die Randomisierung sowohl in Bezug auf die Daten (durch Bagging) als auch in Bezug auf die Features (durch zufällige Auswahl von Features bei jedem Split des Entscheidungsbaums). Diese Randomisierung trägt dazu bei, Overfitting zu reduzieren und die Robustheit des Modells zu verbessern.


## Exkurs: Bootstrapping

Bootstrapping ist eine statistische Methode, die dazu dient, Schätzungen der Verteilung von Schätzern zu erstellen. Der Begriff "Bootstrapping" leitet sich von der Vorstellung ab, dass man sich an den eigenen Stiefelriemen zieht, was darauf hinweist, dass man aus den vorhandenen Daten selbst weitere Stichproben erstellt.

Der Bootstrapping-Prozess erfolgt in folgenden Schritten:

1. **Stichprobe erstellen:**
   Aus einem vorhandenen Datensatz wird eine zufällige Stichprobe mit Wiederholung gezogen. Das bedeutet, dass bestimmte Datenpunkte mehrmals in der Stichprobe erscheinen können, während andere möglicherweise überhaupt nicht ausgewählt werden.

2. **Schätzung berechnen:**
   Mit der erstellten Stichprobe wird eine Schätzung (z. B. Mittelwert, Median, Standardabweichung) des interessierenden Parameters berechnet.

3. **Schritte wiederholen:**
   Die Schritte 1 und 2 werden viele Male wiederholt (typischerweise Tausende von Malen), um eine Verteilung der Schätzungen zu erstellen.

4. **Verteilung analysieren:**
   Durch Analyse der Verteilung der Schätzungen können Konfidenzintervalle und andere statistische Eigenschaften des geschätzten Parameters abgeleitet werden.

Bootstrapping ist besonders nützlich, wenn die analytischen Lösungen kompliziert oder nicht verfügbar sind. Es ermöglicht auch, die Unsicherheit von Schätzern zu quantifizieren, indem man mehrere Stichproben aus denselben Daten erstellt. Bootstrapping wird in verschiedenen Bereichen der Statistik und des maschinellen Lernens verwendet, um bessere Schätzungen von Parametern und deren Unsicherheiten zu erhalten.

**Beispiel:**
```python
from sklearn.utils import resample
from sklearn.datasets import load_iris

# Lade den Iris-Datensatz für das Beispiel
iris = load_iris()
X = iris.data
y = iris.target

# Beispiel für Bootstrapping
def bootstrap_example(data):
    # Erzeuge eine Bootstrap-Stichprobe
    bootstrap_sample = resample(data, replace=True, n_samples=len(data))
    print("Originaldaten:", data[:5])
    print("Bootstrapped Stichprobe:", bootstrap_sample[:5])

# Bootstrapping-Beispiel
print("Bootstrapping-Beispiel:")
bootstrap_example(X)
```

### Exkurs: Bagging(Bootstrap Aggregating)

Bagging (Bootstrap Aggregating) ist eine Ensemble-Lernmethode im Bereich des maschinellen Lernens. Es basiert auf dem Prinzip des Bootstrapping und wird verwendet, um die Vorhersagegenauigkeit und Stabilität von Modellen zu verbessern, insbesondere von Entscheidungsbäumen.

Hier sind die Grundprinzipien des Bagging:

1. **Bootstrapping:**
   Es werden zufällige Stichproben (mit Wiederholung) aus dem Trainingsdatensatz gezogen, um mehrere "bootstrapped" Datensätze zu erstellen.

2. **Modelle erstellen:**
   Auf jedem der bootstrapped Datensätze wird ein separates Modell (typischerweise ein Entscheidungsbaum) trainiert. Da die Datensätze unterschiedlich sind, werden auch die erstellten Modelle unterschiedlich sein.

3. **Aggregation der Vorhersagen:**
   Die Vorhersagen der einzelnen Modelle werden kombiniert, um eine Gesamtvorhersage zu erstellen. Bei Klassifikationsaufgaben geschieht dies oft durch Mehrheitsabstimmung, und bei Regressionsaufgaben wird der Durchschnitt der Vorhersagen genommen.

Der Hauptvorteil von Bagging liegt darin, dass es die Varianz des Modells reduziert, indem es die Modelle auf unterschiedlichen Daten trainiert und dann ihre Vorhersagen aggregiert. Dies hilft, Overfitting zu minimieren und die Modellleistung auf neuen Daten zu verbessern.

Random Forests, einer der bekanntesten Anwendungsbereiche von Bagging, verwenden diese Methode, indem sie mehrere Entscheidungsbäume auf unterschiedlichen Teilmengen des Datensatzes trainieren und deren Vorhersagen kombinieren. Bagging kann jedoch auch mit anderen Basisalgorithmen verwendet werden.

**Beispiel:**
```python
from sklearn.ensemble import BaggingClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Lade den Iris-Datensatz für das Beispiel
iris = load_iris()
X = iris.data
y = iris.target

# Beispiel für Bagging mit Entscheidungsbaum
def bagging_example(X_train, X_test, y_train, y_test):
    # Erzeuge Entscheidungsbaum-Modell
    base_model = DecisionTreeClassifier(random_state=42)
    
    # Erzeuge Bagging-Modell
    bagging_model = BaggingClassifier(base_model, n_estimators=10, random_state=42)
    
    # Trainiere das Bagging-Modell
    bagging_model.fit(X_train, y_train)
    
    # Vorhersagen
    predictions = bagging_model.predict(X_test)
    
    # Auswertung der Genauigkeit
    accuracy = accuracy_score(y_test, predictions)
    print("Bagging-Modell Genauigkeit:", accuracy)

# Aufteilung der Daten in Trainings- und Testsets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Bagging-Beispiel mit Entscheidungsbaum
print("\nBagging-Beispiel:")
bagging_example(X_train, X_test, y_train, y_test)
```


## Kombination von Entscheidungsbäumen

Bei einem Random Forest gibt es verschiedene Möglichkeiten, die Vorhersagen der einzelnen Bäume zu kombinieren. Diese Kombinationsstrategien sind wichtig, um eine robuste und genaue Gesamtvorhersage zu erstellen. Hier sind die Hauptmethoden:

1. **Mehrheitsabstimmung (Classification):**
   In Klassifikationsaufgaben wird die Klasse ausgewählt, die von den meisten Bäumen vorhergesagt wird. Dies wird als Mehrheitsabstimmung oder Mehrheitsregel bezeichnet. Die Klasse mit den meisten Stimmen wird als endgültige Vorhersage verwendet.

2. **Durchschnitt (Regression):**
   In Regressionsaufgaben wird der Durchschnitt der Vorhersagen aller Bäume genommen. Dies führt zu einer stabilen und konsistenten Vorhersage, die weniger anfällig für Ausreißer ist.

3. **Gewichtete Kombination:**
   Es besteht die Möglichkeit, den Vorhersagen der Bäume Gewichte zuzuweisen. Bäume mit höherer Genauigkeit oder Vertrauenswürdigkeit können höhere Gewichte erhalten. Dies ermöglicht eine feinere Steuerung über den Einfluss einzelner Bäume.

4. **Soft Voting (Classification):**
   Anstelle einer harten Mehrheitsabstimmung, bei der einfach die Klasse mit den meisten Stimmen ausgewählt wird, kann auch eine weiche Mehrheitsabstimmung durchgeführt werden. Dabei werden die Wahrscheinlichkeiten für jede Klasse aus den Bäumen aggregiert, und die Klasse mit der höchsten aggregierten Wahrscheinlichkeit wird ausgewählt.

5. **Out-of-Bag (OOB) Schätzung:**
   Bei der Trainingsphase des Random Forests wird für jeden Baum eine OOB-Schätzung erstellt, indem der Baum auf den nicht für die Stichprobe ausgewählten Daten getestet wird. Die Vorhersagen aller Bäume werden dann kombiniert, um eine Gesamtschätzung zu erhalten.

Die Wahl der Kombinationsstrategie hängt von der Art des Problems (Klassifikation oder Regression) und dem Anwendungsfall ab. In der Praxis hat sich die Mehrheitsabstimmung als effektive Methode für Klassifikationsprobleme und der Durchschnitt für Regressionsprobleme bewährt.

## Random Forest vs Decision Tree

Die Wahl zwischen einem Random Forest und einem einzelnen Entscheidungsbaum hängt von den Anforderungen des Problems, der Größe des Datensatzes und den verfügbaren Rechenressourcen ab. In vielen Fällen bieten Random Forests jedoch eine robuste Lösung mit verbesserter Vorhersagegenauigkeit.

**Vorteile von Random Forests gegenüber Entscheidungsbäumen:**

1. **Reduziert Overfitting:**
   Random Forests sind weniger anfällig für Overfitting im Vergleich zu einzelnen Entscheidungsbäumen. Die Randomisierung bei der Erstellung von Teilbäumen trägt dazu bei, dass die Gesamtvorhersage des Modells robuster und besser verallgemeinerungsfähig ist.

2. **Höhere Genauigkeit:**
   In der Regel liefern Random Forests aufgrund ihrer Ensemble-Natur eine höhere Genauigkeit bei Vorhersagen. Indem sie mehrere Entscheidungsbäume kombinieren, reduzieren sie die Varianz und verbessern die Vorhersageleistung.

3. **Bessere Generalisierung:**
   Durch die Verwendung verschiedener Teilmengen der Daten und Features bei jedem Baum verbessern Random Forests die Generalisierungsfähigkeit des Modells. Dies ist besonders wichtig, wenn der Trainingsdatensatz begrenzt ist.

4. **Automatische Feature-Selektion:**
   Random Forests führen eine automatische Feature-Selektion durch, indem sie die Wichtigkeit der Features bewerten. Dies kann dazu beitragen, irrelevante oder redundante Features zu eliminieren.

5. **Out-of-Bag (OOB) Schätzung:**
   Random Forests ermöglichen die Verwendung von Out-of-Bag-Schätzungen, bei denen jedes Beispiel durchschnittlich etwa in einem Drittel der Bäume ausgelassen wird. Dies bietet eine interne Schätzung der Modellgenauigkeit.

**Nachteile von Random Forests gegenüber Entscheidungsbäumen:**

1. **Komplexität und Rechenressourcen:**
   Random Forests sind aufgrund der Notwendigkeit, mehrere Bäume zu trainieren und zu kombinieren, rechenintensiver und komplexer als einzelne Entscheidungsbäume. Dies kann zu längeren Trainingszeiten führen.

2. **Schwer interpretierbar:**
   Die Kombination mehrerer Bäume macht Random Forests schwerer interpretierbar im Vergleich zu einzelnen Entscheidungsbäumen. Es ist schwieriger, den genauen Einfluss jedes Features auf die Vorhersagen zu verstehen.

3. **Overhead durch Randomisierung:**
   In einigen Fällen kann die Randomisierung zu einem gewissen Overhead führen, insbesondere wenn der Datensatz klein ist oder die Features nicht stark differenzierend sind. In solchen Fällen kann ein einfacher Entscheidungsbaum möglicherweise effizienter sein.

4. **Unnötig für klare Zusammenhänge:**
   Wenn die zugrundeliegenden Zusammenhänge im Datensatz bereits einfach und klar sind, kann die Komplexität von Random Forests unnötig sein. In solchen Fällen könnte ein einfacher Entscheidungsbaum ausreichen.


## Referenzen und Nachschlagewerke

- [Listandata.com](https://www.listendata.com/2014/11/random-forest-with-r.html)
- [IMB](https://www.ibm.com/topics/random-forest)
- [Youtube: Visual Guide to Random Forests](https://www.youtube.com/watch?v=cIbj0WuK41w)