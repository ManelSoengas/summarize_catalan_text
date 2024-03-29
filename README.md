# Summarize_catalan_text
Generador de resúmenes automático para el idioma catalán
Implementació en Python d'un senzill generador de resumens automátic per un text en Català.
A la carpeta colab hi ha l'arxiu per pujar-lo a google colab.
A l'exemple s'utilitzen models pre-entrenats. Models que han estat entrenats mitjançant enfocs basats en IA.
Prperament, veurem algún exemple d'entrenament d'un model per utilitzar-lo a una tasca determinada.
```
#Carga de la libreria y modelo
# para el idioma.
!python -m spacy download ca_core_news_sm
import spacy

nlp = spacy.load('ca_core_news_sm')
import nltk
nltk.download('stopwords')
#Visualización de las "stopwords"

from nltk.corpus import stopwords

stops = set(stopwords.words('catalan'))
print(stops)

nltk.download('punkt')
```
A continuació es carreguen els mòduls necessaris.
```
#Importación de los módulos necesarios
from nltk.tokenize import word_tokenize, sent_tokenize
from nltk.tag import pos_tag
from nltk.chunk import ne_chunk
```
S'introdueix el text a resumir.
```
# Introducción del texto a resumir
text = """ Introdueix el text a resumir, en Català"""
palabras = word_tokenize(text)
frases = sent_tokenize(text)
```
Visualització de les paraules tokenizdas
```
print(palabras)
```
Es calcula la freqüència de cada paraula i es mira que no estigui al llistat de stopwords.
```
freqTabla = {}
for word in palabras:
    word = word.lower()
    if word not in stops:
        if word in freqTabla:
            freqTabla[word] += 1
        else:
            freqTabla[word] = 1
```
S'emmagatzema la puntaució de cada frase.
```
fraseValor = {}
for sentence in frases:
    for word, freq in freqTabla.items():
        if word in sentence.lower():
            if sentence in fraseValor:
                fraseValor[sentence] += freq
            else:
                fraseValor[sentence] = freq

```
Detecció de les entitats nombrades ( Nom propi, nom de país, nom de rius, etc...)
Les oracions amb entitats nombrades es consideren com a rellevants en els resums.

```
doc = nlp(text)
relevantes_entidades = []
for ent in doc.ents:
    if ent.label_ == 'PER':
        relevantes_entidades.append(ent.text)

```
Ordenar les oracions segons la seva posició en el text
```
frases_orden = sorted(fraseValor.items(), key=lambda x: x[0])
```
Cálcul del valor mitjà de les oracions del text
```
sumaValores = 0
for sentence in fraseValor:
    sumaValores += fraseValor[sentence]
    print("Puntuación: '{}': {}".format(sentence, fraseValor[sentence]))
average = int(sumaValores / len(fraseValor))
print("Puntuación promedio de las oraciones: {}".format(average))
```
Generar un llista per emmagatzemar les oracions seleccionades i limitar el resum a un nombe de línies determinat.
```
resumen = []
count = 0
for sentence in frases:
    if sentence in fraseValor and fraseValor[sentence] >= average:
        resumen.append(sentence)
        count += 1
        if count == 3:  # Detener el bucle después de agregar 5 oraciones al resumen
            break
```
Evitar repeticions
```
relevantes_frases = []
for entity in relevantes_entidades:
    for sentence in frases:
        if entity in sentence and sentence not in relevantes_frases and sentence not in resumen:
            relevantes_frases.append(sentence)
```
Generació del resum
```
resumen = " ".join(resumen + relevantes_frases)

# Imprimir el resumen por líneas
for line in resumen.splitlines():
    print(line)

```
