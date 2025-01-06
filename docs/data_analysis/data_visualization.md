# Visualisierungen in der Deskriptiven Statistik

Visualisierungen sind ein grundlegendes Werkzeug, um Daten verständlich darzustellen und erste Einsichten zu gewinnen. Im Folgenden werden verschiedene Graphen vorgestellt, die sich für unterschiedliche Anwendungsfälle eignen.

## 1. Histogramm

- **Was zeichnet es aus:** Ein Histogramm zeigt die Verteilung einer numerischen Variable, indem es die Daten in aufeinanderfolgende Intervalle unterteilt und die Häufigkeit dieser Intervalle als Balken darstellt. Die Höhe eines Balkens repräsentiert die Anzahl der Datenpunkte in diesem Intervall.
- **Wann kann ich es besonders gut anwenden:** Histogramme sind ideal, um die Verteilung von Daten, insbesondere deren Form (z. B. Normalverteilung, Schiefe) und Streuung, zu visualisieren.
- **Was wäre eine Alternative:** Alternativen zum Histogramm sind Dichteplots oder Boxplots, die ebenfalls Verteilungen darstellen, jedoch mit anderer Betonung.
- **Wie erstelle ich es:**
    - [Plotly: Histogram](https://plotly.com/python/histograms/)
    - [Seaborn: histplot](https://seaborn.pydata.org/generated/seaborn.histplot.html)
    - [Matplotlib: hist](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.hist.html)


## 2. Boxplot

- **Was zeichnet es aus:** Ein Boxplot veranschaulicht die Verteilung der Daten durch ein Diagramm, das den Median, die oberen und unteren Quartile sowie potenzielle Ausreißer anzeigt. Die „Box“ repräsentiert den Interquartilsabstand, und „Whiskers“ zeigen die Variabilität außerhalb der Quartile.
- **Wann kann ich es besonders gut anwenden:** Boxplots sind besonders nützlich, um die Verteilung und die Symmetrie von Daten sowie mögliche Ausreißer darzustellen. Ideal für den Vergleich von Kategorien oder Gruppen.
- **Was wäre eine Alternative:** Alternativen sind Violinplots, die die Dichte der Verteilung detaillierter darstellen.
- **Wie erstelle ich es:**
    - [Plotly: Boxplot](https://plotly.com/python/box-plots/)
    - [Seaborn: boxplot](https://seaborn.pydata.org/generated/seaborn.boxplot.html)
    - [Matplotlib: boxplot](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.boxplot.html)


## 3. Streudiagramm (Scatter Plot)

- **Was zeichnet es aus:** Streudiagramme visualisieren die Beziehung zwischen zwei numerischen Variablen. Jeder Punkt auf dem Diagramm repräsentiert einen Datenpunkt und die Achsen die Werte der jeweiligen Variablen.
- **Wann kann ich es besonders gut anwenden:** Ideal, um Korrelationen oder Muster zwischen zwei Variablen zu erkennen (z. B. ob ein linearer Zusammenhang besteht).
- **Was wäre eine Alternative:** Alternativen sind Liniendiagramme (wenn eine Reihenfolge wichtig ist) oder Heatmaps für dichtere Datensätze.
- **Wie erstelle ich es:**
    - [Plotly: Scatter Plot](https://plotly.com/python/line-and-scatter/)
    - [Seaborn: scatterplot](https://seaborn.pydata.org/generated/seaborn.scatterplot.html)
    - [Matplotlib: scatter](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html)


## 4. Liniendiagramm

- **Was zeichnet es aus:** Ein Liniendiagramm verbindet Datenpunkte mittels Linien und veranschaulicht so den Verlauf einer oder mehrerer Reihen über eine geordnete Achse (häufig Zeit).
- **Wann kann ich es besonders gut anwenden:** Liniendiagramme eignen sich gut für Zeitreihenanalysen und um Trends oder Zyklen in Daten darzustellen.
- **Was wäre eine Alternative:** Eine Alternative wäre ein Flächendiagramm (Area Chart), das die gleiche Information zeigt, jedoch mit gefüllten Bereichen.
- **Wie erstelle ich es:**
    - [Plotly: Line Chart](https://plotly.com/python/line-charts/)
    - [Seaborn: lineplot](https://seaborn.pydata.org/generated/seaborn.lineplot.html)
    - [Matplotlib: plot](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html)


## 5. Violinplot

- **Was zeichnet es aus:** Der Violinplot kombiniert Elemente von Boxplots und Dichteplots und zeigt die Verteilung der Daten sowie deren Dichte entlang einer Achse.
- **Wann kann ich es besonders gut anwenden:** Violinplots sind nützlich, wenn man die Verteilung und die Dichte einer Variablen gleichzeitig darstellen und dabei symmetrische oder bimodale Muster aufzeigen möchte.
- **Was wäre eine Alternative:** Alternativen sind der Boxplot (für eine weniger detaillierte Darstellung der Dichte) oder der Dichteplot.
- **Wie erstelle ich es:**
    - [Plotly: Violin Plot](https://plotly.com/python/violin/)
    - [Seaborn: violinplot](https://seaborn.pydata.org/generated/seaborn.violinplot.html)
    - [Matplotlib: violinplot](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.violinplot.html)


## 6. Heatmap

- **Was zeichnet es aus:** Heatmaps verwenden Farbschattierungen, um die Intensität von Werten in einer Matrix zu visualisieren. Häufig werden sie verwendet, um Korrelationen zwischen Variablen darzustellen.
- **Wann kann ich es besonders gut anwenden:** Heatmaps sind besonders nützlich, um Korrelationen zwischen vielen Variablen darzustellen, etwa bei der Analyse von Korrelationen in großen Datensätzen.
- **Was wäre eine Alternative:** Eine Alternative zur Heatmap ist das Paarplot, das Korrelationen in Scatterplot-Matrizen zeigt.
- **Wie erstelle ich es:**
    - [Plotly: Heatmap](https://plotly.com/python/heatmaps/)
    - [Seaborn: heatmap](https://seaborn.pydata.org/generated/seaborn.heatmap.html)
    - [Matplotlib: imshow](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.imshow.html)


## 7. Paarplot (Pair Plot)

- **Was zeichnet es aus:** Ein Paarplot visualisiert alle Kombinationen der Variablenpaare in einem Datensatz als Streudiagramme und eignet sich hervorragend zur Erkennung von Korrelationen und Zusammenhängen in multidimensionalen Datensätzen.
- **Wann kann ich es besonders gut anwenden:** Wenn es darum geht, Korrelationen und Beziehungen zwischen mehreren Variablen gleichzeitig zu analysieren, ist der Paarplot das Mittel der Wahl.
- **Was wäre eine Alternative:** Alternativen sind Scatterplot-Matrizen oder einzelne Heatmaps.
- **Wie erstelle ich es:**
    - [Seaborn: pairplot](https://seaborn.pydata.org/generated/seaborn.pairplot.html)
    - [Plotly: scatter_matrix](https://plotly.com/python/splom/)



## 8. Balkendiagramm (Bar Chart)

- **Was zeichnet es aus:** Ein Balkendiagramm stellt kategorische Daten durch rechteckige Balken dar, deren Länge proportional zur Häufigkeit oder zum Wert einer Kategorie ist.
- **Wann kann ich es besonders gut anwenden:** Balkendiagramme sind ideal, um die Größenverhältnisse verschiedener Kategorien direkt miteinander zu vergleichen.
- **Was wäre eine Alternative:** Eine Alternative zum Balkendiagramm ist das Säulendiagramm, das ähnliche Daten vertikal darstellt.
- **Wie erstelle ich es:**
    - [Plotly: Bar Chart](https://plotly.com/python/bar-charts/)
    - [Seaborn: barplot](https://seaborn.pydata.org/generated/seaborn.barplot.html)
    - [Matplotlib: bar](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.bar.html)

## 9, Kreisdiagramm (Pie Chart)

- **Was zeichnet es aus:** Ein Kreisdiagramm teilt einen Kreis in Segmente, die jeweils eine Kategorie repräsentieren, und zeigt deren Anteile am Gesamtwert.
- **Wann kann ich es besonders gut anwenden:** Kreisdiagramme sind gut geeignet, um den Anteil einer Kategorie im Verhältnis zum Ganzen darzustellen, allerdings nicht bei mehr als fünf Kategorien.
- **Was wäre eine Alternative:** Alternativen sind Donut Charts oder gestapelte Balkendiagramme, die Verhältnisse auch darstellen können.
- **Wie erstelle ich es:**
    - [Plotly: Pie Chart](https://plotly.com/python/pie-charts/)
    - [Matplotlib: pie](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.pie.html)


## 10. Flächendiagramm (Area Chart)

- **Was zeichnet es aus:** Ein Flächendiagramm ist eine Variation des Liniendiagramms, bei dem der Bereich unter der Linie ausgefüllt ist, um den Wert über eine geordnete Dimension (häufig Zeit) zu verdeutlichen.
- **Wann kann ich es besonders gut anwenden:** Flächendiagramme eignen sich besonders, um kumulative Daten oder Zeitreihendaten zu visualisieren, bei denen der Bereich unter der Linie eine Bedeutung hat.
- **Was wäre eine Alternative:** Liniendiagramme (ohne ausgefüllte Fläche) oder Stapeldiagramme, wenn mehrere Kategorien dargestellt werden sollen.
- **Wie erstelle ich es:**
    - [Plotly: Area Chart](https://plotly.com/python/filled-area-plots/)
    - [Matplotlib: fill_between](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.fill_between.html)


## 11. Blasendiagramm (Bubble Chart)

- **Was zeichnet es aus:** Ein Blasendiagramm ist ein erweitertes Streudiagramm, bei dem die Größe der Punkte eine zusätzliche Dimension repräsentiert, meist einen numerischen Wert.
- **Wann kann ich es besonders gut anwenden:** Blasendiagramme sind nützlich, wenn man drei Dimensionen (zwei für die Achsen und eine für die Punktgröße) auf einmal visualisieren möchte.
- **Was wäre eine Alternative:** Alternativen sind einfache Streudiagramme (für zwei Dimensionen) oder Heatmaps für Korrelationen zwischen mehreren Variablen.
- **Wie erstelle ich es:**
    - [Plotly: Bubble Chart](https://plotly.com/python/bubble-charts/)
    - [Matplotlib: scatter (mit Größenparameter)](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html)


## 12. Gestapeltes Balkendiagramm (Stacked Bar Chart)

- **Was zeichnet es aus:** Ein gestapeltes Balkendiagramm zeigt mehrere Kategorien übereinander in einem Balken, wodurch die Gesamtmenge sowie die Verteilung der Teilkategorien auf einen Blick erkennbar sind.
- **Wann kann ich es besonders gut anwenden:** Diese Darstellung eignet sich für Daten, bei denen man sowohl die Gesamtwerte als auch die Anteile der Unterkategorien gleichzeitig zeigen möchte.
- **Was wäre eine Alternative:** Eine Alternative ist das 100%-gestapelte Balkendiagramm, bei dem die Balken normalisiert werden, sodass sie immer bis 100% reichen.
- **Wie erstelle ich es:**
    - [Plotly: Stacked Bar Chart](https://plotly.com/python/bar-charts/#stacked-bar-chart)
    - [Matplotlib: bar (mit stacked=True)](https://matplotlib.org/stable/gallery/lines_bars_and_markers/bar_stacked.html)