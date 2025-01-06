# Feature Extraction

Feature Extraction bezeichnet die Ableitung relevanter Informationen aus komplexen Daten wie Text, Bildern oder Zeitreihen. Ziel ist es, die wichtigsten Eigenschaften (Features) aus den Rohdaten zu gewinnen, um die Komplexität zu reduzieren.

Ein Beispiel ist das Extrahieren von Textlänge aus einem Textfeld oder die Frequenzanalyse in Zeitreihendaten.

**Beispiel in Python:**
```python
# Beispiel: Textlänge berechnen
import pandas as pd

# Beispiel-Daten
texte = pd.DataFrame({'Text': ['Hallo Welt', 'Data Science ist spannend', 'Python macht Spaß']})

# Feature: Textlänge
texte['Textlänge'] = texte['Text'].apply(len)
print(texte)
```

**Wann brauche ich das?**
- Wenn deine Rohdaten unstrukturiert sind (z. B. Text, Bilder).
- Um spezifische Eigenschaften zu extrahieren, die für Modelle relevant sind.

