# Vektorisierung und Word Embeddings

## Grundkonzept der Vektorisierung

Computer können nicht direkt mit Text arbeiten - sie brauchen Zahlen. Die Vektorisierung wandelt Text in numerische Vektoren um. Ein Vektor ist dabei einfach eine Liste von Zahlen, die bestimmte Eigenschaften des Textes repräsentieren.

### One-Hot-Encoding

Die einfachste Form der Vektorisierung ist das One-Hot-Encoding. Hier wird jedes Wort durch einen Vektor dargestellt, der überall Nullen enthält, außer an einer Position.

```python
from sklearn.preprocessing import OneHotEncoder
import numpy as np

# Beispiel-Vokabular
vocabulary = ["Hund", "Katze", "Maus"]

# One-Hot-Encoding
one_hot = {word: np.zeros(len(vocabulary)) for word in vocabulary}
for i, word in enumerate(vocabulary):
    one_hot[word][i] = 1

print("One-Hot für 'Hund':", one_hot["Hund"])    # [1, 0, 0]
print("One-Hot für 'Katze':", one_hot["Katze"])  # [0, 1, 0]
```

Problem: Bei einem Vokabular von 50.000 Wörtern wäre jedes Wort ein Vektor mit 49.999 Nullen und einer 1. Das ist sehr ineffizient.

### Bag-of-Words (BoW)

BoW zählt das Vorkommen jedes Wortes in einem Text:

```python
from sklearn.feature_extraction.text import CountVectorizer

texts = [
    "Der Hund spielt",
    "Der Hund bellt",
    "Die Katze miaut"
]

vectorizer = CountVectorizer()
X = vectorizer.fit_transform(texts)

print("Vokabular:", vectorizer.get_feature_names_out())
print("BoW-Vektoren:\n", X.toarray())
```

### TF-IDF (Term Frequency-Inverse Document Frequency)

TF-IDF berücksichtigt nicht nur die Häufigkeit eines Wortes, sondern auch seine Bedeutung im Kontext:

```python
from sklearn.feature_extraction.text import TfidfVectorizer

tfidf = TfidfVectorizer()
X_tfidf = tfidf.fit_transform(texts)

print("TF-IDF Vektoren:\n", X_tfidf.toarray())
```

## Word Embeddings

Embeddings sind fortgeschrittene Vektordarstellungen, die semantische Beziehungen zwischen Wörtern erfassen.

### Word2Vec Beispiel

```python
from gensim.models import Word2Vec

# Beispielsätze
sentences = [
    ["Der", "Hund", "spielt", "im", "Garten"],
    ["Die", "Katze", "schläft", "auf", "dem", "Sofa"],
    ["Ein", "Hund", "bellt", "laut"]
]

# Training eines einfachen Word2Vec Modells
model = Word2Vec(sentences, vector_size=10, window=5, min_count=1)

# Ähnliche Wörter finden
similar_words = model.wv.most_similar("Hund")
print("Ähnliche Wörter zu 'Hund':", similar_words)
```

### Eigenschaften von Word Embeddings

Embeddings haben interessante mathematische Eigenschaften:

```python
# Vektorarithmetik mit Wörtern
königin = model.wv["König"] - model.wv["Mann"] + model.wv["Frau"]
```

Diese Vektoren ermöglichen:

- Analogien ("König" - "Mann" + "Frau" ≈ "Königin")
- Ähnlichkeitsberechnungen (cosine similarity)
- Clustering von ähnlichen Wörtern

### Moderne Kontextuelle Embeddings

BERT und ähnliche Modelle erzeugen kontextabhängige Embeddings:

```python
from transformers import AutoTokenizer, AutoModel
import torch

# Laden von BERT
tokenizer = AutoTokenizer.from_pretrained("bert-base-german-cased")
model = AutoModel.from_pretrained("bert-base-german-cased")

# Text vektorisieren
text = "Die Bank am Fluss ist aus Holz."
inputs = tokenizer(text, return_tensors="pt")
outputs = model(**inputs)

# Embeddings extrahieren
embeddings = outputs.last_hidden_state
print("Shape der Embeddings:", embeddings.shape)
```

## Praktische Anwendung

```python
from sklearn.metrics.pairwise import cosine_similarity

def find_similar_documents(query, documents, vectorizer):
    """
    Findet ähnliche Dokumente basierend auf TF-IDF Vektoren
    """
    # Vektorisierung
    doc_vectors = vectorizer.fit_transform(documents)
    query_vector = vectorizer.transform([query])
    
    # Ähnlichkeitsberechnung
    similarities = cosine_similarity(query_vector, doc_vectors)
    
    # Ergebnisse sortieren
    most_similar = similarities.argsort()[0][::-1]
    
    return [(documents[i], similarities[0][i]) for i in most_similar]

# Beispielanwendung
documents = [
    "Der Hund spielt im Garten",
    "Katzen schlafen gerne",
    "Ein Hund bellt im Park"
]
query = "Hunde im Garten"

similar_docs = find_similar_documents(query, documents, TfidfVectorizer())
for doc, score in similar_docs:
    print(f"Ähnlichkeit {score:.2f}: {doc}")
```

### Unterschiede der Methoden

1. **Statische Embeddings** (Word2Vec, GloVe):
   
   - Ein Wort = Ein Vektor
   - Schnell und effizient
   - Ignoriert Kontext

2. **Kontextuelle Embeddings** (BERT):
   
   - Ein Wort = Verschiedene Vektoren je nach Kontext
   - Erfasst Bedeutungsnuancen
   - Rechenintensiver

Die Wahl der Methode hängt von der Anwendung ab:

- Einfache Textklassifikation: TF-IDF oft ausreichend
- Semantische Suche: Word Embeddings gut geeignet
- Komplexe Sprachverständnisaufgaben: Kontextuelle Embeddings optimal