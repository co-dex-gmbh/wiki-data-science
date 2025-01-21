# Naive Bayes Klassifikatior

Der Naive Bayes Klassifikator ist ein wahrscheinlichkeits-basierter Klassifikator, der auf dem Bayes Theorem basiert. Der Klassifikator ist "naive", weil er die Annahme macht, dass die Features unabhängig voneinander sind. Das bedeutet, dass das Auftreten eines bestimmten Features in einer Klasse nicht von dem Auftreten eines anderen Features in derselben Klasse abhängt. Diese Annahme ist in der Praxis selten erfüllt, wird aber trotzdem oft explizit oder immplizit getroffen, da sie die Berechnung der Wahrscheinlichkeiten vereinfacht.

## Satz von Bayes

Der Satz von Bayes trifft eine Aussage über die bedingte Wahrscheinlichkeit von Ereignissen. Eine bedingte Wahrscheinlichkeit ist die Wahrscheinlichkeit für das Eintreten eines Ereignisses unter der Bedingung, dass ein anderes Ereignis bereits bereits eingetreten ist bzw. mit Sicherheit eintreten wird. Ein Beispiel ist die Wahrscheinlichkeit, dass es regnet, wenn der Himmel bewölkt ist. Der Satz von Bayes lautet: 

$$
P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}
$$

Dabei ist $P(A|B)$ die Wahrscheinlichkeit, dass Ereignis $A$ eintritt, wenn Ereignis $B$ bereits eingetreten ist. $P(B|A)$ ist die Wahrscheinlichkeit, dass Ereignis $B$ eintritt, wenn Ereignis $A$ bereits eingetreten ist. $P(A)$ und $P(B)$ sind die Wahrscheinlichkeiten, dass Ereignis $A$ bzw. Ereignis $B$ unabhängig voneinander eintreten.

### Beispiel

**Endstand im Fußball**

Angenommen, wir wollen die Wahrscheinlichkeit berechnen, dass ein Fußballspiel gewonnen wird, wenn das Team in der ersten Halbzeit führt. Die Wahrscheinlichkeit, dass das Team $A$ in der ersten Halbzeit führt, beträgt $P(A) = 0.6$. Die Wahrscheinlichkeit, dass das Team das Spiel gewinnt, wenn es in der ersten Halbzeit führt, beträgt $P(B|A) = 0.8$. Die Wahrscheinlichkeit, dass das Team $B$ das Spiel gewinnt, beträgt $P(B) = 0.7$. Die Wahrscheinlichkeit, dass das Team in der ersten Halbzeit führt, wenn es das Spiel gewinnt, beträgt $P(A|B) = (0.8*0.7)/0.6 = 0.933$.

## Ablauf

1. **Berechnung der Klassenprioritäten:**
   - Für jede Klasse wird die Wahrscheinlichkeit berechnet, dass eine Instanz zufällig zu dieser Klasse gehört. Dies wird als Prioritäts- oder Apriori-Wahrscheinlichkeit bezeichnet und mit $P(C)$ dargestellt, wobei $C$ die Klasse ist.

2. **Berechnung der bedingten Wahrscheinlichkeiten der Merkmale:**
   - Für jedes Merkmal wird die bedingte Wahrscheinlichkeit berechnet, dass dieses Merkmal in einer gegebenen Klasse auftritt. Das wird als $P(F_i | C)$ dargestellt, wobei $F_i$ ein bestimmtes Merkmal ist und $C$ die Klasse ist.

3. **Anwendung des Bayes-Theorems:**
   - Wenn eine neue Instanz klassifiziert werden soll, werden die Wahrscheinlichkeiten für jede Klasse unter Verwendung der bedingten Wahrscheinlichkeiten der Merkmale und der Klassenprioritäten berechnet.

   $$
   P(C | F_1, F_2, ..., F_n) = \frac{P(F_1 | C) \cdot P(F_2 | C) \cdot ... \cdot P(F_n | C) \cdot P(C)}{P(F_1) \cdot P(F_2) \cdot ... \cdot P(F_n)}
   $$

   Da der Nenner für alle Klassen gleich ist, kann er oft ignoriert werden, und die Klassifizierung erfolgt durch Auswahl der Klasse mit der höchsten Wahrscheinlichkeit.

   $$
   \text{Klassifizierung} = \arg\max_C P(C) \prod_{i=1}^{n} P(F_i | C)
   $$


## Spam Detaction with Naive Bayes (Viktor Reichert)
<iframe src="https://www.kaggle.com/embed/viktorreichert/spam-detaction-with-naive-bayes?kernelSessionId=130998781" height="800" style="margin: 0 auto; width: 100%; max-width: 950px;" frameborder="0" scrolling="auto" title="spam detaction with naive bayes"></iframe>

## Mehr

[Übersicht Naive Bayes](https://www.datacamp.com/tutorial/naive-bayes-scikit-learn)

[Übersicht Naive Bayes zum Nachlesen (IBM)](https://www.ibm.com/de-de/topics/naive-bayes)
[Gaussian Naive Bayes](https://medium.com/@kashishdafe0410/gaussian-naive-bayes-understanding-the-basics-and-applications-52098087b963)
