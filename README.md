# SkimLit

## Overview
SkimLit is an NLP-based project which aims to make medical abstracts easier to read. Harnessing the power of machine learning and deep learning models with transfer learning, to break down the medical abstracts into sub-sections namely: Objective, Methods, Results, and Conclusion. This makes it easier for the user to read the medical abstracts.

## Dataset
The dataset has been sourced from (https://github.com/Franck-Dernoncourt/pubmed-rct). From the repository, **PubMed_20k_RCT_numbers_replaced_with_at_sign**, is the dataset which has been used for this project. The dataset has been pre-processed and created functions to add labels to our dataset, in order to classify the part of the abstract as Objective, Methods, Results or Conclusion.

## Modelling Experiments
Once the dataset has been pre-processed and class labels have been created, the dataset is fit to various models.

**Note**: For all of the deep learning models, the following pattern has been followed:

    Input (text) -> Tokenize -> Embedding -> Layers -> Output (label probability)


### Multinomial Naive Bayes
Baseline model to begin the modelling experiments with. To build it, a Scikit-Learn Pipeline has been created which uses the TfidfVectorizer class to convert the abstract sentences to numbers using the TF-IDF (term frequency-inverse document frequecy) algorithm and then learns to classify the sentences using the MultinomialNB aglorithm.


### Conv1D with token embeddings
Building a one-dimensional Convolutional Neural Network with Global Average Pooling for the data, and used custom token embeddings for the dataset, these embeddings will be fit to the Conv1D model. 

### Feature extraction with pretrained token embeddings
Leveraging the power of transfer learning by using Universal Sentence Encoder, a pre-trained embedding, to create better representations of the abstracts, thus making it eaiser for the model to understand the patterns in the data.

### Conv1D with character embeddings
Repeating the same process as Conv1D with token embeddings, except this time, using a customized character-level embeddings instead of token-level, to experiment if the same model can understand the character-level embeddings better than the token-level embeddings.

### Combining pretrained token embeddings + character embeddings (hybrid embedding layer)
This hybrid token embedding layer is a combination of token embeddings and character embeddings. In other words, they create a stacked embedding to represent sequences before passing them to the sequence label prediction layer.

### Transfer Learning with pretrained token embeddings + character embeddings + positional embeddings
Along with the above hybrid embeddings, further creating positional embeddings which allows to keep track of line numbers in the abstract and the total number of lines for each of the sub-section (or classes). This tribrid embeddings can boost the performance of an already well-performing model.

## Model Evaluation
Once the modelling experiments have been performed, they are compared using the following classification metrics to see how good one model is against others.
1. Accuracy
2. Precision
3. Recall
4. F1-Score

After the comparitive analysis, the tribrid embedding is found to be best suited for the dataset.
