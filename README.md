# Cross-lingual-NLI-for-Thai

## Introduction
### Motivation
### A short Literature Review
### Idea Summarization
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
| Model | Train Language | Test Language | F1 Score |
|-------|----------------|---------------|----------|
| WangchanBERTa| Thai | Thai | |
| Multilingual BERT | Thai | Thai | |
| Multilingual BERT | | Thai | |

### How did it go? + Interpret results (which one is the best with explaination; read the table to reinforce the result)

## Conclusion
### What did we do?
### What task?
### Summary of result
### Literally re-phrasing your work