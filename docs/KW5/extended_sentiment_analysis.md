
# Funktionsweise verschiedener Sentiment Analysis Methoden

## Transformers und BERT

Transformers wie BERT arbeiten fundamental anders als regelbasierte Systeme. Sie basieren auf dem Attention-Mechanismus, der es dem Modell ermöglicht, die Bedeutung eines Wortes im Kontext des gesamten Satzes zu verstehen.

### Grundlegende Funktionsweise:

1. **Tokenisierung**: Der Text wird in Teilwörter (Tokens) zerlegt
2. **Kontextuelle Einbettung**: Jedes Token erhält eine numerische Repräsentation, die sich je nach Kontext ändert
3. **Attention-Mechanismus**: Berechnet die Beziehungen zwischen allen Tokens
4. **Klassifikation**: Die finalen Token-Repräsentationen werden für die Sentimentvorhersage genutzt

```python
from transformers import AutoTokenizer, AutoModelForSequenceClassification

# Laden des Modells
tokenizer = AutoTokenizer.from_pretrained("bert-base-german-cased")
model = AutoModelForSequenceClassification.from_pretrained("bert-base-german-cased")

text = "Das Produkt ist wirklich gut verarbeitet."

# Tokenisierung
tokens = tokenizer(text, return_tensors="pt")
print("Tokens:", tokenizer.convert_ids_to_tokens(tokens['input_ids'][0]))

# Diese Tokens werden durch mehrere Transformer-Layer verarbeitet
# Jeder Layer verfeinert das Verständnis des Kontexts
outputs = model(**tokens)
```

Der Attention-Mechanismus erlaubt es dem Modell zu verstehen, dass "nicht schlecht" eigentlich positiv ist oder "gut, aber..." eine Einschränkung darstellt.

## TextBlob: Pattern-basierte Analyse

TextBlob nutzt einen pattern-basierten Ansatz, der auf linguistischen Regeln und einem Lexikon basiert.

### Funktionsweise im Detail:

1. **Tokenisierung und POS-Tagging**: Identifiziert Wortarten
2. **Pattern-Matching**: Sucht nach bekannten sprachlichen Mustern
3. **Lexikon-Lookup**: Bestimmt die Grundstimmung der Wörter
4. **Modifikator-Verarbeitung**: Berücksichtigt verstärkende oder abschwächende Wörter

```python
from textblob_de import TextBlobDE

def analyze_with_textblob(text):
    blob = TextBlobDE(text)
    
    # POS-Tagging demonstrieren
    print("Wortarten:", blob.tags)
    
    # Grundlegende Sentiment-Analyse
    polarity = blob.sentiment.polarity
    subjectivity = blob.sentiment.subjectivity
    
    return polarity, subjectivity

text = "Das sehr gute Produkt hat mich leider enttäuscht."
polarity, subjectivity = analyze_with_textblob(text)
```

## NLTK mit Custom Lexikon

NLTK ermöglicht eine transparente, lexikonbasierte Analyse, die wir vollständig kontrollieren können.

### Funktionsweise:

1. **Tokenisierung**: Text wird in Wörter zerlegt
2. **Normalisierung**: Wörter werden in Grundform gebracht
3. **Lexikon-Abgleich**: Jedes Wort wird mit dem Sentiment-Lexikon verglichen
4. **Regel-Anwendung**: Spezielle Regeln für Verneinungen, Verstärker etc.

```python
import nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import sentiwordnet as swn

def create_custom_analyzer():
    # Eigenes Sentiment-Lexikon erstellen
    custom_lexicon = {
        'gut': 1.0,
        'schlecht': -1.0,
        'sehr': 1.5,  # Verstärker
        'nicht': -1.0 # Negation
    }
    
    def analyze_text(text):
        tokens = word_tokenize(text.lower())
        score = 0
        modifier = 1
        
        for i, token in enumerate(tokens):
            if token in custom_lexicon:
                # Überprüfe auf Verneinung
                if i > 0 and tokens[i-1] == 'nicht':
                    score -= custom_lexicon[token]
                else:
                    score += custom_lexicon[token]
        
        return score
    
    return analyze_text

analyzer = create_custom_analyzer()
text = "Das Produkt ist nicht gut."
score = analyzer(text)
```

## Deep Learning von Grund auf

Bei diesem Ansatz trainieren wir ein neuronales Netz speziell für unsere Aufgabe.

### Funktionsweise:

1. **Embedding**: Wörter werden in Vektoren umgewandelt
2. **Sequenzverarbeitung**: RNN/LSTM/GRU verarbeitet die Sequenz
3. **Feature-Extraktion**: Wichtige Merkmale werden erkannt
4. **Klassifikation**: Finale Vorhersage des Sentiments

```python
import torch
import torch.nn as nn

class SentimentClassifier(nn.Module):
    def __init__(self, vocab_size, embedding_dim, hidden_dim):
        super().__init__()
        # Embedding-Layer wandelt Wörter in Vektoren um
        self.embedding = nn.Embedding(vocab_size, embedding_dim)
        
        # LSTM verarbeitet die Sequenz
        self.lstm = nn.LSTM(embedding_dim, hidden_dim, batch_first=True)
        
        # Klassifikations-Layer
        self.fc = nn.Linear(hidden_dim, 3)  # 3 Klassen: negativ, neutral, positiv
        
    def forward(self, text):
        # text shape: (batch_size, sequence_length)
        embedded = self.embedding(text)
        lstm_out, _ = self.lstm(embedded)
        # Verwende nur den letzten Output des LSTM
        output = self.fc(lstm_out[:, -1, :])
        return output

# Beispiel für das Training
model = SentimentClassifier(vocab_size=10000, embedding_dim=100, hidden_dim=256)
```

## Vergleich der Verarbeitungsschritte

Bei allen Methoden können wir grundlegende Schritte identifizieren:

1. **Vorverarbeitung**: Text normalisieren und tokenisieren
2. **Feature-Extraktion**: Wichtige Merkmale erkennen
3. **Analyse**: Sentiment bestimmen
4. **Nachbearbeitung**: Ergebnisse aufbereiten

Der Hauptunterschied liegt in der Art der Feature-Extraktion und Analyse:

- VADER/TextBlob: Regelbasiert und lexikonbasiert
- BERT: Kontextuelles Verständnis durch Attention
- Custom NLTK: Anpassbare Regeln und Lexika
- Deep Learning: Gelernte Features aus Trainingsdaten