
Caching ist ein zentraler Bestandteil der Streamlit-Architektur, der dabei hilft, die Leistung von Anwendungen zu optimieren. Es ermöglicht das Zwischenspeichern von aufwendigen Berechnungen, Datenbankabfragen oder anderen ressourcenintensiven Operationen, sodass diese nicht bei jedem Neuladen erneut ausgeführt werden müssen.  

Streamlit bietet zwei Arten von Caching:  

- **Daten-Caching (`@st.cache_data`)**  
  Diese Methode speichert Ergebnisse von Funktionen, die Daten laden oder verarbeiten. Sie ist besonders nützlich für Operationen wie das Laden von großen CSV-Dateien oder API-Anfragen.  

  **Beispiel:**  
  ```python
  import streamlit as st
  import pandas as pd
  
  @st.cache_data
  def load_data():
      return pd.read_csv("daten.csv")
  
  data = load_data()
  st.write(data)
  ```  

- **Objekt-Caching (`@st.cache_resource`)**  
  Diese Methode wird für Objekte genutzt, die instanziiert werden müssen, wie Datenbankverbindungen oder Modelle.  

  **Beispiel:**  
  ```python
  import streamlit as st
  import sqlalchemy
  
  @st.cache_resource
  def create_connection():
      return sqlalchemy.create_engine("sqlite:///datenbank.db")
  
  connection = create_connection()
  ```  

**Grundprinzipien des Cachings**  
- **Determinismus:** Der Output einer gecachten Funktion muss bei gleichen Input-Werten immer gleich sein.  
- **Eingabewerte:** Streamlit verwendet die Parameter der Funktion, um zu entscheiden, ob eine gecachte Version wiederverwendet wird.  
- **Unveränderbarkeit:** Objekte, die an gecachte Funktionen übergeben werden, sollten nicht verändert werden, da dies zu unerwartetem Verhalten führen kann.  

**Wann Cache-Inhalte aktualisiert werden:**  
- Änderungen am Quellcode.  
- Änderungen der Funktionseingaben.  
- Explizites Leeren des Caches über `st.cache_data.clear()` oder `st.cache_resource.clear()`.  

Caching ist ein mächtiges Werkzeug, um die Performance von Streamlit-Apps zu verbessern. Dennoch sollte es bewusst eingesetzt werden, um potenzielle Probleme, wie das Zwischenspeichern veralteter Daten, zu vermeiden.  

**Weitere Informationen:**  
[Streamlit Dokumentation – Caching](https://docs.streamlit.io/develop/concepts/architecture/caching)