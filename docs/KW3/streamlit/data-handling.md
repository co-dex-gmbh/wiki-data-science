


Daten effizient hochzuladen und anzuzeigen ist ein zentraler Bestandteil jedes Dashboards. Streamlit bietet Möglichkeiten, Daten direkt aus Dateien oder Datenbanken zu laden und interaktiv darzustellen.

**Beispiel**  
```python
import streamlit as st
import pandas as pd

uploaded_file = st.file_uploader("Lade eine CSV-Datei hoch")
if uploaded_file is not None:
    df = pd.read_csv(uploaded_file)
    st.dataframe(df)
```

Darüber hinaus können wir Daten auch direkt aus Datenbank abfragen und anzeigen:

**Beispiel**  
```python
import streamlit as st

# Verbindung zur Datenbank
conn = sqlite3.connect("example.db")

# SQL-Abfrage
query = "SELECT * FROM table"
df = pd.read_sql(query, conn)

# Anzeige der Daten
st.dataframe(df)
```

Dies umgeht in einigen Fällen die Notwendigkeit, Daten lokal zu speichern und ermöglicht es, Daten direkt in der Web-App zu verarbeiten.

**Link zum Nachschlagen**  
[Streamlit Dokumentation - File Uploader](https://docs.streamlit.io/library/api-reference/widgets/st.file_uploader)

