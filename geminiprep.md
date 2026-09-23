# Comprehensive NLP Mid-Semester Study & Exam Preparation Guide
**Course:** Natural Language Processing (`20IC403T`)  
**Target Syllabus:** **Unit 1** (Introduction & Pre-processing) & **Unit 2** (Vectorization & $N$-gram Language Models)  
**Format:** 25 Marks | 60 Minutes | Focus: **Numericals, Analyticals, Logicals, and Justifications**

---

# Table of Contents
1. [Exam Blueprint & Strategic Breakdown](#part-1-exam-blueprint--high-yield-strategy)
2. [Unit 1: Theory, Definitions & Core Concepts](#part-2-unit-1--text-preprocessing--speech-foundations)
3. [Unit 2: Theory, Formulas & Analytical Justifications](#part-3-unit-2--vectorization--n-gram-language-models)
4. [Master Numerical Lab: Step-by-Step Solved Templates](#part-4-master-numerical-lab-all-slide--exam-problems)
   - [Numerical 1: Byte Pair Encoding (BPE) Iterative Training & OOV Handling](#numerical-1-byte-pair-encoding-bpe-algorithm)
   - [Numerical 2: Co-Occurrence Matrix, Cosine Similarity & PPMI](#numerical-2-co-occurrence-matrix-cosine-similarity--ppmi)
   - [Numerical 3: TF-IDF with Sklearn Smoothing & $L_2$ Normalization](#numerical-3-tf-idf-vectorization-with-sklearn-smoothing--l_2-normalization)
   - [Numerical 4: $N$-gram MLE & Perplexity (Bigram vs. Trigram)](#numerical-4-n-gram-mle-probability-and-perplexity-bigram-vs-trigram)
   - [Numerical 5: Laplace (Add-1) & Add-$m$ (Lidstone) Smoothed Perplexity](#numerical-5-laplace-add-1-and-add-m-smoothed-probability--perplexity)
   - [Numerical 6: Argmax Probability Sequence Decoding](#numerical-6-argmax-computation-for-a-bigram-sequence)
5. [Slide Justifications & "Why" Questions](#part-5-slide-justifications--why-questions)
6. [Past Year Papers (PYQ) Fully Solved: 2024 & 2025](#part-6-previous-year-question-pyq-solutions-2024--2025)
7. [Predicted 25-Mark Mock Exams with Full Answer Keys](#part-7-predicted-25-mark-mock-exams)

---

# Part 1: Exam Blueprint & High-Yield Strategy

### 1. Structure of the 25-Mark Exam
The 2025 exam allocates 25 marks across 60 minutes:
- **Section A: Definitions / Short Technical Distinctions (5 to 10 Marks):** Core terminology (Tokenization, Stemming vs. Lemmatization, Morphemes, Articulation, Computational Grammar).
- **Section B: Core Numerical / Algorithm Execution (8 to 10 Marks):** Manual execution of BPE merges, TF-IDF calculation with $L_2$ normalization, PPMI matrix, or Bigram/Trigram Perplexity with Smoothing.
- **Section C: Analytical Comparisons / Justifications (5 to 7 Marks):** Logical proofs (e.g., why $\sum P_{\text{Laplace}} = 1$), data attribute classifications, or speech vs. text boundary detection challenges.

### 2. Topic Priority Heatmap
| Priority | Topic | Question Style | Weightage |
| :--- | :--- | :--- | :--- |
| **CRITICAL** | $N$-gram MLE, Perplexity ($PP$), Cross-Entropy ($H$) | Complete Numerical / Comparison | 5–8 Marks |
| **CRITICAL** | Smoothing: Laplace Add-1 & Add-$m$ Lidstone | Formula Derivation & Numerical | 4–6 Marks |
| **CRITICAL** | Subword Tokenization: Byte Pair Encoding (BPE) | Step-by-step Merge Table & OOV | 5–8 Marks |
| **HIGH** | TF-IDF (Sklearn formula + $L_2$ Normalization) | Full Numerical Computation | 5 Marks |
| **HIGH** | PPMI & Co-occurrence Cosine Similarity | Matrix Construction & Log Math | 4–6 Marks |
| **HIGH** | Stemming vs. Morphological Analysis vs. Lemmatization | Comparative Definitions & Examples | 2–5 Marks |
| **MEDIUM** | Word Boundary Detection (Speech vs. Text) | Analytical / Challenge Discussion | 5–10 Marks |
| **MEDIUM** | HMM Architecture in ASR | Diagram & Workflow Explanation | 5–10 Marks |
| **MEDIUM** | Place & Manner of Articulation | Phonetic Classification | 2–5 Marks |

---

# Part 2: Unit 1 — Text Preprocessing & Speech Foundations

```
Raw Text Data (Unstructured, Noisy)
       │
       ▼
 [ Tokenization ] ──► (Whitespace / Word / Subword: BPE, WordPiece)
       │
       ▼
[ Normalization ] ──► (Casing, Stop Word Removal, Stemming / Lemmatization)
       │
       ▼
 [ Enrichment ]   ──► (POS Tagging: Penn Treebank; NER; Dependency Parsing)
       │
       ▼
[ Representation] ──► (Discrete: One-Hot, BoW, TF-IDF | Distributed: Word2Vec, Dense Embeddings)
       │
       ▼
[ Downstream LM ] ──► (N-gram Models, Neural Networks, Transformers)
```

---

### 1. NLP Pipeline Components & Downstream Roles
An NLP pipeline converts raw, unstructured human language into structured numerical representations for machine inference:
1. **Preprocessing / Normalization:** Cleans noise (typos, casing, special symbols), segments strings into atomic linguistic units (tokens), and normalizes surface variants (stemming/lemmatization).
2. **Feature Representation / Vectorization:** Maps symbolic tokens into mathematical objects (sparse vectors via One-Hot/BoW/TF-IDF, or dense vectors via Word2Vec/GloVe/Embeddings).
3. **Inference / Modeling:** Employs statistical algorithms (HMMs, $N$-grams) or neural models (RNNs, Transformers) to execute target objectives (Classification, Sequence Labeling, Generation).
4. **Evaluation:** Validates system output via intrinsic metrics (Perplexity, Cross-Entropy) or extrinsic benchmarks (F1-score, BLEU, Word Error Rate).

---

### 2. Tokenization Paridigms & Comparison
* **Token:** An individual instance of a linguistic type occurring in a specific text.
* **Type:** A unique vocabulary entry ($V$).
* **Heaps’ Law (Herdan’s Law):** Models vocabulary growth relative to corpus size:
  $$|V| = k \cdot N^\beta \quad (\text{typically } 0.67 < \beta < 0.75)$$
  *Takeaway:* Vocabulary grows indefinitely with larger corpora; it does not saturate cleanly.

#### Tokenization Paradigms
| Paradigm | Mechanism | Advantages | Critical Weaknesses |
| :--- | :--- | :--- | :--- |
| **Whitespace Tokenizer** | Splits strictly on spaces, tabs, and newlines (`\s+`). | Simple, computationally negligible. | Fails on contractions (`isn't`), hyphenated compounds (`state-of-the-art`), punctuation attachments (`hello,`), and unspaced scripts (Chinese/Japanese). |
| **Rule-Based Word Tokenizer** (e.g., NLTK `word_tokenize`, spaCy) | Uses regular expressions, language heuristics, and abbreviation lists. | Separates punctuation cleanly; handles contractions (`don't` $\to$ `do`, `n't`). | Struggles with domain-specific neologisms; produces large vocabularies with frequent Out-Of-Vocabulary (OOV) tokens. |
| **Subword Tokenizer** (BPE, WordPiece, SentencePiece) | Data-driven statistical sub-unit segmentation. Starts with base characters and iteratively merges frequent adjacent pairs. | **Solves OOV entirely**; models unseen words via morphological subcomponents (`un`+`read`+`able`). | More complex preprocessing; variable token lengths across words. |

---

### 3. Stemming vs. Lemmatization vs. Morphological Analysis
* **Morpheme:** The smallest meaning-bearing unit of language (e.g., *cats* = *cat* [root] + *-s* [plural morpheme]; *unlikeliest* = *un-* [prefix] + *likely* [root] + *-est* [superlative suffix]).
* **Morphology:** The study of how words are constructed from morphemes.

```
                  ┌─────────────── Word: "changing" ───────────────┐
                  │                                                │
         [ Stemming (Heuristic) ]                      [ Lemmatization (Linguistic) ]
                  │                                                │
       Cuts inflectional suffix "-ing"                 Looks up lemma given POS=Verb
                  │                                                │
                  ▼                                                ▼
            Root: "chang"                                    Lemma: "change"
        (Non-dictionary string)                           (Valid dictionary entry)
```

#### Detailed Comparison Table
| Dimension | Stemming | Lemmatization | Morphological Analysis |
| :--- | :--- | :--- | :--- |
| **Definition** | Heuristic, rule-based chopping of prefixes/suffixes to find a base stem. | Context-aware transformation to canonical base form (*lemma*) using vocab and grammar rules. | Full grammatical breakdown into constituent morphemes (root, prefixes, suffixes, inflections). |
| **Linguistic Knowledge** | **None.** Operates on surface string patterns (e.g., Porter, Snowball). | **High.** Requires vocabulary dictionaries and Part-Of-Speech (POS) awareness. | **Highest.** Involves syntactic, morphological, and structural rules of the language. |
| **Validity of Output** | Frequently results in non-real words (e.g., *university* $\to$ `univers`, *organization* $\to$ `organ`). | Always yields a valid lexical entry (e.g., *better* $\to$ `good`, *was* $\to$ `be`). | Produces structured root + grammatical feature tuples. |
| **Example** | `running` $\to$ `run`<br>`flies` $\to$ `fli`<br>`leaves` $\to$ `leav` | `running` (verb) $\to$ `run`<br>`flies` (noun) $\to$ `fly`<br>`leaves` (noun) $\to$ `leaf` | `unbelievable` $\to$ `un-` [prefix] + `believe` [stem] + `-able` [suffix] |

---

### 4. Stop Word Removal, Casing & Irreversibility
* **Stop Words:** High-frequency, functional, closed-class words (*the, is, at, which, on*) that carry minimal distinctive topical information.
  - *When to remove:* Document classification, TF-IDF vectorization, Information Retrieval (boosts efficiency and removes noise).
  - *When to retain:* Machine Translation, Language Modeling, Sentiment Analysis (where `not`, `nor` flip meaning completely).
* **Casing:** Converting text to uniform lowercase. Simplifies vocabulary cardinality, but destroys distinct proper nouns (e.g., *US* [nation] vs. *us* [pronoun]; *Apple* [company] vs. *apple* [fruit]).
* **Tokenizer Irreversibility:** Because text preprocessing discards capitalization, whitespace boundaries, punctuation markers, and inflections, the transformed output cannot be inverted back to the exact pristine input.

---

### 5. Part-of-Speech (POS) Tagging & Named Entity Recognition (NER)
* **POS Tagging:** The algorithmic assignment of grammatical categories (noun, verb, adjective, adverb, preposition) to each token based on lexical definition and contextual syntax.
  - *Penn Treebank Tagset:* Standard 36-tag system. Common tags:
    - `NN`: Noun, singular/mass (*table*) | `NNS`: Noun, plural (*tables*)
    - `NNP`: Proper noun, singular (*Google*, *London*) | `NNPS`: Proper noun, plural (*Americans*)
    - `VB`: Verb, base form (*eat*) | `VBZ`: Verb, 3rd person singular present (*eats*)
    - `VBG`: Verb, gerund/present participle (*eating*) | `VBD`: Verb, past tense (*ate*)
    - `JJ`: Adjective (*large*) | `JJR`: Comparative (*larger*) | `JJS`: Superlative (*largest*)
    - `RB`: Adverb (*quickly*) | `IN`: Preposition / subordinating conjunction (*in*, *of*)
    - `DT`: Determiner (*the*, *a*) | `CD`: Cardinal number (*one*, *$1 billion*)
  - *Ambiguity Challenge:* The identical surface token functions under distinct tags across contexts:
    - *"Book that flight"* $\to$ `Book` is **Verb** (`VB`).
    - *"Hand me that book"* $\to$ `book` is **Noun** (`NN`).
  - *Methods:* Hidden Markov Models (HMM), Maximum Entropy Markov Models (MEMMs), Conditional Random Fields (CRFs), and Transformer Encoders (BERT). Evaluated via **Token Accuracy** and **Macro-F1**.

* **Named Entity Recognition (NER):** Detection and classification of rigid designators / proper nouns in text into predefined semantic categories:
  - `PERSON` (*Marie Curie*), `ORGANIZATION` (*Google*, *Stanford University*), `GPE`/`LOCATION` (*New York City*, *U.K.*), `MONEY` (*$1 billion*), `DATE`/`TIME` (*March 11, 1983*), `PERCENT` (*95%*).
  - *Key Structural Difference:* Unlike POS tagging (which typically evaluates single tokens), NER spans multiple consecutive tokens (*multi-word entities* like `New York University`).

---

### 6. Speech Processing Foundations (PYQ Essentials)
* **Place of Articulation:** The physical, anatomical location within the vocal tract where the primary airflow obstruction or constriction occurs:
  1. *Bilabial:* Both lips pressed together ($/p/$, $/b/$, $/m/$, $/w/$).
  2. *Labiodental:* Lower lip against upper incisors ($/f/$, $/v/$).
  3. *Dental / Interdental:* Tongue tip touching upper front teeth ($/\theta/$ as in *think*, $/ð/$ as in *this*).
  4. *Alveolar:* Tongue tip against the alveolar ridge behind upper front teeth ($/t/$, $/d/$, $/s/$, $/z/$, $/n/$, $/l/$).
  5. *Post-Alveolar / Palato-Alveolar:* Tongue blade right behind the alveolar ridge ($/\int/$ as in *ship*, $/3/$ as in *measure*).
  6. *Palatal:* Tongue body against hard palate ($/j/$ as in *yes*).
  7. *Velar:* Tongue dorsum against soft palate/velum ($/k/$, $/g/$, $/ŋ/$ as in *sing*).
  8. *Glottal:* At the vocal folds / glottis ($/h/$, glottal stop $/ʔ/$).
* **Manner of Articulation:** The physical method by which the airflow is constricted, routed, or released:
  1. *Stops / Plosives:* Complete closure blocking airflow, followed by abrupt burst release ($/p/, /b/, /t/, /d/, /k/, /g/$).
  2. *Fricatives:* Narrow constriction generating sustained friction/turbulent noise ($/f/, /v/, /s/, /z/, /\theta/, /h/$).
  3. *Affricates:* Stop closure immediately transitioning into a fricative release ($/t\int/$ as in *church*, $/d3/$ as in *judge*).
  4. *Nasals:* Complete oral closure with lowered velum, routing airflow through the nasal cavity ($/m/, /n/, /ŋ/$).
  5. *Approximants / Liquids / Glides:* Articulators approach each other without creating turbulent noise ($/l/, /r/, /w/, /j/$).

* **Hidden Markov Models (HMM) in Automatic Speech Recognition (ASR):**
  - Continuous speech sounds vary dynamically over time. An HMM models speech as a doubly stochastic process:
    1. *Hidden State Sequence ($Q$):* True linguistic acoustic states (phonemes, sub-phonetic triphones). Transitions governed by state transition matrix $A = \{a_{ij} = P(q_t=j \mid q_{t-1}=i)\}$.
    2. *Observable Acoustic Observations ($O$):* Sequence of continuous acoustic feature vectors (MFCCs – Mel-Frequency Cepstral Coefficients) extracted across 25ms overlapping audio windows. Emission probabilities $B = \{b_j(o_t) = P(o_t \mid q_t=j)\}$, typically parameterized via Gaussian Mixture Models (GMM) or Deep Neural Networks (DNN).
  - *Decoding Equation (Bayes' Inversion):*
    $$\hat{W} = \arg\max_W P(W \mid O) = \arg\max_W \frac{P(O \mid W) P(W)}{P(O)} = \arg\max_W \underbrace{P(O \mid W)}_{\text{Acoustic Model (HMM)}} \cdot \underbrace{P(W)}_{\text{Language Model ($N$-gram)}}$$
    The optimal word sequence is decoded in real time using the **Viterbi Algorithm**.

```
                HMM Speech Recognition Architecture
                ───────────────────────────────────
 Acoustic Signal (Waveform)
       │
       ▼
 [ Feature Extraction ] ──► Acoustic Observations O = (o₁, o₂, ..., o_T) [MFCCs]
       │
       ▼
 [ Viterbi Decoder ]   ◄──  Acoustic Model P(O|W) [HMM states / phone transitions]
       ▲               ◄──  Language Model P(W)   [N-gram / syntax grammar]
       │
       ▼
 Best Decoded Word Sequence: Ŵ = argmax [ P(O|W) · P(W) ]
```

* **Word Boundary Detection Challenges (Speech vs. Text):**
  - *In Text:* Many scripts (Chinese, Japanese, Thai, Lao) have no explicit delimiter spaces between words. Compound nouns in German (*Donaudampfschiffahrt*) glue roots into unbroken character streams.
  - *In Speech:* The acoustic signal is continuous; talkers **do not insert silence** between words. Acoustic phenomena create heavy ambiguity:
    - *Co-articulation:* The vocal tract moves continuously, altering phone acoustics based on neighboring sounds (*"did you"* sounds like *"did-jew"*).
    - *Phonetic Ambiguity:* Identical acoustic frames correspond to wildly different segmentations (*"ice cream"* vs. *"I scream"*; *"recognize speech"* vs. *"wreck a nice beach"*).
  - *Remedies:* Subword statistical models, HMM-guided lattice decoding with high-order $N$-gram language models to resolve syntax likelihoods.

---

### 7. Data Attributes & Dataset Structures (PYQ Essentials)
* **Measurement Scales for Attributes:**
  1. *Nominal Data:* Categorical labels lacking any intrinsic mathematical ordering or ranking. Operations: Equality ($=, \neq$).  
     *Examples:* POS tags (`NN`, `VB`), Vocabulary words, Document language labels (`English`, `Hindi`).
  2. *Ordinal Data:* Categorical labels possessing an unambiguous, natural ranking/order, but intervals between consecutive steps are arbitrary and non-quantifiable. Operations: Ordering ($<, >$).  
     *Examples:* Sentiment star ratings (`1-star < 2-star < 3-star`), review polarity (`Negative < Neutral < Positive`).
  3. *Interval-Scaled Data:* Continuous numeric values where intervals/differences are meaningful and equal, but **there is no true absolute zero**. Operations: Addition and subtraction ($+, -$).  
     *Examples:* Temperature in Celsius/Fahrenheit, publication calendar year.
  4. *Ratio-Scaled Data:* Continuous numeric values with equal intervals and an **absolute, non-arbitrary zero point** representing complete absence of the property. Operations: Multiplication and division ($\times, \div$).  
     *Examples:* Word token frequency counts, document lengths in characters, audio frame duration in milliseconds.

* **Text Classification vs. Machine Translation Datasets:**
  | Dimension | Text Classification Datasets | Machine Translation Datasets |
  | :--- | :--- | :--- |
  | **Corpus Structure** | Monolingual text collection mapped to categorical targets. | Parallel, sentence-aligned bilingual/multilingual bitext ($S \leftrightarrow T$). |
  | **Input $\to$ Output** | Variable-length sequence input $\to$ Single discrete scalar label / class. | Sequence input in Source Language $\to$ Equivalent sequence generation in Target Language. |
  | **Attributes** | Text string, Document ID, Class label ($y \in \{C_1, \dots, C_k\}$). | Source string ($S$), Target translation string ($T$), Alignment vectors. |
  | **Evaluation Goal** | Accuracy, Macro-F1, Precision, Recall. | BLEU, METEOR, ROUGE, TER. |

---

# Part 3: Unit 2 — Vectorization & $N$-gram Language Models

```
                          Text Vectorization Hierarchy
                          ────────────────────────────
                                       │
            ┌──────────────────────────┴──────────────────────────┐
            ▼                                                     ▼
 [ Discrete Representations ]                           [ Distributed Embeddings ]
  - High-dimensional, sparse                             - Low-dimensional, dense
  - Orthogonal (no semantic similarity)                  - Continuous vector spaces
  - Suffer from curse of dimensionality                 - Encodes semantic context
            │                                                     │
    ├─ One-Hot Encoding                                   ├─ Word2Vec (Skip-Gram, CBOW)
    ├─ Bag of Words (BoW)                                 ├─ GloVe
    ├─ TF-IDF (Term-Doc Weights)                          └─ FastText
    └─ Co-occurrence Matrix + PPMI
```

---

### 1. Vectorization Paradigms: Discrete vs. Distributed
* **The Fundamental Flaw of Discrete Models (One-Hot & BoW):**
  - Given a vocabulary of size $|V|$, each word is assigned a vector of length $|V|$ containing a single `1` and zeros elsewhere.
  - *Orthogonality:* The dot product between any two distinct one-hot vectors is identically zero:
    $$\mathbf{v}_{\text{cat}} \cdot \mathbf{v}_{\text{dog}} = 0 \implies \text{Cosine Similarity} = 0$$
  - Discrete representations have **no inherent notion of semantic distance or similarity**.
  - *Dimensionality:* Massive storage requirements and extreme matrix sparsity.
* **Distributed Word Representations (Embeddings):**
  - Built upon the **Distributional Hypothesis** (Firth, 1957): *"You shall know a word by the company it keeps."*
  - Projects words into a low-dimensional, dense continuous vector space ($\mathbb{R}^d$, typically $d \in [100, 300]$).
  - Words sharing overlapping linguistic contexts share directional alignment in vector space.

---

### 2. $N$-gram Language Modeling Formulation
* **Objective:** Compute the joint probability of a sequence of words $W = (w_1, w_2, \dots, w_n)$:
  $$P(W) = P(w_1, w_2, \dots, w_n)$$
  Or compute the conditional probability of an upcoming token:
  $$P(w_n \mid w_1, w_2, \dots, w_{n-1})$$

#### The Chain Rule of Probability
Without approximations, joint sentence probability factors into a cascade of conditional probabilities:
$$P(w_1, w_2, \dots, w_n) = \prod_{k=1}^n P(w_k \mid w_1, w_2, \dots, w_{k-1}) = P(w_1)P(w_2 \mid w_1)P(w_3 \mid w_1, w_2)\dots$$
*The Conditioning History Problem:* Long conditioning histories ($w_1, \dots, w_{k-1}$) cannot be calculated directly from corpora because identical long sequences rarely repeat in finite training data.

#### The Markov Approximation
To resolve this, we assume the probability of the upcoming word depends only on the preceding $N-1$ words:
$$P(w_k \mid w_1, \dots, w_{k-1}) \approx P(w_k \mid w_{k-N+1}, \dots, w_{k-1})$$
- **Unigram ($N=1$):** Complete independence assumption.  
  $$P(W) \approx \prod_{k=1}^n P(w_k)$$
- **Bigram ($N=2$):** First-order Markov chain. Depends exclusively on the immediately preceding token.  
  $$P(W) \approx \prod_{k=1}^n P(w_k \mid w_{k-1})$$
- **Trigram ($N=3$):** Second-order Markov chain. Depends on the preceding two tokens.  
  $$P(W) \approx \prod_{k=1}^n P(w_k \mid w_{k-2}, w_{k-1})$$

#### Maximum Likelihood Estimation (MLE) Formulas
Probabilities are estimated directly via raw frequency counts:
$$\text{Unigram: } P_{\text{MLE}}(w_k) = \frac{C(w_k)}{N_{\text{total}}}$$
$$\text{Bigram: } P_{\text{MLE}}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k)}{C(w_{k-1})}$$
$$\text{Trigram: } P_{\text{MLE}}(w_k \mid w_{k-2}, w_{k-1}) = \frac{C(w_{k-2}, w_{k-1}, w_k)}{C(w_{k-2}, w_{k-1})}$$
$$\text{General } N\text{-gram: } P_{\text{MLE}}(w_k \mid w_{k-N+1:k-1}) = \frac{C(w_{k-N+1:k-1}, w_k)}{C(w_{k-N+1:k-1})}$$

---

### 3. Intrinsic Evaluation: Perplexity ($PP$) and Cross-Entropy ($H$)
* **Perplexity ($PP$):** The standard metric for measuring how well a probability model predicts an unseen test sample. It is defined as the inverse joint probability of the test set, normalized by sequence length $n$:
  $$PP(W) = P(w_1, w_2, \dots, w_n)^{-\frac{1}{n}} = \sqrt[n]{\frac{1}{\prod_{k=1}^n P(w_k \mid w_{k-N+1:k-1})}}$$

* **Log-Space Computation (Cross-Entropy Form):**  
  Multiplying raw probabilities leads to floating-point numerical underflow. We compute in $\log_2$ space:
  $$H(W) = -\frac{1}{n} \sum_{k=1}^n \log_2 P(w_k \mid w_{k-N+1:k-1}) \quad (\text{bits per word})$$
  $$PP(W) = 2^{H(W)}$$

#### Mathematical Interpretation: Effective Branching Factor
* Perplexity represents the **effective branching factor**: the size of an equivalent uniform pool of words from which the model would have to choose randomly at each step to match its current uncertainty.
  - *Uniform Uncertainty (Worst Case):* For vocabulary $|V|$, if $P(w) = \frac{1}{|V|}$ for all words:
    $$H = -\log_2 \left(\frac{1}{|V|}\right) = \log_2 |V| \implies PP = 2^{\log_2 |V|} = |V|$$
    Here, the effective branching factor is exactly $|V|$ (the model is completely uninformed).
  - *Skewed / Informed Distribution:* A well-trained model concentrates probability mass on likely candidates, lowering entropy ($H < \log_2 |V|$) and shrinking the effective branching factor ($PP \ll |V|$).

---

### 4. Smoothing Techniques (Handling Sparsity)

```
                       Probability Mass Redistribution
                       ───────────────────────────────
   Unsmoothed MLE:
   [ Observed Word Combinations: C > 0 ] ────► Holds 100% Probability Mass
   [ Unseen Word Combinations:   C = 0 ] ────► Holds 0% Mass (Causes Model Crash)

   Smoothed Models (Discounting):
   [ Observed N-grams ] ──(Deduct Mass)──► [ Reserved Mass Pool ] ──► [ Unseen Events ]
```

#### 1. Laplace (Add-1) Smoothing
Assumes every possible event in the vocabulary has been observed one extra virtual time:
$$P_{\text{Laplace}}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + |V|}$$

##### Formal Proof: Normalization to 1
$$\sum_{w_k \in V} P_{\text{Laplace}}(w_k \mid w_{k-1}) = \sum_{w_k \in V} \frac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + |V|} = \frac{\sum_{w_k} C(w_{k-1}, w_k) + \sum_{w_k} 1}{C(w_{k-1}) + |V|}$$
Since $\sum_{w_k} C(w_{k-1}, w_k) = C(w_{k-1})$ and $\sum_{w_k \in V} 1 = |V|$:
$$= \frac{C(w_{k-1}) + |V|}{C(w_{k-1}) + |V|} = 1 \quad \blacksquare$$

#### 2. Add-$m$ (Lidstone) Smoothing
Replaces the integer count `1` with a tuned fractional pseudo-count $m \in (0, 1)$ (e.g., $m = 0.05$ or $0.1$):
$$P_{\text{Add-}m}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + m}{C(w_{k-1}) + m|V|}$$
- *Limit Behavior:* As $m \to 0$, the formula converges to pure MLE. As $m \to 1$, it becomes standard Laplace smoothing.
- *Hyperparameter Selection:* $m$ is tuned on a held-out validation set to minimize validation perplexity.

#### 3. Linear Interpolation
Blends probability estimates across multiple model orders, ensuring lower-order information is always utilized:
$$\hat{P}(w_k \mid w_{k-2}, w_{k-1}) = \lambda_3 P_{\text{MLE}}(w_k \mid w_{k-2}, w_{k-1}) + \lambda_2 P_{\text{MLE}}(w_k \mid w_{k-1}) + \lambda_1 P_{\text{MLE}}(w_k)$$
$$\text{Subject to: } \sum_{j=1}^3 \lambda_j = 1 \quad \text{and} \quad \lambda_j \ge 0$$

#### 4. Katz Back-off
Uses the highest-order $N$-gram if observed; otherwise, falls back to lower-order models using discounted probability mass:
$$P_{\text{BO}}(w_k \mid w_{k-2}, w_{k-1}) = \begin{cases} 
P^*(w_k \mid w_{k-2}, w_{k-1}) = \frac{C(w_{k-2}, w_{k-1}, w_k) - d}{C(w_{k-2}, w_{k-1})} & \text{if } C(w_{k-2}, w_{k-1}, w_k) > 0 \\ 
\alpha(w_{k-2}, w_{k-1}) \cdot P_{\text{BO}}(w_k \mid w_{k-1}) & \text{if } C(w_{k-2}, w_{k-1}, w_k) = 0 
\end{cases}$$
Where $d \in (0, 1)$ is the absolute discount parameter, and $\alpha(w_{k-2}, w_{k-1})$ is the normalization back-off weight:
$$\alpha(w_{k-2}, w_{k-1}) = \frac{1 - \sum_{w: C(w_{k-2}, w_{k-1}, w) > 0} P^*(w \mid w_{k-2}, w_{k-1})}{\sum_{w: C(w_{k-2}, w_{k-1}, w) = 0} P_{\text{BO}}(w \mid w_{k-1})}$$

---

# Part 4: Master Numerical Lab (All Slide & Exam Problems)

---

### Numerical 1: Byte Pair Encoding (BPE) Algorithm
*(Source: Text Preprocessing PPT, Slides 18–21)*

#### Problem Setup
Given the training corpus table with word counts:
- `read`: 3
- `reads`: 2
- `reader`: 2
- `reading`: 2
- `unread`: 1
- `readers`: 1

**Task:**
1. Represent each word as character sequences terminated by the end-of-word marker `_`.
2. Determine the initial base character vocabulary.
3. Perform **exactly 6 BPE training merge steps**. Show counts for each adjacent pair at every step.  
   *Tie-breaker:* Select the leftmost pair from the root word `read` if applicable; otherwise choose alphabetically.
4. Tokenize the test words: `read`, `reader`, `readers`, `reading`, `unread`, `readable`, `reread`, `unreader`.
5. Show how the OOV word `readable` is handled and decoded.

---

#### Step-by-Step Solution

##### Step 1: Initial Character Representation with Frequencies
Append `_` to represent word boundaries:
- `r e a d _` : 3
- `r e a d s _` : 2
- `r e a d e r _` : 2
- `r e a d i n g _` : 2
- `u n r e a d _` : 1
- `r e a d e r s _` : 1

Total word instances = $3 + 2 + 2 + 2 + 1 + 1 = 11$.

##### Step 2: Initial Base Vocabulary
$$V_0 = \{ \_, \text{a}, \text{d}, \text{e}, \text{g}, \text{i}, \text{n}, \text{r}, \text{s}, \text{u} \}$$

##### Step 3: The 6 BPE Training Merges

* **Merge Iteration 1:**
  - Count adjacent pairs:
    - `(r, e)`: occurs in `read_` (3), `reads_` (2), `reader_` (2), `reading_` (2), `unread_` (1), `readers_` (1).  
      $\text{Count} = 3 + 2 + 2 + 2 + 1 + 1 = 11$.
    - `(e, a)`: occurs in all 6 words. $\text{Count} = 11$.
    - `(a, d)`: occurs in all 6 words. $\text{Count} = 11$.
  - *Tie-breaker rule:* Select the leftmost pair from `read`, which is `(r, e)`.
  - **New Token Created:** `re`
  - Corpus update: Replace `r e` with `re`.
    - `re a d _` : 3
    - `re a d s _` : 2
    - `re a d e r _` : 2
    - `re a d i n g _` : 2
    - `u n re a d _` : 1
    - `re a d e r s _` : 1

* **Merge Iteration 2:**
  - Count pairs:
    - `(re, a)`: $\text{Count} = 3 + 2 + 2 + 2 + 1 + 1 = 11$.
    - `(a, d)`: $\text{Count} = 11$.
  - *Tie-breaker:* Leftmost pair in `read` is `(re, a)`.
  - **New Token Created:** `rea`
  - Corpus update:
    - `rea d _` : 3
    - `rea d s _` : 2
    - `rea d e r _` : 2
    - `rea d i n g _` : 2
    - `u n rea d _` : 1
    - `rea d e r s _` : 1

* **Merge Iteration 3:**
  - Pair `(rea, d)` has frequency 11 (highest).
  - **New Token Created:** `read`
  - Corpus update:
    - `read _` : 3
    - `read s _` : 2
    - `read e r _` : 2
    - `read i n g _` : 2
    - `u n read _` : 1
    - `read e r s _` : 1

* **Merge Iteration 4:**
  - Count pairs:
    - `(read, _)`: occurs in `read _` (3) and `u n read _` (1). $\text{Count} = 4$.
    - `(read, e)`: occurs in `read e r _` (2) and `read e r s _` (1). $\text{Count} = 3$.
    - `(read, s)`: occurs in `read s _` (2). $\text{Count} = 2$.
    - `(read, i)`: occurs in `read i n g _` (2). $\text{Count} = 2$.
    - `(e, r)`: occurs in `read e r _` (2) and `read e r s _` (1). $\text{Count} = 3$.
  - Most frequent pair is `(read, _)`.
  - **New Token Created:** `read_`
  - Corpus update:
    - `read_` : 3
    - `read s _` : 2
    - `read e r _` : 2
    - `read i n g _` : 2
    - `u n read_` : 1
    - `read e r s _` : 1

* **Merge Iteration 5:**
  - Count pairs:
    - `(read, e)`: $\text{Count} = 2 + 1 = 3$.
    - `(e, r)`: $\text{Count} = 2 + 1 = 3$.
  - *Tie-breaker:* Leftmost pair in the string is `(read, e)`.
  - **New Token Created:** `reade`
  - Corpus update:
    - `read_` : 3
    - `read s _` : 2
    - `reade r _` : 2
    - `read i n g _` : 2
    - `u n read_` : 1
    - `reade r s _` : 1

* **Merge Iteration 6:**
  - Pair `(reade, r)` occurs in `reade r _` (2) and `reade r s _` (1). $\text{Count} = 3$.
  - **New Token Created:** `reader`
  - Corpus update:
    - `read_` : 3
    - `read s _` : 2
    - `reader _` : 2
    - `read i n g _` : 2
    - `u n read_` : 1
    - `reader s _` : 1

##### Summary Table of 6 Merges
| Merge # | Most Frequent Pair | New Token Added |
| :---: | :---: | :---: |
| 1 | `(r, e)` | `re` |
| 2 | `(re, a)` | `rea` |
| 3 | `(rea, d)` | `read` |
| 4 | `(read, _)` | `read_` |
| 5 | `(read, e)` | `reade` |
| 6 | `(reade, r)` | `reader` |

Final Learned Vocabulary:
$$V = \{ \_, \text{a}, \text{d}, \text{e}, \text{g}, \text{i}, \text{n}, \text{r}, \text{s}, \text{u}, \text{re}, \text{rea}, \text{read}, \text{read\_}, \text{reade}, \text{reader} \}$$

---

##### Step 4: Tokenization of Test Words
Apply learned merge rules in exact chronological order:

| Test Word | In Training Set? | Initial Character Form | Merge Trace | Final BPE Token Sequence |
| :--- | :---: | :--- | :--- | :--- |
| `read` | Yes | `r e a d _` | `re` $\to$ `rea` $\to$ `read` $\to$ `read_` | `[read_]` |
| `reader` | Yes | `r e a d e r _` | `re` $\to$ `rea` $\to$ `read` $\to$ `reade` $\to$ `reader` | `[reader, _]` |
| `readers` | Yes | `r e a d e r s _`| `re` $\to$ `rea` $\to$ `read` $\to$ `reade` $\to$ `reader` | `[reader, s, _]` |
| `reading` | Yes | `r e a d i n g _`| `re` $\to$ `rea` $\to$ `read` | `[read, i, n, g, _]` |
| `unread` | Yes | `u n r e a d _` | `re` $\to$ `rea` $\to$ `read` $\to$ `read_` | `[u, n, read_]` |
| `readable` | **No (OOV)** | `r e a d a b l e _` | `re` $\to$ `rea` $\to$ `read` (no merges for `a b l e _`) | `[read, a, b, l, e, _]` |
| `reread` | **No (OOV)** | `r e r e a d _` | First `r e` $\to$ `re`, second `r e a d _` $\to$ `read_` | `[re, read_]` |
| `unreader` | **No (OOV)** | `u n r e a d e r _`| `re` $\to$ `rea` $\to$ `read` $\to$ `reade` $\to$ `reader` | `[u, n, reader, _]` |

##### Step 5: Handling of OOV Word `readable`
- Characters `b` and `l` never appeared in the original training corpus.
- *Handling:* Because BPE falls back to individual base characters, missing subwords simply default to raw character tokens without triggering an unknown token error.
- *Decoding:* Concatenate tokens and remove `_`:
  $$\text{read} + \text{a} + \text{b} + \text{l} + \text{e} + \_ \implies \mathbf{readable}$$

---

### Numerical 2: Co-Occurrence Matrix, Cosine Similarity & PPMI
*(Source: Vectorization PPT, Slides 1–7)*

#### Problem Setup
Given the 2-sentence corpus:
1. `"data science drives insight"`
2. `"data analysis drives insight"`

Use a **symmetrical context window of size 1** (one word to the left and right).
1. Construct the raw term-by-term co-occurrence matrix $C$.
2. Calculate the **Cosine Similarity** between the row vectors for `science` and `analysis`. Explain the semantic result.
3. Compute the full **Positive Pointwise Mutual Information (PPMI)** matrix. Show calculations for:
   - $\text{PPMI}(\text{data}, \text{science})$
   - $\text{PPMI}(\text{science}, \text{drives})$
   - $\text{PPMI}(\text{drives}, \text{insight})$

---

#### Step-by-Step Solution

##### Step 1: Raw Co-occurrence Matrix Construction
Extract context pairs (window = 1, symmetrical):
- Sentence 1:
  - `data`: context = [`science`]
  - `science`: context = [`data`, `drives`]
  - `drives`: context = [`science`, `insight`]
  - `insight`: context = [`drives`]
- Sentence 2:
  - `data`: context = [`analysis`]
  - `analysis`: context = [`data`, `drives`]
  - `drives`: context = [`analysis`, `insight`]
  - `insight`: context = [`drives`]

**Raw Matrix $C$:**
| Target Word | data | science | analysis | drives | insight | Marginal Count $C(w)$ |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **data** | 0 | 1 | 1 | 0 | 0 | **2** |
| **science** | 1 | 0 | 0 | 1 | 0 | **2** |
| **analysis** | 1 | 0 | 0 | 1 | 0 | **2** |
| **drives** | 0 | 1 | 1 | 0 | 2 | **4** |
| **insight** | 0 | 0 | 0 | 2 | 0 | **2** |
| **Marginal Count $C(c)$** | **2** | **2** | **2** | **4** | **2** | **Total $N = 12$** |

##### Step 2: Cosine Similarity Computation
Extract raw row vectors:
$$\mathbf{v}_{\text{science}} = [1, 0, 0, 1, 0]$$
$$\mathbf{v}_{\text{analysis}} = [1, 0, 0, 1, 0]$$

$$\text{Cosine Similarity}(\mathbf{v}_{\text{science}}, \mathbf{v}_{\text{analysis}}) = \frac{\mathbf{v}_{\text{science}} \cdot \mathbf{v}_{\text{analysis}}}{\|\mathbf{v}_{\text{science}}\| \|\mathbf{v}_{\text{analysis}}\|} = \frac{(1 \times 1) + (0 \times 0) + (0 \times 0) + (1 \times 1) + (0 \times 0)}{\sqrt{1^2 + 0^2 + 0^2 + 1^2 + 0^2} \sqrt{1^2 + 0^2 + 0^2 + 1^2 + 0^2}}$$
$$= \frac{1 + 1}{\sqrt{2} \sqrt{2}} = \frac{2}{2} = \mathbf{1.0}$$
*Semantic Justification:* Even though `science` and `analysis` never directly co-occur with each other, they map to identical directional vectors because they appear in identical contextual environments (`data` on the left, `drives` on the right).

---

##### Step 3: PPMI Calculations
Formulas:
$$\text{PMI}(w, c) = \log_2 \left( \frac{C(w, c) \cdot N}{C(w) \cdot C(c)} \right), \quad \text{PPMI}(w, c) = \max(0, \text{PMI}(w, c))$$
Where total sum of co-occurrences $N = 12$.

* **1. Pair (data, science):**
  $$C(\text{data}, \text{science}) = 1, \quad C(\text{data}) = 2, \quad C(\text{science}) = 2$$
  $$\text{PMI} = \log_2 \left( \frac{1 \times 12}{2 \times 2} \right) = \log_2 \left( \frac{12}{4} \right) = \log_2(3) \approx \mathbf{1.585}$$
  $$\text{PPMI}(\text{data}, \text{science}) = \mathbf{1.585}$$
  *(By symmetry, this also equals $\text{PPMI}(\text{data}, \text{analysis}) = \text{PPMI}(\text{science}, \text{data}) = \text{PPMI}(\text{analysis}, \text{data}) = 1.585$)*

* **2. Pair (science, drives):**
  $$C(\text{science}, \text{drives}) = 1, \quad C(\text{science}) = 2, \quad C(\text{drives}) = 4$$
  $$\text{PMI} = \log_2 \left( \frac{1 \times 12}{2 \times 4} \right) = \log_2 \left( \frac{12}{8} \right) = \log_2(1.5) \approx \mathbf{0.585}$$
  $$\text{PPMI}(\text{science}, \text{drives}) = \mathbf{0.585}$$
  *(By symmetry, this also equals $\text{PPMI}(\text{analysis}, \text{drives}) = \text{PPMI}(\text{drives}, \text{science}) = \text{PPMI}(\text{drives}, \text{analysis}) = 0.585$)*

* **3. Pair (drives, insight):**
  $$C(\text{drives}, \text{insight}) = 2, \quad C(\text{drives}) = 4, \quad C(\text{insight}) = 2$$
  $$\text{PMI} = \log_2 \left( \frac{2 \times 12}{4 \times 2} \right) = \log_2 \left( \frac{24}{8} \right) = \log_2(3) \approx \mathbf{1.585}$$
  $$\text{PPMI}(\text{drives}, \text{insight}) = \mathbf{1.585}$$

* **4. Non-co-occurring Pairs ($C(w, c) = 0$):**
  $$\text{PMI} = \log_2(0) \to -\infty \implies \text{PPMI} = \mathbf{0.0}$$

##### Final PPMI Matrix
| Target Word | data | science | analysis | drives | insight |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **data** | 0.000 | 1.585 | 1.585 | 0.000 | 0.000 |
| **science** | 1.585 | 0.000 | 0.000 | 0.585 | 0.000 |
| **analysis** | 1.585 | 0.000 | 0.000 | 0.585 | 0.000 |
| **drives** | 0.000 | 0.585 | 0.585 | 0.000 | 1.585 |
| **insight** | 0.000 | 0.000 | 0.000 | 1.585 | 0.000 |

---

### Numerical 3: TF-IDF Vectorization with Sklearn Smoothing & $L_2$ Normalization
*(Source: Vectorization PPT, Slides 10–12)*

#### Problem Setup
Given the 2-document corpus:
- **$D_1$:** `"The stock price of google jumps on the earning data today"`
- **$D_2$:** `"Google plunge on China Data!"`

Preprocessing specifications: Lowercase, strip punctuation, remove English stop words (`the`, `of`, `on`).
Use the **Scikit-Learn modified formula**:
$$\text{IDF}(t, D) = \ln \left( \frac{1 + |D|}{1 + \text{DF}(t)} \right) + 1$$
$$\text{TF}(t, d) = C(t, d) \quad (\text{raw term count in document } d)$$
Calculate the final $L_2$-normalized TF-IDF vectors for $D_1$ and $D_2$.

---

#### Step-by-Step Solution

##### Step 1: Preprocessing & Vocabulary Extraction
- Filtered $D_1$: `['stock', 'price', 'google', 'jumps', 'earning', 'data', 'today']`
- Filtered $D_2$: `['google', 'plunge', 'china', 'data']`
- Total documents $|D| = 2$.
- Sorted Vocabulary ($|V| = 9$):
  1. `china`, 2. `data`, 3. `earning`, 4. `google`, 5. `jumps`, 6. `plunge`, 7. `price`, 8. `stock`, 9. `today`

##### Step 2: Document Frequency ($\text{DF}$) and $\text{IDF}$ Scores
- `data`: appears in $D_1, D_2 \implies \text{DF} = 2$
- `google`: appears in $D_1, D_2 \implies \text{DF} = 2$
- `china`, `earning`, `jumps`, `plunge`, `price`, `stock`, `today`: appear in 1 document each $\implies \text{DF} = 1$

Calculate $\text{IDF}$:
* For terms with $\text{DF} = 2$ (`data`, `google`):
  $$\text{IDF} = \ln \left( \frac{1 + 2}{1 + 2} \right) + 1 = \ln(1) + 1 = 0 + 1 = \mathbf{1.0000}$$
* For terms with $\text{DF} = 1$ (`china`, `earning`, etc.):
  $$\text{IDF} = \ln \left( \frac{1 + 2}{1 + 1} \right) + 1 = \ln(1.5) + 1 \approx 0.405465 + 1 = \mathbf{1.4055}$$

---

##### Step 3: Unnormalized TF-IDF Vectors
$$\text{Unnormalized TF-IDF}(t, d) = \text{TF}(t, d) \times \text{IDF}(t)$$

* **For Document 1 ($D_1$):**
  - `china`: $0 \times 1.4055 = 0.0$
  - `data`: $1 \times 1.0000 = 1.0$
  - `earning`: $1 \times 1.4055 = 1.4055$
  - `google`: $1 \times 1.0000 = 1.0$
  - `jumps`: $1 \times 1.4055 = 1.4055$
  - `plunge`: $0 \times 1.4055 = 0.0$
  - `price`: $1 \times 1.4055 = 1.4055$
  - `stock`: $1 \times 1.4055 = 1.4055$
  - `today`: $1 \times 1.4055 = 1.4055$

  $$\mathbf{v}_1 = [0.0,\, 1.0,\, 1.4055,\, 1.0,\, 1.4055,\, 0.0,\, 1.4055,\, 1.4055,\, 1.4055]$$

* **For Document 2 ($D_2$):**
  - `china`: $1 \times 1.4055 = 1.4055$
  - `data`: $1 \times 1.0000 = 1.0$
  - `earning`: $0 \times 1.4055 = 0.0$
  - `google`: $1 \times 1.0000 = 1.0$
  - `jumps`: $0 \times 1.4055 = 0.0$
  - `plunge`: $1 \times 1.4055 = 1.4055$
  - `price`: $0 \times 1.4055 = 0.0$
  - `stock`: $0 \times 1.4055 = 0.0$
  - `today`: $0 \times 1.4055 = 0.0$

  $$\mathbf{v}_2 = [1.4055,\, 1.0,\, 0.0,\, 1.0,\, 0.0,\, 1.4055,\, 0.0,\, 0.0,\, 0.0]$$

---

##### Step 4: $L_2$ Normalization
$$\|\mathbf{v}\|_2 = \sqrt{\sum_{i=1}^{|V|} v_i^2}, \quad \mathbf{v}_{\text{normalized}} = \frac{\mathbf{v}}{\|\mathbf{v}\|_2}$$

* **Normalize $D_1$:**
  $$\|\mathbf{v}_1\|_2 = \sqrt{2 \times (1.0)^2 + 5 \times (1.4055)^2} = \sqrt{2(1.0) + 5(1.97543)} = \sqrt{2 + 9.87715} = \sqrt{11.87715} \approx \mathbf{3.4463}$$
  - For `data`, `google`: $\frac{1.0}{3.4463} \approx \mathbf{0.2902}$
  - For `earning`, `jumps`, `price`, `stock`, `today`: $\frac{1.4055}{3.4463} \approx \mathbf{0.4078}$
  - Others: $\mathbf{0.0000}$

  $$\mathbf{v}_{1, \text{norm}} = [0.0,\, 0.2902,\, 0.4078,\, 0.2902,\, 0.4078,\, 0.0,\, 0.4078,\, 0.4078,\, 0.4078]$$

* **Normalize $D_2$:**
  $$\|\mathbf{v}_2\|_2 = \sqrt{2 \times (1.0)^2 + 2 \times (1.4055)^2} = \sqrt{2(1.0) + 2(1.97543)} = \sqrt{2 + 3.95086} = \sqrt{5.95086} \approx \mathbf{2.4394}$$
  - For `china`, `plunge`: $\frac{1.4055}{2.4394} \approx \mathbf{0.5762}$
  - For `data`, `google`: $\frac{1.0}{2.4394} \approx \mathbf{0.4099}$
  - Others: $\mathbf{0.0000}$

  $$\mathbf{v}_{2, \text{norm}} = [0.5762,\, 0.4099,\, 0.0,\, 0.4099,\, 0.0,\, 0.5762,\, 0.0,\, 0.0,\, 0.0]$$

---

### Numerical 4: $N$-gram MLE Probability and Perplexity (Bigram vs. Trigram)
*(Source: Intro to $N$-grams PPT, Slides 20–24)*

#### Problem Setup
Given the training corpus:
1. `<s> I am Sam </s>`
2. `<s> Sam I am </s>`
3. `<s> I do not like green eggs </s>`

**Test Sequence:** `<s> I am Sam </s>`  
*(Tokenization convention: evaluated tokens $n = 4$: $w_1 = \text{I}$, $w_2 = \text{am}$, $w_3 = \text{Sam}$, $w_4 = \text{</s>}$, conditioned on start marker).*

**Tasks:**
1. Estimate the total sequence probability $P(W)$ under a **Bigram MLE model**.
2. Compute the Bigram **Perplexity ($PP$)** using the direct root formula and log cross-entropy base 2.
3. Repeat the complete probability and perplexity calculations for a **Trigram MLE model**.
4. Justify why the Trigram model achieves a lower perplexity score.

---

#### Step-by-Step Solution

##### Step 1: Bigram MLE Model
Token counts from training corpus:
- Unigram counts:
  - $C(\text{<s>}) = 3$
  - $C(\text{I}) = 3$
  - $C(\text{am}) = 2$
  - $C(\text{Sam}) = 2$
- Bigram counts:
  - $C(\text{<s>}, \text{I}) = 2$
  - $C(\text{I}, \text{am}) = 2$
  - $C(\text{am}, \text{Sam}) = 1$
  - $C(\text{Sam}, \text{</s>}) = 1$

Calculate conditional probabilities:
1. $P(\text{I} \mid \text{<s>}) = \frac{C(\text{<s>}, \text{I})}{C(\text{<s>})} = \frac{2}{3} \approx 0.66667$
2. $P(\text{am} \mid \text{I}) = \frac{C(\text{I}, \text{am})}{C(\text{I})} = \frac{2}{3} \approx 0.66667$
3. $P(\text{Sam} \mid \text{am}) = \frac{C(\text{am}, \text{Sam})}{C(\text{am})} = \frac{1}{2} = 0.50000$
4. $P(\text{</s>} \mid \text{Sam}) = \frac{C(\text{Sam}, \text{</s>})}{C(\text{Sam})} = \frac{1}{2} = 0.50000$

Joint Sentence Probability:
$$P(W) = \frac{2}{3} \times \frac{2}{3} \times \frac{1}{2} \times \frac{1}{2} = \frac{4}{36} = \frac{1}{9} \approx \mathbf{0.11111}$$

Bigram Perplexity ($n = 4$):
* Direct calculation:
  $$PP(W) = \left( \frac{1}{9} \right)^{-\frac{1}{4}} = 9^{\frac{1}{4}} = \sqrt{\sqrt{9}} = \sqrt{3} \approx \mathbf{1.732}$$
* Cross-Entropy calculation ($\log_2$):
  $$\log_2 P(\text{I} \mid \text{<s>}) = \log_2(2/3) \approx -0.58496$$
  $$\log_2 P(\text{am} \mid \text{I}) = \log_2(2/3) \approx -0.58496$$
  $$\log_2 P(\text{Sam} \mid \text{am}) = \log_2(1/2) = -1.00000$$
  $$\log_2 P(\text{</s>} \mid \text{Sam}) = \log_2(1/2) = -1.00000$$
  $$H(W) = -\frac{1}{4} [-0.58496 - 0.58496 - 1.00000 - 1.00000] = -\frac{1}{4} [-3.16992] = \mathbf{0.79248} \text{ bits/word}$$
  $$PP(W) = 2^{0.79248} = \sqrt{3} \approx \mathbf{1.732}$$

---

##### Step 2: Trigram MLE Model
Prepend two boundary markers: `<s> <s> I am Sam </s>`
- Trigram context counts:
  - $C(\text{<s>}, \text{<s>}) = 3$
  - $C(\text{<s>}, \text{<s>}, \text{I}) = 2$
  - $C(\text{<s>}, \text{I}) = 2$
  - $C(\text{<s>}, \text{I}, \text{am}) = 1$
  - $C(\text{I}, \text{am}) = 2$
  - $C(\text{I}, \text{am}, \text{Sam}) = 1$
  - $C(\text{am}, \text{Sam}) = 1$
  - $C(\text{am}, \text{Sam}, \text{</s>}) = 1$

Calculate conditional probabilities:
1. $P(\text{I} \mid \text{<s>}, \text{<s>}) = \frac{C(\text{<s>}, \text{<s>}, \text{I})}{C(\text{<s>}, \text{<s>})} = \frac{2}{3} \approx 0.66667$
2. $P(\text{am} \mid \text{<s>}, \text{I}) = \frac{C(\text{<s>}, \text{I}, \text{am})}{C(\text{<s>}, \text{I})} = \frac{1}{2} = 0.50000$
3. $P(\text{Sam} \mid \text{I}, \text{am}) = \frac{C(\text{I}, \text{am}, \text{Sam})}{C(\text{I}, \text{am})} = \frac{1}{2} = 0.50000$
4. $P(\text{</s>} \mid \text{am}, \text{Sam}) = \frac{C(\text{am}, \text{Sam}, \text{</s>})}{C(\text{am}, \text{Sam})} = \frac{1}{1} = \mathbf{1.00000}$

Joint Sentence Probability:
$$P(W) = \frac{2}{3} \times \frac{1}{2} \times \frac{1}{2} \times 1 = \frac{2}{12} = \frac{1}{6} \approx \mathbf{0.16667}$$

Trigram Perplexity ($n = 4$):
* Direct calculation:
  $$PP(W) = \left( \frac{1}{6} \right)^{-\frac{1}{4}} = 6^{\frac{1}{4}} = \sqrt{\sqrt{6}} = \sqrt{2.44949} \approx \mathbf{1.565}$$
* Cross-Entropy calculation ($\log_2$):
  $$\log_2 P(\text{I} \mid \text{<s>}, \text{<s>}) = \log_2(2/3) \approx -0.58496$$
  $$\log_2 P(\text{am} \mid \text{<s>}, \text{I}) = \log_2(1/2) = -1.00000$$
  $$\log_2 P(\text{Sam} \mid \text{I}, \text{am}) = \log_2(1/2) = -1.00000$$
  $$\log_2 P(\text{</s>} \mid \text{am}, \text{Sam}) = \log_2(1) = 0.00000$$
  $$H(W) = -\frac{1}{4} [-0.58496 - 1.00000 - 1.00000 + 0] = -\frac{1}{4} [-2.58496] = \mathbf{0.64624} \text{ bits/word}$$
  $$PP(W) = 2^{0.64624} \approx \mathbf{1.565}$$

##### Step 3: Analytical Justification
The Trigram model achieves lower perplexity ($1.565 < 1.732$) because conditioned on a two-word history (`am Sam`), the model resolves ambiguity completely: $P(\text{</s>} \mid \text{am}, \text{Sam}) = 1.0$ (entropy = 0 for that step). Holding the test set constant, higher context informs the distribution, reduces uncertainty, and lowers perplexity.

---

### Numerical 5: Laplace (Add-1) and Add-$m$ Smoothed Probability & Perplexity
*(Source: Data Sparsity PPT, Slides 8–11)*

#### Problem Setup
Using the same training corpus:
1. `<s> I am Sam </s>`
2. `<s> Sam I am </s>`
3. `<s> I do not like green eggs </s>`

Unique word types:
$$V = \{ \text{<s>}, \text{</s>}, \text{I}, \text{am}, \text{Sam}, \text{do}, \text{not}, \text{like}, \text{green}, \text{eggs} \} \implies |V| = 10$$
**Test Sequence:** `<s> I am Sam </s>` ($n = 4$ tokens).

**Tasks:**
1. Compute all bigram conditional probabilities using **Laplace (Add-1) Smoothing**.
2. Compute the total sequence probability $P_{\text{Laplace}}(W)$.
3. Compute the smoothed **Perplexity ($PP$)** and **Cross-Entropy ($H$)**.
4. Contrast this outcome against the unsmoothed Bigram perplexity ($1.732$) and explain why perplexity increased.

---

#### Step-by-Step Solution

##### Step 1: Laplace Smoothed Conditional Probabilities
Formula:
$$P_{\text{Laplace}}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + |V|} = \frac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + 10}$$

1. $P_{\text{Laplace}}(\text{I} \mid \text{<s>}) = \frac{C(\text{<s>}, \text{I}) + 1}{C(\text{<s>}) + 10} = \frac{2 + 1}{3 + 10} = \frac{3}{13} \approx \mathbf{0.23077}$
2. $P_{\text{Laplace}}(\text{am} \mid \text{I}) = \frac{C(\text{I}, \text{am}) + 1}{C(\text{I}) + 10} = \frac{2 + 1}{3 + 10} = \frac{3}{13} \approx \mathbf{0.23077}$
3. $P_{\text{Laplace}}(\text{Sam} \mid \text{am}) = \frac{C(\text{am}, \text{Sam}) + 1}{C(\text{am}) + 10} = \frac{1 + 1}{2 + 10} = \frac{2}{12} = \frac{1}{6} \approx \mathbf{0.16667}$
4. $P_{\text{Laplace}}(\text{</s>} \mid \text{Sam}) = \frac{C(\text{Sam}, \text{</s>}) + 1}{C(\text{Sam}) + 10} = \frac{1 + 1}{2 + 10} = \frac{2}{12} = \frac{1}{6} \approx \mathbf{0.16667}$

##### Step 2: Total Sequence Probability
$$P_{\text{Laplace}}(W) = \frac{3}{13} \times \frac{3}{13} \times \frac{1}{6} \times \frac{1}{6} = \frac{9}{169 \times 36} = \frac{9}{6084} = \frac{1}{676} \approx \mathbf{0.00147929}$$

##### Step 3: Perplexity and Cross-Entropy Calculations
* Direct Perplexity ($n = 4$):
  $$PP(W) = \left( \frac{1}{676} \right)^{-\frac{1}{4}} = 676^{\frac{1}{4}} = \sqrt{\sqrt{676}} = \sqrt{26} \approx \mathbf{5.099}$$
* Via Cross-Entropy:
  $$\log_2 P(\text{I} \mid \text{<s>}) = \log_2(3/13) \approx -2.11547$$
  $$\log_2 P(\text{am} \mid \text{I}) = \log_2(3/13) \approx -2.11547$$
  $$\log_2 P(\text{Sam} \mid \text{am}) = \log_2(1/6) \approx -2.58496$$
  $$\log_2 P(\text{</s>} \mid \text{Sam}) = \log_2(1/6) \approx -2.58496$$
  $$H(W) = -\frac{1}{4} [-2.11547 - 2.11547 - 2.58496 - 2.58496] = -\frac{1}{4} [-9.40086] \approx \mathbf{2.35022} \text{ bits/word}$$
  $$PP(W) = 2^{2.35022} \approx \mathbf{5.099}$$

##### Step 4: Analytical Justification
- *Unsmoothed Bigram Perplexity:* $1.732$
- *Laplace Smoothed Bigram Perplexity:* $5.099$
- *Why did perplexity worsen on this test set?*  
  Laplace smoothing artificially allocates a count of 1 to every unseen bigram in the vocabulary matrix. Because the test sequence was already composed entirely of known transitions, Laplace smoothing **discounted** the probability mass from these observed transitions and distributed it to unseen combinations. This reduces the probability of known sequences, increasing cross-entropy and raising perplexity. However, smoothing prevents the probability from collapsing to zero if an unseen token does occur.

---

### Numerical 6: Argmax Computation for a Bigram Sequence
*(Source: 2024 PYQ Q1(C))*

#### Problem Setup
Find the most probable sequence of words $\hat{W}$ for the sentence:
`"The cat chased the mouse"` using a Bigram Language Model under the **Argmax** formulation.

---

#### Step-by-Step Solution

##### Step 1: Formal Argmax Formulation
Under a generative statistical framework, we seek the sequence of words $W = (w_1, w_2, \dots, w_n)$ that maximizes the joint sequence likelihood:
$$\hat{W} = \arg\max_{W} P(W)$$

Applying the chain rule under the first-order Markov assumption (Bigram model) with sentence boundary markers (`<s>`, `</s>`):
$$\hat{W} = \arg\max_{W} \prod_{k=1}^{n+1} P(w_k \mid w_{k-1})$$
Where $w_0 = \text{<s>}$ and $w_{n+1} = \text{</s>}$.

##### Step 2: Expansion for the Target Sentence
For the sequence $W = (\text{The}, \text{cat}, \text{chased}, \text{the}, \text{mouse})$:
$$P(W) = P(\text{The} \mid \text{<s>}) \cdot P(\text{cat} \mid \text{The}) \cdot P(\text{chased} \mid \text{cat}) \cdot P(\text{the} \mid \text{chased}) \cdot P(\text{mouse} \mid \text{the}) \cdot P(\text{</s>} \mid \text{mouse})$$

##### Step 3: Formulation in Log-Likelihood Space
To avoid floating-point underflow and convert products into linear summations:
$$\hat{W} = \arg\max_{W} \sum_{k=1}^{n+1} \log P(w_k \mid w_{k-1})$$
$$= \arg\max_{W} \left[ \log P(\text{The} \mid \text{<s>}) + \log P(\text{cat} \mid \text{The}) + \log P(\text{chased} \mid \text{cat}) + \log P(\text{the} \mid \text{chased}) + \log P(\text{mouse} \mid \text{the}) + \log P(\text{</s>} \mid \text{mouse}) \right]$$

##### Step 4: Algorithmic Resolution
In language generation or speech transcription tasks with multiple path candidates, computing the argmax across all combinatorial paths is solved using dynamic programming via the **Viterbi Search Algorithm**, which prunes paths while retaining maximum forward probabilities at each time step.

---

# Part 5: Slide Justifications & "Why" Questions

### 1. Why does an unseen $N$-gram cause Sequence Probability Collapse and Perplexity Explosion?
* **Probability Collapse:** Joint sentence probability is computed as a product of terms:
  $$P(W) = \prod_{k=1}^n P(w_k \mid w_{k-N+1:k-1})$$
  If a single transition was never seen during training, its MLE probability is:
  $$P_{\text{MLE}}(w_k \mid w_{k-N+1:k-1}) = \frac{0}{C(\text{context})} = 0$$
  A single zero causes the entire product to evaluate to zero: $P(W) = 0$.
* **Perplexity Explosion:** Perplexity is the inverse $n$-th root:
  $$PP(W) = \left( \frac{1}{P(W)} \right)^{1/n} = \left( \frac{1}{0} \right)^{1/n} \to \infty$$
  In log space, cross-entropy $H(W)$ evaluates $\log_2(0) \to -\infty$, making $H(W) = +\infty$ and $PP(W) = 2^\infty = \infty$.
  *Takeaway:* An empirical count of zero does not mean a phrase is linguistically impossible; it simply means the training sample was not large enough to observe it.

### 2. Why is $|V|$ added to the denominator in Laplace Smoothing?
* If we add 1 to the numerator of each word in vocabulary $V$, we are adding 1 across $|V|$ distinct possible outcomes:
  $$\sum_{w_k \in V} [C(w_{k-1}, w_k) + 1] = \left( \sum_{w_k} C(w_{k-1}, w_k) \right) + |V| = C(w_{k-1}) + |V|$$
  To ensure the conditional distribution sums to 1 ($\sum_{w_k \in V} P(w_k \mid w_{k-1}) = 1$), the denominator must scale by $+|V|$:
  $$P(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + |V|}$$

### 3. Why is Laplace Smoothing problematic for large $|V|$ and how does Lidstone ($m$) solve it?
* In real-world NLP corpora, $|V|$ is large (e.g., $|V| = 50,000$).
* Adding a full count of 1 to every transition adds a total virtual count of $50,000$ to the denominator.
* This takes too much probability mass away from frequently observed words and shifts it to unseen pairs, degrading model accuracy.
* **Lidstone Solution:** Replaces 1 with a small fraction $m$ (e.g., $m = 0.05$):
  $$P_{\text{Add-}m}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + m}{C(w_{k-1}) + m|V|}$$
  This provides non-zero probabilities for unseen events without disproportionately discounting observed data.

### 4. Why is Perplexity identical to the Effective Branching Factor?
* In a uniform distribution over $K$ alternatives, probability $P = 1/K$.
  Entropy $H = -\log_2(1/K) = \log_2 K$, and perplexity $PP = 2^{\log_2 K} = K$.
* For non-uniform natural language, perplexity $PP(W)$ maps continuous entropy back into an intuitive discrete scale: a model with $PP = 50$ is, on average, as uncertain about the next word as if it were choosing uniformly among 50 equally likely candidates.

### 5. Why must two Language Models share an Identical Vocabulary for a fair Perplexity comparison?
* Perplexity is normalized by dividing mass across vocabulary types.
* If Model A has $|V| = 1,000$ and Model B has $|V| = 50,000$, Model A divides its probability mass across fewer options, which artificially deflates its perplexity.
* Similarly, if an open-vocabulary model maps out-of-vocabulary words to a single `<UNK>` token, its perplexity becomes artificially low because `<UNK>` absorbs high probability mass. Fair comparison requires identical vocabularies, identical tokenization, and identical handling of sentence boundaries.

### 6. Why does Raw Co-occurrence suffer from Frequency Bias, and how does PPMI correct it?
* **Frequency Bias:** High-frequency, uninformative words (*the*, *is*, *and*) co-occur frequently with almost every word, dominating raw counts without providing meaningful semantic context.
* **PPMI Correction:** PMI divides joint probability by the product of individual marginal probabilities:
  $$\text{PMI}(w, c) = \log_2 \left( \frac{P(w, c)}{P(w)P(c)} \right)$$
  If word $c$ is common, $P(c)$ is large, which scales down the ratio. A high PMI score requires the joint co-occurrence $P(w, c)$ to be substantially higher than expected by random chance.

---

# Part 6: Previous Year Question (PYQ) Solutions (2024 & 2025)

---

## 2024 Paper Solutions (Course: 20IC403T)

#### Q1(A) Design a regular expression (RE) to detect email addresses from the given sentence:
`"I am a student with email id abc@xyz.com and my friend’s email is abc.def@xyz.co.in."` **[3 Marks]**
* **Target Matches:** `abc@xyz.com` and `abc.def@xyz.co.in`
* **Optimal Regular Expression:**
  ```regex
  [a-zA-Z0-9]+(?:\.[a-zA-Z0-9]+)*@[a-zA-Z0-9]+(?:\.[a-zA-Z0-9]+)+
  ```
* **Explanation:**
  - `[a-zA-Z0-9]+`: Matches leading alphanumeric characters (`abc`).
  - `(?:\.[a-zA-Z0-9]+)*`: Non-capturing group matching optional dot-separated strings in local user names (`.def`).
  - `@`: Matches the mandatory separator.
  - `[a-zA-Z0-9]+`: Matches domain host name (`xyz`).
  - `(?:\.[a-zA-Z0-9]+)+`: Matches one or more domain suffixes (`.com` or `.co.in`).

---

#### Q1(B) What is Part-of-Speech (POS) tagging with example? **[1 + 2 = 3 Marks]**
* **Definition:** POS tagging is the process of assigning a grammatical category (such as noun, verb, adjective, adverb) to each word in a text sequence based on both its definition and its surrounding context.
* **Example:**
  Consider the sentence: *"They book a flight to London."*
  - `They` $\to$ Pronoun (`PRP`)
  - `book` $\to$ Verb (`VBP`)
  - `a` $\to$ Determiner (`DT`)
  - `flight` $\to$ Noun (`NN`)
  - `to` $\to$ Preposition (`TO` / `IN`)
  - `London` $\to$ Proper Noun (`NNP`)
* *Contextual Ambiguity Note:* In *"He read an interesting book"*, the word `book` is tagged as a Noun (`NN`), demonstrating how the tag depends on context.

---

#### Q1(C) Use Argmax computation to find the most probable sequence of words for the sentence "The cat chased the mouse" in a simple bigram model. **[4 Marks]**
*(Refer to [Numerical 6](#numerical-6-argmax-computation-for-a-bigram-sequence) for the complete derivation.)*

---

#### Q2(A) Explain the concept of place and manner of articulation in speech processing. **[5 Marks]**
*(Refer to [Part 2, Section 6](#6-speech-processing-foundations-pyq-essentials) for full definitions of all 8 places and 5 manners with acoustic phonetic examples.)*

---

#### Q2(B) Differentiate between stemming and morphological analysis. Provide an example for each. **[2.5 + 2.5 = 5 Marks]**
*(Refer to [Part 2, Section 3](#3-stemming-vs-lemmatization-vs-morphological-analysis) for the comparative table and examples.)*

---

#### Q3(A) Illustrate how word-tokenization can be applied to the following sentence:
`"Natural language processing is a field of computer science."` **[5 Marks]**
* **Input String:** `"Natural language processing is a field of computer science."`
* **Step-by-Step Processing:**
  1. *Rule-Based Whitespace Splitting:* Isolates substrings on space boundaries:
     `['Natural', 'language', 'processing', 'is', 'a', 'field', 'of', 'computer', 'science.']`
  2. *Punctuation Separation:* Detaches terminal punctuation mark `.` from `science.`:
     `'science.'` $\to$ `'science'`, `'.'`
* **Final List of Tokens:**
  ```python
  ["Natural", "language", "processing", "is", "a", "field", "of", "computer", "science", "."]
  ```
* **Metrics:**
  - Total Tokens ($N$): $10$
  - Unique Types ($|V|$): $10$ (all distinct)

---

#### Q3(B) Construct a basic HMM model for speech recognition and show how the model processes an input speech signal. **[5 Marks]**
*(Refer to [Part 2, Section 6](#6-speech-processing-foundations-pyq-essentials) for the HMM architecture diagram, MFCC extraction, emission/transition matrices, and Viterbi decoding equation.)*

---

#### Q4(A) Analyze the role of computational grammar in language structure analysis. Why is it necessary for NLP? **[5 Marks]**
* **Definition:** Computational grammar refers to formal, mathematically explicit systems of rules (such as Context-Free Grammars (CFGs), Lexical Functional Grammars, and Dependency Grammars) that describe syntactic structure and sentence construction.
* **Why it is necessary for NLP:**
  1. *Resolving Structural Ambiguity:* Surface strings often allow multiple interpretations.
     - *Example:* *"I saw the man with a telescope."*
     - Attachment 1: [Saw [the man] [with a telescope]] $\to$ Instrument of seeing.
     - Attachment 2: [Saw [the man with a telescope]] $\to$ The man possesses the telescope.
     Computational grammar parses these alternatives into explicit syntax trees.
  2. *Compositional Semantics:* Enables the principle of compositionality—the meaning of a sentence is built from the meanings of its syntactic parts.
  3. *Syntax Validation:* Distinguishes grammatically valid constructs from ill-formed word soups, which is essential for grammatical error correction and rule-based machine translation.

---

#### Q4(B) Evaluate the importance of word boundary detection in speech recognition systems and propose strategies to handle boundary detection errors. **[5 Marks]**
* **Importance:** Speech waveforms are continuous; speakers rarely insert pauses between words. Accurate boundary detection is critical because errors propagate downstream, altering sentence syntax and meaning.
* **Acoustic Challenges:** Co-articulation blurs phonetic transitions; homophones and continuous sounds create acoustic ambiguity (e.g., *"gray tape"* vs. *"great ape"*).
* **Strategies to Resolve Boundary Errors:**
  1. *Subword / Character Modeling:* Using Phone-state HMMs or Connectionist Temporal Classification (CTC) to decode sub-phonetic units without forcing hard boundary commitments early.
  2. *Language Model Integration:* Applying $N$-gram or neural language models during beam search decoding to weight linguistically plausible word transitions higher.
  3. *Lattice Rescoring:* Preserving multiple boundary hypotheses in a word lattice and rescoring them using long-range context.

---

#### Q4(A) OR: Apply appropriate preprocessing techniques on the following dataset containing text data in a .txt file. Explain each step:
Text: `"NLP is an exciting field of artificial intelligence."` **[5 Marks]**
1. **Sentence Segmentation:** Identifies sentence boundaries:
   `"NLP is an exciting field of artificial intelligence."`
2. **Word Tokenization:** Splits the string into atomic word tokens and isolates punctuation:
   `['NLP', 'is', 'an', 'exciting', 'field', 'of', 'artificial', 'intelligence', '.']`
3. **Case Folding (Lowercasing):** Normalizes tokens to uniform case:
   `['nlp', 'is', 'an', 'exciting', 'field', 'of', 'artificial', 'intelligence', '.']`
4. **Punctuation Stripping:** Removes non-alphanumeric symbols:
   `['nlp', 'is', 'an', 'exciting', 'field', 'of', 'artificial', 'intelligence']`
5. **Stop Word Removal:** Filters out high-frequency functional stop words (`is`, `an`, `of`):
   `['nlp', 'exciting', 'field', 'artificial', 'intelligence']`
6. **Lemmatization / Stemming:** Reduces inflectional forms to root bases (e.g., `exciting` $\to$ `excite`):
   `['nlp', 'excite', 'field', 'artificial', 'intelligence']`

---

#### Q4(B) OR: Describe the advantages and disadvantages to store speech information in MP3 and FLAC format. **[5 Marks]**
* **MP3 (MPEG-1 Audio Layer III):**
  - *Mechanism:* Lossy perceptual compression. Discards high-frequency sounds outside the typical human auditory threshold based on psychoacoustic modeling.
  - *Advantages:* Small file sizes (approx. 10:1 compression ratio), lower bandwidth/storage requirements.
  - *Disadvantages:* Discards subtle acoustic information; can degrade high-frequency phonetic features (such as fricatives $/s/, /z/, /f/$), reducing accuracy in ASR acoustic feature extraction (MFCCs).
* **FLAC (Free Lossless Audio Codec):**
  - *Mechanism:* Lossless linear predictive compression. Retains 100% of the original uncompressed audio waveform.
  - *Advantages:* Full signal fidelity and dynamic range preserved; ideal for training speech recognition acoustic models.
  - *Disadvantages:* Significantly larger file sizes (roughly 5 to 6 times larger than MP3), increasing storage and transfer overhead.

---

#### Q5(A) Analyze the differences between datasets prepared for text classification versus machine translation tasks in NLP. How does the nature of the corpus and attributes change? **[6 Marks]**
*(Refer to [Part 2, Section 7](#7-data-attributes--dataset-structures-pyq-essentials) for the full comparative matrix.)*

---

#### Q5(B) State the difference between nominal data and ordinal data with example. Moreover, explain interval-scaled and ratio-scale attributes with example. **[4 Marks]**
*(Refer to [Part 2, Section 7](#7-data-attributes--dataset-structures-pyq-essentials) for detailed explanations and examples for all 4 measurement scales.)*

---

#### Q5(B) OR: Compare the use of different file formats for text corpora, such as JSON and CSV with example. **[4 Marks]**
* **CSV (Comma-Separated Values):**
  - *Structure:* Flat, two-dimensional tabular grid (rows and columns).
  - *Best Suited For:* Simple tabular datasets like document-level text classification (e.g., `text, label`).
  - *Disadvantages:* Poor support for hierarchical, nested, or token-level metadata (such as bounding boxes or token alignments); multi-line text with commas requires careful escaping.
  - *Example:*
    ```csv
    id,text,label
    101,"The movie was fantastic!",Positive
    ```
* **JSON (JavaScript Object Notation):**
  - *Structure:* Semi-structured, hierarchical key-value dictionaries and arrays.
  - *Best Suited For:* Complex, nested NLP annotations like NER spans, dependency trees, and parallel translations.
  - *Disadvantages:* Larger file sizes due to repetitive keys; higher parsing overhead compared to flat files.
  - *Example:*
    ```json
    {
      "id": 101,
      "text": "Google acquired Android.",
      "entities": [
        {"token": "Google", "label": "ORG", "start": 0, "end": 6},
        {"token": "Android", "label": "PRODUCT", "start": 16, "end": 23}
      ]
    }
    ```

---

## 2025 Paper Solutions (Course: 20IC403T)

#### Q1. What are the components of an NLP system and explain differences among them? **[5 Marks]**
*(Refer to [Part 2, Section 1](#1-nlp-pipeline-components--downstream-roles) for the complete pipeline diagram, component breakdown, and stage comparisons.)*

---

#### Q2. Discuss the challenges in word boundary detection for speech and text in different languages. Provide suitable examples? **[10 Marks]**
*(Refer to [Part 2, Section 6](#6-speech-processing-foundations-pyq-essentials) for cross-lingual text issues, Chinese/German examples, speech co-articulation, and phonetic boundary challenges.)*

---

#### Q2 OR: Describe the role of Hidden Markov Model (HMM) in automatic speech recognition. Illustrate with example? **[10 Marks]**
*(Refer to [Part 2, Section 6](#6-speech-processing-foundations-pyq-essentials) for the HMM formulation, acoustic vs. language modeling, and decoding equation.)*

---

#### Q3. Define the following (2 marks each): **[5 × 2 = 10 Marks]**
* **(a) Tokenization:** The computational process of segmenting a continuous stream of written text into discrete linguistic units (tokens), such as words, punctuation marks, or subwords, for downstream modeling.
* **(b) Stemming:** A fast, heuristic, rule-based technique that strips common grammatical affixes (prefixes and suffixes) from words to arrive at a base form (stem), often resulting in non-dictionary character strings (e.g., *troubled* $\to$ `troubl`).
* **(c) Morphological Analysis:** The linguistic analysis of word structures into their smallest meaning-bearing constituent units (*morphemes*), identifying root stems and associated grammatical inflections (such as tense, number, gender, and case).
* **(d) Computational Grammar:** A formal, computationally implementable system of rules (such as Context-Free Grammars) used by parsers to analyze syntactic structure, validate sentence grammaticality, and resolve structural ambiguities.
* **(e) Place and Manner of Articulation:**
  - *Place of Articulation:* The anatomical site in the vocal tract where airflow constriction occurs (e.g., Bilabial, Alveolar, Velar).
  - *Manner of Articulation:* The physical way the airstream is obstructed or released (e.g., Stops, Fricatives, Nasals).

---

# Part 7: Predicted 25-Mark Mock Exams

## Mock Exam Paper 1 (Heavily Numerical & Analytical)
**Time:** 60 Minutes | **Max Marks:** 25

### Questions
1. **[Numerical – 6 Marks]**  
   Given a training corpus with two sentences:  
   `<s> John likes programming </s>`  
   `<s> John likes coffee </s>`  
   - Calculate the Bigram MLE probabilities for:  
     $P(\text{likes} \mid \text{John})$, $P(\text{programming} \mid \text{likes})$, and $P(\text{</s>} \mid \text{coffee})$.  
   - Using **Laplace (Add-1) Smoothing** with an extracted vocabulary size $|V| = 6$, compute the smoothed probability:  
     $P_{\text{Laplace}}(\text{tea} \mid \text{likes})$, where `tea` is an unseen word in $V$.  
   - Mathematically prove why Laplace smoothing is guaranteed to yield a valid probability distribution.

2. **[Numerical – 6 Marks]**  
   Given a collection of two documents:  
   - $D_1$: `"deep learning"`  
   - $D_2$: `"deep neural learning"`  
   Using the Scikit-Learn TF-IDF formula:  
   $$\text{IDF}(t) = \ln \left( \frac{1 + |D|}{1 + \text{DF}(t)} \right) + 1$$  
   Compute the unnormalized and $L_2$-normalized TF-IDF vector for Document 2 ($D_2$). (Alphabetical vocabulary: `deep`, `learning`, `neural`).

3. **[Analytical / Logicals – 5 Marks]**  
   - Define Perplexity ($PP$) and state its mathematical relationship with Cross-Entropy ($H$).  
   - Explain what is meant by the "Effective Branching Factor". If an $N$-gram model achieves a perplexity score of $28.4$ on a test text, what does this tell us about the model's uncertainty?

4. **[Applied Algorithm – 8 Marks]**  
   A toy corpus contains the following word tokens:  
   `low` (5), `lowest` (2), `new` (6), `newer` (4).  
   - Write out the initial base character representations with end-of-word markers `_`.  
   - Show the first 3 merge operations using the Byte Pair Encoding (BPE) algorithm. Show pair frequency calculations at each step.  
   - Explain how BPE avoids Out-Of-Vocabulary (OOV) errors during test inference.

---

## Solutions for Mock Exam Paper 1

### Solution 1
* **Part 1: Bigram MLE**
  - $C(\text{John}) = 2$, $C(\text{John}, \text{likes}) = 2 \implies P(\text{likes} \mid \text{John}) = \frac{2}{2} = \mathbf{1.0}$
  - $C(\text{likes}) = 2$, $C(\text{likes}, \text{programming}) = 1 \implies P(\text{programming} \mid \text{likes}) = \frac{1}{2} = \mathbf{0.5}$
  - $C(\text{coffee}) = 1$, $C(\text{coffee}, \text{</s>}) = 1 \implies P(\text{</s>} \mid \text{coffee}) = \frac{1}{1} = \mathbf{1.0}$
* **Part 2: Laplace Smoothed Probability for Unseen Token**
  - Unseen pair: $C(\text{likes}, \text{tea}) = 0$. $C(\text{likes}) = 2$, $|V| = 6$.
  $$P_{\text{Laplace}}(\text{tea} \mid \text{likes}) = \frac{0 + 1}{2 + 6} = \frac{\mathbf{1}}{\mathbf{8}} = \mathbf{0.125}$$
* **Part 3: Normalization Proof**
  $$\sum_{w \in V} P_{\text{Laplace}}(w \mid w_{k-1}) = \frac{\sum_{w \in V} C(w_{k-1}, w) + \sum_{w \in V} 1}{C(w_{k-1}) + |V|} = \frac{C(w_{k-1}) + |V|}{C(w_{k-1}) + |V|} = 1 \quad \blacksquare$$

---

### Solution 2
* **Step 1: Vocabulary & Document Frequencies**
  $|D| = 2$. Vocabulary: `['deep', 'learning', 'neural']` ($|V| = 3$).
  - `deep`: in $D_1, D_2 \implies \text{DF} = 2$
  - `learning`: in $D_1, D_2 \implies \text{DF} = 2$
  - `neural`: in $D_2 \implies \text{DF} = 1$
* **Step 2: IDF Calculations**
  $$\text{IDF}(\text{deep}) = \ln(3/3) + 1 = 0 + 1 = \mathbf{1.0}$$
  $$\text{IDF}(\text{learning}) = \ln(3/3) + 1 = 0 + 1 = \mathbf{1.0}$$
  $$\text{IDF}(\text{neural}) = \ln(3/2) + 1 = \ln(1.5) + 1 \approx 0.4055 + 1 = \mathbf{1.4055}$$
* **Step 3: Unnormalized Vector for $D_2$**
  $$\text{TF}(\text{deep}) = 1 \implies 1 \times 1.0 = 1.0$$
  $$\text{TF}(\text{learning}) = 1 \implies 1 \times 1.0 = 1.0$$
  $$\text{TF}(\text{neural}) = 1 \implies 1 \times 1.4055 = 1.4055$$
  $$\mathbf{v}_2 = [1.0,\, 1.0,\, 1.4055]$$
* **Step 4: $L_2$ Normalization**
  $$\|\mathbf{v}_2\|_2 = \sqrt{1.0^2 + 1.0^2 + 1.4055^2} = \sqrt{1 + 1 + 1.97543} = \sqrt{3.97543} \approx \mathbf{1.9938}$$
  $$\text{Normalized: } \left[ \frac{1.0}{1.9938},\, \frac{1.0}{1.9938},\, \frac{1.4055}{1.9938} \right] \approx [\mathbf{0.5016},\, \mathbf{0.5016},\, \mathbf{0.7049}]$$

---

### Solution 3
* **Part 1:** Perplexity is the normalized inverse probability:
  $$PP(W) = P(W)^{-1/n} = 2^{H(W)}$$
  Where $H(W) = -\frac{1}{n} \sum_{k=1}^n \log_2 P(w_k \mid w_{k-N+1:k-1})$.
* **Part 2:** The effective branching factor represents the number of equally likely words among which the model must choose randomly at each step. A perplexity of $28.4$ indicates that predicting the next word in the test text is as difficult for this model as picking uniformly from a bucket of roughly 28 equally likely candidates.

---

### Solution 4
* **Initial Corpus Representation:**
  - `l o w _` : 5
  - `l o w e s t _` : 2
  - `n e w _` : 6
  - `n e w e r _` : 4
* **Merge Step 1:**
  Pair counts:
  - `(l, o)`: $5 + 2 = 7$
  - `(o, w)`: $5 + 2 = 7$
  - `(e, w)`: $6 + 4 = 10$
  - `(n, e)`: $6 + 4 = 10$
  - `(w, _)`: occurs in `low _` (5) and `new _` (6) $\implies \mathbf{11}$
  Most frequent pair is `(w, _)`.
  **Merge 1:** `(w, _)` $\to$ `w_`
* **Merge Step 2:**
  Pair counts:
  - `(n, e)`: $6 + 4 = 10$
  - `(e, w)`: $6 + 4 = 10$
  - `(l, o)`: $5 + 2 = 7$
  - `(o, w)`: 7
  Tie between `(n, e)` and `(e, w)`. Leftmost rule selects `(n, e)`.
  **Merge 2:** `(n, e)` $\to$ `ne`
* **Merge Step 3:**
  Pair `(ne, w)` has frequency 10.
  **Merge 3:** `(ne, w)` $\to$ `new`
* **OOV Resolution:** If an unseen word arrives (e.g., `newer`), BPE breaks it down into known subwords and individual base characters (`new` + `e` + `r`). Because individual characters remain in the base vocabulary, the model can tokenize any string without producing an out-of-vocabulary error.

---

## Mock Exam Paper 2 (Theory, Justifications & Derivations)
**Time:** 60 Minutes | **Max Marks:** 25

### Questions
1. **[Analytical Justifications – 6 Marks]**  
   Explain clearly:
   - Why do discrete text representations (One-Hot and BoW) fail to capture semantic similarity?
   - What is the difference between Linear Interpolation and Katz Back-off when handling the data sparsity problem?

2. **[Definitions / Distinctions – 6 Marks]**  
   Differentiate between:
   - **Stemming** vs. **Lemmatization** (provide an illustrative example of each).
   - **Nominal** vs. **Ordinal** data attributes in NLP corpora.

3. **[PPMI & Cosine Vector Numerical – 7 Marks]**  
   Given the symmetrical co-occurrence counts ($N = 20$):  
   $C(\text{apple}, \text{pie}) = 4$, Marginal $C(\text{apple}) = 5$, Marginal $C(\text{pie}) = 4$.  
   $C(\text{banana}, \text{pie}) = 1$, Marginal $C(\text{banana}) = 2$.  
   - Calculate $\text{PPMI}(\text{apple}, \text{pie})$ and $\text{PPMI}(\text{banana}, \text{pie})$.  
   - Which word pair has a stronger semantic association? Justify mathematically.

4. **[Speech Processing – 6 Marks]**  
   - Define **Place of Articulation** and **Manner of Articulation**. Provide one consonant example for each.  
   - State the Bayes' inversion decoding formula used in an HMM-based speech recognizer and identify its two main model components.

---

## Solutions for Mock Exam Paper 2

### Solution 1
* **Part 1:** One-Hot and BoW representations assign each word to an independent coordinate axis in a $|V|$-dimensional space. Distinct word vectors are completely orthogonal:
  $$\mathbf{v}_{\text{hotel}} \cdot \mathbf{v}_{\text{motel}} = 0 \implies \text{Cosine Similarity} = 0$$
  These representations capture lexical presence and frequency, but cannot represent semantic proximity or shared context.
* **Part 2:**
  - **Linear Interpolation:** Always blends probability mass across all $N$-gram orders simultaneously:
    $$\hat{P} = \lambda_3 P(w_k \mid w_{k-2}, w_{k-1}) + \lambda_2 P(w_k \mid w_{k-1}) + \lambda_1 P(w_k)$$
    Lower-order distributions contribute even when the higher-order count is high.
  - **Katz Back-off:** Relies exclusively on the highest-order $N$-gram whenever sufficient evidence exists ($C > 0$). It falls back to lower-order models **only when** the higher-order count is zero (or below a threshold), redistributing probability mass freed up by absolute discounting.

---

### Solution 2
* **Part 1:**
  - *Stemming:* Uses heuristic rules to strip prefixes and suffixes. Fast, but often produces non-real words.  
    *Example:* `caring` $\to$ `car`
  - *Lemmatization:* Uses full morphological dictionaries and POS tags to reduce words to their true lexical roots.  
    *Example:* `caring` (Verb) $\to$ `care`; `better` (Adjective) $\to$ `good`
* **Part 2:**
  - *Nominal Data:* Discrete categories with no intrinsic ordering.  
    *Example:* POS tags (`NN`, `VB`), Language IDs (`en`, `es`).
  - *Ordinal Data:* Discrete categories with an unambiguous, natural ranking, but without equal intervals.  
    *Example:* Sentiment ratings (`Bad < Neutral < Good`).

---

### Solution 3
Formula:
$$\text{PMI}(w, c) = \log_2 \left( \frac{C(w, c) \cdot N}{C(w) \cdot C(c)} \right), \quad \text{PPMI} = \max(0, \text{PMI})$$

* **Pair 1: (apple, pie)**
  $$\text{PMI}(\text{apple}, \text{pie}) = \log_2 \left( \frac{4 \times 20}{5 \times 4} \right) = \log_2 \left( \frac{80}{20} \right) = \log_2(4) = \mathbf{2.000}$$
  $$\text{PPMI}(\text{apple}, \text{pie}) = \mathbf{2.000}$$

* **Pair 2: (banana, pie)**
  $$\text{PMI}(\text{banana}, \text{pie}) = \log_2 \left( \frac{1 \times 20}{2 \times 4} \right) = \log_2 \left( \frac{20}{8} \right) = \log_2(2.5) \approx \mathbf{1.322}$$
  $$\text{PPMI}(\text{banana}, \text{pie}) = \mathbf{1.322}$$

* **Mathematical Justification:**
  $\text{PPMI}(\text{apple}, \text{pie}) = 2.000 > 1.322 = \text{PPMI}(\text{banana}, \text{pie})$.  
  The pair `(apple, pie)` co-occurs $2^{2.0} = 4\times$ more often than expected by random independent chance, compared to $2^{1.322} = 2.5\times$ for `(banana, pie)`. Thus, `apple` has a significantly stronger statistical association with `pie`.

---

### Solution 4
* **Definitions & Examples:**
  - *Place of Articulation:* The physical location in the vocal tract where airflow is obstructed.  
    *Example:* Bilabial ($/b/$, $/p/$), Alveolar ($/t/$, $/d/$).
  - *Manner of Articulation:* How the airstream is constricted or released.  
    *Example:* Stop/Plosive (complete blockage followed by release: $/p/, /k/$), Fricative (sustained turbulent friction: $/s/, /f/$).
* **ASR Decoding Formula:**
  $$\hat{W} = \arg\max_W P(W \mid O) = \arg\max_W \underbrace{P(O \mid W)}_{\text{Acoustic Model (HMM)}} \cdot \underbrace{P(W)}_{\text{Language Model ($N$-gram)}}$$
  - **Acoustic Model $P(O \mid W)$:** Evaluates the probability of observing the continuous acoustic feature frames $O$ given an underlying phone/word sequence $W$.
  - **Language Model $P(W)$:** Evaluates the prior probability and syntactic likelihood of the word sequence $W$.

---

## Final Quick-Review Checklist Before Entering the Exam Hall
- [ ] Log base conversion: $\log_2(x) = \frac{\ln(x)}{\ln(2)} = \frac{\ln(x)}{0.693147}$.
- [ ] Perplexity is $2^{H(W)}$, where $H(W) = -\frac{1}{n}\sum \log_2 P(\cdot)$. Lower is always better.
- [ ] Normalization proof for Laplace smoothing: remember to show the $+|V|$ in the denominator balances the $\sum_{w \in V} 1 = |V|$ in the numerator.
- [ ] In BPE, remember that word boundaries are preserved by appending `_` to each word before merging.
- [ ] For Scikit-Learn TF-IDF, remember the `+1` inside the log and the `+1` outside: $\text{IDF} = \ln\left(\frac{1+|D|}{1+\text{DF}}\right) + 1$, and always finish with $L_2$ vector normalization.
- [ ] Distinct one-hot vectors always have a dot product of 0 (orthogonal), which is why they cannot represent semantic similarity.
