# Datenmodelle mit Pydantic in FastAPI

Datenmodelle sind ein wesentlicher Bestandteil von APIs, da sie definieren, welche Art von Daten zwischen dem Server und den Clients ausgetauscht werden kann. In FastAPI übernimmt die Bibliothek **Pydantic** diese Aufgabe, indem sie Python-Datenstrukturen in valide JSON-Objekte verwandelt. Pydantic bietet starke Validierungs- und Typisierungsfunktionen und ermöglicht es uns, Daten mit minimalem Aufwand zu strukturieren und zu validieren.

## Warum Pydantic?

Pydantic ist eine zentrale Bibliothek in FastAPI, da sie eine einfache Möglichkeit bietet, Daten zu validieren und zu serialisieren. Mit Pydantic können wir sicherstellen, dass die Daten, die von einem Client gesendet werden oder an diesen zurückgegeben werden, den gewünschten Typen entsprechen. Dies verringert potenzielle Fehler und macht den Code robuster und lesbarer.

### Typisierung und Validierung

Pydantic nutzt Python’s Typannotation, um die Struktur der Daten zu definieren und die Validierung basierend auf den angegebenen Datentypen durchzuführen. Wenn du also ein Modell mit Feldern wie `str`, `int` oder `EmailStr` erstellst, stellt Pydantic sicher, dass die Daten den entsprechenden Typen entsprechen.

Ein Beispiel für eine einfache Typisierung:

```python
from pydantic import BaseModel, EmailStr

class User(BaseModel):
    name: str
    email: EmailStr
    age: int
```

Hier sorgt Pydantic dafür, dass die `email`-Adresse als gültige E-Mail-Adresse formatiert ist, während der Name ein String und das Alter eine Ganzzahl ist.

### Unterstützte Datentypen

Pydantic unterstützt eine breite Palette von Datentypen, um unterschiedliche Anwendungsfälle abzudecken. Zu den wichtigsten gehören:

- **Primitive Typen**: `str`, `int`, `float`, `bool`
- **Spezielle Typen**: `EmailStr`, `UUID`, `IPv4`, `IPv6`
- **Optionale Felder**: `Optional[T]`, um Felder als optional zu kennzeichnen
- **Listen und Tupel**: `List[T]`, `Tuple[T, ...]`
- **Datum und Uhrzeit**: `datetime`, `date`, `time`


## Erstellen eines einfachen Datenmodells

Schauen wir uns ein einfaches Beispiel an: Wir möchten eine API, die Benutzerdaten wie `name`, `email` und `age` verarbeitet. Mit Pydantic definieren wir die Struktur der zu verarbeitenden Daten.

```python
from pydantic import BaseModel, EmailStr

class User(BaseModel):
    name: str
    email: EmailStr
    age: int
```

In diesem Modell wird `name` als `str`, `email` als `EmailStr` und `age` als `int` validiert. Die `EmailStr`-Typisierung stellt sicher, dass die Eingabe eine gültige E-Mail-Adresse ist.

### Aufgabe

Erweitere das `User`-Modell, indem du ein optionales Feld für `city` hinzufügst, das einen Standardwert hat, zum Beispiel `"Unbekannt"`. Füge außerdem ein Feld `is_active` hinzu, das einen `bool`-Wert erwartet und standardmäßig auf `True` gesetzt ist.


## Modell in FastAPI einbinden

Nachdem wir das Datenmodell mit Pydantic erstellt haben, wollen wir es in einer FastAPI-Anwendung verwenden. FastAPI ermöglicht es uns, Pydantic-Modelle direkt in Routen zu integrieren. So können wir sicherstellen, dass alle eingehenden Daten den definierten Anforderungen entsprechen.

```python
from fastapi import FastAPI
from pydantic import BaseModel, EmailStr
from typing import Optional

app = FastAPI()

class User(BaseModel):
    name: str
    email: EmailStr
    age: int
    city: Optional[str] = "Unbekannt"
    is_active: bool = True

@app.post("/users/")
async def create_user(user: User):
    return {"user": user}
```

In diesem Beispiel haben wir die Route `/users/` erstellt, die einen `POST`-Request erwartet. FastAPI übernimmt die Validierung der Daten und gibt die gültigen Daten als Antwort zurück.

### Aufgabe

Teste die `/users/`-Route mit einem API-Client wie Postman. Sende ein JSON-Objekt, das die Felder `name`, `email` und `age` enthält, und überprüfe, wie FastAPI das Modell validiert und zurückgibt.


## Validierung und Fehlerbehandlung

FastAPI und Pydantic bieten umfangreiche Möglichkeiten, Daten zu validieren. Wenn Daten nicht den Anforderungen entsprechen, gibt FastAPI eine detaillierte Fehlermeldung zurück, die den Entwickler genau darüber informiert, welcher Wert nicht gültig ist.

### Beispiel für eine Validierung:

```python
from pydantic import BaseModel, Field

class User(BaseModel):
    name: str = Field(..., min_length=2, max_length=50)
    email: EmailStr
    age: int = Field(..., gt=0, le=120)  # Altersbeschränkung
    city: Optional[str] = "Unbekannt"
    is_active: bool = True
```

In diesem Beispiel haben wir Einschränkungen für das Feld `name` (minimale und maximale Länge) und `age` (größer als 0 und maximal 120 Jahre) definiert.

Wenn jemand beispielsweise eine ungültige E-Mail-Adresse sendet oder das Alter zu hoch ist, gibt FastAPI eine Fehlerantwort zurück.

### Aufgabe

Teste das Modell in einer einfachen `POST`-Route, indem du es in FastAPI integrierst. Übermittle verschiedene `name`- und `age`-Werte und beobachte die Fehlermeldungen, die FastAPI automatisch generiert, wenn die Validierungen fehlschlagen.



## Eigene Validierungen

Pydantic ermöglicht es, benutzerdefinierte Validierungen hinzuzufügen. Wenn du komplexere Anforderungen hast, die über die Standardvalidierung hinausgehen, kannst du eigene Validierungsfunktionen implementieren.

Ein Beispiel für eine benutzerdefinierte Validierung:

```python
from pydantic import validator

class User(BaseModel):
    name: str
    email: EmailStr
    age: int

    @validator("name")
    def name_must_not_contain_numbers(cls, v):
        if any(char.isdigit() for char in v):
            raise ValueError("Name darf keine Zahlen enthalten")
        return v
```

In diesem Beispiel wird eine Validierung für das Feld `name` hinzugefügt, die sicherstellt, dass der Name keine Zahlen enthält.

### Aufgabe

Erweitere den `name`-Validator, sodass er auch sicherstellt, dass der Name keine Sonderzeichen enthält. Teste den Validator, indem du Namen wie „John@Doe“ und „123Peter“ eingibst und überprüfe die Fehlermeldungen.
