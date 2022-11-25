# Cross-lingual-NLI-for-Thai

## Introduction
### Motivation
Natural Language Inference (NLI) is one of the most important fields of NLP as it can be developed to help in many use cases like automatic auditing, improving search engine, question answering or sentence paraphrasing in various of domains such as banking, retail, finance etc. However, there are still not so many work of NLI in Thai language. Besides, the datasets from crowdsourcing which are often used to train the model for NLI still face many problems of artifacts. Therefore, we would like to train model to do the NLI task in Thai language including using the dataset with the least artifacts as possible.

Moreover, we also want to try implementing the Cross-Lingual Data Augmentation method on our project, as Thai language is among the Low-resources Languages, which means there are not as many data for the language to be used in training AI as other High-resources Languages like English or Chinese.

### Review of Literature
- Cross-Lingual Data Augmentation for NLI

Singh et al. (2019) introduced cross-lingual data augmentation in NLI task with the improvements of up to 4.8%. The method includes replacing a segment of the input text with the translation in other languages. Their experiments showed that with the augmentors of higher resources languages, the performances of NLI task in the target of lower resources languages improved. English and Chinese are among the High-resources Language that can help improving the performance of other languages the most. Therefore, we are using English and Chinese as the augmentors for target of Thai in this project.

- Annotation Artifacts in NLI data

Gururangan et al. (2018) suggested that the datasets for NLI that are commonly created by presenting the crowd workers with premise sentences and asking them to generate three hypothesis sentences for each premises have artifacts which lead to the models being able to correctly predict the hypothesis alone with out the premises in about 67% of SNLI and 53% of MultiNLI. Their analysis reveals the liguistics phenomena that are highly correlated with certain inference classes and making the performance of NLI over-estimated. Therefore, we would avoid using those liguistic fetures in data annotation of this project.

### Idea Summarization
The idea of this project is to use the Cross-Lingual Data Augmentation method for Thai NLI while avoiding the common annotation artifacts in training data in order to see the most accurate performance of the model.

### Result Summarization

## Approach/Methodology/Model
### Input
### Output
### Model Description
### Equation as Necessary
### Process Explaination

## Dataset
### Data Collection
We collect premises from Twitter by scraping Tweets using TWINT lybrary in Python. The Tweets are from hashtags and accounts about news and general topics. Then, we cleaned irrelavant tweets (ads, spams, links, English tweets, emojis etc.)

| hashtags / accounts | Raw Tweets | Cleaned Tweets|
|---------------------|------------|---------------|
| #โหนกระแส |  302 | 32 |
| #อิแทวอน | 148 | 22 |
| #แดนแพตตี้ | 24 | 15 |
| account1 | 300 | 120 |
| account2 | 300 | 130 |
| account3 | 60 | 33 |

Summary : 352 Tweets

### Annotation guidelines

### Result
We got data of 1056 pairs of premises and hypothesis with relations as labels (Entailment / Contradiction / Neutral) translated into English and Chinese. 

### Label distribution (w/table)
| Label | Premise | Hypothesis|
|-------|---------|-----------|
| Entailment | 1760 | 1760 |
| Contradiction | 1760 | 1760 |
| Neutral | 1757 | 1757 |

## Experiment Setup
### Which pre-trained model? How did you pre-train embeddings?
### How long?
### Hyperparameter tuning? Dropout? How many epochs?


## Results
| Model | Train Language | F1 Score |
|-------|----------------|----------|
| WangchanBERTa| Thai | 0.30 |
| Multilingual BERT | Thai | 0.28 |
| Multilingual BERT | Thai-English-Chinese | 0.37 |

### How did it go? + Interpret results (which one is the best with explaination; read the table to reinforce the result)

## Conclusion
### What did we do?
### What task?
### Summary of result
### Literally re-phrasing your work