

Oftmals möchten wir unsere App in mehrere Bereiche aufteilen. Dies können wir beispiesweise druch Spalten und Zeilen umsetzen. In Streamlit erfolgt dies durch die Erstellung eines Zeilen/ Spaltenobjektes. Den einzelnen Spalten/ Zeilen können anschließend Komponenten zugewiesen werden.

**Beispiel**  
```python
import streamlit as st

st.title("Dashboard Layout")
col1, col2 = st.columns(2)
col1.write("Dies ist Spalte 1")
col2.write("Dies ist Spalte 2")
```


Neben Spalten und Zeilen können wir auch weitere Elemente, wie beispieldweise eine Seitenleiste hinzufügen. Hierfür können wir die `st.sidebar`-Funktion verwenden.

**Beispiel**  
```python
import streamlit as st

# Using object notation
add_selectbox = st.sidebar.selectbox(
    "How would you like to be contacted?",
    ("Email", "Home phone", "Mobile phone")
)

# Using "with" notation
with st.sidebar:
    add_radio = st.radio(
        "Choose a shipping method",
        ("Standard (5-15 days)", "Express (2-5 days)")
    )
```


**Link zum Nachschlagen**  
[Streamlit Dokumentation - Columns](https://docs.streamlit.io/library/api-reference/layout/st.columns)
[Sreamlit Dokumentation - Sidebar](https://docs.streamlit.io/get-started/fundamentals/main-concepts#layout)

---
