# Script-Pre-processing-Data
import pandas as pd
data = pd.read_csv('data fix.csv')
data.head()

#link https://github.com/har07/PySastrawi
!pip install Sastrawi
#stopword sastrawi di link  'https://devtrik.com/python/stopword-removal-bahasa-indonesia-python-sastrawi/'
from Sastrawi.StopWordRemover.StopWordRemoverFactory import StopWordRemoverFactory
 
factory = StopWordRemoverFactory()
stopwords = factory.get_stop_words()
print(stopwords)

# import StopWordRemoverFactory class
from Sastrawi.StopWordRemover.StopWordRemoverFactory import StopWordRemoverFactory
 factory = StopWordRemoverFactory()
stopword =  factory.get_stop_words()

import requests
def stopwords():
    r = requests.get("https://raw.githubusercontent.com/masdevid/ID-Stopwords/master/id.stopwords.02.01.2016.txt").text
    data = []
    for x in r.split("\n"):
        data.append(x)
    return data

stopwords()
# Import Stopword Factory class
from Sastrawi.StopWordRemover.StopWordRemoverFactory import StopWordRemoverFactory

#Create factory
factory = StopWordRemoverFactory()
more_stopword = ['school','acu','ad','ora','or','bah','bro','sis','sist','dong','tuh','oh','begitu','b','pas','gak','dongs','hehe','haha','hihi','dih','duh','wah','ya','yah','eh','deh','dah',
                 'wkwk','wow','si','guys','gaes','mba','mbak','mas','anjir','kkkkk', 'aaaaaa', 'jwkakekdkdk', 'aaaaaaihuuuuueeeeeeoooooooo',
                 'min','yes','bang','kak','mah','anjim','anjir','sihh','yuk','bet','loh','woy','doang','tuh','euy','doi','yuhu','ada','aku','gw','gue','gua','elu','lu','kamu','yang','adaitu',
                'kita','gitu','aja','saja','abang','ah','ih','hey','hai','pubg','jt','om','nana','ken','nas','n','kagok','c', 'otw', 'mu',
                'sippp','ih','woi','ew','zoe','lur','da','kyung','aa','v','nih','hadeh','yuk','nder','pakde','uwu','tos','po','a','b','bin','goblok','nih','bu','wes','anjeng','njeng',
             'gaess','t','pe','cua','ca','men','pre','via','rt','ft','zullies','nas','jancuk','o','t','n','i','b','who','hshs','nder','e','t','p','ha','jok','seko','sek']

stopwordplus = factory.get_stop_words()+stopwords()+more_stopword

data['text'] = data['text'].apply(lambda x: " ".join(x for x in x.split() if x not in stopwordplus))
data['text']

stopwordplus

import re
# Function to Tokenize words
def tokenize(text):
    tokens = re.split('\W+', text) #W+ means that either a word character (A-Za-z0-9_) or a dash (-) can go there.
    return tokens
def convertToString(term):
  if type(term) is str:
    return term
  else:
    return str(term)
data['text'] = data['text'].apply(lambda x: tokenize(x.lower())) 
#We convert to lower as Python is case-sensitive. 
data.head()
#import StemmerFactory class
from Sastrawi.Stemmer.StemmerFactory import StemmerFactory
#create stemmer
factory = StemmerFactory()
stemmer = factory.create_stemmer()
#stemming process
def kata_stem(teks):
    stem_teks = " ".join([stemmer.stem(i) for i in teks])
    return stem_teks
data['text'] = data['text'].apply(lambda x: kata_stem(x))
data['text'].head()

import re
#Function to Tokenize words
def tokenize(text):
    tokens = re.split('\W+', text) #W+ means that either a word character (A-Za-z0-9_) or a dash (-) can go there.
    return tokens
data['Komentar'] = data['Komentar'].apply(lambda x: tokenize(x.lower())) 
#We convert to lower as Python is case-sensitive. 
data.head()

#simpan dalam bentuk csv
data.to_csv("ptm.csv", sep=',')
#membaca dalam bentuk csv
import pandas as pd
data = pd.read_csv('ptm.csv')
data.head()
