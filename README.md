# Cross-lingual-NLI-for-Thai

## Introduction
Natural Language Inference (NLI) is one of the most important fields of NLP as it can be developed to help in many use cases like automatic auditing, improving search engine, question answering or sentence paraphrasing in various of domains such as banking, retail, finance etc. However, there are still not so many work of NLI in Thai language. Besides, the datasets from crowdsourcing which are often used to train the model for NLI still face many problems of artifacts. Therefore, we would like to train model to do the NLI task in Thai language including using the dataset with the least artifacts as possible.

Moreover, we also want to try implementing the Cross-Lingual Data Augmentation method on our project, as Thai language is among the relatively Low-resources Languages, which means there are not as many data for the language to be used in training AI as other High-resources Languages like English or Chinese.

#### Review of Literature
- Cross-Lingual Data Augmentation for NLI

Singh et al. (2019) introduced cross-lingual data augmentation in NLI task with the improvements of up to 4.8%. The method includes replacing a segment of the input text with the translation in other languages. Their experiments showed that with the augmentors of higher resources languages, the performances of NLI task in the target of lower resources languages improved. English and Chinese are among the High-resources Language that can help improving the performance of other languages the most. Therefore, we are using English and Chinese as the augmentors for target of Thai in this project.

- Annotation Artifacts in NLI data

Gururangan et al. (2018) suggested that the datasets for NLI that are commonly created by presenting the crowd workers with premise sentences and asking them to generate three hypothesis sentences for each premises have artifacts which lead to the models being able to correctly predict the hypothesis alone with out the premises in about 67% of SNLI and 53% of MultiNLI. Their analysis reveals the liguistics phenomena that are highly correlated with certain inference classes and making the performance of NLI over-estimated. Therefore, we would avoid using those liguistic fetures in data annotation of this project.

#### Idea Summarization
The idea of this project is to use the Cross-Lingual Data Augmentation method for Thai NLI while avoiding the common annotation artifacts in training data in order to see the most accurate performance of the model.

## Methodology
### Input-Output
As training the NLI task requires more than one input, premise and hypothesis, which are sequences of tokens that entail, contradict or not related to each other. Special tokens [CLS] and [SEP] are required to help the model understand the end of the first input and the start of another input in the same sequence input properly. The final input must looks like:
```
[CLS] premise [SEP] hypothesis [SEP]
```
### Model Description
We used 3 transformer models including 1 monolingual model, WangchanBERTa [Lowphansirikul et al., 2021], the pre-training Thai language model, and 2 multilingual models that are pre-trained on several languages including three languages used in our dataset, mBERT [Devlin et al., 2019] and XLM RoBERTa base [Conneau et al., 2020].

## Dataset
### Data Collection
We collect premises from Twitter by scraping Tweets using TWINT library in Python. The Tweets are from hashtags and accounts about news and general topics. Then, we cleaned irrelevant tweets (ads, spams, links, English tweets, emojis etc.).

| Hashtags/Accounts |Category| Raw Tweets | Cleaned Tweets|
|-------------------|--------|------------|---------------|
| #โหนกระแส | news |  302 | 32 |
| #อิแทวอน | news |148 | 22 |
| #แดนแพตตี้ |entertainment | 24 | 15 |
| account1 | general topics |300 | 120 |
| account2 | news |300 | 130 |
| account3 | general topics |60 | 33 |

Summary : 352 Tweets

### Annotation guidelines
We generated the hypothesis to the premises we got from Twitter according to this guideline.

Entailment: h is definitely true when p is true
- Do not just change the noun with their hypernym nor the number. Try to change the verb.
- Do not just cut out the modifier part of the sentence. Try to change the formation.

Contradiction: h is definitely not true when p is true
- Do not just add the negation and/or change the number.
- If the negation is added and/or the number is changed, change the verb, too.

Neutral: h might be true or not when p is true
- Do not just add the modifier part and/or superlative to the sentence.
- Try to change the matter within the topic of premise.

### Data Result
We got data of 1056 pairs of premises and hypotheses with relations as labels (Entailment/ Contradiction/ Neutral), then we translated them into Chinese and English, which resulted in a total of 5280 pairs. We selected 200 pairs of Thai premises and hypotheses for the test set. In total, we have a train set of 5080 pairs divided by label as follows:

##### Train set
| Label | Premise | Hypothesis|
|-------|---------|-----------|
| Entailment | 1693 | 1693 |
| Contradiction | 1694 | 1694 |
| Neutral | 1693 | 1693 |


##### Test set
| Label | Premise | Hypothesis|
|-------|---------|-----------|
| Entailment | 67 | 67 |
| Contradiction | 66 | 66 |
| Neutral | 67 | 66 |

## Experiment Setup
We prepared a dataset for Thai-only NLI and the cross-lingual augmented dataset by replacing some segments of the original Thai input texts with the translation in English and Chinese.

### Pre-trained Model
We used WangchanBERTa [Lowphansirikul et al. 2021], the pretraining transformer-based Thai Language Models for Thai-only data as the baseline. Then, we used mBERT [Devlin et al., 2019] and XLM RoBERTa base [Conneau et al., 2020], the multilingual version of BERT-base and RoBERTa base that pre-trained on several languages include Thai, English and Chinese for Thai-only and cross-lingual augmented data in Thai-English-Chinese. The hyperparameter tuning was done by adjusting learning rate, batch size and epochs as seen in the table below:

| Model             | Dataset | Learning Rate | Batch Size | Epochs | Time usage |
|-------------------|---------|---------------|------------|--------|------------|
| WangchanBERTa     |  Thai   |               |            |        |            |
| XLM RoBERTa base |  Thai    |               |            |        |            |
| XLM RoBERTa base | Thai-English |    8e-6   | 16         | 12     | 10m        |
| XLM RoBERTa base | Thai-Chinese | 8e-6      | 24         | 15     | 9m 55s     |
| XLM RoBERTa base |  Thai-English-Chinese | 8e-6 | 16     | 12     | 21m        |
| Multilingual BERT |  Thai   |       8e-6    |      32    |   10    |    5m 56s |
| Multilingual BERT | Thai-English |     8e-6 |      32     |   10    |  10m 14s |
| Multilingual BERT | Thai-Chinese |    8e-6  |      32     |   10    |  9m 41s  |
| Multilingual BERT | Thai-English-Chinese |  8e-6 |    24      |    15    |  40m   |

## Results
### Model comparison
| Model | Dataset |F1 Score |
|-------|---------|---------|
| WangchanBERTa| Thai | 0.38 |
| XLM RoBERTa base | Thai | |
| XLM RoBERTa base | Thai-English | 0.55 |
| XLM RoBERTa base | Thai-Chinese | 0.49 |
| XLM RoBERTa base | Thai-English-Chinese | 0.87 |
| Multilingual BERT | Thai | 0.67 |
| Multilingual BERT | Thai-English | 0.53 |
| Multilingual BERT | Thai-Chinese | 0.48 |
| Multilingual BERT | Thai-English-Chinese | 0.88 |

According to the table, models using cross-lingual dataset from both high-resource languages give better results than those using Thai-only dataset or cross-lingual dataset using only one high-resource language. The reason is that cross-lingual data augmentation give more amount of data to train the models which leads to better efficiency of the models just like Singh et al. (2019) said in their research. For the model, XLM RoBERTa base has their best F1 score at 0.87.

## Conclusion
The problem of low-resource languages is lack of data to train language models efficiently. Moreover, huge amount of data annotation requires time, resources and guidelines in order to avoid artifacts or bias in data as much as possible. Also, there are not so many experiments in NLI of Thai language. Therefore, we introduce “Cross-lingual Data Augmentation for Thai NLI Task” by using high-resource languages like English and Chinese as augmenters to help increase the amount of training data making it five times as much as original data in Thai only. This method significantly helps increasing the models efficiency with XLM RoBERTa having the best performance at F1 score of 0.87 following by mBERT at F1 score of 0.74. Both surpassed our monolingual baseline model WangchanBERTa with twice more F1 score.
