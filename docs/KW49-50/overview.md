# Grundlagen von Data Science

Data Science ist ein interdisziplinäres Feld, das datengetriebene Erkenntnisse gewinnt, um Entscheidungsprozesse zu verbessern und neue Muster sowie Zusammenhänge aufzudecken. Dieses Kapitel bietet dir eine Einführung in die grundlegenden Konzepte und Prinzipien, die im Zentrum dieses spannenden Bereichs stehen.

---

## Was ist Data Science?

Data Science kombiniert verschiedene Disziplinen, darunter:

- **Statistik**: Die Wissenschaft der Datenanalyse und des Schlussfolgerns.
- **Informatik**: Methoden zur Verarbeitung, Analyse und Visualisierung großer Datenmengen.
- **Domänenwissen**: Spezifisches Wissen über den Anwendungsbereich der Datenanalyse.

Das Ziel von Data Science ist es, aus strukturierten und unstrukturierten Daten Wissen zu generieren.


Wir haben in der Einführung zur Data Analysis bereits 4 Grundlegende Arten der Datenanalyse (Descriptive Analysis, Diagnostic Analysis, Predictive Analysis, Prescriptive Analysis) kennengelernt. Die einzelnen Schritte dieser Analysen sind ein wesentlicher Bestandteil der Data Science. Darüber hinaus gibt es weitere wichtige Konzepte und Methoden, die in der Datenwissenschaft eine Rolle spielen. In einem Kompletten Data Science Prozess werden unter anderem die folgenden Schritte durchlaufen:

### **1. Problemdefinition**
- **Ziel**: Verstehen, welches Problem gelöst werden soll.
- **Fragen**: Welche Entscheidungen sollen unterstützt werden? Welche Daten sind verfügbar?

### **2. Datenbeschaffung**
- **Quellen**: Daten können aus internen Systemen, externen APIs, Sensoren oder Web-Scraping stammen.
- **Wichtig**: Qualität und Verfügbarkeit der Daten beurteilen.

### **3. Datenaufbereitung**
- **Data Cleaning**: Umgang mit fehlenden Werten, Duplikaten oder Ausreißern.
- **Feature Engineering**: Erstellung relevanter Variablen, die Modelle verbessern.
- **Preprocessing**: Skalieren, Normalisieren und Kodieren von Daten.
- **ETL-Prozesse**: (Extract, Transform, Load) Umwandlung und Integration von Daten aus verschiedenen Quellen.

### **4. Modellierung**
- **Ziel**: Aufbau von prädiktiven oder deskriptiven Modellen.
- **Methoden**: Klassifikation, Regression, Clustering, etc.

### **5. Validierung**
- **Metriken**: Genauigkeit, F1-Score, RMSE.
- **Cross-Validation**: Prüfung der Generalisierungsfähigkeit eines Modells.

### **(6. Deployment)**
- **Anwendung**: Bereitstellung von Modellen in produktiven Systemen.
- **Wartung**: Monitoring der Modellleistung und Aktualisierung.

---

## Mathematische Optimierung in Data Science

Data Science setzt sich zwar primär aus den Statistik, Informatik und Domänenwissen zusammen, aber es gibt auch viele andere Disziplinen, die in diesem Bereich eine Rolle spielen. Zu diesen gehört insbesondere die Mathematische Optimierung. Bei vielen statistischen Methoden und Machine-Learning-Modellen handelt es sich um Optimierungsprobleme, bei denen das Ziel darin besteht, die besten Parameter für ein Modell zu finden. Wir gehen im Nachfolgenden auf einige Begrifflichkeiten und Konzepte der Mathematischen Optimierung ein, welche uns als Data Scientisten regelmäßig begegnen werden.


### **1. Definition**
- **Ziel**: Finden der besten Lösung für ein Problem unter gegebenen Einschränkungen.
- **Beispiele**: Minimierung des Fehlers eines Modells, Maximierung der Genauigkeit oder Optimierung von Ressourcen.

### **2. Gradient Descent**
- **Beschreibung**: Iterativer Algorithmus, um die optimalen Parameter eines Modells zu finden.
- **Funktionsweise**: Bewegung in Richtung des steilsten Gradienten der Fehlerfunktion, um das Minimum zu erreichen.
- **Einsatzgebiete**: Training neuronaler Netzwerke, lineare Regression.

### **3. Regularisierung**
- **Ziel**: Verhindern von Overfitting durch Hinzufügen von Straftermen in die Optimierungsfunktion.
- **Beispiele**: L1-Regularisierung (Lasso), L2-Regularisierung (Ridge).

### **4. Optimierungsprobleme im Kontext von Data Science**
- **Lineare Programmierung**: Optimierung einer linearen Zielfunktion unter linearen Nebenbedingungen.
- **Nichtlineare Optimierung**: Behandlung komplexerer Probleme, bei denen Zielfunktion oder Nebenbedingungen nicht linear sind.
- **Kombinatorische Optimierung**: Lösung diskreter Probleme, wie z. B. die Auswahl der besten Feature-Kombination.

---


Vor einigen Jahren wurde unter dem Begriff "Data Science" nahezu alles zusammengefasst, was mit Daten zu tun hatte. Heute hat sich das Feld weiterentwickelt und spezialisiert, wobei verschiedene Rollen und Aufgabenbereiche entstanden sind. Im Folgenden werden einige wichtige Rollen in Data Science vorgestellt, die in Unternehmen und Organisationen eine zentrale Rolle spielen.

##  Wichtige Rollen in Data Science

### **Data Scientist**
- Verantwortlich für die Analyse und Modellierung der Daten.
- Kombiniert Statistik, Programmierung und Domänenwissen.

### **Data Engineer**
- Entwickelt und pflegt Datenpipelines und Infrastruktur.
- Sicherstellung, dass Daten effizient und skalierbar verarbeitet werden.

### **Data Analyst**
- Fokus auf Datenvisualisierung und Berichterstattung.
- Ziel: Geschäftsrelevante Erkenntnisse kommunizieren.

### **Machine Learning Engineer**
- Spezialisiert auf die Entwicklung und Implementierung von ML-Modellen.
- Arbeitet eng mit Data Scientists zusammen, um Modelle in Produktionsumgebungen zu überführen.

### **Business Analyst**
- Übersetzt Geschäftsanforderungen in datenbasierte Lösungen.
- Fokussiert auf die Anwendung von Daten zur Optimierung von Geschäftsprozessen.

### **Data Architect**
- Entwirft und implementiert Datenbanken und -architekturen.
- Sicherstellung, dass Daten effizient gespeichert und abgerufen werden können.


---

In der Umgangssprache werden datengbasierte Projekte und teilweise sogar Software Projekte einfach als KI Projekte bezeichnet. In der Realität ist KI jedoch nur ein Teilbereich der Data Science. In diesem Abschnitt werden die Unterschiede und Beziehungen zwischen KI, Maschinellem Lernen, Deep Learning und Statistik erläutert.

## Begriffe aus dem Data Science Kosmos

In der Welt von Data Science gibt es viele Begriffe, die oft synonym oder missverständlich verwendet werden. Wir führen hier einige der wichtigsten Begriffe auf und erklären ihre Bedeutung und Beziehung zueinander. Die Berufsfelder aus dem obigen Abschnitt werden dabei nicht wiederholend aufgeführt.

- **Künstliche Intelligenz (KI)**: Der Überbegriff für Technologien, die menschenähnliches Denken und Handeln nachahmen.
- **Maschinelles Lernen (ML)**: Ein Teilbereich der KI, der sich auf Algorithmen konzentriert, die aus Daten lernen können.
- **Deep Learning**: Ein Teilbereich des ML, der neuronale Netze mit vielen Schichten verwendet.
- **Statistik**: Fundamentale Methoden zur Analyse und Interpretation von Daten.
- **Data Mining**: Extraktion von Mustern und Informationen aus großen Datenmengen.
- **Big Data**: Verarbeitung und Analyse großer Datenmengen, die mit traditionellen Methoden nicht möglich wären.
- **Business Intelligence (BI)**: Technologien und Anwendungen zur Analyse von Geschäftsdaten.

---





Wir werden uns in den nächsten Abschnitten mit der Datenverarbeitung beschäftigen. Genauer werden wir auf Feature Enigneering eingehen. Feature Engineering ist ein wichtiger Schritt im Data-Science-Prozess, bei dem neue, aussagekräftige Variablen aus vorhandenen Daten erstellt werden. Dieser Prozess ermöglicht es, relevante Informationen zu extrahieren und in einer Form bereitzustellen, die von Algorithmen optimal genutzt werden kann.
