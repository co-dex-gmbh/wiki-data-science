# Word2Vec und GloVe: Eine vollständige Betrachtung

## Grundlegendes Konzept

Word2Vec und GloVe sind zwei fundamentale Ansätze zur Erstellung von Word Embeddings. Beide Methoden basieren auf der linguistischen Annahme, dass die Bedeutung eines Wortes durch seinen Kontext bestimmt wird. Diese Idee wird in der Linguistik als distributionelle Semantik bezeichnet.

## Word2Vec im Detail

Word2Vec verwendet ein neuronales Netzwerk mit einer versteckten Schicht, um Wörter in einen kontinuierlichen Vektorraum abzubilden. Es gibt zwei grundlegende Architekturen:

1. **CBOW (Continuous Bag of Words)**: Vorhersage eines Wortes aus seinem Kontext
2. **Skip-gram**: Vorhersage des Kontexts aus einem Wort

### Grundlegende Implementierung

```python
from gensim.models import Word2Vec

# Beispiel für Skip-gram
sentences = [["Der", "Hund", "bellt", "laut"], 
            ["Die", "Katze", "miaut", "leise"]]

model = Word2Vec(sentences, vector_size=100, window=2, sg=1)
```

### EXKURS: Skip-gram Algorithmus im Detail
Der Skip-gram Algorithmus maximiert die bedingte Wahrscheinlichkeit des Kontexts, gegeben ein Zielwort. Der mathematische Prozess läuft wie folgt ab:

```python
def skip_gram_detailed(center_word_idx, context_window, W, C):
    # Center word vector
    v_c = W[center_word_idx]
    
    total_loss = 0
    gradients = []
    
    for pos in context_window:
        # Context word vector
        u_o = C[pos]
        
        # Softmax Berechnung
        score = np.dot(v_c, u_o)
        prob = np.exp(score) / np.sum(np.exp(np.dot(v_c, C.T)))
        
        # Loss berechnen
        loss = -np.log(prob)
        total_loss += loss
        
        # Gradienten speichern
        grad = (prob - 1) * u_o
        gradients.append(grad)
        
    return total_loss, gradients
```

## GloVe: Global Vectors

GloVe unterscheidet sich von Word2Vec durch seinen globalen Ansatz. Statt einzelner Kontextfenster betrachtet GloVe die gesamte Wort-Kookkurrenz-Matrix des Textkorpus.

### Grundlegende Implementierung

```python
def create_cooccurrence_matrix(sentences, window_size=2):
    vocab = {}
    word_count = 0
    
    # Vokabular erstellen
    for sentence in sentences:
        for word in sentence:
            if word not in vocab:
                vocab[word] = word_count
                word_count += 1
    
    # Kookkurrenz-Matrix aufbauen
    cooc = np.zeros((len(vocab), len(vocab)))
    
    for sentence in sentences:
        for i, word in enumerate(sentence):
            for j in range(max(0, i-window_size), 
                         min(len(sentence), i+window_size+1)):
                if i != j:
                    cooc[vocab[word]][vocab[sentence[j]]] += 1
    
    return cooc, vocab
```

### EXKURS: GloVe Algorithmus im Detail
GloVe optimiert eine spezielle Verlustfunktion, die die globalen Kookkurrenzen berücksichtigt:

```python
def glove_loss_detailed(W, W_context, b_w, b_c, X, f_max=100, alpha=0.75):
    vocab_size = W.shape[0]
    loss = 0
    gradients = {
        'W': np.zeros_like(W),
        'W_context': np.zeros_like(W_context),
        'b_w': np.zeros_like(b_w),
        'b_c': np.zeros_like(b_c)
    }
    
    for i in range(vocab_size):
        for j in range(vocab_size):
            if X[i,j] > 0:
                # Gewichtungsfunktion
                weight = (X[i,j]/f_max)**alpha if X[i,j] < f_max else 1
                
                # Berechne Vorhersage und Ziel
                prediction = np.dot(W[i], W_context[j]) + b_w[i] + b_c[j]
                target = np.log(X[i,j])
                
                # Berechne gewichteten Verlust
                diff = prediction - target
                loss += weight * (diff ** 2)
                
                # Aktualisiere Gradienten
                gradients['W'][i] += weight * diff * W_context[j]
                gradients['W_context'][j] += weight * diff * W[i]
                gradients['b_w'][i] += weight * diff
                gradients['b_c'][j] += weight * diff
    
    return loss, gradients
```

## Vergleich und praktische Anwendung

### Stärken von Word2Vec:

- Effizient bei großen Datensätzen
- Gut bei seltenen Wörtern
- Lernt aus lokalem Kontext

### Stärken von GloVe:

- Nutzt globale Statistiken
- Bessere Performance bei häufigen Wörtern
- Explizite Modellierung von Wortbeziehungen

### EXKURS: Optimierungstechniken
Beide Methoden verwenden unterschiedliche Optimierungstechniken:

```python
def adagrad_optimizer(params, gradients, learning_rate=0.05, epsilon=1e-8):
    """AdaGrad Optimierung für GloVe"""
    if not hasattr(adagrad_optimizer, "hist_grads"):
        adagrad_optimizer.hist_grads = {k: np.zeros_like(v) 
                                      for k, v in params.items()}
    
    updated_params = {}
    for param_name in params:
        # Akkumuliere quadrierte Gradienten
        adagrad_optimizer.hist_grads[param_name] += \
            gradients[param_name]**2
        
        # Berechne adaptierte Lernrate
        adapted_lr = learning_rate / (np.sqrt(
            adagrad_optimizer.hist_grads[param_name] + epsilon))
        
        # Update Parameter
        updated_params[param_name] = params[param_name] - \
                                   adapted_lr * gradients[param_name]
    
    return updated_params

def negative_sampling(positive_word_idx, vocab_size, n_samples=5):
    """Negative Sampling für Word2Vec"""
    negatives = []
    while len(negatives) < n_samples:
        neg_idx = np.random.randint(0, vocab_size)
        if neg_idx != positive_word_idx:
            negatives.append(neg_idx)
    return negatives
```

## Praktische Implementierung und Anwendung

Ein vollständiges Beispiel für die Verwendung beider Methoden:

```python
def compare_embeddings(texts):
    # Word2Vec Training
    w2v_model = Word2Vec(texts, vector_size=100, window=5, 
                        min_count=1, workers=4)
    
    # GloVe Vorbereitung
    cooc_matrix, vocab = create_cooccurrence_matrix(texts)
    
    # Vergleiche Wortähnlichkeiten
    test_word = "Hund"
    similar_words_w2v = w2v_model.wv.most_similar(test_word)
    
    print("Word2Vec ähnliche Wörter:", similar_words_w2v)
    
    return w2v_model
```

### EXKURS: Fortgeschrittene Anwendungen
In der Praxis werden oft spezielle Techniken verwendet, um die Qualität der Embeddings zu verbessern:

1. **Subword Information**: Behandlung von unbekannten Wörtern
2. **Dynamic Window Size**: Anpassung der Kontextgröße
3. **Frequency Weighting**: Gewichtung basierend auf Worthäufigkeit

```python
def advanced_preprocessing(text):
    """Fortgeschrittene Vorverarbeitung für bessere Embeddings"""
    # Subword-Tokenisierung
    subwords = break_into_subwords(text)
    
    # Dynamische Fenstergröße
    window_size = calculate_dynamic_window(text)
    
    # Frequenzgewichtung
    weights = calculate_frequency_weights(text)
    
    return subwords, window_size, weights
```

Die Wahl zwischen Word2Vec und GloVe hängt von spezifischen Anforderungen ab:

- Datenmenge und Rechenressourcen
- Gewünschte semantische Eigenschaften
- Bedeutung seltener Wörter
- Notwendigkeit globaler Statistiken