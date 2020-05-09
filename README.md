# Word Representation for Cyber Security Vulnerability Domain
This repo provides a word representation (SecVuln_WE) and a dataset for benchmarking word similarity and relatedness for cyber security vulnerability domain. The following paper describes the step-by-step procedure for training the word embedding and construction of similarity dataset. 

## SecVuln_WE
A word2vec model trained on multiple heterogeneous sources including Vulners, English Wikipedia (Security category), Information Security Stack Exchange Q&As, Common Weakness Enumeration (CWE) and Stack Overﬂow.
### Model file
The pre-trained WE (SecVuln) is stored in a .bin file (of approximate size 160 MB).

### Instructions on how to use the model
#### Prerequisites
To load the model you will need Python 3.5 and the [gensim](https://radimrehurek.com/gensim/) library.

#### Loading the model
```
from gensim.models.keyedvectors import KeyedVectors
word_vect = KeyedVectors.load_word2vec_format("vulner_embedding.bin", binary=True)
```
#### Querying the model

Examples of semantic similarity queries
```
words=['cve','patch','sql']
for w in words:
    try:
        print(word_vect.most_similar(w))
    except KeyError as e:
            print(e)
```
```
print(word_vect.doesnt_match("exploit attack weakness python".split()))
```
Examples of analogy queries

```
print(word_vect.most_similar(positive=['exploit', 'title'], negative=['ubuntu']))
```

## Word Similarity Dataset
Word Similarity dataset is a collection of words for measuring the similarity and relatedness of cyber security words.
The dataset is available here for download.
