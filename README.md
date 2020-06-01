#COVID-19 literature: Topic modeling with scispaCy and LDA 

## What this article covers:

1) Read files and extract text 

2) Text preprocessing 

3) Topic modeling 

4) Topic visualization 



## Read and filter articles:

**Load files:**

The data, which was in Json formate, was downloaded from Kaggle. All research articles were loaded into jupyter notebook using 'glob' module in Python. It was  used to retrieve files/pathnames matching a specified pattern. From the articles 'paper id', 'title', 'abstract' and 'full text' were extracted and made into a data frame. 

**Filter articles:**

Once data frame was ready COVID-19 related articles were filtered by a condition that either title or full text of the article containing "corona/covid-19/novel corona/SARS-CoV-2".

Articles were in a mix of different languages and the aim was to make sure to get articles that are in English. Using spaCy's  language detector module, spacy-langdetect, we can filter articles that are "en" (English). 

## Text preprocessing using scispaCy

**What is scispaCy?**

Python library offers pretrained models for biomedical/scientific text processing, which heavily leverages the spaCy library. A pretrained model "en_core_sci_lg" which is a spaCy pipeline for scientific text with a larger vocabularym was used. Check the link(https://allenai.github.io/scispacy/) for more details.

**Corpus is preprocessed for:**

Remove stop words and punctuations.

**Tokenization:**  split corpus into individual tokens(words).

**Lammetization: ** convert words to it's base form.

**Named entity recognition:**  Involves identification, chunking and extraction of named entities from the unstructured text. spaCy can recognize real world objects like persons or companies, in this case COVID or infection. 

**Visualize words**

Word Cloud is one of the data visualization techniques used to represent text. In each graphical representation, size of the word indicates its frequency of occurence or importance.

**Custom stop words:**

Custom stop words can be made by appending unrelated words that appear in WordCloud to stop words.

## Topic modeling with LDA

**What is LDA?** 

LDA stands for Latent Dirichlet Allocation. Latent because topic structure is hidden and Dirichlet is a type of probability distribution. LDA assumes that each document is a distribution of topics and each topic is further a distribution of words. 

**Make corpus usable to LDA** 

LDA takes two types of input, 1)  a dictionary that has mapping of word IDs to words and,  2) Bag of words for each document in the corpus. Using Gensim LDA model, let's create a dictionary and bag of words from the corpus. 

**Base model**

A base model was first run with number of topics 5, corpus is BoW and id2word is dictionary created using gensim. 

**Evaluate model**

Every word in the corpus can exist in each topic but with different probability. The words with high probability in each topic were most likely to move together. These high probability words in each topic are nothing but top 10 or 15 words which was used to interpret the topic. Coherence was applied to these top  words from each topic and it is the relative distance between the top words in each topic.

Coherence score 0.4 is low, so the model was further improved by fine tuning the hyper parameters.

**Hyperparameter tuning**

LDA model hyperparameters num_topics, 𝛼, and 𝜷 (in gensim eta) impact model coherene score. 

Number of topics of 8 gave highest coherence score and alpha is 'symmetric'.

By keeping the number of topics 8 and changing alpha values, a value at 0.15 or symmetric gave the better coherence value 0.56.

**Run model with updated values** 

Number of topics = 8

alpha = 0.15

## Visualize topics

Although the topic modeling was evaluated using coherence score, the objective is to verify how effectively topics have been segregated. This can be achieved  with domain expertise to rank topics that provides  a comparison of topic quality from a human perspective.

There are tools to visualize toipcs:

1) WordCloud

2) pyLDAvis

3) t-SNE etc.

In this project  pyLDAvis is used to  visualizes topics.

## Scope of the project

This can be used to retrieve COVID information the literature.













