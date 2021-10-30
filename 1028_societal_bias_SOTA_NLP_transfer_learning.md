# Analysis of Societal Bias in State of the Art NLP Transfer Learning

## Bias
* Types of Bias
    * Data Bias
    * Interpretation Bias

## Harm
* Impact of bias

## Bias in Corpora
* BookCorpus - used by BERT et al
    * sentences extracted from books
    * skewed religious representation (Christianity)
    * Skewed genres - towards romance and fantasy
    * Potential for harmful gender stereotypes
* CC-NEWS - BERT et al
    * News articles from news sites worldwide, 2017-2019
    * Potential political skew
    * Potential harmful racial stereotypes
    * Potential harmful socio economic stereotypes
* C4 - cleaned up Common Crawl - T5, Pegasus
    * Bad words removed
    * lacking minority ethnic english
    * potential for harmful racial stereotypes
* Wikipedia: BERT, GPT-n
    * eacg document contains content of one full Wikipedia article with markdown and unwanted sections (e.g. references) stripped
    * inherent gender inequalities - *Ms.Categorized: Gender, notability and inequality on Wikipedia*    

## Addressing Bias
* Discussed pre-trianed models designed to be fine-tuned (e.g. BERT)
* Pre-training approaches
    * Data Augmentations: identify points where a pre-definied set of gendered wodard used, and switch them for counterpart (he to she worked as a doctor)
    * Bias-Aware Objective Function: introduce an additional component to model loss that is defined as the variance in the model's output when its input is augmented with counterfactual gendered words. Dual objective - train classifier, and minimise difference between he/she outputs
    * BUT these methods are very computationally expensive    
* Extracting gender bias from the embeddings - manipulating embeddings post training
    * research that projected gendered words into subspace via PCA, then applied transforms non-gendered words are equidistant from gender ends
    * concentrate gender elements in specific part of embedding, which is then removed
    * BUT shown to only remove certain elements of gender bias
* **Iterative Nullspace Projection**
    * Create gendered subspace (PCA)
    * Identify bias-sensitive words
    * Train a classifier to identify gender from embedding (e.g. captian > he, tanning > she)
        * weights of classifier capture gendered elements of embedding
        * obtain nullspace of classifier weights so that classifier cannot predict gender of word
        * Define liniear guarding function: then Null Space dot embedding = de-gendered embedding
        * DEMO: nullspace_bert_demonstration.ipynb: github.com/BenAjayiObe/pydata-bias-in-bert


