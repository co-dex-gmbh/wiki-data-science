
In Streamlit-Anwendungen ermöglicht der **Session State**, Daten und Zustände über mehrere Interaktionen hinweg zu speichern. Er ist essenziell, um dynamische und interaktive Anwendungen zu erstellen, bei denen Werte nicht bei jedem Skript-Neustart zurückgesetzt werden.  

### **Funktionen von Session State**  
Der Session State bietet eine Möglichkeit, Informationen wie Benutzerinteraktionen, Zähler oder Formulareingaben während der Laufzeit der App zu verwalten. 

### **Verwendung von Session State**  
- **Initialisierung von Zuständen:**  
  Überprüfe, ob ein Zustand existiert, und setze einen Standardwert, falls nicht.  
  ```python
  import streamlit as st

  if "counter" not in st.session_state:
      st.session_state.counter = 0
  ```  

- **Manipulation von Zuständen:**  
  Aktualisiere den Zustand durch Interaktionen, z. B. bei Button-Klicks.  
  ```python
  if st.button("Zähler erhöhen"):
      st.session_state.counter += 1

  st.write(f"Aktueller Zählerwert: {st.session_state.counter}")
  ```  

- **Callbacks mit Session State:**  
  Widgets können durch Callbacks Zustände direkt ändern.  
  ```python
  def reset_counter():
      st.session_state.counter = 0

  st.button("Zähler zurücksetzen", on_click=reset_counter)
  ```  

### **Besonderheiten von Session State**  
1. **Permanenz während der Sitzung:** Werte bleiben während einer Benutzersitzung erhalten, unabhängig davon, wie oft das Skript neu geladen wird.  
2. **Key-basierte Struktur:** Zustände werden mithilfe eines Dictionary-ähnlichen Keys gespeichert und abgerufen.  
   ```python
   st.session_state["username"] = "Benutzer123"
   st.write(st.session_state["username"])
   ```  

### **Anwendungsfälle für den Session State**  
- **Interaktive Formulare:** Bewahre Zwischenergebnisse und Eingabewerte während einer Sitzung.  
- **Fortschrittsverfolgung:** Verwalte schrittweise Prozesse wie Multi-Step-Formulare oder Workflow-Apps.  
- **Zustandsabhängige UI:** Ändere die Darstellung von Elementen basierend auf gespeicherten Werten.  

### **Best Practices**  
- Initialisiere alle Schlüssel zu Beginn der App, um Probleme mit nicht existierenden Werten zu vermeiden.  
- Nutze Callbacks, um Code sauber und modular zu halten.  
- Lösche den Zustand gezielt, falls veraltete Werte das Verhalten der App beeinträchtigen könnten.  

**Weitere Informationen:**  
[Streamlit Dokumentation – Session State](https://docs.streamlit.io/develop/concepts/architecture/session-state)