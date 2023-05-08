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
S'introdueix el text a resumir.
···
# Introducción del texto a resumir
text = """ L'Institut Català de Tecnologia ha informat de l'augment del nombre de persones que utilitzen Internet per comprar productes. 
És evident que el mitjà informàtic permet estalviar temps en moltes activitats diàries, a més d'evitar desplaçaments. 
D'una banda, són moltes les activitats que es poden organitzar virtualment: des de fer una senzilla compra fins a realitzar complicades transferències bancàries, passant per reservar un bitllet d'avió o comprar una entrada per al teatre. 
D'altra banda, més enllà de la comoditat evident que suposa aquest avenç tecnològic i l'estalvi de temps, desplaçaments i diners, no hem d'oblidar que al cap i a la fi un ordinador està substituint el treball que hauria de fer una o diverses persones. 
En conseqüència, aquest canvi d'hàbits ens acabarà fent perdre el plaer del dia en família que ens proporciona anar a fer la compra el dissabte o poder parlar amb la noia de l'agència de viatges, que sempre ens recomana la millor opció. 
Per tant, considero que si aquest recurs no es gestiona de forma adequada, podria portar a una notable disminució en les relacions humanes directes. 
Joan García Petit. 
Tàrrega"""
palabras = word_tokenize(text)
frases = sent_tokenize(text)
···
Visualització de les paraules tokenizdas
···
print(palabras)
···
