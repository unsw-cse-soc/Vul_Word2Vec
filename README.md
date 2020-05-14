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
words=['vulnerability','patch']
for w in words:
    try:
        print(word_vect.most_similar(w)[:5])
    except KeyError as e:
            print(e)
>> [(u'vulnerabilities', 0.889), (u'bug', 0.786), (u'flaw', 0.742), (u'exploit', 0.740), (u'issues', 0.739)]
>> [(u'patches', 0.816), (u'updates', 0.707), (u'fixes', 0.702), (u'fix', 0.688), (u'upgrade', 0.667)]
```
```
print(word_vect.similarity('bug', 'flaw'))
>> 0.72691536
```
```
print(word_vect.doesnt_match("exploit attack weakness python".split()))
>> python
```
Examples of analogy queries

```
print(word_vect.most_similar(positive=['exploit', 'title'], negative=['ubuntu']))
>> [(u'vulnerability', 0.571), (u'xss', 0.556), (u'injection', 0.501)]
```

## Word Similarity Dataset
Word Similarity dataset is a collection of words for measuring the similarity and relatedness of cyber security words.
The dataset file is available here for download. The file is in csv format and consists of two columns with word1 and word2. The dataset is available [here](https://drive.google.com/drive/folders/1srBKurZ4wePoAriwuXXKSvW7jmf4cF6X) for download.
