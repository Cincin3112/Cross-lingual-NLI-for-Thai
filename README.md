# Cross-lingual-NLI-for-Thai

## Introduction
### Motivation
Natural Language Inference (NLI) is one of the most important fields of NLP as it can be developed to help in many use cases like automatic auditing, improving search engine, question answering or sentence paraphrasing in various of domains such as banking, retail, finance etc. However, there are still not so many work of NLI in Thai language. Besides, the datasets from crowdsourcing which are often used to train the model for NLI still face many problems of artifacts. Therefore, we would like to train model to do the NLI task in Thai language including using the dataset with the least artifacts as possible.

Moreover, we also want to try implementing the Cross-Lingual Data Augmentation method on our project, as Thai language is among the relatively Low-resources Languages, which means there are not as many data for the language to be used in training AI as other High-resources Languages like English or Chinese.

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
We got data of 1056 pairs of premises and hypothesis with relations as labels (Entailment / Contradiction / Neutral) translated into English and Chinese using Google Translation. 

### Label distribution
The labels are distributed according to types of inference which are "Entailment", "Contradiction" and "Neutral"

| Label | Premise | Hypothesis|
|-------|---------|-----------|
| Entailment | 1760 | 1760 |
| Contradiction | 1760 | 1760 |
| Neutral | 1760 | 1760 |

## Experiment Setup
We prepared a dataset for Thai-only NLI and the cross-lingual augmented dataset by replacing some segments of the original Thai input texts with the translation in English and Chinese.

### Pre-trained Model
We used WangchanBERTa[Lowphansirikul et al. 2021], the pretraining transformer-based Thai Language Models for Thai-only data as the baseline. Then, we used mBERT[Devlin et al., 2019], the BERT-based multilingual language model that includes Thai, English and Chinese for Thai-only and cross-lingual augmented data in Thai-English-Chinese.

| Model | Train Language | Time usage |
|-------|----------------|------------|
| WangchanBERTa| Thai |  |
| Multilingual BERT | Thai |  2 m 30 s |
| Multilingual BERT | Thai-English-Chinese | 10 m |

### Hyperparameter tuning? Dropout? How many epochs?


## Results
| Model | Train Language | epochs |F1 Score |
|-------|----------------|--------|----------|
| WangchanBERTa| Thai | 3 | 0.30 |
| XLM RoBERTa large | Thai | 3 | |
| XLM RoBERTa large | Thai-English-Chinese | 3 | |
| Multilingual BERT | Thai | 5 | 0.43 |
| Multilingual BERT | Thai-English | 5 | 0.43 |
| Multilingual BERT | Thai-Chinese | 5 | 0.48 |
| Multilingual BERT | Thai-English-Chinese | 5 | 0.49 |
| Multilingual BERT | Thai-English-Chinese | 10 | 0.71 |
| Multilingual BERT | Thai-English-Chinese | 15 | 0.74 |

### How did it go? + Interpret results (which one is the best with explaination; read the table to reinforce the result)

## Conclusion
### What did we do?
### What task?
### Summary of result
### Literally re-phrasing your work