# Erstellung neuer Features

Die Erstellung neuer Features (Feature Engineering) ist der Prozess, aus vorhandenen Daten neue, aussagekräftige Variablen zu generieren. Ziel ist es, die Beziehung zwischen Features und Zielvariablen zu verbessern.

Ein Beispiel ist die Berechnung von Geschwindigkeiten aus Distanz- und Zeitdaten oder die Aggregation von Transaktionsdaten zu monatlichen Summen.

**Beispiel in Python:**
```python
# Beispiel: Geschwindigkeit berechnen
import pandas as pd

# Beispiel-Daten
daten = pd.DataFrame({'Distanz_km': [100, 200, 150], 'Zeit_h': [2, 4, 3]})

# Neues Feature: Geschwindigkeit
daten['Geschwindigkeit_kmh'] = daten['Distanz_km'] / daten['Zeit_h']
print(daten)
```

**Wann brauche ich das?**
- Wenn du die Leistung deiner Modelle verbessern möchtest.
- Um verborgene Zusammenhänge in den Daten aufzudecken.

