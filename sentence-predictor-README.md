Probabilistic Word Prediction & Phonetic Spell Checker (Jupyter Notebook)

This notebook implements a combined N-gram language model and phonetic
spell checker using NLTK. It corrects words in an input sentence and
then predicts the most likely next word based on 1–4 gram statistics.
This prediction model loops until the next suggested token is a noun
or punctuation mark.

Features

-   Trains 1–4 gram models on Brown + Reuters corpora
-   Interpolated probabilities with configurable lambda weights
-   Prefix-sum precomputation for fast conditional probability lookup
-   Phonetic spell checking via CMU Pronouncing Dictionary
-   Reverse-lookup for homophones / similar pronunciations
-   Context-aware correction using both past and future tokens
-   Next-word prediction loop that stops at nouns or punctuation

Notebook Workflow

1.  Load Corpora – fuse Brown + Reuters; create filtered and unfiltered
    versions
2.  Build N-gram Counts – unigram to 4-gram frequency tables
3.  Precompute – prefix denominators + total count masses
4.  Phonetic Lookup – build pronunciation dictionary + reverse map
5.  Contextual Spell Correction
    -   Generate phonetic candidates
    -   Score with past + future N-gram probabilities
6.  Next-Word Prediction
    -   Use the N-gram model to propose the most likely continuation

Example

Input:

    i think there good at

Output (approximate):

    i think they're good at that

Running the Notebook

1.  Download sentence-predictor.ipynb and go to Google Colabs (colab.research.google.com)
2.  Upload the file to Google Colab.
3.  Run all cells sequentially.

Configuration

Key parameters appear at the top of the notebook:

    LAMBDA = [0.05, 0.15, 0.3, 0.5]
    SMOOTH = 1e-8
    MAX_NGRAM = len(LAMBDA)

Notes

-   CMUdict does not include slang or proper nouns
-   Short contexts (1–2 words) produce weaker predictions
-   Future improvements: caching, hybrid corpus weighting, POS-aware
    word generation
