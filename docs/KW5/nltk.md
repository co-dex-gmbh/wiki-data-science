# Natural Language Processing (NLP)

## 1. Grundidee
NLP befasst sich mit Interaktionen zwischen Computern und menschlichen (natürlichen) Sprachen. Viele der uns bekannten Technologien basieren auf Anwendungen von NLP. Zum Beispiel haben viele Smartphones und Online-Suchmaschinen Textvorhersagefunktionen, die vervollständigen können, was man eingibt.

## 2. einfache Beispielprobleme
### 2.1 Features sind in längerer Textform gegeben
Die länge von Texten in Features können unbegrenzt sein. Sie können teilweise nur zwei Wörter enthalten aber auch ohne Probleme ganze Emails. Bei kürzeren Texten kann es Sinn machen nur die wichtigsten Inhalten zu entnehmen. Beispielsweise haben wir in einem DataFrame die Spalte "Models". Diese enthält verschiedene Automodelle inklusive des Motors und des Hubraumes. 

```python
import pandas as pd
import re

cars = ["Caravan Grand FWD V6",
        "MALIBU 4C",
        "TAURUS 3.0L V6 EFI",
        "PT CRUISER 2.4L I4 S",
        "STRATUS V6 2.7L V6 M",
        "GRAND PRIX 3.8L V6 S"]
df_models = pd.DataFrame(cars, columns=["Models"])

re.findall(r"V\d+", df_models.iloc[0,0])
```
Das Modul 're' bietet hier eine Möglichkeit nach speziellen Mustern in strings zu suchen und diese zu extrahieren. Hierfür bietet re eine umfangreiche auswahl an Ausdrücken um das Suchuster zu definieren. Hier haben wir als Suchmuster r"V\d+". das 'r' gehört hierbei nicht zum Suchmuster, sondern sagt lediglich Python, dass es sich um einen raw-string handelt und jedes Zeichen als ein solches auch behandlet werden soll. Das '\d' sagt, dass an dieser Stelle eine beliebige Ziffer stehen soll, während das '+' sagt, dass der vorangegangene Ausdruck mindestens 1 Mal auftaucht. D.h. hier soll mindestens eine Ziffer stehen und würden darauf direkt weitere Ziffern folgen, sollen diese auch zu dem Ausdruck dazugehören.
Für die Bearbeitung von DataFrames ist diese Funktionalität in pandas bereits implementiert:

```Python
df_models["MotorType"] = df_models["Models"].str.extract(r"(V\d+)")
df_models["Liter"] = df_models["Models"].str.extract(r"(\d\.\dL)")
```

### 2.2 Spamfilter
Diese Methode aus dem Vorangegangenen Beispiel lässt sich leider nicht mehr effektiv nutzen wenn die Texte eine gewisse länge erreicht haben. So möchte man bspw. im Posteingang seiner Mail-Adresse nach Spam Mails filtern, welche sich anhand des Inhaltes erkennen lassen. 

```python
mails = ["Hello, I need a favor from you kindly email me back as soon as possible.",
         "Hi Max, I just wanted to resurface my below email in case it got buried in your inbox. Have you given any thought to adding our link to your post?",
         "The password to your email m.mustermann@seinprovider.de is expiring on 2:17:12 PM. You are required to use below services to update password otherwise access to your mailbox will be denied.",
         "Hey folks, I will be on vacation between April 2 - Mai 1. I'm going on an expedition to fish in the Arctic. Brrr! Best, Chanpory"]
df_mails = pd.DataFrame(mails, columns=["Mails"])
```
## 3. Idee des Spamfilters
Eine Möglichkeit den Text für uns Nutzbar zu machen wäre ein Art One-Hot-Encoding. Jedes Wort was in den gesamten Emails vorkommt bekommt eine Spalte. Dadurch wird der DataFrame allerdings sehr schnell sehr groß. Dies kann man leider nicht umgehen, allerdings kann man dafür sorgen, dass die Größe etwas reduziert wird:

### 3.1 Umwandeln in ein Doc-Objekt
Zur besseren Bearbeitung von Texten bieten verschiedene Module verschiedene Funktionalitäten an. Ein auf den ersten Blick nicht ganz so ein großer Vorteil bietet der objektorientierte Ansatz der Umwandlung in ein Doc-Objekt. Ein Doc-Objekt ist hierbei aus mehreren Tokens zusammengesetzt, welche aus den einzelnen Wörtern der Texte entstehen.

```Python
# Funktion zur Umwandlung in ein Doc-Objekt von spacy
nlp = spacy.load("en_core_web_sm")

# Umwandlung der ersten Mail in ein Doc-Objekt
doc = nlp(df_mails.loc[0, "Mails"])
```

Ein Vorteil der hierdurch hinzu kommt ist die Möglichkeit des Durchlaufens des Doc-Objektes anhand der Tokens. Hierdurch lässt sich das Doc-Objekt leicht als Liste schreiben. token.text enthält hierbei den ursprünglichen string, während token selbst ein spacy-Objekt ist.

```Python
# Umwandlung in eine Liste
text_list = [token.text for token in doc]
```

### 3.2 Entfernen der Satzzeichen
In der Regel brauchen wir für Analysen von Texten die Satzzeichen nicht zu beachten. Hierfür bietet das modul 'string' eine Ansammlung aller Satzzeichen. Diese lassen sich direkt in der List Comprehension anwenden:

```Python
# Laden aller Satzzeichen
punctuation = string.punctuation

# Umwandlung in eine Liste ohne Satzzeichen
text_list_punc = [token.text for token in doc if token.text not in punctuation]
```

### 3.3 Lemmatisierung
Eine weitere gute Möglichkeit der Reduzierung der Wörter ist die Lemmatisierung. Hierbei werden Wörter wieder auf ihre Basisform zurück gebracht. 'be', 'am', 'are' und 'is' benötigen 4 Spalten, allerdings sind Konjugationen,Deklinationen, etc. meist nicht von großer Bedeutung, weswegen wir diese Formen auf die Form 'be' reduzieren können und somit nur eine Spalte benötigen würden. Hierfür gibt es bereits in spacy eine Implementierung:

```Python
# Lemmatisierung
text_list_lemmatized = [token.lemma_ for token in doc if token.text not in punctuation]
```
### 3.4 Groß- und Kleinschreibung
Das wahrscheinlich am Naheliegensten ist, dass die Groß-und Kleinschreibung in den meisten Fällen keine Relevanz hat. Hierfür brauchen wir kein spezielles Modul, sondern können einfache string-Operationen durchführen:

```Python
# Wörter klein geschrieben
text_list_lemmatized = [token.lemma_.lower() for token in doc if token.text not in punctuation]
```

### 3.5 Stoppwort-Entfernung
Es gibt viele Wörter, die in eigentlich jeden Texten vorkommen. Dies sind bspw. 'I' und 'you' oder Artikel wie 'the' und 'a'. Diese bieten auch meist wenig Erkenntnisse, und auch hier gibt es eine schnelle Möglichkeit diese zu entfernen. Das Modul nltk bietet zu verschiedenen Sprachen eine Liste an Stoppwörtern, die wir wie die Satzzeichen in die List Comprehension mit aufnehmen können:

```Python
# Laden der Stopwörter
stopwords = nltk.corpus.stopwords.words("english")

text_list_lemmatized = [token.lemma_.lower() for token in doc if token.text not in punctuation and token.lemma_.lower() not in stopwords]
```

Auf diese Weise ließ sich die erste Mail von 17 Wörtern und Zeichen auf die eher wichtigen 8 Wörter reduzieren. Diese Wörter brauchen wir allerdings nicht als Liste, sondern wieder als einzelnen string in unserem DataFrame.

## 4. Aufbereitung der Daten
Die einzelnen vorhergegangenen Schritte lassen sich zusammenfassen und auf unseren DataFrame anwenden:

```Python
# Funktionsdefinition zur Text-Preparation
def text_cleaner(text):
    doc = nlp(text)
    text_list_lemmatized = [token.lemma_.lower() for token in doc if token.text not in punctuation and token.lemma_.lower() not in stopwords]
    final_text = " ".join(text_list_lemmatized)
    return final_text

# Anwenden der Funktion auf die Spalte "Mails"
df_mails["Mails_lemmatized"] = df_mails["Mails"].apply(text_cleaner)
```

## 5. CountVectorizer (BoW-Methode)
Nachdem die Texte bereinigt wurden lassen sie sich nun Vektorisieren. die sogenante 'Bag of Words-Methode' (BoW) funktioniert hierbei ähnlich zum One-Hot-Encoding:
Jedes Wort bekommt eine eigene Spalte, in welcher die Anzahl dieses Wortes in den Texten notiert wird. Kommt in einem Text 2x das wort gread vor, so steht in der Zeile von diesem Text und der Spalte "great" eine '2'. Die Position des Wortes innerhalb des Satzes spielt hierbei keinerlei Rolle.
Hierfür bietet sklearn den CountVectorizer an, welcher die Arbeit für uns übernimmt:

```Python
# Initialisieren des CountVectorizer
from sklearn.feature_extraction.text import CountVectorizer
count_vectorizer = CountVectorizer()

# Features auswählen
features_train = df_mails["Mails_lemmatized"]

# fit_transform
# Wichtig: Der CountVectorizer nimmt nur Series an, keine DataFrames!
features_train_bow = count_vectorizer.fit_transform(features_train)
```

## 6. Gewichten der einzelnen Wörter
in vielerlei Hinsicht kann es Sinn machen die Wörter zu Gewichten. So könnte das Wort "great", welches in einem Text mit 7 Wörtern vorkommt viel wichtiger sein als wenn es in einem Text mit 100 Wörtern vorkommt. Genau so andersherum kann das Wort "great" sehr wichtig sein, wenn es nur in einem einzelnen Text vorkommt, als wenn es in jedem Text vorkommt, da es in diesem Fall kaum bis gar keine Erkenntnis liefert.

### 6.1 Term-Frequency (TF)
Die Term-Frequency gibt die relative Häufigkeit an, wie oft ein Wort in einem Text vorkommt. Hierbei wird die Anzahl des entsprechenden Wortes durch die Anzahl aller Wörter geteilt.
Beispiel:
    "Great food and great staff!"
    TF("great") = 2/5 = 0.4
Die TF kann dadurch Werte von 0 bis 1 erreichen. Hierbei würde ein 0 gleichbedeutend mit "Das Wort kommt gar nicht in dem Text vor" und eine 1 mit "Der Text besteht nur aus dem Wort" sein.

### 6.2 Inverse-Document-Frequency (IDF)
Die Inverse-Document-Frequency setzt in Relation in wie vielen Texten ein Wort kommt zu der Gesamtanzahl aller Texte. Hierbei wird die Gesamtanzahl aller Texte durch die Anzahl der Texte geteilt, die das entsprechende Wort enthalten. Anschlißend wird von dem Ergebnis der Logarithmus genommen.
Beispiel:
    "Great food and great staff"
    "A great spot for dinner and drinks!"
    "an exellent spot for fine dining!"
    "Slow service and rude staff, will not be coming back."
    "I enjoyed the great wine selection!"

    Wir haben von 5 Texten 3 Texte, in denen das Wort "great" vorkommt. Damit ergibt sich folgende Rechnung:
    IDF("great") = log(5/3) = 0.51
Die IDF kann dadurch Werte größer gleich 0 erreichen. Hierbei würde eine 0 gleichbedeutend mit "Das Wort kommt in jedem Text vor" sein. Mit steigendem Wert kommt das Wort in weniger Texten vor.

### 6.3 TF-IDF
Um beide Gewichtungen gleichermaßen zu betrachten lässt sich das Produkt von TF und IDF bilden. Beide Gewichtungen sind gleich monoton: Mit steigendem Wert nimmt die Wichtigkeit eines Wortes zu.
    TF-IDF = TF * IDF

## 7. TfidfVectorizer
Der TfidfVectorizer arbeitet ähnlich zu dem CountVectorizer, allerdings bestimmt dieser nicht die aboluten Häufigkeiten, sondern den TF-IDF Wert eines Wortes pro Text.

```Python
# Initialisieren des TfidfVectorizer
from sklearn.feature_extraction.text import TfidfVectorizer
tfidf_vectorizer = TfidfVectorizer()

# Wichtig: Der CountVectorizer nimmt nur Series an, keine DataFrames!
features_train_tfidf = tfidf_vectorizer.fit_transform(features_train)

```

## 8. Zusammenfassung
    - Aufbereitung der Daten durch Entfernung der Satzzeichen, Entfernung von Stoppwörtern, Lemmatisierung und Umnwandlung von Grpßschreibung zu Kleinschreibung
    - Vektorisierung durch die BoW-Methode (CountVectorizer) anhand der Häufigkeiten im Text
    - Vektorisierung durch TF-IDF-Vektorisierung (TfidfVektorizer) anhand der Relevanz eines Wortes 
    