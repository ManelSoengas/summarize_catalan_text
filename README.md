# summarize_catalan_text
Generador de resúmenes automático para el idioma catalán
Implementació en Python d'un senzill generador de resumens automátic per un text en Català.
A la carpeta colab hi ha l'arxiu per pujar-lo a google colab.
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
