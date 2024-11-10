# Vorhersage des Einkommens basierend auf dem Adult Income Dataset

In dieser Aufgabe wirst du das **Adult Income Dataset** verwenden, um ein einfaches API-Modell zu erstellen, das die Wahrscheinlichkeit vorhersagt, ob jemand mehr als 50.000 USD jährlich verdient, basierend auf verschiedenen demografischen Merkmalen. Du wirst SQLModel für das Speichern der Daten in einer Datenbank und FastAPI für die API-Erstellung verwenden.

## Aufgabe 1: Datenvorbereitung und -verständnis

Lade das [**Adult Income Dataset**](https://archive.ics.uci.edu/dataset/2/adult) herunter und analysiere die Spalten. Erstelle ein Streamlit Dashboard oder Jupyter Notebook, um den Datensatz visuell aufzubereiten. Der Datensatz enthält folgende Merkmale:

- `age`: Alter der Person
- `workclass`: Arbeitsverhältnis (z.B. privat, öffentlich)
- `fnlwgt`: Gewicht (repräsentiert die Anzahl der Menschen, die in der Stichprobe repräsentiert sind)
- `education`: Höchster Bildungsabschluss
- `education-num`: Bildung in numerischer Form
- `marital-status`: Familienstand
- `occupation`: Beruf
- `relationship`: Beziehung zum Haushaltsvorstand
- `race`: Rasse
- `sex`: Geschlecht
- `capital-gain`: Kapitalgewinne
- `capital-loss`: Kapitalverlust
- `hours-per-week`: Arbeitsstunden pro Woche
- `native-country`: Geburtsland
- `income`: Einkommen (mehr als 50K oder weniger)

## Aufgabe 2: Erstellen eines SQLModel-Datenmodells

Erstelle ein `User`-Datenmodell mit SQLModel, das die oben genannten Merkmale repräsentiert. Definiere auch den Typ der Merkmale (z. B. `age` als Integer, `education` als String). 

<!-- Beispiel:
```python
from sqlmodel import SQLModel, Field
from typing import Optional

class AdultIncomeData(SQLModel, table=True):
    id: Optional[int] = Field(default=None, primary_key=True)
    age: int
    workclass: str
    fnlwgt: int
    education: str
    education_num: int
    marital_status: str
    occupation: str
    relationship: str
    race: str
    sex: str
    capital_gain: int
    capital_loss: int
    hours_per_week: int
    native_country: str
    income: str
``` -->

## Aufgabe 3: API-Erstellung mit FastAPI

Erstelle eine FastAPI-Anwendung, die folgende Funktionalitäten bietet:

1. **Daten hinzufügen**: Erstelle eine POST-Route, die es ermöglicht, neue Benutzerdaten hinzuzufügen. Die Route sollte alle Merkmale des Datensatzes akzeptieren.
   
2. **Daten abfragen**: Erstelle eine GET-Route, um alle gespeicherten Benutzerdaten abzurufen.

3. **Einkommensvorhersage**: Erstelle eine weitere POST-Route, die basierend auf den eingegebenen demografischen Merkmalen vorhersagt, ob das Einkommen mehr als 50.000 USD beträgt oder nicht. Diese Route sollte ein Modell wie z. B. einen einfachen Entscheidungsbaum verwenden (der zuvor auf den Daten trainiert wurde), um die Vorhersage zu treffen.
<!-- 
Beispiel:
```python
from fastapi import FastAPI
from sqlmodel import Session, create_engine
from sqlalchemy.orm import sessionmaker
from pydantic import BaseModel
from typing import Optional

# FastAPI-Instanz
app = FastAPI()

# Pydantic-Modell für die Anfrage
class AdultIncomeRequest(BaseModel):
    age: int
    workclass: str
    fnlwgt: int
    education: str
    education_num: int
    marital_status: str
    occupation: str
    relationship: str
    race: str
    sex: str
    capital_gain: int
    capital_loss: int
    hours_per_week: int
    native_country: str

# API-Route zur Vorhersage des Einkommens
@app.post("/predict-income/")
async def predict_income(data: AdultIncomeRequest):
    # Hier kannst du den Vorhersage-Algorithmus (z. B. Entscheidungsbaum) anwenden
    # Beispiel: Ein einfaches Modell, das "income" auf Grundlage von Alter und Stunden pro Woche vorhersagt.
    if data.age > 50 and data.hours_per_week > 40:
        return {"income": ">50K"}
    else:
        return {"income": "<=50K"}
``` -->

## Aufgabe 4: Testen der API mit Postman oder einem anderen API-Client

1. **Daten hinzufügen**: Verwende die POST-Route `/add-user` (oder eine benannte Route) zum Hinzufügen eines neuen Datensatzes.
   
2. **Daten abfragen**: Verwende die GET-Route `/users`, um alle gespeicherten Benutzer abzurufen.

3. **Einkommensvorhersage**: Teste die `/predict-income/`-Route, indem du verschiedene Werte für `age`, `hours-per-week` und andere Merkmale eingibst.

## Aufgabe 5 (Zusatz): Analyse und Modellverbesserung

Nachdem du die API erstellt hast, analysiere die Vorhersageergebnisse und überlege, wie du das Modell verbessern kannst

