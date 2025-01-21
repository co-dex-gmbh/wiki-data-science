

In Streamlit gibt es Layout-Optionen, um Inhalte effizient zu organisieren. Mit diesen kannst du die Inhalte deiner App durch Layout-Optionen wie Seitenleisten oder Mehrspaltenansichten übersichtlich gestalten.

**Beispiel**  
```python
import streamlit as st

# Sidebar und Hauptbereich
st.sidebar.title("Navigation")
st.sidebar.radio("Seiten", ["Home", "Kontakt"])

st.title("Hauptbereich")
st.write("Hier steht der Hauptinhalt.")
```

Die Struktur ist grundsätzlich so aufgebaut, dass Elemente untereinander in einer Spalte organisiert werden. Die einzelnen Elemente (Widgets) werden über `st.__element_name__ `aufgerufen.


Um eine App zu starten, wird der Befehl `streamlit run your_script.py`verwendet. Das funktioniert übrigens sogar mit Github URLs. 


### Funktionsweise von Streamlit Apps

Streamlit-Apps basieren auf einer Architektur, die das Schreiben wie bei gewöhnlichen Python-Skripten ermöglicht. Die gesamte App wird bei Änderungen neu ausgeführt, und zwar in folgenden Fällen:

- Wenn der Quellcode der App geändert wird.  
- Wenn Nutzer mit Widgets interagieren (z. B. Schieberegler bewegen, Text eingeben, Buttons klicken).  
- Bei Nutzung von Callbacks (z. B. über `on_change` oder `on_click`), die immer vor dem Rest des Skripts ausgeführt werden.  

Um die Performance zu optimieren, nutzt Streamlit den `@st.cache_data`-Decorator, der teure Berechnungen beim erneuten Ausführen der App überspringt.

**Link zum Nachschlagen**  
[Streamlit Dokumentation - Hauptkonzepte](https://docs.streamlit.io/get-started/fundamentals/main-concepts)
