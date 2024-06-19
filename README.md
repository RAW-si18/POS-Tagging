## Parts-of-Speech Tagging (POS)

### Introduction

Parts-of-speech tagging (POS tagging) is the process of assigning a part-of-speech tag (Noun, Verb, Adjective, etc.) to each word in a text corpus. This task is crucial for natural language processing tasks as it helps in understanding the grammatical structure of sentences and is fundamental in applications like speech recognition and machine translation.

### Data Sources

The dataset used for training and testing the POS tagger is the Wall Street Journal (WSJ). Two files are utilized:
- **WSJ-2_21.pos**: Used for training, it contains tagged sentences which help in building the transition and emission matrices.
- **WSJ-24.pos**: Used for testing, it contains untagged sentences where POS tags are predicted and compared against the true tags.

Additionally:
- **hmm_vocab.txt**: Vocabulary derived from the training set containing words that occur two or more times.
- **test_words.txt**: Preprocessed version of WSJ-24.pos containing only the words for testing.

### Implementation Overview

#### Training

1. **Transition Matrix (A)**
   - Counts transitions between POS tags (`transition_counts` dictionary).
   - Computes probabilities of transitioning from one tag to another.

2. **Emission Matrix (B)**
   - Counts emissions of words given POS tags (`emission_counts` dictionary).
   - Computes probabilities of a word being emitted by a POS tag.

3. **Tag Counts**
   - Counts occurrences of each POS tag (`tag_counts` dictionary).

#### Testing

- **Accuracy Calculation**: Evaluates how well the POS tagger performs using the `emission_counts` dictionary on the test set (`WSJ-24.pos`).

#### Predicting POS Tags

- **Predict_pos**: Simple model that assigns the most frequent POS tag for each word in the test set.

### Hidden Markov Models (HMM) for POS

1. **Transition Matrix (A)**
   - Represents probabilities of transitioning between POS tags.
   - Uses smoothing to handle unseen transitions.

2. **Emission Matrix (B)**
   - Represents probabilities of words being emitted from POS tags.
   - Uses smoothing to handle unseen emissions.

### Viterbi Algorithm and Dynamic Programming

1. **Initialization**
   - Initializes matrices (`best_probs` and `best_paths`) to store probabilities and paths.
   - Starts with the assumption that the first word is preceded by a start token.

2. **Viterbi Forward Algorithm (`viterbi_forward`)**:
   - Computes the most probable sequence of POS tags using dynamic programming.
   - Updates `best_probs` and `best_paths` based on transition and emission probabilities.

3. **Viterbi Backward Algorithm (`viterbi_backward`)**:
   - Predicts POS tags for each word by tracing back through `best_paths` and `best_probs`.
   - Identifies the most likely POS tag sequence for the entire corpus.

### Example and Debugging

- Prints the predicted POS tags for the last few words of the corpus during the testing phase.
- Helps in understanding and verifying the correctness of the predicted POS tags.

This README provides an overview of Parts-of-Speech Tagging, the dataset used, implementation details including HMM for POS tagging, and the Viterbi algorithm for sequence prediction. It serves as a guide to understanding and implementing a POS tagger using Python and natural language processing techniques.