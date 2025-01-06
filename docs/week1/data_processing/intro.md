# Datenvorverareitung

Einer der wichtigsten Schritte in der Data Science ist das bearbeiten und aufbereiten von Daten. Unsere Modelle sind nur so gut wie die Daten, die wir ihnen geben. Daher wird die Qualität unser Modelle maßgeblich von der Qualität unser Datenverarbeitung beeinflusst.

Die Datenverarbeitung wird in verschiedene Untergebiete aufgeteilt. Zu diesen zählen unter anderem das Data Cleaning, Preprocessing und Feature Engineering.

### **Data Cleaning**
Data Cleaning ist der Prozess der Bereinigung von Daten, um deren Qualität und Konsistenz zu verbessern. Dies ist ein entscheidender Schritt, da unvollständige oder fehlerhafte Daten die Leistung von Modellen erheblich beeinträchtigen können. 

- **Fokus**: Bereinigung der Daten.
- **Beispiele**:
    - **Umgang mit fehlenden Werten**: Fehlende Daten können durch Imputation (z. B. Mittelwert, Median) oder durch Entfernen der betroffenen Einträge behandelt werden.
    - **Entfernung von Duplikaten**: Doppelte Einträge in den Daten können zu Verzerrungen führen und sollten identifiziert und entfernt werden.
    - **Korrektur von Inkonsistenzen**: Unterschiedliche Formate oder Schreibweisen (z. B. Datumsformate) sollten vereinheitlicht werden.

### **Preprocessing**
Preprocessing umfasst alle Schritte, die notwendig sind, um Rohdaten in ein Format zu bringen, das für die Modellierung geeignet ist. Dies beinhaltet die Transformation und Normalisierung der Daten, um sicherzustellen, dass sie von Algorithmen effizient verarbeitet werden können.

- **Fokus**: Vorbereitung der Daten für Modelle.
- **Beispiele**:
    - **Skalieren von Werten**: Daten können auf einen bestimmten Bereich (z. B. 0 bis 1) skaliert werden, um die Leistung von Algorithmen zu verbessern.
    - **Normalisierung**: Anpassung der Datenverteilung, z. B. durch Z-Score-Normalisierung, um die Vergleichbarkeit der Variablen zu gewährleisten.

### **Feature Engineering**
Feature Engineering ist der  Prozess der Erstellung neuer, relevanter Features aus den vorhandenen Daten. Ziel ist es, die Leistungsfähigkeit der Modelle zu steigern, indem zusätzliche Informationen extrahiert und bereitgestellt werden. Das Feature Engineering baut auf den vorherigen Schritten auf und ermöglicht es, die Daten optimal für die Modellierung vorzubereiten.

- **Fokus**: Erstellen neuer, relevanter Features.
- **Beispiele**:
    - **Berechnung einer neuen Variable**: Erstellen neuer Features durch Kombination oder Transformation bestehender Daten, z. B. das Verhältnis von zwei Variablen.
    - **Zeit- und Ortsbezug**: Extrahieren von Informationen wie Wochentagen, Uhrzeiten oder geografischen Regionen aus Datums- oder Standortdaten.
    - **Transformation bestehender Daten**: Anwenden von mathematischen Transformationen wie Logarithmieren oder Skalieren, um die Datenverteilung zu verbessern.
    - **Kodierung kategorialer Daten**: Umwandlung von Kategorien in numerische Werte, um sie für Algorithmen nutzbar zu machen.

Feature Engineering erfordert sowohl technisches Wissen als auch ein tiefes Verständnis der Daten und des Anwendungsbereichs, um die relevantesten und aussagekräftigsten Features zu identifizieren und zu erstellen.

---

## 7. Einführung in Feature Engineering

Feature Engineering ist ein essenzieller Schritt im Data-Science-Prozess, der den Übergang von Rohdaten zu aussagekräftigen Variablen ermöglicht. Dabei geht es darum, die relevanten Informationen aus den Daten zu extrahieren und in einer Form bereitzustellen, die Algorithmen optimal nutzen können.

### **Einordnung von Feature Engineering**
Feature Engineering gehört in den Bereich der Datenvorbereitung, grenzt sich jedoch durch den Fokus auf die Erstellung neuer Variablen ab. Während Data Cleaning und Preprocessing die Qualität und Struktur der Daten verbessern, zielt Feature Engineering darauf ab, Informationen für Modelle nutzbar zu machen.

### **Warum ist Feature Engineering wichtig?**
- **Verbesserte Modellleistung**: Gut gestaltete Features erhöhen die Genauigkeit und Robustheit von Modellen.
- **Domänenwissen einbinden**: Durch spezifisches Wissen über den Anwendungsbereich können wichtige Zusammenhänge besser dargestellt werden.
- **Reduktion von Komplexität**: Feature Engineering kann helfen, irrelevante Informationen zu entfernen und die Analyse zu fokussieren.

### **Methoden des Feature Engineering**
1. **Transformation bestehender Daten**: Logarithmieren, Skalieren oder Normalisieren von Variablen.
2. **Kombination von Variablen**: Erstellen neuer Features durch Kombination bestehender Variablen (z. B. Verhältnisse oder Differenzen).
3. **Ableitung von Zeit- oder Ortsbezug**: Extrahieren von Wochentagen, Uhrzeiten oder geografischen Regionen aus Datums- oder Standortinformationen.
4. **Kodierung kategorialer Daten**: Umwandlung von Kategorien in numerische Werte (z. B. One-Hot-Encoding).

Im Nachfolgenden Abschnitt werden wir uns zunächst mit Methoden des Data Cleaning und Preprocessing beschäftigen, bevor wir tiefer in die Methoden des Feature Engineering eintauchen.