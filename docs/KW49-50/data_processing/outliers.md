# Umgang mit Ausreißern


Ausreißer sind Datenpunkte, die erheblich von anderen Beobachtungen in einem Datensatz abweichen. Sie können wertvolle Informationen enthalten oder die Analyse stören, weshalb es wichtig ist, sie zu erkennen und sinnvoll zu behandeln.

---

## Warum sind Ausreißer wichtig?
Ausreißer können sowohl negative als auch positive Auswirkungen auf die Datenanalyse haben. Negative Effekte umfassen die Verzerrung statistischer Kennzahlen wie Mittelwert und Standardabweichung, was zu fehlerhaften Schlussfolgerungen führen kann. Auf der anderen Seite können Ausreißer auch positive Effekte haben, indem sie auf seltene, aber wichtige Ereignisse hinweisen, wie zum Beispiel Betrug, Fehler oder extreme Phänomene.

Ein Beispiel für einen negativen Effekt wäre ein Monatsgehalt von 1.000.000 € in einem Datensatz von Durchschnittsgehältern, das den Mittelwert stark nach oben verzerren würde. Ein Beispiel für einen positiven Effekt wäre eine Temperaturmessung von 80 °C in einer Klimadatenreihe, die auf ein außergewöhnliches Wetterereignis hinweisen könnte.

---

## Erkennung von Ausreißern

### **Visuelle Methoden**
Visuelle Methoden zur Erkennung von Ausreißern umfassen Boxplots und Scatterplots. Boxplots zeigen potenzielle Ausreißer oberhalb oder unterhalb der "Whisker". Um einen Boxplot für die Variable "Preis" in einem Datensatz zu erstellen, kann folgender Python-Code verwendet werden:

```python
import matplotlib.pyplot as plt
import seaborn as sns

sns.boxplot(x=df['Preis'])
plt.show()
```

Scatterplots hingegen zeigen Ausreißer in zweidimensionalen Daten. Um "Größe" gegen "Preis" zu plotten und auffällige Punkte zu identifizieren, kann folgender Python-Code verwendet werden:

```python
plt.scatter(df['Größe'], df['Preis'])
plt.xlabel('Größe')
plt.ylabel('Preis')
plt.show()
```

### **Statistische Methoden**
Die IQR-Methode (Interquartilsabstand) ist eine gängige Methode zur Identifizierung von Ausreißern. Werte, die außerhalb des Bereichs [Q1 - 1,5 * IQR, Q3 + 1,5 * IQR] liegen, gelten als Ausreißer. Um die IQR-Methode zu implementieren und die Ausreißer aufzulisten, kann folgender Python-Code verwendet werden:

```python
Q1 = df['Preis'].quantile(0.25)
Q3 = df['Preis'].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

ausreisser = df[(df['Preis'] < lower_bound) | (df['Preis'] > upper_bound)]
print(ausreisser)
```

- **Z-Score**:
 Der Z-Score ist ein statistisches Maß, das angibt, wie viele Standardabweichungen ein Datenpunkt vom Mittelwert entfernt ist. Werte mit einem absoluten Z-Score größer als 3 werden oft als Ausreißer betrachtet.

Um den Z-Score für alle Werte zu berechnen und die Ausreißer zu finden, kann folgender Python-Code verwendet werden:


    ```python
    from scipy.stats import zscore
    df['z_score'] = zscore(df['Preis'])
    ausreisser = df[abs(df['z_score']) > 3]
    print(ausreisser)
    ```
In diesem Code wird die Funktion zscore aus dem Modul scipy.stats verwendet, um den Z-Score der Spalte Preis in einem DataFrame df zu berechnen. Anschließend werden alle Zeilen, deren absoluter Z-Score größer als 3 ist, als Ausreißer identifiziert und ausgegeben.

---

## Umgang mit Ausreißern

### **Entfernen von Ausreißern**
Die IQR-Methode (Interquartilsabstand) ist eine gängige statistische Methode zur Identifizierung und Entfernung von Ausreißern in einem Datensatz. Der Interquartilsabstand ist der Bereich zwischen dem ersten Quartil (Q1) und dem dritten Quartil (Q3) eines Datensatzes. Ausreißer sind Werte, die entweder unterhalb von Q1 - 1.5 * IQR oder oberhalb von Q3 + 1.5 * IQR liegen.

Um problematische Werte zu entfernen, wenn sie Fehler oder nicht relevant sind, kann die IQR-Methode verwendet werden. Zuerst werden die Quartile Q1 und Q3 berechnet, dann wird der IQR als die Differenz zwischen Q3 und Q1 bestimmt. Schließlich werden die unteren und oberen Grenzen festgelegt, um Ausreißer zu identifizieren und zu entfernen. Der bereinigte Datensatz enthält nur die Werte, die innerhalb dieser Grenzen liegen.
   ```python
    Q1 = df['Preis'].quantile(0.25)
    Q3 = df['Preis'].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
   ```
df_cleaned = df[(df['Preis'] >= lower_bound) & (df['Preis'] <= upper_bound)]

In diesem Beispiel wird der bereinigte Datensatz df_cleaned erstellt, indem alle Ausreißer basierend auf der IQR-Methode entfernt werden.

### **Transformation von Daten**
Die Log-Transformation wird verwendet, um extreme Werte zu glätten. Dies geschieht, indem die Werte einer Variable mit der Logarithmusfunktion transformiert werden. Hier ist ein Beispiel in Python:
    ```python
    df['Preis_log'] = np.log1p(df['Preis'])
    ```
Die Log-Transformation reduziert die Skala der Daten, insbesondere bei großen Werten. Dies liegt daran, dass der Logarithmus einer Zahl langsamer wächst als die Zahl selbst. Dadurch werden große Werte komprimiert und die Verteilung der Daten wird symmetrischer. Dies kann hilfreich sein, um die Auswirkungen von Ausreißern zu minimieren und die Datenanalyse zu verbessern.

### **Winsorizing**
Um Extremwerte zu begrenzen, können wir die Werte auf vordefinierte Schwellen beschränken. In dieser Aufgabe sollen die Preise auf das 5. und 95. Perzentil begrenzt werden.

Perzentile sind Maßeinheiten, die die Verteilung von Daten in 100 gleiche Teile unterteilen. Das 5. Perzentil bedeutet, dass 5% der Daten unter diesem Wert liegen, während das 95. Perzentil bedeutet, dass 95% der Daten unter diesem Wert liegen.

Im folgenden Python-Code wird dies umgesetzt:
    ```python
    lower_percentile = df['Preis'].quantile(0.05)
    upper_percentile = df['Preis'].quantile(0.95)

    df['Preis_winsorized'] = np.clip(df['Preis'], lower_percentile, upper_percentile)
    ```

Hier berechnen wir zunächst das 5. und 95. Perzentil der Preisdaten. Anschließend verwenden wir die np.clip-Funktion, um die Preise auf diese Perzentile zu begrenzen. Dies bedeutet, dass alle Preise, die unter dem 5. Perzentil liegen, auf das 5. Perzentil gesetzt werden, und alle Preise, die über dem 95. Perzentil liegen, auf das 95. Perzentil gesetzt werden.

### **Beibehalten von Ausreißern**
In manchen Fällen sollten Ausreißer bewusst beibehalten werden, insbesondere wenn sie für das Problem relevant sind, wie zum Beispiel bei der Betrugserkennung.

---

## Best Practices
- **Analysiere den Ursprung**: Prüfe, ob der Ausreißer ein Messfehler, ein Dateneingabefehler oder ein echtes Signal ist.
- **Domänenwissen einbeziehen**: Besprich Auffälligkeiten mit Experten aus dem jeweiligen Bereich.
- **Dokumentiere deine Entscheidungen**: Notiere, welche Schritte unternommen wurden und warum.

