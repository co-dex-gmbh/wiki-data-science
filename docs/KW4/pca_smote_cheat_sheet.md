## Schritte zum Anwenden von SMOTE

1. Klassenverteilungen ansehen.
2. Minderheitsklassen (weniger als 1 % der meistvertretenden Klasse) entfernen oder gesondert behandeln. Erstellen von Duplikaten wollen wir meistens vermeiden.
3. In numerische Werte überführen. Für SMOTE selbt ist es egal, wie wir das machen. Für die nachfolgednen Werte möglicherweise nicht. Es können im Standard überall auch fraktionale Werte entstehen.
4. Teilen in Trainings und Testdaten. `stratify=df["target"]` kann bei kleinen Datasets und wenn eine Klasse selten vorhandne ist, sinnvoll sein.
5. smote initialisieren und anwenden, aber nur auf die Trainingsdaten


## Schritte zum Anwenden vom PCA 

1. Skalieren/ Normalisieren
2. PCA initialisieren und erklärende Varianz betrachten 
3. Anzahl der Komponenten anhand der kummilierten Varianz oder Ellenbogen-Kriterium bestimmen
4. Transformation der Trainingsdaten anhand der PCA durchführen
5. Gleiches können wir danach über `model.transform()` auch für die Testdaten machen