# Umgang mit Duplikaten in Daten

In der Datenbereinigung stellen Duplikate ein häufiges Problem dar. Duplikate sind Einträge in einem Datensatz, die identisch oder nahezu identisch sind und die Analyse verfälschen können. Ein bewusster und systematischer Umgang mit Duplikaten ist entscheidend, um valide Ergebnisse zu erzielen.

---

## Warum sind Duplikate problematisch?

Duplikate können aus verschiedenen Gründen auftreten:

- **Fehlerhafte Datenintegration**: Beim Zusammenführen von Daten aus unterschiedlichen Quellen entstehen oft redundante Einträge.
- **Mehrfache Datenerfassung**: Beispielsweise können Kunden ein Formular mehrfach ausgefüllt haben.
- **Automatisierte Prozesse**: Systeme, die ohne ausreichende Kontrollmechanismen Daten generieren, können unbeabsichtigt doppelte Werte erzeugen.

Konsequenzen von Duplikaten sind unter anderem:

- Verzerrte Analysen durch überrepräsentierte Werte.
- Ineffiziente Speicher- und Rechenressourcen.
- Probleme bei Modellen, die davon ausgehen, dass jeder Datensatz einzigartig ist.

---

## Arten von Duplikaten

Es gibt verschiedene Arten von Duplikaten, die je nach Kontext unterschiedlich behandelt werden müssen:

**Exakte Duplikate**
   - Diese Einträge stimmen in allen Feldern überein.
   - Beispiel:
     | ID  | Name       | Alter | Ort    |
     | --- | ---------- | ----- | ------ |
     | 001 | Anna Meier | 29    | Berlin |
     | 001 | Anna Meier | 29    | Berlin |

**Nahezu Duplikate**
   - Diese Einträge unterscheiden sich geringfügig, z. B. durch Tippfehler oder unterschiedliche Schreibweisen.
   - Beispiel:
     | ID  | Name          | Alter | Ort     |
     | --- | ------------- | ----- | ------- |
     | 002 | Thomas Schmid | 35    | Hamburg |
     | 003 | T. Schmid     | 35    | Hamburg |

---

## Vorgehen zur Identifikation und Behandlung von Duplikaten

### **Identifikation von Duplikaten**
Die Identifikation ist der erste Schritt und kann je nach Art der Duplikate unterschiedlich erfolgen:

- **Exakte Duplikate finden**:
  - In Python können exakte Duplikate mit Pandas identifiziert werden:
    ```python
    import pandas as pd

    # Beispiel-Datensatz
    data = {
        'ID': [1, 2, 3, 1],
        'Name': ['Anna Meier', 'Thomas Schmid', 'Maria Kurz', 'Anna Meier'],
        'Alter': [29, 35, 40, 29]
    }
    df = pd.DataFrame(data)

    # Duplikate finden
    duplicates = df[df.duplicated()]
    print(duplicates)
    ```

- **Nahezu Duplikate finden**:
  - Hier helfen Ansätze wie Fuzzy Matching, beispielsweise mit der Bibliothek `fuzzywuzzy` oder ähnlichen Tools:
    ```python
    from fuzzywuzzy import fuzz
    from fuzzywuzzy import process

    # Beispiel: Vergleich zweier Namen
    score = fuzz.ratio("Thomas Schmid", "T. Schmid")
    print(score)  # Ausgabe: Über 80%, also wahrscheinlich Duplikat
    ```

### **Behandlung von Duplikaten**

#### **Exakte Duplikate entfernen**
- **Einfaches Entfernen:**
  ```python
  # Entfernen von exakten Duplikaten
  df_cleaned = df.drop_duplicates()
  ```
- **Erhalt bestimmter Einträge:** Wenn du die erste oder letzte Instanz eines Duplikats behalten möchtest, kannst du dies steuern:
  ```python
  df_cleaned = df.drop_duplicates(keep='first')  # Behalte den ersten Eintrag
  ```

#### **Nahezu Duplikate bereinigen**
- **Manuelle Prüfung:** Besonders bei kleineren Datensätzen lohnt sich die manuelle Sichtung.
- **Automatisierte Verfahren:**
  - Berechnung von Ähnlichkeitsscores.
  - Erstellung von Regeln zur Vereinheitlichung (z. B. Namenskonventionen).

#### **Zusammenführen von Duplikaten**
- Wenn Informationen in den Duplikaten variieren, kannst du diese zusammenführen:
  ```python
  # Gruppieren und Aggregieren
  df_grouped = df.groupby('ID').agg({
      'Name': 'first',
      'Alter': 'mean'
  })
  ```

---

## Beispiele aus der Praxis

- **Kundenlisten bereinigen:**
  Ein Unternehmen hat mehrere Listen von Kunden aus verschiedenen Regionen zusammengeführt. Dabei entstehen oft exakte und nahe Duplikate, die manuell oder mit Matching-Algorithmen behandelt werden müssen.

- **Web-Scraping-Daten:**
  Beim Scraping von Websites entstehen oft doppelte Einträge, wenn dieselbe Seite mehrfach abgefragt wird. Hier hilft die Verwendung einer eindeutigen ID oder eines Hashes, um Duplikate zu identifizieren.
