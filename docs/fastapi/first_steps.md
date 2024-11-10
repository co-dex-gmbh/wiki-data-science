# Erste Schritte mit FastAPI: HTTP-Routen

In diesem Abschnitt sehen wir uns die Grundlagen von HTTP-Routen und die Erstellung von API-Endpunkte in fastapi an. HTTP-Routen sind das Herzstück jeder API. Sie definieren die verschiedenen Wege, auf denen Clients (wie Webbrowser oder mobile Apps) mit unserem Server kommunizieren können. FastAPI macht es besonders einfach, diese Routen zu erstellen und für verschiedene Anfragen zu konfigurieren.

## Unsere erste Route: `GET`

Beginnen wir noch einmal mit einer grundlegenden Route, die eine Nachricht an den Client zurückgibt. Der `GET`-Anfragetyp ist der einfachste und am häufigsten verwendete HTTP-Methodentyp – er ruft einfach Daten ab, ohne dass eine Änderung am Server oder in der Datenbank vorgenommen wird.

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def read_root():
    return {"message": "Hello, World!"}
```

In diesem Beispiel erstellen wir eine FastAPI-Instanz namens `app`. Dann definieren wir eine `GET`-Route mit dem Endpunkt `/`, die einfach „Hello, World!“ zurückgibt. Der `@app.get("/")`-Dekorator sagt FastAPI, dass dieser Endpunkt auf `GET`-Anfragen wartet.

### Aufgabe

Starte den Server und rufe `http://127.0.0.1:8000/` in deinem Browser oder einem API-Client wie Postman auf. Siehst du die Nachricht? Experimentiere, indem du den Text änderst. Teste, was passiert, wenn du den Rückgabewert veränderst – z. B. durch eine andere Nachricht oder eine Zahl.


## Parameter in der URL

Ein häufiges Szenario ist, dass wir Daten dynamisch basierend auf der Anfrage bereitstellen wollen. Nehmen wir an, wir möchten eine Nachricht zurückgeben, die den Namen des Benutzers enthält. Dazu fügen wir einen URL-Parameter hinzu, der in die Route integriert wird.

```python
@app.get("/hello/{name}")
async def read_item(name: str):
    return {"message": f"Hello, {name}!"}
```

Hier erstellen wir eine `GET`-Route mit einem dynamischen Segment `{name}`, das wir im Funktionsparameter `name` auffangen. Wenn wir `http://127.0.0.1:8000/hello/Alex` aufrufen, erhalten wir die Antwort: „Hello, Alex!“

### Aufgabe

Erweitere die Route, um eine zweite Variable wie `age` oder `city` aufzunehmen. Erstelle eine Antwort, die beide Parameter in einem Begrüßungssatz verwendet. Teste verschiedene Namen und Werte, um zu sehen, wie FastAPI die Eingaben verarbeitet.


## Verwendung von HTTP-Methoden: `POST`

Neben `GET` gibt es noch weitere HTTP-Methoden wie `POST`, `PUT` und `DELETE`, die alle unterschiedliche Zwecke erfüllen. `POST`-Anfragen werden typischerweise verwendet, um Daten an den Server zu senden, z. B. zum Erstellen eines neuen Eintrags.

Angenommen, wir möchten eine einfache Route erstellen, bei der der Benutzer eine Nachricht an den Server senden kann. Dabei nutzen wir die Methode `POST`, um die Nachricht vom Client entgegenzunehmen und eine Bestätigung zurückzugeben.

```python
from pydantic import BaseModel

class Message(BaseModel):
    content: str

@app.post("/send-message/")
async def create_message(message: Message):
    return {"received_message": message.content}
```

In diesem Beispiel erstellen wir ein Modell `Message` mit dem Attribut `content`, das eine Zeichenkette ist. Das `@app.post("/send-message/")` zeigt FastAPI, dass dieser Endpunkt eine `POST`-Anfrage erwartet. Der Inhalt wird in Form eines JSON-Objekts vom Client gesendet und in das `message`-Objekt des Typs `Message` umgewandelt. Anschließend geben wir die empfangene Nachricht als Bestätigung zurück.

### Aufgabe

Teste diese `POST`-Route mit einem API-Client wie Postman oder durch einen Browser-Extension. Sende eine JSON-Nachricht wie `{"content": "Dies ist meine erste Nachricht"}`. Experimentiere mit verschiedenen Nachrichten und überprüfe, wie FastAPI die Antwort generiert.


## Arbeiten mit Query-Parametern

Neben Routenparametern und `POST`-Daten bietet FastAPI die Möglichkeit, Query-Parameter zu verwenden. Diese Art von Parametern befindet sich in der URL nach einem `?` und wird häufig für zusätzliche, optionale Informationen genutzt. Beispielsweise möchten wir eine Route erstellen, bei der der Benutzer seinen Namen als Query-Parameter senden kann, ohne ihn in der URL selbst zu definieren.

```python
@app.get("/greet/")
async def greet_user(name: str = "Gast"):
    return {"message": f"Hallo, {name}!"}
```

In dieser Route verwenden wir den Query-Parameter `name`, der standardmäßig „Gast“ ist, falls kein Wert übergeben wird. Wenn wir `http://127.0.0.1:8000/greet/?name=Lisa` aufrufen, erhalten wir die Antwort „Hallo, Lisa!“.

### Aufgabe

Experimentiere mit der URL und dem `name`-Parameter. Probiere verschiedene Namen und teste, was passiert, wenn du den Parameter weglässt. Erweitere das Beispiel, indem du weitere optionale Query-Parameter hinzufügst, etwa `age` oder `city`.
