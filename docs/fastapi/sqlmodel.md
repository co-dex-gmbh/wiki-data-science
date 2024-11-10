# Arbeiten mit SQLModel in FastAPI

**SQLModel** ist eine Bibliothek, die SQLAlchemy und Pydantic kombiniert. Sie ermöglicht es dir, Datenbankmodelle in FastAPI zu integrieren, ohne auf umfangreiche ORM-Definitionen verzichten zu müssen. SQLModel baut auf SQLAlchemy auf und verwendet Pydantic zur Validierung der Daten, sodass du Datenbankmodelle erstellen und gleichzeitig die Vorteile der Datenvalidierung von Pydantic nutzen kannst.

## Was ist SQLModel?

SQLModel ist eine Bibliothek, die es ermöglicht, SQL-Datenbanken in FastAPI-Anwendungen zu integrieren. Sie stellt eine einfache Schnittstelle zur Verfügung, die es dir ermöglicht, sowohl Datenbankmodelle zu definieren als auch mit der Datenbank zu interagieren – alles in einer sauberen und einheitlichen API.

SQLModel ermöglicht die Definition von **Pydantic-Modellen**, die gleichzeitig auch **Datenbankmodelle** sind. Das bedeutet, dass du nur ein Modell schreiben musst, um sowohl mit der Datenbank als auch mit FastAPI zu arbeiten.

### Installation

```bash
pip install sqlmodel
```

### Erstellen eines einfachen SQLModel-Datenmodells

Ein SQLModel-Datenmodell ist sehr ähnlich wie ein Pydantic-Modell, aber mit zusätzlichen SQLAlchemy-Features wie `Field` und `Relationship` für die Datenbankinteraktion. 

```python
from sqlmodel import Field, SQLModel

class User(SQLModel, table=True):
    id: int = Field(default=None, primary_key=True)
    name: str
    email: str
    age: int
```

In diesem Beispiel haben wir ein einfaches **User-Modell** erstellt, das die Felder `id`, `name`, `email` und `age` enthält. Das `table=True`-Attribut signalisiert, dass dieses Modell eine Tabelle in der Datenbank repräsentiert.

### Aufgabe

Erstelle ein weiteres Datenmodell, das `Product`-Daten mit den Feldern `name`, `price` und `description` speichert. Vergiss nicht, die `id` als Primärschlüssel hinzuzufügen.


## Datenbankverbindungen und Sessions

Eine der wichtigsten Aufgaben beim Arbeiten mit SQLModel ist die Verbindung zur Datenbank und die Verwaltung von Sessions, um Transaktionen durchzuführen. SQLModel baut auf SQLAlchemy auf, sodass wir die gleiche Methode verwenden, um die Verbindung zur Datenbank herzustellen.

### Verbindung zur Datenbank herstellen

Du kannst SQLModel mit einer SQLite-Datenbank oder einer anderen unterstützten Datenbank wie PostgreSQL oder MySQL verwenden. Hier ist ein einfaches Beispiel für die Verbindung zu einer SQLite-Datenbank:

```python
from sqlmodel import create_engine, Session

# Erstelle die Verbindung zur SQLite-Datenbank
engine = create_engine("sqlite:///database.db")

# Erstelle die Tabellen in der Datenbank (falls sie noch nicht existieren)
SQLModel.metadata.create_all(engine)
```

### Arbeiten mit Sessions

Um mit der Datenbank zu interagieren, musst du eine Session erstellen, die es dir ermöglicht, Datensätze zu lesen, zu schreiben und zu aktualisieren.

```python
from sqlmodel import Session

# Öffne eine Session, um mit der Datenbank zu interagieren
with Session(engine) as session:
    # Beispiel: Hinzufügen eines neuen Benutzers
    user = User(name="John Doe", email="johndoe@example.com", age=30)
    session.add(user)
    session.commit()
```

### Aufgabe

Erstelle eine neue `Product`-Instanz, füge sie zur Datenbank hinzu und bestätige die Transaktion mit `session.commit()`.


## CRUD-Operationen mit SQLModel

SQLModel macht es einfach, grundlegende **CRUD**-Operationen (Create, Read, Update, Delete) auf Datenbanken durchzuführen. Nachdem du die Datenbankverbindung und das Modell eingerichtet hast, kannst du Datensätze einfach erstellen und abfragen.

### Erstellen eines Datensatzes (Create)

```python
with Session(engine) as session:
    new_user = User(name="Jane Doe", email="janedoe@example.com", age=25)
    session.add(new_user)
    session.commit()
```

### Lesen von Datensätzen (Read)

```python
with Session(engine) as session:
    user = session.query(User).filter(User.name == "Jane Doe").first()
    print(user)
```

### Aktualisieren von Datensätzen (Update)

```python
with Session(engine) as session:
    user = session.query(User).filter(User.name == "Jane Doe").first()
    if user:
        user.age = 26
        session.commit()
```

### Löschen von Datensätzen (Delete)

```python
with Session(engine) as session:
    user = session.query(User).filter(User.name == "Jane Doe").first()
    if user:
        session.delete(user)
        session.commit()
```

### Aufgabe

Erweitere das `User`-Modell um ein `address`-Feld und führe eine `UPDATE`-Operation durch, um die Adresse eines bestimmten Benutzers zu ändern.


## Integration von SQLModel mit FastAPI

Ein großer Vorteil von SQLModel ist, dass es nahtlos mit FastAPI integriert werden kann. Du kannst SQLModel-Modelle direkt in deine FastAPI-Routen einbinden, um API-Endpunkte zu erstellen, die mit der Datenbank interagieren.

### Beispiel für einen FastAPI-Endpunkt mit SQLModel

```python
from fastapi import FastAPI
from sqlmodel import Session, select

app = FastAPI()

@app.post("/users/")
async def create_user(user: User):
    with Session(engine) as session:
        session.add(user)
        session.commit()
    return {"user": user}
```

In diesem Beispiel haben wir eine `POST`-Route erstellt, die ein `User`-Objekt entgegennimmt und es in die Datenbank speichert.

### Aufgabe

Erstelle eine `GET`-Route, die alle Benutzer aus der Datenbank abruft und zurückgibt.
