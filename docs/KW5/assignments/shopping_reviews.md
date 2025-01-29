# Praktische NLP-Übungen mit spaCy und NLTK

Ausgangslage ist der nachfolgende Datensatz: [https://www.kaggle.com/datasets/nicapotato/womens-ecommerce-clothing-reviews/data](https://www.kaggle.com/datasets/nicapotato/womens-ecommerce-clothing-reviews/data)


## Aufgabe 1: Grundlegende Textanalyse
Analysieren Sie die Review-Texte hinsichtlich ihrer Länge und häufigsten Wörter.

1. Wie viele Wörter enthält durchschnittlich ein Review?
2. Was sind die 10 häufigsten Wörter in allen Reviews?
3. Wie viele einzigartige Wörter gibt es insgesamt?
   
```python
from collections import Counter
import nltk
from nltk.tokenize import word_tokenize
nltk.download('punkt')

# Beispiel-Reviews
reviews = df['Review Text'].fillna('').tolist()

```

## Aufgabe 2: Named Entity Recognition
Identifizieren Sie Produktmarken, Größenangaben und andere relevante Entities in den Reviews.


1. Welche Entities werden in diesem Review erkannt?
2. Welche Größenangaben kommen in den Reviews am häufigsten vor?
3. Welche Produkttypen werden am häufigsten genannt?

```python
import spacy
nlp = spacy.load('en_core_web_sm')

# Beispiel-Review
review = "I bought a size M dress from this retailer and it fits perfectly."

```

## Aufgabe 3: Textbereinigung
Bereinigen Sie die Reviews von Stoppwörtern und Sonderzeichen.

1. Entfernen Sie alle Stoppwörter aus den Reviews
2. Entfernen Sie alle Sonderzeichen
3. Konvertieren Sie den Text in Kleinbuchstaben

```python
from nltk.corpus import stopwords
nltk.download('stopwords')
```

## Aufgabe 4: Part-of-Speech Tagging
Analysieren Sie die Wortarten in den Reviews.


1. Welche Adjektive werden am häufigsten verwendet?
2. Wie viele Verben enthält ein durchschnittliches Review?
3. Identifizieren Sie häufige Adjektiv-Nomen-Kombinationen

```python
from nltk import pos_tag
nltk.download('averaged_perceptron_tagger')
```

## Aufgabe 5: Tokenisierung und Lemmatisierung
Vergleichen Sie verschiedene Tokenisierungsmethoden.

1. Teilen Sie die Reviews in Sätze auf
2. Tokenisieren Sie jeden Satz in Wörter
3. Lemmatisieren Sie die Wörter und vergleichen Sie die Ergebnisse

```python
from nltk.tokenize import word_tokenize, sent_tokenize
from nltk.stem import WordNetLemmatizer
nltk.download('wordnet')
```

## Erwartete Ergebnisse

Bei der Analyse der Daten sollten Sie folgende Erkenntnisse gewinnen:

- Typische Länge der Reviews
- Häufig verwendete beschreibende Wörter
- Produkteigenschaften, die oft erwähnt werden
- Muster in der Sprachverwendung

## Weiterführende Fragen

1. Wie unterscheiden sich positive und negative Reviews in ihrer Wortwahl?
2. Welche Adjektive werden besonders häufig mit bestimmten Produktkategorien verwendet?
3. Gibt es typische Satzmuster in den Reviews?