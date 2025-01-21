


Anders als in Flask wird Interaktivität in Streamlit sehr intuitiv ermöglicht. Zustände können wir so entweder in der Session oder sogar in Variablen direkt speichern und aktualisieren. Zu beachten ist hierbei jedoch, dass im Standardzustand das Streamlit Skript lediglich einmal von oben nach unten durchlaufend interpretiert wird.

**Beispiel**  
```python
import streamlit as st

if "counter" not in st.session_state:
    st.session_state.counter = 0

if st.button("Erhöhe Zähler"):
    st.session_state.counter += 1

st.write(f"Zähler: {st.session_state.counter}")
```

**Link zum Nachschlagen**  
[Streamlit Dokumentation - Session State](https://docs.streamlit.io/library/api-reference/session-state)

---