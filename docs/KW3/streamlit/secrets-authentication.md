In Streamlit gibt es eine einfache Möglichkeit, geheime Daten wie API-Schlüssel oder Passwörter sicher zu verwalten: Das **Secrets Management**. Hierbei wird eine Datei namens `.streamlit/secrets.toml` verwendet, um diese sensiblen Informationen zu speichern. Diese Datei wird im Projektverzeichnis abgelegt und ermöglicht es, die Daten über den Befehl `st.secrets` im Code zu verwenden, ohne sie direkt im Quellcode zu hinterlegen.

Die Struktur der Datei folgt dem **TOML**-Format und könnte beispielsweise folgendermaßen aussehen:

```toml
[database]
host = "localhost"
user = "user"
password = "password"
```

Auf die in der Datei gespeicherten Werte kann im Code wie folgt zugegriffen werden:

```python
import streamlit as st
db_host = st.secrets["database"]["host"]
db_user = st.secrets["database"]["user"]
db_password = st.secrets["database"]["password"]
```

Dieses Vorgehen schützt sensible Informationen vor unbeabsichtigtem Zugriff, etwa über öffentliche Repositories. Bei der Bereitstellung der Anwendung auf **Streamlit Cloud** können geheime Daten über das Interface im Dashboard hinzugefügt werden, sodass diese ebenfalls sicher und ohne manuelle Konfiguration verfügbar sind.

Vorteile des Secrets Managements:
- **Sicherheit**: Keine sensiblen Daten im Quellcode.
- **Nachvollziehbarkeit**: Eine klare Trennung zwischen Code und geheimen Informationen.
- **Einfache Handhabung**: Sicherer Zugriff auf vertrauliche Daten ohne zusätzliche Setup-Schritte. 

Durch diese Methode wird gewährleistet, dass deine sensiblen Daten jederzeit sicher bleiben, insbesondere bei der Bereitstellung in der Cloud.