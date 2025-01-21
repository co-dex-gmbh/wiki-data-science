
Mit Multipage-Apps ermöglicht Streamlit die Erstellung von Anwendungen mit mehreren Ansichtsseiten. Dies verbessert die Benutzerfreundlichkeit und Struktur von komplexen Dashboards und Apps, indem Inhalte logisch auf verschiedene Seiten verteilt werden können.  

---

### **Grundkonzept**  
Eine **Multipage-App** in Streamlit basiert auf dem Konzept eines `pages`-Verzeichnisses:  
- Jede Unterseite ist eine eigene Python-Datei im Ordner `pages`.  
- Streamlit lädt diese Seiten automatisch und fügt sie als auswählbare Tabs in die Anwendung ein.  
- Jede Datei wird unabhängig ausgeführt, sobald sie ausgewählt wird.  

---

### **Einrichten einer Multipage-App**  
1. **Hauptskript:**  
   Das Hauptskript bleibt die Startseite deiner App.  
   ```python
   import streamlit as st

   st.title("Hauptseite")
   st.write("Willkommen zu meiner Multipage-App!")
   ```  

2. **Erstellen des `pages`-Ordners:**  
   Lege ein Verzeichnis namens `pages` im gleichen Verzeichnis wie dein Hauptskript an.  

3. **Erstellen von Seiten:**  
   Füge Python-Dateien in den `pages`-Ordner ein, z. B.:  
   - `pages/Seite_1.py`  
   - `pages/Seite_2.py`  
   Jede Datei entspricht einer eigenen Seite.  

4. **Seitenstruktur und Inhalte:**  
   Jede Datei verhält sich wie ein normales Streamlit-Skript:  
   ```python
   import streamlit as st

   st.title("Seite 1")
   st.write("Dies ist die erste Unterseite.")
   ```  

---

### **Dateibenennung und Reihenfolge**  
- Standardmäßig werden die Seiten alphabetisch im Menü sortiert.  
- Für eine benutzerdefinierte Reihenfolge kannst du Zahlen voranstellen:  
  - `pages/1_Seite_1.py`  
  - `pages/2_Seite_2.py`  
- Diese Zahlen erscheinen nicht im Menü, sondern dienen nur der Sortierung.  

---

### **Navigation zwischen Seiten**  
Streamlit fügt automatisch ein Menü in der linken Seitenleiste hinzu, über das Benutzer zwischen den Seiten navigieren können.  



**Weitere Informationen:**  
[Streamlit Dokumentation – Multipage Apps](https://docs.streamlit.io/develop/concepts/multipage-apps/pages-directory)  