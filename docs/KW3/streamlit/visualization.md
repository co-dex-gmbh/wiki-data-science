

Einer der Hauptvorteile von Streamlit ist, dass es dafür ausgelegt wurde, mit Dataframes und Visualisierungen zu arbeiten. Dadurch können grafiken sehr schnell und einfach erstellt werden. Bibliotheken wie Matplotlib, Seaborn oder Plotly sind direkt integriert. Diese Flexibilität ermöglicht es, visuelle Darstellungen individuell an die Bedürfnisse deines Projekts anzupassen, sei es für explorative Analysen oder die Kommunikation von Ergebnissen.

**Beispiel**  
```python
import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

# Daten und Plot
data = pd.DataFrame({"Kategorie": ["A", "B", "C"], "Werte": [10, 20, 15]})
fig, ax = plt.subplots()
data.plot(kind="bar", x="Kategorie", y="Werte", ax=ax)

# Ausgabe
st.pyplot(fig)
```


Streamlit bietet mit sogenannten `magic commands` sogar eine Abkürzung, um Texte und Dataframes auszugeben. Diese können direkt in den Code integriert werden und ersparen dir das Schreiben von `st.write()` oder `st.dataframe()`.

**Link zum Nachschlagen**  
[Streamlit Dokumentation - Charts](https://docs.streamlit.io/get-started/fundamentals/main-concepts)
[Streamlit Magic Commands](https://docs.streamlit.io/develop/api-reference/write-magic/magic)

---