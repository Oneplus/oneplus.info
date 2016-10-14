---
layout: post
published: true
title: New neural parser added to LTP
author: Oneplus
tags:
- NLP
---

[[Github](https://github.com/HIT-SCIR/ltp/releases/tag/v3.3.0)]
[[Pre-trained Model](http://pan.baidu.com/share/link?shareid=1988562907&uk=2738088569#path=%252Fltp-models%252F3.3.0)]

We recently added a new dependency parser to LTP.
This parser is a transiton-based neural network parser, which mainly based on Chen and Manning (2014).
Besides the parser originally described in their work, additional features are also incorporated in our parser, including global feature (Zhang and Nivre, 2011), word cluster and dynamic oracle (Goldberg et. al. 2014).
Dr. Jiang Guo developed the prototype for this parser in his _ACL2015_ work.

For quick summary, our new parser's main features includes

- Fast linear parsing time: over 8,000 tokens/second.
- High parsing accuracy: 85.24 (UAS) on CTB5

and the key techniques includes

- Linear time transition-based parsing.
- Neural network classifier with cubic active function
- Supporting clustering features and global features
- Supporting learning from dynamic oracle

### Word Cluster

Word cluster can be the most reliable feature acrossing the syntactic tasks, including POS tagging, NER and parsing.
Thus, the performance improvement we gain from word cluster is as expected.
In our system, word cluster is added to as another 'POS tag'.

### Global Feature

Zhang and Nivre (2012) study the problem of interaction between searching and learning. Their work can be summarized as

- local learning + greedy search: [good]
- local learning + beam search: [bad]
- global learning + greedy search: [bad]
- global learning + beam search: [good]

They also say that

- local learning + global features: [bad]
- global learning + global features: [good]

We also found that global features contribute nothing if they are added to the parser standalone.
But we found that when coupled with word cluster, the global feature can further help.
Thus, this feature is add in our released version.

### Dynamic Oracle

Dynamic oracle is another reliable stuff!
On the NLTK's issues list, Dr. Honnibal (author of spaCy) quoted that

> Second, when you train the parser, you parser, you should really use the Goldberg and Nivre (2012) "dynamic oracle" strategy.

We also found dynamic oracle works great on Chinese dataset.
The detailed result will be presented in experiment section.

### Experiment

We report our parser's performance on Chinese treebank 5 and Chinese dependency treebank.
Parsing accuray is evaluated using UAS/LAS.
We also compare our result with the our old LTP parser and the other state-of-the-art parsers.

#### CTB5 experiment

CTB5 data is splited according to Zhang and Clark (2008), with 16,091 for training, 1,910 for testing and 803 for development.
Word embedding trained on Gigawords xinhua news with word2vec is used as initialization embedding.
Brown clustering result with 1000 clusters on the same data are also used in our experiment.

 Parser                     | Dev.UAS| Dev.LAS| Test.UAS| Test.LAS| Test Speed(tokens/sec.)
-------------------------------------------|-------|-------|-------|-------|---------------
 ZPar (b=64)                               | 85.15 | 85.45 | 85.82 | 84.54 | (about-) 700  
 LTP (o2sib)                               | 84.46 | 82.96 | 84.05 | 82.62 | 40.99(?)      
 NN (e=50,h=200)                           | 82.87 | 81.13 | 83.22 | 81.68 | 16737.41      
 NN-nondet(e=50,h=200)                     | 83.48 | 81.75 | 83.95 | 82.40 |               
 NN-explore(e=50,h=200)                    | 84.42 | 82.68 | 84.44 | 82.70 |               
 NN-explore+glob.feat(e=50,h=200)          | 84.48 | 82.79 | 84.74 | 83.02 | 14627.79      
 NN-explore+cluster(e=50,h=200)            | 85.08 | 83.26 | 84.98 | 83.28 | 9734.88       
 NN-explore+glob.feat+cluster(e=50,h=200)  | 85.16 | 83.54 | 85.24 | 83.61 | 9325.72       

#### CDT experiment

Suggested data split is used in CDT experiment.
Embedding and cluster settings are almost identical to the CTB5 experiment except that data are segmented with a PKU standard segmentor.

 Parser                     | Dev.UAS| Dev.LAS| Test.UAS| Test.LAS| Test Speed(tokens/sec.)
-------------------------------------------|-------|-------|-------|-------|---------------
 ZPar (b=64)                               | 86.43 | 83.68 | 85.48 | 82.41 |  
 LTP (o2sib)                               | 84.95 | 82.09 | 83.99 | 81.31 | 263.89
 NN (e=50,h=400)                           | 84.33 | 81.57 | 83.04 | 80.01 | 11478.48
 NN-explore(e=50,h=400)                    | 85.02 | 82.41 | 83.74 | 80.81 |               
 NN-explore+glob.feat(e=50,h=400)          | 84.81 | 82.23 | 83.56 | 80.65 | 
 NN-explore+cluster(e=50,h=400)            | 85.82 | 83.25 | 83.49 | 80.60 | 
 NN-explore+glob.feat+cluster(e=50,h=400)  | 85.80 | 83.19 | 84.11 | 81.17 | 8448.45

Generally speaking, the dynamic oracle shows to improve parsing accuracy on both dataset.
What's more, brown cluster is also a great feature to boost up the score.

### "In a way to kill old people"

<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/1.0.2/Chart.min.js"></script>

We can see the parsing accuracy and speed benchmark with our the old LTP parser in the following chart.

<canvas id="speed" width="200" height="300"></canvas>
<canvas id="accuracy" width="200" height="300"></canvas>

<script>
var spd_dat = {
    labels: ["old parser", "new parser",],
    datasets: [
    {
        label: "parsing speed",
        fillColor: "rgba(220,220,220,0.5)",
        strokeColor: "rgba(220,220,220,0.8)",
        highlightFill: "rgba(220,220,220,0.75)",
        highlightStroke: "rgba(220,220,220,1)",
        data: [263.89, 8448.45]
    }]
};
var acc_dat = {
    labels: ["old parser", "new parser",],
    datasets: [
    {
        label: "parsing accuracy",
        fillColor: "rgba(220,220,220,0.5)",
        strokeColor: "rgba(220,220,220,0.8)",
        highlightFill: "rgba(220,220,220,0.75)",
        highlightStroke: "rgba(220,220,220,1)",
        data: [83.99, 84.11]
    }]
};

var spd_ctx= document.getElementById("speed").getContext("2d");
new Chart(spd_ctx).Bar(spd_dat, {barShowStroke: false});
var acc_ctx= document.getElementById("accuracy").getContext("2d");
new Chart(acc_ctx).Bar(acc_dat, {barShowStroke: false});
</script>
In a way to kill old people, as the phrase is.

### Reference

- Danqi Chen and Christopher Manning, 2014, A Fast and Accurate Dependency Parser using Neural Networks, In Proc. _EMNLP2014_
- Yue Zhang and Joakim Nivre, 2011, Transition-based Dependency Parsing with Rich Non-local Features, In Proc _ACL2011_
- Yoav Goldberg, Francesco Sartorioand Giorgio Satta, 2014, A Tabular Method for Dynamic Oracles in Transition-Based Parsing, In _TACL2014_
- Jiang Guo, Wanxiang Che, David Yarowsky, Haifeng Wang and Ting Liu, 2015, Cross-lingual Dependency Parsing Based on Distributed Representations, (to apper) In Proc _ACL2015_
- Yue Zhang and Joakim Nivre, 2012, Analyzing the Effect of Global Learning and Beam-Search on Transition-Based Dependency Parsing, In Proc _COLING2012_
- Yue Zhang and Stephen Clark, A Tale of Two Parsers: Investigating and Combining Graph-based and Transition-based Dependency Parsing, In Proc _ACL2008_

<style>
table{ border-collapse: collapse; border-spacing: 0; border:2px solid #ff0000; width: 100%; }
th{ border:2px solid #000000; }
td{ border:1px solid #000000; }
</style>

