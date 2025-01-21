# Scaling

Scaling (Skalierung) wird verwendet, um numerische Features in einen einheitlichen Wertebereich zu bringen. Dies ist besonders wichtig für Algorithmen, die empfindlich auf die Skala der Eingabedaten reagieren, wie z. B. lineare Regression oder k-Nearest Neighbors.

Die zwei häufigsten Methoden sind:
- **Standardisierung**: Zentriert die Daten auf Mittelwert 0 und Standardabweichung 1.
- **Min-Max-Skalierung**: Skaliert Werte in einen Bereich zwischen 0 und 1.

**Beispiel in Python:**
```python
import pandas as pd
from sklearn.preprocessing import MinMaxScaler

# Beispiel-Daten
daten = pd.DataFrame({'Alter': [25, 35, 45, 55], 'Einkommen': [40000, 50000, 60000, 80000]})

# Min-Max-Skalierung
scaler = MinMaxScaler()
skalierte_daten = scaler.fit_transform(daten)

# Ergebnis anzeigen
skalierte_df = pd.DataFrame(skalierte_daten, columns=['Alter', 'Einkommen'])
print(skalierte_df)
```

**Wann brauche ich das?**
- Wenn deine Features unterschiedliche Skalen haben (z. B. Alter in Jahren und Einkommen in Euro).
- Besonders wichtig bei Algorithmen wie k-Means, kNN oder neuronalen Netzen.

