# Vul_Word2vec
A word2vec model trained on multiple heterogeneous sources including Vulners, English Wikipedia, Information Security Stack Exchange Q&As, Common Weakness Enumeration (CWE) and Stack Overﬂow.
## Model file
The the pre-trained model is stored in a .bin file (of approximate size 160 MB).

## Instructions on how to use the model
### Prerequisites
To load the model you will need Python 3.5 and the [gensim](https://radimrehurek.com/gensim/) library.

### Loading the model
```
from gensim.models.keyedvectors import KeyedVectors
word_vect = KeyedVectors.load_word2vec_format("vulner_embedding.bin", binary=True)
```
### Querying the model

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
