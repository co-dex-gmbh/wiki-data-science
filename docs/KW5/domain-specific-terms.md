# Wichtige Fachbegriffe in der Sentiment Analysis

## Grundlegende NLP-Begriffe

### Tokenisierung
Die Tokenisierung ist der erste Schritt bei der Textverarbeitung. Dabei wird ein Text in kleinere Einheiten zerlegt. Diese Einheiten nennt man Tokens. 

Ein Beispiel:
```python
text = "Der schnelle braune Fuchs springt."
tokens = ["Der", "schnelle", "braune", "Fuchs", "springt", "."]
```

Bei modernen Systemen wie BERT werden auch Teilwörter als Tokens verwendet:
```python
text = "unvergesslich"
subtokens = ["un", "##ver", "##gess", "##lich"]
```

### Embedding
Ein Embedding wandelt Wörter in Zahlen-Vektoren um. Diese Vektoren erfassen die Bedeutung der Wörter, sodass ähnliche Wörter ähnliche Vektoren haben.

Beispiel: Das Wort "König" könnte als Vektor dargestellt werden:
```python
"König" → [0.2, -0.5, 0.8, 0.1]
"Königin" → [0.3, -0.4, 0.7, 0.2]  # Ähnlicher Vektor
"Auto" → [-0.8, 0.2, -0.3, 0.9]     # Sehr unterschiedlicher Vektor
```

### Attention-Mechanismus
Der Attention-Mechanismus hilft einem Modell zu "fokussieren". Er berechnet, wie wichtig jedes Wort im Kontext der anderen Wörter ist. 

Ein einfaches Beispiel:
"Das Essen war gut, aber der Service war schlecht."

- Beim Wort "aber" achtet das Modell besonders auf die Wörter davor und danach
- Es erkennt, dass "gut" und "schlecht" in Kontrast stehen

## Modellarchitekturen

### Transformer
Ein Transformer ist eine moderne Architektur für Sprachmodelle. Die wichtigsten Merkmale sind:

- Verarbeitet alle Wörter parallel (nicht nacheinander)
- Nutzt mehrere Attention-Schichten
- Kann lange Texte gut verstehen

### BERT (Bidirectional Encoder Representations from Transformers)
BERT ist ein spezieller Transformer, der:

- Text in beide Richtungen liest (vorwärts und rückwärts)
- Vortrainiert wurde auf großen Textmengen
- An spezifische Aufgaben angepasst werden kann

### RNN (Recurrent Neural Network)
Ein neuronales Netz, das Text Wort für Wort verarbeitet und sich vorherige Wörter "merkt". RNNs:

- Verarbeiten Text sequentiell
- Haben ein "Gedächtnis" für vorherige Wörter
- Werden heute oft durch Transformer ersetzt

### LSTM (Long Short-Term Memory)
Eine verbesserte Version des RNN, die:

- Besser mit langen Texten umgehen kann
- Wichtige Informationen länger speichern kann
- Unwichtiges "vergessen" kann

## Verarbeitungsschritte

### POS-Tagging (Part-of-Speech-Tagging)
Hier wird jedem Wort seine Wortart zugeordnet:
```python
text = "Der schnelle Fuchs läuft"
pos_tags = [
    ("Der", "ART"),      # Artikel
    ("schnelle", "ADJ"), # Adjektiv
    ("Fuchs", "NN"),     # Nomen
    ("läuft", "VVFIN")   # Verb
]
```

### Lexikon-Lookup
Der Prozess, bei dem Wörter in einem Wörterbuch nachgeschlagen werden. Beispiel für ein Sentiment-Lexikon:
```python
sentiment_lexicon = {
    "gut": 1.0,      # Positiv
    "schlecht": -1.0,# Negativ
    "okay": 0.0      # Neutral
}
```

### Feature-Extraktion
Das Erkennen wichtiger Merkmale in einem Text. Dies kann verschiedene Formen annehmen:
- Zählen bestimmter Wörter
- Erkennen von Mustern
- Berechnen von Wortbeziehungen

### Batch-Verarbeitung
Die gleichzeitige Verarbeitung mehrerer Texte, um die Geschwindigkeit zu erhöhen:
```python
texte = ["Text 1", "Text 2", "Text 3"]
# Verarbeitung als Batch ist schneller als einzeln
ergebnisse = model.predict(texte)
```

Diese Fachbegriffe bilden die Grundlage für das Verständnis von Sentiment Analysis und NLP im Allgemeinen. Die Konzepte bauen aufeinander auf, wobei moderne Systeme wie BERT viele dieser Aspekte in einer komplexen Architektur vereinen.