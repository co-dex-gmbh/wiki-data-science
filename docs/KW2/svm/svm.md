# Support Vector Machines
Support Vector Machines (SVM) sind maschinelle Lernmodelle, die in verschiedenen Anwendungsgebieten weit verbreitet sind. Ihre Beliebtheit gründet sich auf ihrer Fähigkeit, komplexe Entscheidungsgrenzen zu modellieren und gleichzeitig eine effiziente Verarbeitung großer Datenmengen zu ermöglichen. Die Motivation hinter Support Vector Machines liegt in ihrer Fähigkeit, Muster in Daten zu erkennen und Klassifikationsprobleme präzise zu lösen. SVMs zeichnen sich durch ihre Robustheit und Flexibilität aus, wodurch sie sowohl für binäre als auch für mehrklassige Klassifikationsaufgaben geeignet sind. Ihr fundamentales Prinzip besteht darin, eine optimale Trennebene zwischen verschiedenen Klassen zu finden, wobei der Abstand zu den nächsten Datenpunkten maximiert wird. Diese Eigenschaft macht SVMs zu einem bevorzugten Werkzeug in Bereichen wie Mustererkennung, Bildverarbeitung, Textanalyse und vielen anderen Anwendungen im Bereich des maschinellen Lernens.

Die SVM ist ein Modell aus dem überwachten Lernen. Wir schauen uns die SVM als Klassifikationsmodell an. Sie kann allerdings auch für Regressionen verwendet werden.


![Grafik SVM](https://miro.medium.com/v2/resize:fit:1100/1*XE9jt0r1yAW8LnliQ3mllQ.png)


## Wann ist eine SVM geeignet?

Support Vector Machines (SVMs) sind besonders geeignet, wenn bestimmte Merkmale in den Daten hervorgehoben werden sollen oder wenn die Daten hochdimensional sind. Hier sind einige Szenarien, in denen die Verwendung von SVMs angebracht sein könnte:

1. **Klassifikation mit klaren Entscheidungsgrenzen:**
   SVMs eignen sich gut für Aufgaben, bei denen klare Entscheidungsgrenzen zwischen verschiedenen Klassen erforderlich sind. Ihr Hauptziel ist es, eine Trennebene zu finden, die den maximalen Abstand zu den nächstgelegenen Datenpunkten jeder Klasse aufweist.

2. **Hochdimensionale Daten:**
   SVMs sind effektiv, wenn der Datensatz viele Merkmale oder Dimensionen aufweist. Sie können gut mit hochdimensionalen Daten umgehen, ohne anfällig für den sogenannten "Fluch der Dimensionalität" zu sein.

3. **Daten mit nicht-linearen Strukturen:**
   SVMs können durch den Einsatz von Kernel-Tricks auch nicht-lineare Entscheidungsgrenzen modellieren. Das macht sie geeignet für Aufgaben, bei denen die Beziehung zwischen Eingangsmerkmalen und Zielvariablen komplex und nicht linear ist.

4. **Kleine Datensätze mit hoher Dimensionalität:**
   Wenn die Anzahl der Beobachtungen relativ gering ist, aber die Anzahl der Merkmale hoch ist, können SVMs aufgrund ihrer Fähigkeit, mit hochdimensionalen Daten umzugehen, gute Ergebnisse liefern.

5. **Anwendungen mit klaren Trennkriterien:**
   SVMs eignen sich gut für Anwendungen, bei denen eine klare Entscheidung oder Trennung zwischen verschiedenen Klassen erforderlich ist, wie beispielsweise in der Gesichtserkennung oder bei der Erkennung von Anomalien.

6. **Text- und Bildklassifikation:**
   In Anwendungen wie Textklassifikation (z. B. Spam-Erkennung) und Bildklassifikation (z. B. Objekterkennung) haben sich SVMs als leistungsstark erwiesen.

7. **Geriner Datenumfang**
   SVMs sind gut geeignet, wenn der Datensatz relativ klein ist, da sie mit wenigen Daten gut funktionieren können.


## Mathematische Formulierung

Siehe [hier](https://scikit-learn.org/stable/modules/svm.html#svc)

- Die SVM maximiert den Abstand zwischen der separierenden Hyperebene und den nächstgelegenen Klassfikationspunkten (Support Vektoren)
- Die Hyperebene wird durch die Gleichung $w^Tx + b = 0$ beschrieben
- Die Klassifikation erfolgt durch die Vorhersage des Vorzeichens von $w^Tx + b$
- Um die SVM auch auf nicht linear separierbare Daten anwenden zu können, wird die sog. Soft-Margin SVM verwendet. Hierbei wird eine Strafterm eingeführt, der die Anzahl der falsch klassifizierten Punkte minimiert. Dieser Strafterm wird durch den Parameter $C$ gesteuert. Je größer $C$ ist, desto mehrwerden falsch klassifizierte Punkte bestraft.
- Sind die in der Ausgangsdimension nicht linear separierbar, kann der Kernel-Trick verwendet werden, um die Daten in eine höhere Dimension zu transformieren, in der sie linear separierbar sind. Die SVM wird dann in dieser höheren Dimension trainiert und die Vorhersage erfolgt in der ursprünglichen Dimension.
![SVM Aufbau](https://i.stack.imgur.com/FsYi6.png)

- In der Regel wird der RBF Kernel $K(x,y)=exp(-\frac{\| x - y \|}{2*\sigma^2})$ verwendet.
- Weitere Kernel sind der 
>  - lineare Kernel $K(x,y)=\langle x^Ty\rangle$
>  - Polynomiale Kernel $K(x,y)= \gamma \langle x^Ty \rangle + r^d$
>  - Sigmoid Kernel $K(x,y)=tanh(\gamma \langle x^Ty \rangle + r)$

![Kernel](https://miro.medium.com/v2/resize:fit:838/1*gXvhD4IomaC9Jb37tzDUVg.png)

Technisch wird das Optimierungsproblem der SVM durch eine Lagrange Multiplikation umgeschrieben. Dadurch entstehen $\alpha_i$, welche als Ein- bzw. Ausschalter für die Gewichtung einer Vorhersage bei der Optimierung interpretiert werden können. Die Gewichtung der Vorhersage erfolgt durch die Summe der Produkte aus $\alpha_i$ und dem Kernel $K(x_i,x)$, also $\sum_{i=1}^n \alpha_i K(x_i,x)$. 

Bei der Verwendung eines Soft-Margins werden Schlupfvariablen $\xi_i$ einfedührt, welche bei falschen Klassifizierungen den Einflus des Fehlers redizieren können. Dadurch werden beim Training Fehler zugelassen. Die Gewichtung der Fehler erfolgt dann durch $C \sum_{i=1}^n \xi_i$. $C$ steuert also, wie Stark Fehler gewichtet werden. Je größer $C$ ist, desto stärker werden Fehler gewichtet.

Der Parameter Gamma aus den Kernel-Funktionen gewichtet ebenfalls, wie stark die einzelnen Punkte in der Vorhersage gewichtet werden. Je größer Gamma ist, desto stärker werden die einzelnen Punkte gewichtet. Dies kann zu einer Überanpassung führen.

In der Praxis sollte Gammach nach Möglichkeit gering gehalten werden, um eine Überanpassung zu vermeiden. $C$ sollte so gewählt werden, dass die Anzahl der falsch klassifizierten Punkte möglichst gering ist. Dies kann durch eine Kreuzvalidierung ermittelt werden. Gute Parameterkombinationen können beispielsweise durch eine GridSearch ermittelt werden.

Aufgrund der Konstruktion der SVM kann diese zunächst nur in 2 Klassen (binär) unterscheiden. Um trotzdem mehr als 2 Klassen behandeln zu können, gibt es verschiedene Ansätze. Diese vergleichen die einzelenen Klasse untereinander oder fassen sie zu temporär zu Oberklassen zusamme. Eine Übersicht zu zwei verbreiteten Ansätzen findet ihr [hier](/machine_learning_basics/klassifikationen#multi-klassen-klassifikation).

<!-- ## Checkliste

**Checkliste für SVM (Support Vector Machines)-Teilnehmer:**

1. [ ] Ich kann den Zweck von SVM in der maschinellen Lernens erklären.
1. [ ] Ich verstehe das Konzept der Trennfläche und wie SVM Entscheidungsgrenzen erstellt.
1. [ ] Ich verstehe, wie lineare und nichtlineare SVM funktionieren.
1. [ ] Ich kann den Begriff der Margen und Support-Vektoren in SVM erklären.
1. [ ] Ich verstehe die Rolle von Kernels in nichtlinearen SVMs.
1. [ ] Ich kann SVM-Modelle für Klassifikation erstellen.
1. [ ] Ich kann die Auswirkungen von SVM-Parametern wie dem C-Parameter und dem Kerneltyp erklären.
1. [ ] Ich kann den Unterschied zwischen Soft Margin und Hard Margin SVM erklären.
1. [ ] Ich verstehe, wie man den C-Parameter einstellt, um den Trade-off zwischen Fehler und Margin zu steuern.
1. [ ] Ich kann SVM für Mehrklassen-Klassifikation anwenden, z.B., durch One-vs-One oder One-vs-Rest Ansätze.
1. [ ] Ich verstehe, wie SVM mit mehreren Klassen umgeht.
1. [ ] Ich kann die Vor- und Nachteile von SVM im Vergleich zu anderen maschinellen Lernalgorithmen erklären.
1. [ ] Ich verstehe, in welchen Situationen SVM besonders effektiv ist. -->




## Referenzen und Nachschlagmaterial

- [Support Vector Machines in scikit-learn](https://scikit-learn.org/stable/modules/svm.html)
- [Erklärung SVM und Kernel](https://www.analyticsvidhya.com/blog/2021/10/support-vector-machinessvm-a-complete-guide-for-beginners/)
- [Youtube Video zu SVM](https://www.youtube.com/watch?v=ny1iZ5A8ilA)