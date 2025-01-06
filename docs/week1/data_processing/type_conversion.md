# Typenkonvertierungen (Wird noch behandelt)

Typenkonvertierungen sind ein essenzieller Bestandteil des Data Cleanings. Häufig stammen Daten aus unterschiedlichen Quellen, was zu inkonsistenten Datentypen führen kann. Beispielsweise kann ein numerischer Wert als Text gespeichert sein oder ein Datum in einem unüblichen Format vorliegen. Um Analysen durchführen zu können, müssen solche Werte in geeignete Datentypen konvertiert werden.

## Warum Typenkonvertierungen wichtig sind

- **Korrekte Verarbeitung:** Viele Analyse- und Modellierungsmethoden erfordern spezifische Datentypen (z. B. numerische Werte für Berechnungen).
- **Effizienz:** Die Arbeit mit korrekt typisierten Daten ist meist schneller und ressourcenschonender.
- **Fehlervermeidung:** Inkompatible Typen können zu Laufzeitfehlern oder falschen Ergebnissen führen.

## Typische Herausforderungen

**Numerische Werte als Text:**
   Daten wie "1000" oder "3,14" werden oft als Zeichenketten gespeichert, müssen aber für Berechnungen in numerische Werte konvertiert werden.

**Datumsangaben:**
   Formate wie "12/31/2024" oder "31-12-2024" erfordern eine einheitliche Konvertierung in ein Datumsobjekt.

**Kategorische Daten:**
   Kategorien wie "Ja" und "Nein" oder "True" und "False" sollten in standardisierte Werte umgewandelt werden.

**Fehlende Werte:**
   Leere Felder oder Platzhalter wie "N/A" oder "-" müssen erkannt und behandelt werden.

## Methoden zur Typenkonvertierung

### **Numerische Werte**

Mit Bibliotheken wie Pandas in Python können Zeichenketten in numerische Werte umgewandelt werden:

```python
import pandas as pd

# Beispiel-Daten
data = {"Werte": ["100", "200", "300"]}
df = pd.DataFrame(data)

# Typenkonvertierung
df["Werte"] = pd.to_numeric(df["Werte"])
```

Falls die Konvertierung fehlschlägt, kann der Parameter `errors='coerce'` verwendet werden, um problematische Werte in `NaN` umzuwandeln.

### **Datumsangaben**

Datumswerte lassen sich mit `pd.to_datetime` standardisieren:

```python
# Beispiel-Daten
data = {"Datum": ["31/12/2024", "01-01-2025", "2024.12.30"]}
df = pd.DataFrame(data)

# Typenkonvertierung
df["Datum"] = pd.to_datetime(df["Datum"], dayfirst=True)
```

Der Parameter `dayfirst=True` stellt sicher, dass das europäische Datumsformat korrekt interpretiert wird.

### **Kategorische Daten**

Kategorische Daten können in numerische Codes oder `category`-Typen umgewandelt werden:

```python
# Beispiel-Daten
data = {"Antworten": ["Ja", "Nein", "Ja"]}
df = pd.DataFrame(data)

# Typenkonvertierung
df["Antworten"] = df["Antworten"].astype("category")
```

Kategorien haben den Vorteil, weniger Speicherplatz zu beanspruchen und effizienter verarbeitet zu werden.

### **Fehlende Werte behandeln**

Vor der Typenkonvertierung müssen Platzhalter wie "N/A" entfernt oder ersetzt werden:

```python
# Beispiel-Daten
data = {"Werte": ["100", "N/A", "200"]}
df = pd.DataFrame(data)

# Fehlende Werte ersetzen und konvertieren
df["Werte"] = pd.to_numeric(df["Werte"], errors='coerce')
```


