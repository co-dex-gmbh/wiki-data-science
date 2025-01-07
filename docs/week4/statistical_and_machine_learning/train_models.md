# Unser erstes Modell trainieren

Der Ablauf, um ein Modell zu trainieren, ist in der Regel wie folgt:

1. **Daten laden**: Lade die Daten, die du für das Training des Modells verwenden möchtest.
2. **Daten vorbereiten**: Bereite die Daten so auf, dass sie von einem Modell verarbeitet werden können.
3. **Daten aufteilen**: Teile die Daten in Trainings- und Testdaten auf.
4. **Modell erstellen**: Wähle ein Modell aus, das du trainieren möchtest.
5. **Modell trainieren**: Trainiere das Modell mit den vorbereiteten Daten.
6. **Modell evaluieren**: Bewerte das Modell, um zu sehen, wie gut es funktioniert.
7. **Modell anwenden**: Wende das trainierte Modell auf neue Daten an, um Vorhersagen zu treffen.
   

## Date aufteilen

Damit wir wissen, ob unser Modell gut funktioniert, müssen wir es testen. Dazu teilen wir unsere Daten in zwei Teile auf: Trainingsdaten und Testdaten. Die Trainingsdaten verwenden wir, um das Modell zu trainieren, und die Testdaten verwenden wir, um das Modell zu evaluieren. Für das Aufteilen der Daten wird oftmal ein Verhältnis von 80% Trainingsdaten und 20% Testdaten verwendet. 

Je nach größe des Datensets, Verteilung Samples und den Anforderungen an das Modell kann dieses Verhältnis jedoch variieren. 


In Python können wir die Funktion `train_test_split` aus dem Modul `sklearn.model_selection` verwenden, um die Daten aufzuteilen. 

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

Dabei sind:
- `X` die Features (Eigenschaften) der Daten
- `y` die Zielvariable (was wir vorhersagen wollen)
- `test_size` der Anteil der Testdaten (hier 20%)
- `random_state` ein Wert, der festlegt, wie die Daten aufgeteilt werden. Wenn du den gleichen Wert verwendest, erhältst du bei jedem Durchlauf die gleiche Aufteilung.
- `X_train`, `X_test` die aufgeteilten Features
- `y_train`, `y_test` die aufgeteilten Zielvariablen

## Modell erstellen

Nachdem wir die Daten aufgeteilt haben, können wir ein Modell erstellen. Dazu wählen wir ein Modell aus, das wir trainieren möchten. Es gibt viele verschiedene Modelle, die für verschiedene Aufgaben geeignet sind. In unserem Fall verwenden wir den Gaussian Naive Bayes Klassifikator, der für Klassifikationsprobleme geeignet ist.

```python
from sklearn.naive_bayes import GaussianNB

model = GaussianNB()
```

## Modell trainieren

Nachdem wir das Modell erstellt haben, können wir es mit den Trainingsdaten trainieren. Dazu verwenden wir die `fit` Methode des Modells.

```python
model.fit(X_train, y_train)
```

## Modell evaluieren

Nachdem wir das Modell trainiert haben, können wir es mit den Testdaten evaluieren. Dazu verwenden wir den `accuracy_score` aus dem Modul `sklearn.metrics`, der die Genauigkeit des Modells berechnet.

```python
from sklearn.metrics import accuracy_score

y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
print(f'Genauigkeit: {accuracy}')
```

### Accuracy Score

Die Genauigkeit (Accuracy) ist eine Metrik, die angibt, wie gut ein Modell funktioniert. Sie berechnet sich als der Anteil der korrekt vorhergesagten Instanzen an der Gesamtzahl der Instanzen. Die Genauigkeit liegt zwischen 0 und 1, wobei 1 für 100% Genauigkeit steht.

