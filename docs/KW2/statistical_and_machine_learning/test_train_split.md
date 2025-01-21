# Test-Train Split

Möchten wir ein Modell lernen lassenm, so müssen wir ein Verfahren nutzen, um diesen Lernprozess überprüfen. Dieses Überprüfen des Lernprozesses sollte natürlich wieder auf Daten stattfinden. Die einfachste Möglichkeit für diese Überprüfung wäre das Verwenden von Daten, welchen wir auch für das Training verwendet haben. Bereits in der Einleitung zu Machine Learning haben wir jedoch gelernt, dass möglich ist dass ein Modell seie Daten einfach auswendig lernt. Wir haben dies als Overfitting bezeichnet. Würden wir die Performance des Modells auf den Trainingsdaten testen, würden wir dieses Overfitting wahrscheinlich nicht erkennen.

Daher ist es ratsam, für das Evaluieren des Modells Daten zu verwenden, welche das Modell noch nicht gesehen hat. Dafür teilen wir unseren Datensatz in 3 Teile auf: Trainingsdaten, Validationsdaten und Testdaten. Die Trainingsdaten werden verwendet, um das Modell zu trainieren. Die Validationsdaten werden verwendet, um das Modell zu evaluieren und die Hyperparameter zu optimieren. Die Testdaten werden verwendet, um die Performance des Modells zu evaluieren. Dies Geschieht nach dem Training und der Optimierung der Hyperparameter.

![https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/61568656a13218cdde7f6166_training-data-validation-test.png](https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/61568656a13218cdde7f6166_training-data-validation-test.png)

## Trainingsdaten und Validationsdaten

Die Aufteilung des Datensatzes in Trainings-, Test- und Validationsdaten sollte in den meisten Fällen zufällig erfolgen. Ausnahmen können zum Beispiel dann gemacht werden, wenn die Daten zeitlich geordnet sind. In diesem Fall könnten die Trainingsdaten die älteren Daten enthalten und die Test-/Validationsdaten die neueren. Bei der Aufteilung kann als Ausgangwert eine Aufteilung von 60% Trainingsdaten und jeweils 20% für Validations- und Testdaten verwendet werden. Diese Werte können jedoch je nach Anwendungsfall und größe des Datensatzes variieren.

### Anzahl der Hyperparameter

Je größer die Anzahl an Hyperparametern sit, desto größer ist die Wahrscheinlichkeit, dass das Modell die Trainingsdaten auswendig lernt. Daher ist es ratsam, bei einer großen Anzahl an Hyperparametern die Anzahl der Validationsdaten zu erhöhen.

### Dimenaionalität der Daten

Bei hochdimensionalen Daten ist es ebenfalls ratsam, die Anzahl der Testdaten zu erhöhen. Dies liegt daran, dass die Wahrscheinlichkeit, dass das Modell die Trainingsdaten auswendig lernt, bei hochdimensionalen Daten größer ist. Der Grund dafür ist, dass jeder zusätzliche Parameter die Anzahl der möglichen Kombinationen erhöht. Die Anzahl der Freiheitsgrade steigt also.

### Ziel des Modells

Das Ziel des Modells kann ebenfalls Einfluss auf die Anzahl der Validationsdaten haben. Soll das Modell zum Beispiel eine Krankheit mit hoher Sicherheit erkennen, so ist es ratsam, die Anzahl der Validationsdaten zu erhöhen. Somit kann die Sicherheit des Modells besser validiert werden, was in diesem Fall eine höhere Priorität hat, also alle möglichen Krankheiten zu erkennen.


Generell hat die Wahl des Test/Train Split eine Auswirkung auf die Varianz in den Daten. Je mehr Daten wir für das Training verwenden, desto geringer ist die Varianz auf den Trainingsdaten. Dafür wird die Varianz auf den Validations- und Testdaten wahrscheinlich größer. Umgekehrt ist es bei einer geringen Anzahl an Trainingsdaten. Die Varianz auf den Trainingsdaten ist dann wahrscheinlich größer, während die Varianz auf den Validations- und Testdaten geringer ist.

Die nachfolgende Grafik zeigt häufig verwendete Test/Train Split Verhältnisse.

![https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/613ec5b6c3da5313e1abcc47_UeKfm9v6E9QobwFfG3ud_20Q82QoqI8W6kXQnDm_QBnOVyQXCNmwjWtMI5vD9du4cjovnpzSYBbIDHdSU-57H1Bb4DfuUCaSjZjozKIwD0IQsH7FyMuFTW7aYVW-zelk2RNMAez3%3Ds0.png](https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/613ec5b6c3da5313e1abcc47_UeKfm9v6E9QobwFfG3ud_20Q82QoqI8W6kXQnDm_QBnOVyQXCNmwjWtMI5vD9du4cjovnpzSYBbIDHdSU-57H1Bb4DfuUCaSjZjozKIwD0IQsH7FyMuFTW7aYVW-zelk2RNMAez3%3Ds0.png)

