# Encoding

Encoding ist der Prozess, kategorische Daten in numerische Werte umzuwandeln, damit maschinelle Lernalgorithmen mit ihnen arbeiten können. Das ist notwendig, da viele Algorithmen nur mit numerischen Daten umgehen können und kategoriale Werte – wie "rot", "blau", "grün" – nicht direkt verarbeiten können.

Ein Beispiel ist das One-Hot-Encoding, bei dem jede Kategorie in eine binäre Spalte umgewandelt wird. Wenn es zum Beispiel drei Farben gibt („rot“, „blau“, „grün“), werden daraus drei Spalten: „rot“, „blau“ und „grün“, in denen jede Zeile entweder eine 1 (aktiv) oder 0 (nicht aktiv) enthält.

**Beispiel in Python:**
```python
import pandas as pd
from sklearn.preprocessing import OneHotEncoder

# Beispiel-Daten
farben = pd.DataFrame({'Farbe': ['rot', 'blau', 'grün', 'rot']})

# One-Hot-Encoding
encoder = OneHotEncoder(sparse=False)
encoded = encoder.fit_transform(farben[['Farbe']])

# Ergebnis anzeigen
encoded_df = pd.DataFrame(encoded, columns=encoder.get_feature_names_out())
print(encoded_df)
```

**Wann brauche ich das?**
- Wenn dein Datensatz kategorische Variablen enthält.
- Besonders wichtig bei Algorithmen wie linearen Modellen, die nicht mit Kategorien arbeiten können.

