# Begriffe aus dem Data-Science-Kosmos

In der Welt der Datenwissenschaft begegnen wir häufig Begriffen, die eng miteinander verwandt sind, aber unterschiedliche Bedeutungen haben. Dieses Kapitel bietet dir eine strukturierte Übersicht, um Klarheit in die wichtigsten Begriffe zu bringen und sie einzuordnen.

---

## 1. Grundlagenbegriffe

### **Künstliche Intelligenz (KI)**

- **Definition**: KI umfasst Systeme, die menschenähnliches Denken und Verhalten simulieren, z. B. durch Problemlösung, Mustererkennung oder Entscheidungsfindung.
- **Einsatzgebiete**: Sprachübersetzung, Bilderkennung, autonome Fahrzeuge.
- **Beziehung zu anderen Begriffen**: Oberbegriff für Machine Learning und Deep Learning.

### **Machine Learning (ML)**

- **Definition**: Teilbereich der KI, der es Systemen erlaubt, aus Daten zu lernen und Vorhersagen oder Entscheidungen zu treffen, ohne explizit programmiert zu sein.
- **Typen von ML**:
  - Supervised Learning (z. B. Regression, Klassifikation)
  - Unsupervised Learning (z. B. Clustering, Dimensionsreduktion)
  - Reinforcement Learning (z. B. Steuerung von Robotern)
- **Beispiel**: Vorhersage von Hauspreisen basierend auf historischen Daten.

### **Deep Learning (DL)**

- **Definition**: Spezialisierter Bereich des Machine Learning, der auf neuronalen Netzwerken mit vielen Schichten basiert.
- **Anwendung**: Bilderkennung, Spracherkennung, Generative Modelle (z. B. Text-to-Image-Generierung).
- **Beziehung zu ML und KI**: Deep Learning ist ein Teilbereich von ML und somit auch der KI zuzuordnen.

### **Statistik**

- **Definition**: Wissenschaft der Datenanalyse zur Gewinnung von Informationen und zur Entscheidungsfindung.
- **Rolle im Data Science**: Grundlage vieler Algorithmen im ML (z. B. lineare Regression, Hypothesentests).
- **Abgrenzung zu ML**: Statistik betont Erklärbarkeit und Hypothesentestung, während ML primär auf Vorhersage fokussiert ist.

---

## 2. Datenverarbeitung und -strukturen

### **Datenpipeline**

- **Definition**: Prozess, der Daten von der Sammlung über die Verarbeitung bis zur Analyse automatisiert.
- **Bestandteile**: Extraktion, Transformation, Laden (ETL-Prozesse).
- **Beispiel**: Daten von IoT-Geräten werden gesammelt, bereinigt und an ein Analysemodell übergeben.

### **Big Data**

- **Definition**: Verarbeitung und Analyse extrem großer Datenmengen, die mit traditionellen Methoden nicht effizient bearbeitet werden können.
- **Merkmale (die 4 Vs)**: Volume, Velocity, Variety, Veracity.
- **Technologien**: Hadoop, Spark.

### **Cloud Computing**

- **Definition**: Bereitstellung von Rechenleistung, Speicher und Anwendungen über das Internet.
- **Bezug zu Data Science**: Ermöglicht skalierbare Speicherung und Verarbeitung großer Datenmengen.
- **Beispiele**: Amazon Web Services (AWS), Google Cloud Platform (GCP).

---

## 3. Analysemethoden und Modellierung

### **Explorative Datenanalyse (EDA)**

- **Definition**: Erste Analyse von Daten zur Entdeckung von Mustern, Anomalien und Zusammenhängen.
- **Werkzeuge**: Pandas, Seaborn, Matplotlib.
- **Beziehung zu ML**: Bereitet Daten für ML-Modelle vor.

### **Feature Engineering**

- **Definition**: Erstellung neuer Variablen (Features), um die Leistung eines Modells zu verbessern.
- **Beispiele**: Normalisierung, One-Hot-Encoding, Feature-Auswahl.
- **Rolle in ML**: Entscheidender Faktor für Modellgenauigkeit.

### **Preprocessing**

- **Definition**: Vorbereitung der Rohdaten für die Modellierung.
- **Beispiele**: Skalierung, fehlende Werte behandeln, Kategorisierung.
- **Unterschied zu Feature Engineering**: Beim Preprocessing geht es um generelle Datenvorbereitung, während Feature Engineering neue Informationen aus bestehenden Daten erzeugt.

### **Data Cleaning**

- **Definition**: Identifikation und Korrektur fehlerhafter, unvollständiger oder ungenauer Daten.
- **Beispiele**: Entfernen von Duplikaten, Bereinigung von Textdaten, Umgang mit Ausreißern.
- **Rolle im Workflow**: Grundlegender Schritt, der sicherstellt, dass Daten verlässlich sind.

---

## 4. Technologische Begriffe

### **APIs (Application Programming Interfaces)**

- **Definition**: Schnittstellen, die den Zugriff auf Funktionen oder Daten eines Systems erlauben.
- **Rolle in Projekten**: Verbindung von Modellen mit Anwendungen oder Datenquellen.
- **Beispiel**: REST-APIs, FastAPI.

### **Datenbanken**

- **Relational**: Daten in Tabellenform (z. B. MySQL, PostgreSQL).
- **NoSQL**: Flexible Speicherung von unstrukturierten Daten (z. B. MongoDB, Cassandra).
- **Relevanz**: Speicherung, Abfrage und Analyse von Daten.

### **Containerization**

- **Definition**: Verpackung einer Anwendung mit ihrer gesamten Abhängigkeit in einem Container.
- **Technologie**: Docker.
- **Nutzen**: Erleichtert die Bereitstellung und Skalierung.

---

## 5. Abgrenzung ähnlicher Begriffe

### **KI vs. ML vs. DL vs. Statistik**

- **KI**: Der umfassende Rahmen.
- **ML**: Lässt Maschinen aus Daten lernen.
- **DL**: Subdisziplin, spezialisiert auf neuronale Netzwerke.
- **Statistik**: Fokus auf Dateninterpretation und Erklärbarkeit.

### **Big Data vs. Datenanalyse**

- **Big Data**: Umgang mit der Masse an Daten.
- **Datenanalyse**: Fokus auf das Verstehen und die Interpretation der Daten.

### **Feature Engineering vs. Preprocessing vs. Data Cleaning**

- **Feature Engineering**: Erstellung neuer Features, die die Modellleistung verbessern (z. B. Kombination von Variablen, Erstellung von Zeitmerkmalen).
- **Preprocessing**: Allgemeine Datenvorbereitung wie Normalisierung, Skalierung oder Encoding.
- **Data Cleaning**: Beseitigung von Problemen in den Rohdaten, wie fehlerhaften Einträgen oder fehlenden Werten.

