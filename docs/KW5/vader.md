# Sentiment Analysis und VADER im Natural Language Processing

## Motivation

Wir haben täglich mit Bewertungen, Kommentaren und Feedback zu tun. Ob Produktrezensionen, Social Media Posts oder Kundenfeedback - die manuelle Auswertung dieser Texte ist zeitaufwändig. Sentiment Analysis automatisiert diesen Prozess und ermöglicht uns, die emotionale Tendenz in Texten zu erkennen.

## VADER

VADER ist ein regelbasiertes System für Sentiment Analysis, optimiert für kurze Texte und Social Media. Es berücksichtigt:

- Zeichensetzung ("gut!!!")
- Großschreibung ("GUT")
- Verstärker ("sehr gut")
- Kontrastformulierungen ("gut, aber...")
- Emojis

## Praktische Implementierung

```python
from vaderSentiment.vaderSentiment import SentimentIntensityAnalyzer
import pandas as pd
import matplotlib.pyplot as plt

# Initialisierung
analyzer = SentimentIntensityAnalyzer()

# Beispieltexte
texts = [
    "Das Produkt ist fantastisch! Sehr zu empfehlen.",
    "Okay, aber zu teuer.",
    "Absolut enttäuschend. Nie wieder.",
    "Gute Qualität, könnte aber besser sein.",
]

# Analyse-Funktion
def analyze_texts(texts):
    results = []
    for text in texts:
        scores = analyzer.polarity_scores(text)
        scores['text'] = text
        results.append(scores)
    return pd.DataFrame(results)

# Durchführung
results = analyze_texts(texts)
print("Sentiment-Analyse:")
print(results[['text', 'compound']])
```

## Interpretation

VADER liefert vier Werte:

- positive (0 bis 1)
- neutral (0 bis 1)
- negative (0 bis 1)
- compound (-1 bis 1)

Der Compound-Score zeigt die Gesamtbewertung:

- Positiv: ≥ 0.05
- Neutral: -0.05 bis 0.05
- Negativ: ≤ -0.05

## Praktisches Beispiel: Social Media Monitoring

```python
def analyze_social_media(posts, critical_threshold=-0.2):
    """Überwacht Posts auf negative Stimmung"""
    results = []
    for post in posts:
        score = analyzer.polarity_scores(post)['compound']
        if score < critical_threshold:
            results.append({
                'post': post,
                'sentiment': score,
                'priority': 'HOCH' if score < -0.5 else 'MITTEL'
            })
    return pd.DataFrame(results)

# Beispiel
posts = [
    "@firma Katastrophaler Service! #verärgert",
    "@firma Produkt entspricht nicht der Beschreibung.",
    "@firma Preis zu hoch für diese Qualität."
]

alerts = analyze_social_media(posts)
print("\nKritische Posts:")
print(alerts)
```

## Grenzen von VADER

VADER hat einige Einschränkungen:

- Ursprünglich für Englisch entwickelt
- Erkennt komplexe Ironie nicht
- Branchenspezifische Begriffe können falsch interpretiert werden

Die Ergebnisse sollten daher immer im Kontext betrachtet werden.