# Einführung in FastAPI

## Was ist FastAPI?

**FastAPI** ist ein Web-Framework zur Entwicklung von APIs mit Python. Es wurde für den Einsatz in produktionskritischen Anwendungen entwickelt und zeichnet sich durch eine hohe Performance und einfache Handhabung aus.

### Kernmerkmale von FastAPI

- **Automatische Dokumentation**: FastAPI generiert automatisch interaktive API-Dokumentationen (Swagger UI, Redoc) auf Basis des OpenAPI-Standards.
- **Asynchrone Verarbeitung**: Unterstützung für `async` und `await` erleichtert das Handling von asynchronen Aufgaben und macht FastAPI ideal für Anwendungen mit hohen Anforderungen an die Skalierbarkeit.
- **Einfache Validierung**: FastAPI verwendet Pydantic zur Validierung und Serialisierung von Daten, wodurch die Datenintegrität automatisch gesichert wird.

### Beispiel einer FastAPI-Anwendung

Hier eine grundlegende FastAPI-Anwendung, die einen "Hello World"-Endpunkt bereitstellt:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def root():
    return {"message": "Hello, World!"}
```

### Installation
FastAPI kann über `pip` installiert werden:

```bash
pip install fastapi[all]
```

Zusätzlich wird ein ASGI-Server wie **uvicorn** benötigt, um die Anwendung zu starten:

```bash
pip install uvicorn
uvicorn main:app --reload
```


## FastAPI vs. Flask

FastAPI und Flask sind beide beliebte Python-Frameworks zur API-Entwicklung, unterscheiden sich jedoch erheblich in ihrer Funktionsweise und ihrem Anwendungsbereich.

### Hauptunterschiede

| Merkmal              | Flask                                                                                 | FastAPI                                                              |
| -------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Asynchronität**    | Unterstützung nur mit zusätzlichen Bibliotheken wie `flask-async`                     | Eingebaute Unterstützung für `async` und `await`                     |
| **Performance**      | Moderate Geschwindigkeit                                                              | Hohe Performance durch asynchrone Architektur                        |
| **Datenvalidierung** | Keine eingebaute Validierung, zusätzliche Bibliotheken wie `marshmallow` erforderlich | Integrierte Validierung mit Pydantic                                 |
| **Dokumentation**    | Keine automatische Dokumentation                                                      | Automatische Generierung von Swagger UI und Redoc                    |
| **Ideal für**        | Einfache APIs und Anwendungen                                                         | APIs mit hoher Leistung und komplexen Datenvalidierungsanforderungen |

### Wann man FastAPI verwenden sollte
- Wenn hohe Performance und Skalierbarkeit gefordert sind.
- Für APIs, die asynchrone Verarbeitung benötigen.
- Bei Projekten, in denen die automatische Dokumentation nützlich ist.

### Wann Flask geeigneter ist
- Bei einfachen Anwendungen oder Prototypen, die nur grundlegende Funktionalitäten benötigen.
- Wenn Asynchronität und Performance keine kritischen Anforderungen sind.
