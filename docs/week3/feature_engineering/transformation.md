# Transformation

Transformationen werden genutzt, um die Verteilung der Daten zu ändern, z. B. um Schiefe zu korrigieren oder lineare Zusammenhänge zu verstärken. Eine gängige Methode ist die logarithmische Transformation, die oft bei schiefen Daten angewendet wird.

**Beispiel in Python:**
```python
import numpy as np
import pandas as pd

# Beispiel-Daten
werte = pd.DataFrame({'Umsatz': [100, 500, 1000, 5000, 10000]})

# Log-Transformation
werte['Log-Umsatz'] = np.log(werte['Umsatz'])
print(werte)
```

**Wann brauche ich das?**
- Wenn deine Daten stark schief verteilt sind.
- Wenn du exponentielle Trends oder Skaleneffekte linear darstellen möchtest.
