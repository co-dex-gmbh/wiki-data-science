# Evaluierungsmetriken

## Überblick der Evaluierungsmetriken

| Metrik    | Formel                          | Anwendungsbereich     | Wertebereich | Primärer Einsatzzweck          |
| --------- | ------------------------------- | --------------------- | ------------ | ------------------------------ |
| Accuracy  | (TP + TN) / (TP + TN + FP + FN) | Klassifikation        | [0,1]        | Allgemeine Klassifikationsgüte |
| Precision | TP / (TP + FP)                  | Klassifikation        | [0,1]        | FP-Minimierung                 |
| Recall    | TP / (TP + FN)                  | Klassifikation        | [0,1]        | FN-Minimierung                 |
| F1-Score  | 2 * (P * R) / (P + R)           | Klassifikation        | [0,1]        | Kombinierte Bewertung          |
| ROC-AUC   | Integral ROC-Kurve              | Binäre Klassifikation | [0,1]        | Schwellwert-unabhängig         |
| MSE       | Σ(y_true - y_pred)² / n         | Regression            | [0,∞)        | Quadratische Fehlerbewertung   |
| RMSE      | √(MSE)                          | Regression            | [0,∞)        | Skalenkonforme Bewertung       |
| MAE       | Σ                               | y_true - y_pred       | / n          | Regression                     | [0,∞) | Lineare Fehlerbewertung |
| R²        | 1 - (MSE / Var(y))              | Regression            | (-∞,1]       | Varianzbasierte Bewertung      |


## Klassifikationsmetriken

### Accuracy
Die Accuracy ist die am einfachsten zu verstehende Metrik, da sie direkt den Anteil der korrekten Vorhersagen misst. Sie berechnet sich aus der Anzahl der richtigen Vorhersagen geteilt durch die Gesamtzahl aller Vorhersagen. Während diese Metrik bei ausgeglichenen Datensätzen sehr aussagekräftig ist, verliert sie bei unbalancierten Daten stark an Bedeutung. 

In einem Datensatz zur Krankheitserkennung mit 98% gesunden und 2% kranken Patienten würde ein Modell, das einfach immer "gesund" vorhersagt, eine Accuracy von 0.98 erreichen - trotz seiner offensichtlichen Nutzlosigkeit. Dies führt uns zu differenzierteren Metriken.

```python
from sklearn.metrics import accuracy_score
import numpy as np

# Simulieren eines Klassifikationsproblems: Spam-Erkennung
# 0 = normale E-Mail, 1 = Spam
y_true = np.array([0, 0, 1, 1, 0, 0, 1, 0, 0, 1])  # Wahre Labels
y_pred = np.array([0, 0, 1, 0, 0, 0, 1, 1, 0, 1])  # Vorhersagen des Modells

accuracy = accuracy_score(y_true, y_pred)
print(f"Accuracy: {accuracy:.2f}")  # 0.80 = 80% korrekte Vorhersagen

# Zeigt das Problem bei unbalancierten Daten
y_true_unbalanced = np.array([0]*90 + [1]*10)  # 90% normale Mails, 10% Spam
y_pred_naive = np.array([0]*100)  # Modell sagt immer "normale Mail"

accuracy_unbalanced = accuracy_score(y_true_unbalanced, y_pred_naive)
print(f"Accuracy (unbalanciert): {accuracy_unbalanced:.2f}")  # 0.90, aber nutzlos!
```

### Precision
Precision fokussiert sich auf die Qualität der positiven Vorhersagen. Sie beantwortet die Frage: "Wenn unser Modell etwas als positiv klassifiziert, wie oft stimmt das?" Diese Metrik ist besonders wichtig, wenn falsche positive Vorhersagen kostspielig oder problematisch sind.

Ein Beispiel: Bei einem Spam-Filter ist eine hohe Precision wichtig, da fälschlicherweise als Spam klassifizierte wichtige E-Mails (falsch positive) sehr störend für den Nutzer sind. Die Precision gibt uns hier den Anteil der tatsächlichen Spam-Mails unter allen als Spam klassifizierten E-Mails.

```python
from sklearn.metrics import precision_score, recall_score, precision_recall_curve
import matplotlib.pyplot as plt

# Medizinische Diagnose: Krankheitserkennung
# Simuliere Testdaten mit Wahrscheinlichkeiten
np.random.seed(42)
n_samples = 1000
# Generiere Wahrscheinlichkeiten für positive Klasse
y_scores = np.random.rand(n_samples)
# Wahre Labels (5% Krankheitsfälle)
y_true = np.random.choice([0, 1], size=n_samples, p=[0.95, 0.05])

# Verschiedene Schwellenwerte testen
thresholds = [0.3, 0.5, 0.7]
for threshold in thresholds:
    # Konvertiere Wahrscheinlichkeiten zu binären Vorhersagen
    y_pred = (y_scores >= threshold).astype(int)
    
    precision = precision_score(y_true, y_pred)
    recall = recall_score(y_true, y_pred)
    
    print(f"\nSchwellenwert: {threshold}")
    print(f"Precision: {precision:.2f}")
    print(f"Recall: {recall:.2f}")

# Precision-Recall Kurve
precisions, recalls, _ = precision_recall_curve(y_true, y_scores)

plt.figure(figsize=(10, 6))
plt.plot(recalls, precisions)
plt.xlabel('Recall')
plt.ylabel('Precision')
plt.title('Precision-Recall Kurve')
plt.grid(True)
```

### Recall
Der Recall hingegen konzentriert sich auf die Vollständigkeit der positiven Klassifikationen. Er beantwortet die Frage: "Von allen tatsächlich positiven Fällen, wie viele haben wir gefunden?" Diese Metrik ist entscheidend, wenn das Übersehen positiver Fälle schwerwiegende Folgen hat.

In der medizinischen Diagnostik ist ein hoher Recall oft wichtiger als eine hohe Precision. Wenn es um die Erkennung einer schweren Krankheit geht, ist es besser, einige falsche Alarme zu haben (niedrige Precision), als kranke Patienten zu übersehen (niedriger Recall).

### F1-Score
Der F1-Score vereint Precision und Recall in einer einzigen Metrik durch Bildung des harmonischen Mittels. Dies ist besonders nützlich, wenn wir einen ausgewogenen Kompromiss zwischen Precision und Recall benötigen. Das harmonische Mittel reagiert besonders empfindlich auf niedrige Werte, wodurch ein Modell nur dann einen hohen F1-Score erreichen kann, wenn sowohl Precision als auch Recall gut sind.

Der F1-Score eignet sich besonders für Anwendungsfälle, in denen sowohl falsch positive als auch falsch negative Vorhersagen wichtig sind, wie etwa bei der Qualitätskontrolle in der Produktion.


```python
from sklearn.metrics import f1_score
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

# Qualitätskontrolle in der Produktion
# Simuliere Produktionsdaten mit Features und Defekt-Labels
np.random.seed(42)
n_samples = 1000
n_features = 5

# Generiere Features (z.B. Temperatur, Druck, Geschwindigkeit etc.)
X = np.random.randn(n_samples, n_features)
# Generiere Labels (10% defekte Produkte)
y = np.random.choice([0, 1], size=n_samples, p=[0.9, 0.1])

# Daten aufteilen und Modell trainieren
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Feature-Skalierung
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Modell trainieren
model = LogisticRegression()
model.fit(X_train_scaled, y_train)

# Vorhersagen
y_pred = model.predict(X_test_scaled)

# Metriken berechnen
precision = precision_score(y_test, y_pred)
recall = recall_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)

print("\nQualitätskontrolle Metriken:")
print(f"Precision: {precision:.2f}")
print(f"Recall: {recall:.2f}")
print(f"F1-Score: {f1:.2f}")
```

### ROC-AUC mit vollständigem Beispiel
```python
from sklearn.metrics import roc_curve, auc
import matplotlib.pyplot as plt

# Kreditkarten-Betrug Erkennung
# Simuliere Transaktionsdaten
np.random.seed(42)
n_samples = 10000

# Generiere Wahrscheinlichkeiten für betrügerische Transaktionen
fraud_probs = np.random.beta(2, 10, n_samples)  # Beta-Verteilung für realistische Wahrscheinlichkeiten
# Echte Labels (1% Betrug)
is_fraud = np.random.choice([0, 1], size=n_samples, p=[0.99, 0.01])

# ROC-Kurve berechnen
fpr, tpr, thresholds = roc_curve(is_fraud, fraud_probs)
roc_auc = auc(fpr, tpr)

# Visualisierung
plt.figure(figsize=(10, 6))
plt.plot(fpr, tpr, color='darkorange', lw=2, 
         label=f'ROC curve (AUC = {roc_auc:.2f})')
plt.plot([0, 1], [0, 1], color='navy', lw=2, linestyle='--')
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.title('ROC Curve - Betrugserkennungsmodell')
plt.legend(loc="lower right")
plt.grid(True)
```


### ROC-AUC
Die ROC-AUC (Area Under the Receiver Operating Characteristic Curve) ist eine besonders aussagekräftige Metrik, da sie die Leistung des Modells über verschiedene Schwellenwerte hinweg bewertet. Sie zeigt, wie gut das Modell positive von negativen Fällen trennen kann, unabhängig von einem spezifischen Schwellenwert.

Diese Metrik ist besonders wertvoll beim Vergleich verschiedener Modelle, da sie von der konkreten Wahl des Schwellenwerts unabhängig ist. Ein perfektes Modell hätte eine AUC von 1.0, während ein zufälliges Modell eine AUC von 0.5 erreicht.

## Regressionsmetriken

### Mean Squared Error (MSE)
Der MSE ist die grundlegendste Regressionsmetrik. Er bestraft große Fehler überproportional stark durch die Quadrierung der Differenzen. Dies macht ihn besonders empfindlich gegenüber Ausreißern. 

Diese Eigenschaft ist in manchen Fällen erwünscht - etwa wenn einzelne große Abweichungen besonders problematisch sind, wie bei der Steuerung von Industrieanlagen. In anderen Fällen kann diese Übergewichtung großer Fehler aber auch zu verzerrten Optimierungen führen.

### Root Mean Squared Error (RMSE)
Der RMSE ist die Quadratwurzel des MSE und hat den großen Vorteil, dass er in der gleichen Einheit wie die Zieldaten gemessen wird. Dies macht ihn deutlich intuitiver interpretierbar als den MSE. 

Bei einer Verkaufspreisprognose in Euro gibt der RMSE direkt die durchschnittliche Abweichung in Euro an, während der MSE in quadrierten Euro gemessen würde. Dennoch behält der RMSE die charakteristische überproportionale Bestrafung großer Fehler bei.

```python
from sklearn.metrics import mean_squared_error
from sklearn.ensemble import RandomForestRegressor

# Hauspreisvorhersage
# Simuliere Immobiliendaten
np.random.seed(42)
n_samples = 1000

# Features: Größe (m²), Alter, Anzahl Zimmer, Entfernung zum Zentrum
X = np.random.rand(n_samples, 4)
X[:, 0] = X[:, 0] * 150 + 50  # Größe: 50-200m²
X[:, 1] = X[:, 1] * 50        # Alter: 0-50 Jahre
X[:, 2] = np.round(X[:, 2] * 4 + 2)  # Zimmer: 2-6
X[:, 3] = X[:, 3] * 30        # Entfernung: 0-30km

# Preise generieren (in Tausend Euro)
base_price = 200 + X[:, 0] * 2 - X[:, 1] * 1.5 + X[:, 2] * 20 - X[:, 3] * 2
noise = np.random.normal(0, 20, n_samples)
y = base_price + noise

# Modell trainieren
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

model = RandomForestRegressor(n_estimators=100)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

# Metriken berechnen
mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)

print("\nHauspreisvorhersage Metriken:")
print(f"MSE: {mse:.2f} (Tausend Euro²)")
print(f"RMSE: {rmse:.2f} (Tausend Euro)")
```

### Mean Absolute Error (MAE)
Der MAE unterscheidet sich fundamental von MSE und RMSE, da er Fehler linear und nicht quadratisch bestraft. Er gibt den durchschnittlichen absoluten Fehler an und ist damit robuster gegenüber Ausreißern.

Diese Metrik eignet sich besonders, wenn einzelne große Abweichungen nicht überproportional ins Gewicht fallen sollen. Ein typisches Beispiel sind Nachfrageprognosen im Einzelhandel, wo einzelne größere Abweichungen nicht dramatisch sind, solange der durchschnittliche Fehler gering bleibt.

```python
from sklearn.metrics import mean_absolute_error

# Energieverbrauchsvorhersage
# Simuliere stündlichen Energieverbrauch
hours = np.arange(24)
base_consumption = 100 + np.sin(hours * np.pi/12) * 50  # Tagesrhythmus
noise = np.random.normal(0, 10, 24)
actual_consumption = base_consumption + noise

# Modellvorhersagen simulieren (mit systematischer Abweichung)
predicted_consumption = base_consumption + np.random.normal(5, 15, 24)

mae = mean_absolute_error(actual_consumption, predicted_consumption)
mse = mean_squared_error(actual_consumption, predicted_consumption)
rmse = np.sqrt(mse)

print("\nEnergieverbrauch Vorhersage Metriken:")
print(f"MAE: {mae:.2f} kWh")
print(f"RMSE: {rmse:.2f} kWh")

# Visualisierung
plt.figure(figsize=(12, 6))
plt.plot(hours, actual_consumption, label='Tatsächlicher Verbrauch')
plt.plot(hours, predicted_consumption, label='Vorhergesagter Verbrauch')
plt.xlabel('Stunde des Tages')
plt.ylabel('Energieverbrauch (kWh)')
plt.title('Tatsächlicher vs. Vorhergesagter Energieverbrauch')
plt.legend()
plt.grid(True)
```

### R² mit ausführlichem Beispiel
```python
from sklearn.metrics import r2_score
from sklearn.linear_model import LinearRegression

# Verkaufsprognose
# Simuliere monatliche Verkaufsdaten mit saisonalem Effekt
months = 24
seasonal_pattern = np.sin(np.arange(months) * 2 * np.pi / 12)

# Features: Werbeausgaben, Saisonalität, Preis
X = np.random.rand(months, 3)
X[:, 1] = seasonal_pattern  # Saisonaler Effekt
X[:, 2] = np.random.rand(months) * 0.2 + 0.9  # Preisfaktor

# Verkaufszahlen generieren
sales = 1000 + X[:, 0] * 500 + X[:, 1] * 200 - X[:, 2] * 300
noise = np.random.normal(0, 50, months)
y = sales + noise

# Modell trainieren
model = LinearRegression()
model.fit(X, y)
y_pred = model.predict(X)

# R² berechnen
r2 = r2_score(y, y_pred)

print("\nVerkaufsprognose Metrik:")
print(f"R² Score: {r2:.3f}")

# Visualisierung der Anpassungsgüte
plt.figure(figsize=(10, 6))
plt.scatter(y, y_pred, alpha=0.5)
plt.plot([y.min(), y.max()], [y.min(), y.max()], 'r--', lw=2)
plt.xlabel('Tatsächliche Verkäufe')
plt.ylabel('Vorhergesagte Verkäufe')
plt.title('Tatsächliche vs. Vorhergesagte Verkäufe')
plt.grid(True)
```


### R² (Bestimmtheitsmaß)
R² ist eine besonders intuitive Metrik, da sie angibt, welchen Anteil der Varianz in den Daten das Modell erklären kann. Ein R² von 0.7 bedeutet, dass 70% der Varianz in den Daten durch das Modell erklärt werden.

Diese Metrik ist besonders nützlich für die Kommunikation mit nicht-technischen Stakeholdern, da sie leicht verständlich ist. Allerdings sollte beachtet werden, dass R² bei nicht-linearen Zusammenhängen oder bei Modellen mit vielen Features irreführend sein kann.

## Vergleichende Entscheidungshilfe

Die Wahl der richtigen Metrik hängt von mehreren Faktoren ab:

1. **Problemtyp**
   - Bei unbalancierten Klassifikationsproblemen: Precision, Recall, F1-Score
   - Bei balancierten Klassifikationsproblemen: Accuracy oder ROC-AUC
   - Bei Regressionen mit Ausreißern: MAE
   - Bei Regressionen mit kritischen großen Fehlern: RMSE

2. **Anwendungskontext**
   - Kritische Sicherheitsanwendungen: Fokus auf Recall
   - Qualitätssicherung: Ausgewogener F1-Score
   - Kostenoptimierung: MSE bei quadratischem Kostenwachstum

3. **Kommunikationsbedarf**
   - Technisches Publikum: Detaillierte Metriken wie ROC-AUC
   - Nicht-technisches Publikum: Intuitive Metriken wie Accuracy oder R²
   - Management: Geschäftsrelevante Metriken wie kostengewichtete Fehlerraten
<!-- 
## Praktische Empfehlungen

1. **Mehrere Metriken betrachten**
Es ist oft sinnvoll, mehrere komplementäre Metriken zu betrachten:
```python
def evaluate_comprehensive(y_true, y_pred, y_prob=None):
    """
    Umfassende Evaluation mit mehreren Metriken
    """
    metrics = {
        'accuracy': accuracy_score(y_true, y_pred),
        'precision': precision_score(y_true, y_pred),
        'recall': recall_score(y_true, y_pred),
        'f1': f1_score(y_true, y_pred)
    }
    if y_prob is not None:
        metrics['roc_auc'] = roc_auc_score(y_true, y_prob)
    return metrics
```

2. **Domänenspezifische Metriken**
In manchen Fällen ist es sinnvoll, problemspezifische Metriken zu entwickeln:
```python
def custom_weighted_error(y_true, y_pred, weights):
    """
    Gewichteter Fehler basierend auf Geschäftsregeln
    """
    errors = np.abs(y_true - y_pred)
    weighted_errors = errors * weights
    return np.mean(weighted_errors)
```

3. **Validierung über Zeit**
Bei Zeitreihendaten sollten die Metriken über verschiedene Zeiträume betrachtet werden:
```python
def temporal_metrics(y_true, y_pred, time_periods):
    """
    Berechnet Metriken für verschiedene Zeiträume
    """
    results = {}
    for period in time_periods:
        mask = (time_index >= period[0]) & (time_index < period[1])
        results[period] = calculate_metrics(
            y_true[mask], 
            y_pred[mask]
        )
    return results
``` -->


