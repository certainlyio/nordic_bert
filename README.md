Nordic BERT
============

BERT (Bidirectional Encoder Representations from Transformers) is a deep neural network model used in Natural Language Processing. The network learns the grammar and semantics of human language by training on large bodies of text. Google has released BERT models for English and Chinese as well as a single multilingual model for all other languages. The multilingual model performs poorly for languages such as the Nordic languages because of underrepresentation in the training data.

This repository provides downloadable weights for a Danish, a Norwegian and a Swedish BERT model trained from scratch. The models can be used in downstream tasks to improve the performance of Nordic Natural Language Processing systems.

### Download weights

- Danish Model: (Trained on 9.5gb text)
[Version 1](https://www.dropbox.com/s/b2ycb6l3icla0m1/danish_bert_uncased.zip?dl=1),
[Version 2](https://www.dropbox.com/s/19cjaoqvv2jicq9/danish_bert_uncased_v2.zip?dl=1)

- Norwegian Model: (Trained on 4.5gb text)
[Version 1](https://www.dropbox.com/s/avlcftcfm9k6gp0/norwegian_bert_uncased.zip?dl=1) 

- Swedish Model: (Trained on 24.7gb text)
[Version 1](https://www.dropbox.com/s/w38jslro7tb1j4m/swedish_bert_uncased.zip?dl=1) 

- Finnish Model:
(In progress, in the meantime we refer to: https://github.com/TurkuNLP/FinBERT)

### Data

A major challenge of training mid-resources languages such as the Nordic languages is the scarcity of available training data, as General Purpose Language models require very large corpora.

The Danish corpus was compiled by combing multiple sources:

- All Danish language text from Common Crawl (9.5 gb)
- The Danish Wikipedia (221 mb)
- Custom scraped data from the two biggest Danish debate forums (dindebat.dk and hestenettet.dk), (123 mb, 45 mb)
- Danish OpenSubtitles (881 mb)

The Norwegian corpus consists of 5 gb data from Common Crawl.

The Finnish corpus consists of 13 gb data from Common Crawl.

All sources have been cleaned for HTML tags and deduplicated. We have used topic modeling to remove highly overrepresented topics from documents (e.g. cookie policies).

All characters have been converted into either ASCII or one of the special Danish vowels Æ (æ) Ø (ø) and Å (å).

Danish Corpus statistics:

```
Number of sentences: 92,929,330
Number of documents: 26894472
Number of tokens: 1,611,153,110
Number of characters: 9,745,453,532
Number of unique tokens: 19,562,832

Average sentences per document: 3.46
Average tokens per sentence: 17.34
Average characters per token': 6.05
```

### Training

We trained this model on 8 v3 TPUs, achieving a throughput of ~950 training examples / second.

We used the following hyperparameters:

```
Batch size: 1280
Max predictions per training sentence: 20
Max training sentence length: 256
Probability of masking word in training sentence: 0.15
Learning rate: 2e-5
Training steps: 1.000.000
A custom BPE vocabulary of 32.000 tokens.
```

We hold out 5% of the training corpus to be used in evaluation.

### Evaluation

The original BERT model was evaluated on the The Stanford Question Answering Dataset v2.0 (SQuAD v2.0). The loss of the original model was not reported. We provide a graph of the training loss / per iteration:

![BERT Loss](/img/BERT%20loss.png)

### Example Usage

The model can be used directly, or (preferably) fine-tuned on a downstream task. The README in the official Google [BERT repository](https://github.com/google-research/bert) provides instructions and example scripts. It should be noted that the embeddings are trained on lowercase texts, so you should lowercase your input before generating the embeddings.

### Would you like a model in your language / trained on your own custom data?

It requires vast amounts of compute resources to train a BERT model.

We have the technical expertise required to train models, but not the funds.

If your organization would benefit from a BERT model pretrained on a custom dataset, or is interested in sponsoring Nordic AI initiatives, please contact us at jdm@botxo.co.

The price for training a custom model will depend on data size and availability.

#### Why train the original BERT, why not AlBERT, RoBERTa, GPT-2, XLNet etc.?

We believe that establishing an ecosystem around a few standardized models is more important
for most production systems than minor performance improvements.

For better or worse, BERT has gotten a lot of public attention, and as a result, we've started to see an ecosystem of tools
(e.g. [bert-as-service](https://github.com/hanxiao/bert-as-service)) be developed for this model.

### Paper

- Original BERT: https://arxiv.org/pdf/1810.04805.pdf

- Optimizations: https://arxiv.org/pdf/1904.00962.pdf

### Sponsor

If you use this work, please consider staring this repository.

This work was sponsored by Danish Conversational AI & chatbot company BotXO
http://www.botxo.ai

### Licence

Shield: [![CC BY 4.0][cc-by-shield]][cc-by]

This work is licensed under a [Creative Commons Attribution 4.0 International
License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg
