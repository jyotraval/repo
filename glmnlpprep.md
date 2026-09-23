# NLP Mid-Semester Exam — Complete Preparation Guide

> **Course:** Natural Language Processing (20IC403T) — ICT, Semester 7
> **Institute:** Pandit Deendayal Energy University (PDEU), Gandhinagar
> **Instructor:** Dr. Jigar Shah (Asst. Prof., ICT)
> **Mid-sem:** 25 marks · 60 minutes
> **Syllabus (per professor's email):** Unit 1 (Introduction & Pre-processing) + Unit 2 (Vectorization & N-gram Language Models)
> **Coverage:** All PPTs up to Week 9
> **Question style (per professor):** Numericals, Analyticals, Logicals, Justifications

---

## How to Use This Guide

1. **Section A — Exam Intelligence:** Read this *first*. It tells you exactly what was asked in 2024 and 2025, what is most likely this year, and which topics carry the highest marks weight.
2. **Section B — Unit 1 Concept Notes:** Full theory of every topic from Week 1 to Week 3 PPTs, plus the speech-processing fundamentals that PYQs repeatedly test (place/manner of articulation, word boundary detection, Argmax, HMM).
3. **Section C — Unit 2 Concept Notes:** Full theory of vectorization (one-hot, BoW, TF-IDF, PMI/PPMI, cosine similarity) and N-gram language models (MLE, perplexity, smoothing, back-off, interpolation).
4. **Section D — Numerical Worked Examples:** Step-by-step solutions of every numerical pattern that has appeared or can appear: BPE merges, cosine similarity, PPMI, TF-IDF, bigram/trigram MLE probability, perplexity (direct + cross-entropy), Laplace smoothing.
5. **Section E — PYQ Solutions (2024 & 2025):** Model answers with the correct marks-split for every question asked in the last two years.
6. **Section F — Python Code Snippets:** Quick reference of the exact library calls (NLTK / spaCy / TextBlob / sklearn) used in the lab-style questions.
7. **Section G — Formula Cheat-Sheet:** Every formula on one page. Memorise this.
8. **Section H — Last-Minute Checklist:** Read this the morning of the exam.

---

## Section A — Exam Intelligence & PYQ Pattern Analysis

### A.1 Format of the Upcoming Mid-sem

Based on the professor's email and the 2025 PYQ (which is the most recent and matches the 25-mark / 60-minute pattern):

| Attribute | Value |
|---|---|
| Total marks | **25** |
| Time | **60 minutes** |
| Number of questions | **3** (typical; one may have an OR option) |
| Question types | Numericals, analyticals, logicals, justifications |
| Units covered | Unit 1 (Intro + Pre-processing) + Unit 2 (Vectorization + N-gram LMs) |
| PPT coverage | Weeks 1 → 9 |

> **Note on the 2024 vs 2025 pattern:** The 2024 paper was 50 marks / 2 hours with 5 questions; the 2025 paper was 25 marks / 60 minutes with 3 questions. The 2025 pattern is the one you should expect, because it matches the 25-mark mid-sem weight declared in the Week 1 PPT teaching scheme.

### A.2 Topic-wise PYQ Frequency (2024 + 2025 combined)

| Topic | Asked in 2024 | Asked in 2025 | Probability this year |
|---|:---:|:---:|---|
| Components of NLP system | — | ✅ Q1 (5 marks) | **High** |
| Word boundary detection | ✅ Q4(B) | ✅ Q2 (10 marks) | **Very high** |
| HMM in speech recognition | ✅ Q3(B) | ✅ Q2 OR (10 marks) | **Very high** |
| Place & manner of articulation | ✅ Q2(A) | ✅ Q3(e) (2 marks) | **Very high** |
| Tokenization (definition + application) | ✅ Q3(A) | ✅ Q3(a) (2 marks) | **Very high** |
| Stemming (definition + differentiate) | ✅ Q2(B) | ✅ Q3(b) (2 marks) | **Very high** |
| Morphological analysis | ✅ Q2(B) | ✅ Q3(c) (2 marks) | **Very high** |
| Computational grammar | ✅ Q4(A) | ✅ Q3(d) (2 marks) | **Very high** |
| POS tagging | ✅ Q1(B) | — | Medium |
| Argmax computation (bigram) | ✅ Q1(C) | — | Medium (but explicitly in syllabus) |
| Regular expressions (email) | ✅ Q1(A) | — | Medium |
| Preprocessing pipeline | ✅ Q4(A) OR | — | Medium |
| MP3 vs FLAC | ✅ Q4(B) OR | — | Medium |
| Text classification vs MT datasets | ✅ Q5(A) | — | Lower |
| Speech recognition components | ✅ Q5(A) OR | — | Medium |
| Data attribute types (nominal/ordinal/interval/ratio) | ✅ Q5(B) | — | Medium |
| JSON vs CSV file formats | ✅ Q5(B) OR | — | Medium |
| **Vectorization (TF-IDF, BoW, PMI)** | — | — | **High** (in syllabus, not yet asked) |
| **N-gram LMs & perplexity** | — | — | **High** (in syllabus, not yet asked) |
| **BPE numerical** | — | — | **High** (in syllabus, professor said "numericals") |
| **Smoothing (Laplace)** | — | — | **High** (in syllabus, professor said "numericals") |

### A.3 Strategic Prediction for This Year

Given that (a) professor explicitly said "Questions will be based on **numericals**, analyticals, logicals and justifications" and (b) the 2025 paper had **no numericals**, this year's paper is almost certain to include at least one numerical. The most likely numericals are:

1. **BPE merges** — given a small training corpus, perform k merges (Week 3 PPT has this exact example).
2. **N-gram MLE probability** — compute P(W) for a test sentence using a given corpus (Week 6-7 PPT has this exact example).
3. **Perplexity** — compute PP(W) using direct formula and via cross-entropy (Week 6-7 PPT has this exact example).
4. **Laplace (Add-1) smoothing** — compute smoothed bigram probabilities and perplexity (Week 8-9 PPT has this exact example).
5. **TF-IDF** — compute unnormalised + L2-normalised TF-IDF vectors for a 2-document toy corpus (Week 5 PPT has this exact example).
6. **PPMI** — compute PMI/PPMI matrix for a small co-occurrence matrix (Week 5 PPT has this exact example).
7. **Cosine similarity** — compute cosine similarity between two word vectors (Week 5 PPT has this exact example).

The 3 most likely to actually appear, in order: **Perplexity (bigram) → Laplace smoothing → BPE merges**.

### A.4 Time-Allocation Strategy (60 min, 25 marks)

- **Marks-per-minute target:** ~0.42 marks/min (so a 10-mark question deserves ~24 min, a 5-mark question ~12 min, a 2-mark definition ~5 min).
- Suggested split if paper is {5, 10, 10}:
  - 5-mark Q1: ~12 minutes
  - 10-mark Q2: ~22 minutes
  - 10-mark Q3: ~22 minutes
  - Buffer / revision: ~4 minutes
- If a numerical appears, **write the formula first, then plug in numbers** — partial credit is almost always given for the correct formula even if the arithmetic slips.

### A.5 Mark-Allocation Heuristics for Written Answers

| Marks | Expected depth |
|:---:|---|
| 2 marks | Definition (1–2 lines) + 1 small example or 1 formula |
| 3 marks | Definition + formula + worked micro-example OR 3 distinct bullet points |
| 5 marks | Definition + 3–4 properties/methods + example + diagram/equation |
| 6 marks | Definition + comparison table + 2 examples + application + limitations |
| 10 marks | Full treatment: definition, formula, step-by-step example, diagram, advantages, disadvantages, applications |

---

## Section B — Unit 1: Introduction & Pre-processing

### B.1 What is Natural Language Processing?

**Natural language** is any language that evolved naturally through human use (English, Hindi, Mandarin, Gujarati, etc.), as opposed to artificial languages such as programming languages (Python, C) or formal mathematical notations. Natural languages are unstructured, ambiguous, context-dependent, and continuously evolving — properties that make them far harder for machines to process than formal languages.

**Natural Language Processing (NLP)** is the sub-field of Artificial Intelligence that aims to make computers understand, interpret, manipulate, and generate human language in a useful way. More specifically, NLP attempts to design, implement and test systems that process natural languages for practical applications such as text translation, text summarisation, speech-to-text conversion, chatbots, sentiment analysis, question answering, and information extraction. The field has evolved from rule-based and statistical approaches (conventional NLP) to machine-learning, deep-learning, and transformer-based approaches (modern NLP, including LLMs such as GPT and Gemini).

The dual goal of NLP is captured succinctly: **making computers understand what we write or speak, and making computers write or speak.** This dual goal maps to the two broad sub-fields **Natural Language Understanding (NLU)** and **Natural Language Generation (NLG)**.

### B.2 NLP Tasks (memorise this list — asked in 2025 Q1)

Common NLP tasks that the professor listed in the Week 1 PPT are:

1. **Sentiment Analysis** — classifying text as positive / negative / neutral (used in product reviews, social media monitoring).
2. **Machine Translation** — translating text from one language to another (Google Translate, e.g., English → Hindi).
3. **Text Classification** — assigning predefined categories to text (spam detection, news categorisation).
4. **Text Summarisation** — producing a shorter version of a long document while preserving key information.
5. **Question Answering** — building systems that answer user questions in natural language (BERT-based QA, retrieval-augmented generation).
6. **Text Entailment** — deciding whether one sentence (the premise) logically implies another (the hypothesis).
7. **Named Entity Recognition (NER)** — locating and classifying named entities (persons, organisations, locations) in text.
8. **Chatbots** — conversational agents that interact with users (ChatGPT, customer-service bots).
9. **Language Modelling** — predicting the next word in a sequence; the foundational task behind LLMs.

A **Large Language Model (LLM)** is an advanced AI system built on deep learning and the transformer architecture, trained on vast amounts of text to predict the next word in a sequence. Popular examples include OpenAI's GPT family and Google's Gemini. LLMs contain billions of internal parameters ("weights") that act like the synapses of a human brain and are responsible for the model's emergent abilities (in-context learning, chain-of-thought reasoning, code generation, etc.).

### B.3 NLP Paradigms (mapping problems to ML settings)

Most NLP problems can be mapped onto three classic ML paradigms:

| NLP problem | ML paradigm |
|---|---|
| Sentiment analysis, news-article grouping, spam detection | **Text Classification** (multi-class / multi-label) |
| Named entity recognition, code-mixing detection, POS tagging | **Sequence Labelling** (token-level classification) |
| Machine translation, summarisation, chatbots | **Text Generation** (seq2seq) |

This mapping is not merely academic — it determines which loss function, which evaluation metric, and which model architecture is appropriate.

### B.4 NLP Progression Timeline (high-level milestones)

| Era | Approach | Representative work |
|---|---|---|
| 1950s | Rule-based / symbolic | ELIZA chatbot, early MT |
| 1990s | Statistical NLP | HMMs, IBM alignment models, n-gram LMs |
| 2000s | Linear ML | CRFs, MaxEnt, SVM for text |
| 2013 | Word embeddings | **Word2Vec** (Mikolov et al.) |
| 2014 | Sequence-to-sequence | Sutskever et al. — encoder-decoder RNNs |
| 2015 | Attention | Bahdanau et al. — attention for MT |
| 2017 | Transformer | Vaswani et al. — "Attention is all you need" |
| 2018 | Pre-trained contextual embeddings | **ELMo**, then **BERT** (Bidirectional Encoder Representations from Transformers) |
| 2018–20 | Generative pre-training | **GPT** family (Generative Pre-trained Transformer) |
| 2022+ | Instruction-tuned LLMs / chatbots | ChatGPT, Gemini, Llama |

BERT = **B**idirectional **E**ncoder **R**epresentations from **T**ransformers.
GPT = **G**enerative **P**re-trained **T**ransformer.

### B.5 Components of an NLP System  *(PYQ 2025 Q1, 5 marks)*

A complete NLP system is a pipeline of layered analysis stages. The five canonical components are:

1. **Lexical Analysis (Tokenisation)** — breaks raw text into tokens (words, sub-words, punctuation). It also handles lowercasing, punctuation stripping, and OOV handling. This is the first step of every NLP pipeline and is essential because all downstream stages operate on tokens, not on raw characters.

2. **Syntactic Analysis (Parsing)** — analyses the grammar of the token stream and produces a parse tree showing how words combine into phrases and clauses. This stage reveals grammatical roles (subject, object, verb) and dependencies. Tools: dependency parsers, constituency parsers (spaCy, Stanford CoreNLP).

3. **Semantic Analysis** — extracts the meaning of the sentence: word-sense disambiguation, semantic role labelling, and resolving entity references. The goal is to map the parse tree to a meaning representation (e.g., First-Order Logic, lambda calculus, or a vector embedding).

4. **Discourse Integration / Pragmatic Analysis** — deals with context that lies *outside* the single sentence: pronoun resolution (coreference), conversational implicature, and intention recognition. Without pragmatic analysis, a chatbot cannot tell whether "Can you?" is a question about ability or a polite request.

5. **Application Layer** — the task-specific top of the pipeline (sentiment classifier, MT engine, QA system, etc.). This is what the end user interacts with.

**Differences among them (the crux of the question):**

| Component | Level | Input | Output | Question it answers |
|---|---|---|---|---|
| Lexical | Word | Raw text | Tokens | "What are the units?" |
| Syntactic | Sentence | Tokens | Parse tree | "Is it grammatical? How is it structured?" |
| Semantic | Sentence | Parse tree | Meaning representation | "What does it mean?" |
| Discourse / Pragmatic | Document / dialogue | Sentences | Resolved references, intents | "What was intended in context?" |
| Application | Task | Any of the above | Task output (label, translation, answer) | "What should I do with this?" |

### B.6 Challenges in NLP

The challenges that make NLP harder than, say, image classification, include:

- **Ambiguity** — at every level: lexical ("bank" = river/financial), syntactic ("I saw the man with the telescope"), semantic, and pragmatic.
- **Disparity between languages** — word order, morphology, and writing systems vary enormously; models trained on English do not transfer to morphologically rich languages like Turkish or Hindi.
- **Domain dependence** — a model trained on news text fails on medical records or legal contracts.
- **Lack of labelled data** — supervised NLP needs expensive human annotations.
- **Spelling / OCR / speech-recognition noise** — real-world text is dirty.
- **Long-tail vocabulary** — natural language follows Zipf's law: a small number of words occur very often, but a long tail of rare words accounts for a large fraction of unique tokens.
- **Common-sense and world knowledge** — many inferences require knowledge not present in the text.
- **Computational scale** — modern LLMs need GPU clusters to train.

### B.7 Text Pre-processing Pipeline

Text pre-processing is an essential step in NLP that involves cleaning and transforming unstructured text data to prepare it for analysis. The standard pipeline (covered across Weeks 2–3 PPTs) is:

```
Raw text
   │
   ├── 1. Tokenisation         (split into tokens)
   ├── 2. Lowercasing          (case normalisation)
   ├── 3. Stop-word removal    (remove "the", "is", "a", ...)
   ├── 4. Stemming / Lemmatisation  (reduce to root form)
   ├── 5. Punctuation & number removal
   ├── 6. POS tagging          (optional, but useful)
   ├── 7. NER                  (optional)
   └── 8. Vectorisation        (BoW / TF-IDF / embeddings)
```

After pre-processing, the cleaned tokens are passed to a **statistical inference** stage (model) which either (i) infers a decision (supervised — RNN, Transformer; or unsupervised — LSA) or (ii) embeds them into a vector space for downstream use.

**Important caveat from the PPT:** With pre-trained language models (BERT, GPT), the *only* pre-processing step typically applied is tokenisation (often sub-word). Stop-word removal, stemming, and lemmatisation are *not* done — the model learns to handle them itself. This is a meaningful shift from the pre-2018 era.

### B.8 Tokenisation *(PYQ 2024 Q3(A), 2025 Q3(a))*

**Definition (2-mark answer):** Tokenisation is the fundamental NLP process of breaking a stream of text into smaller units called **tokens** using a set of predetermined rules. A token may be a word, a sub-word, a character, or even a punctuation mark, depending on the tokeniser.

**Token vs Type (Week 2 PPT):**

> "they lay back on the San Francisco grass and looked at the stars and their"

- **Type** = an element of the vocabulary (unique word form).
- **Token** = an instance of a type in running text.
- This sentence has **15 tokens** but only **13 types** (because "the", "and", "their" repeat).

**5-mark answer must include the methods below:**

#### B.8.1 Whitespace Tokenisation

Simplest method: split text wherever whitespace (spaces, tabs, newlines) occurs.

```python
from nltk.tokenize import WhitespaceTokenizer
text = "Hello, world! This is NLP."
tokens = WhitespaceTokenizer().tokenize(text)
# ['Hello,', 'world!', 'This', 'is', 'NLP.']
```

**Five major issues** (memorise these — they were explicitly listed in the PPT):

1. **Multi-word expressions are split incorrectly.** "New York University" → `['New', 'York', 'University']` — the entity meaning is lost. Same for "San Francisco", "Los Angeles", "ice cream".
2. **Punctuation stays attached to words.** `"Hello, world!"` → `['Hello,', 'world!']` instead of `['Hello', ',', 'world', '!']`. This complicates downstream NER and sentiment analysis.
3. **Languages without spaces fail completely.** Chinese, Japanese, Thai, Korean have no inter-word spaces — whitespace tokenisation produces a single token per sentence.
4. **Special constructs are broken.** Email addresses (`john.doe@email.com`), URLs, phone numbers `(800) 234-2333`, dates `Mar 11, 1983`, and hyphenated words `state-of-the-art` are fragmented.
5. **Retrieval problems.** A search for "York University" might match documents containing "New York University" because both contain the tokens "York" and "University" separately.

**Solutions:** Use sub-word tokenisation (BPE, WordPiece, SentencePiece) or production libraries (spaCy, NLTK's `word_tokenize`, HuggingFace tokenisers).

#### B.8.2 Worked Example (5-mark pattern, PYQ 2024 Q3(A))

**Question:** Illustrate word-tokenisation on:
> "Natural language processing is a field of computer science."

**Model answer:**

Step 1 — Whitespace split (naive):
```
['Natural', 'language', 'processing', 'is', 'a', 'field', 'of', 'computer', 'science.']
```
Notice `science.` keeps the period attached — this is an issue.

Step 2 — Rule-based / `word_tokenize` (NLTK Punkt):
```
['Natural', 'language', 'processing', 'is', 'a', 'field', 'of', 'computer', 'science', '.']
```
Now the period is a separate token, suitable for downstream parsing.

Step 3 — Remove stop-words + punctuation:
```
['Natural', 'language', 'processing', 'field', 'computer', 'science']
```

Step 4 — Lowercase + lemmatise (optional):
```
['natural', 'language', 'processing', 'field', 'computer', 'science']
```

Step 5 — Sub-word (BPE) tokenisation might further split rare words; here all words are common so no splits occur.

**Key takeaway:** tokenisation is *irreversible* — once we strip casing and punctuation, we cannot perfectly recover the original raw text.

#### B.8.3 Sub-word Tokenisation & BPE *(critical numerical topic)*

Sub-word tokenisation breaks rare words into meaningful sub-word units, handles compound words, and elegantly manages **OOV (Out-of-Vocabulary)** words — words the model never saw during training. The most important sub-word algorithm is **Byte-Pair Encoding (BPE)**.

**Key terms:**
- **Morpheme** — the smallest meaning-bearing unit of a language. E.g., `cats` = `cat` + `-s` (plural morpheme). `unlikeliest` = `{un-, likely, -est}`.
- **Morphology** — the study of how words are built from morphemes.
- **Word forms** — variations of a word that express grammatical categories (tense, case, number, gender).

**BPE algorithm — Token Learner (training):**

1. Pre-tokenise the corpus into words and append a special end-of-word symbol `_` (or `</w>`) to each word, so that word boundaries are preserved after merges.
2. Initialise the vocabulary with the set of all individual characters seen in the corpus (plus `_`).
3. Count all adjacent token pairs in the corpus, weighted by word frequency.
4. Choose the pair `(A, B)` with the highest count.
5. Add a new merged symbol `AB` to the vocabulary.
6. Replace every occurrence of `(A, B)` in the corpus with `AB`.
7. Repeat steps 3–6 until **k merges** have been performed (k is a hyper-parameter; choosing it is an open research question).

**BPE algorithm — Token Segmenter (testing):**

Run the learned merges greedily, *in the order they were learned*, on the test sentence. First segment each test word into characters, then apply merge rule 1, then merge rule 2, and so on.

**Why is BPE useful for OOV?** Even if a test word was never seen, BPE can still tokenise it by falling back to character-level tokens that *were* in the vocabulary. E.g., if `b` and `l` are individual characters in the vocabulary (they were initialised as such), then `readable` (an OOV word) becomes `read a b l e _` — the model has seen all sub-word pieces even though it never saw `readable` as a whole.

#### B.8.4 BPE Worked Example *(from Week 3 PPT)*

**Training corpus & frequencies:**

| Word | Frequency |
|---|---:|
| read | 3 |
| reads | 2 |
| reader | 2 |
| reading | 2 |
| unread | 1 |
| readers | 1 |

**Step 1:** Represent each word as characters followed by `_`:
```
read_       (×3)
reads_      (×2)
reader_     (×2)
reading_    (×2)
unread_     (×1)
readers_    (×1)
```

**Step 2:** Initial vocabulary = `{_, a, d, e, g, i, n, r, s, u}`.

**Step 3:** Perform 6 merges. At each step, pick the most frequent adjacent pair (weighted by word frequency). If there is a tie, prefer the leftmost pair from the word `read`; otherwise choose alphabetically.

**Result of the 6 merges (memorise this table):**

| Merge # | Most frequent pair | New token |
|:---:|---|---|
| 1 | (r, e) | `re` |
| 2 | (re, a) | `rea` |
| 3 | (rea, d) | `read` |
| 4 | (read, _) | `read_` |
| 5 | (read, e) | `reade` |
| 6 | (reade, r) | `reader` |

**Final vocabulary** = initial 10 characters + 6 merged tokens = `{_, a, d, e, g, i, n, r, s, u, re, rea, read, read_, reade, reader}`.

**Testing on new words (apply learned merges in order):**

| Test word | Initial char form | Final BPE tokens |
|---|---|---|
| read | `r e a d _` | `read_` (in vocab) |
| reader | `r e a d e r _` | `reader _` |
| readers | `r e a d e r s _` | `reader s _` |
| reading | `r e a d i n g _` | `read i n g _` |
| unread | `u n r e a d _` | `u n read_` |
| **readable (OOV)** | `r e a d a b l e _` | `read a b l e _` |
| **reread (OOV)** | `r e r e a d _` | `re read_` |
| **unreader (OOV)** | `u n r e a d e r _` | `u n reader _` |

**Decoding:** concatenate tokens and remove `_`. For `read a b l e _` → `readable`. ✓ Matches original.

> **Crucial insight:** In `readable`, the characters `b` and `l` never appeared in any *learned sub-word*, but they were in the initial character vocabulary, so BPE falls back to them. **BPE never produces an OOV token** — it always falls back to characters. This is one of the key properties that made BPE the de-facto tokeniser for transformer LLMs (GPT-2, GPT-3, GPT-4).

### B.9 Stop-word Removal

Stop words are commonly used words in a language that are filtered out before or after processing of natural language text because they carry little discriminative information. Examples in English: `a, the, is, are, in, on, of, and, to, ...`

**Why remove them?** They:
- inflate the vocabulary size,
- dominate frequency counts (e.g., `the` is the most frequent word in any English corpus),
- add noise to BoW / TF-IDF vectors without contributing meaning.

**Python (NLTK):**
```python
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize
text = "S&P and NASDAQ are the two most popular indices in US"
tokens = word_tokenize(text)
tokens_without_sw = [w for w in tokens if w not in stopwords.words('english')]
# Output: ['S', '&', 'P', 'NASDAQ', 'two', 'popular', 'indices', 'US']
```

**Caution:** `S&P` was tokenised into `['S', '&', 'P']` by `word_tokenize`, so the output looks odd. This shows that *order matters* — NER should ideally be done before stop-word removal to keep multi-word entities intact.

### B.10 Stemming vs Lemmatization *(PYQ 2024 Q2(B), 2025 Q3(b)(c))*

| Aspect | Stemming | Lemmatization |
|---|---|---|
| **Definition** | Heuristic process that chops off suffixes / prefixes to reduce a word to a base form called a **stem**. | Sophisticated process that transforms a word to its base dictionary form called a **lemma**, considering the word's meaning, context, and Part-of-Speech. |
| **Approach** | Rule-based (e.g., Porter, Snowball, Lancaster stemmers). | Dictionary + morphological analysis (e.g., WordNet lemmatiser, spaCy lemmatiser). |
| **Output** | Stem — may not be a real word. | Lemma — always a real dictionary word. |
| **Speed** | Fast (string operations). | Slower (dictionary lookup + POS). |
| **Accuracy** | Lower. | Higher. |
| **Context-aware?** | No. | Yes. |
| **Example 1** | `studies` → `studi` (Porter). | `studies` → `study`. |
| **Example 2** | `running` → `run`. | `running` → `run` (verb) / `running` → `running` (noun, as in "the running of the river"). |
| **Example 3** | `better` → `better` (Porter fails). | `better` → `good` (lemmatiser knows it's a comparative of "good"). |
| **Python** | `SnowballStemmer('english').stem('Stemming')` → `'stem'` | `Word('has').lemmatize()` → `'ha'` (TextBlob has quirks); spaCy is more accurate. |

**Sample Python (Stemming — SnowballStemmer):**
```python
from nltk.stem.snowball import SnowballStemmer
from nltk.tokenize import word_tokenize
text = "It's a Stemming testing"
parsed = word_tokenize(text)
stemmer = SnowballStemmer('english')
[(w, stemmer.stem(w)) for w in parsed if w.lower() != stemmer.stem(w)]
# [('Stemming', 'stem'), ('testing', 'test')]
```

**Sample Python (Lemmatisation — TextBlob):**
```python
from textblob import TextBlob
text = "This world has a lot of faces"
parsed = TextBlob(text).words
[(w, w.lemmatize()) for w in parsed if w != w.lemmatize()]
# [('has', 'ha'), ('faces', 'face')]
```
(Note: TextBlob's default lemmatiser is not perfect — `has` → `ha` is wrong; the correct lemma is `have`. For serious work, use spaCy.)

**Morphological Analysis (PYQ 2024 Q2(B), 2025 Q3(c)) — definition (2 marks):**
Morphological analysis is the process of breaking a word into its constituent **morphemes** — the smallest meaning-bearing units of a language. It considers both the *stem* and the *affixes* (prefixes, suffixes, infixes) and their grammatical roles (tense, number, case, gender). For example, `unhappiness` = `un-` (negative prefix) + `happy` (root) + `-ness` (nominalising suffix). Morphological analysis is more sophisticated than stemming because it uses linguistic knowledge rather than heuristic chopping.

**Difference between Stemming and Morphological Analysis (PYQ pattern, 2.5 + 2.5 marks):**

- **Stemming** is a crude, heuristic operation that strips suffixes from words using fixed rules. It does not consult a lexicon and does not understand the part-of-speech of the input. Example: `running → run` (correct), but `studies → studi` (wrong, not a real word).
- **Morphological analysis** is a deeper, lexicon-driven process that decomposes a word into morphemes and identifies the grammatical role of each (root, plural marker, tense marker, etc.). Example: `cats` → root `cat` + plural morpheme `-s`. It produces linguistically meaningful units, not just shorter strings.

### B.11 Part-of-Speech (POS) Tagging *(PYQ 2024 Q1(B))*

**Definition:** POS tagging is the process of assigning a grammatical category — such as noun, verb, adjective, adverb, pronoun, preposition, conjunction, participle, or article — to each word in a sentence. It is a sequence-labelling task: the input is a sequence of tokens and the output is a sequence of POS tags of the same length.

**Why POS-tag?** It helps machines understand the syntactic structure of sentences, which is essential for downstream tasks such as machine translation, information extraction, question answering, and text-to-speech conversion (where word pronunciation depends on POS).

**Eight basic parts of speech** (Dionysius Thrax of Alexandria, c. 100 BC):
noun, verb, pronoun, preposition, adverb, conjunction, participle, article.

**Ambiguity example (the crux of POS tagging):**
- VERB: "Book that flight." (`book` = verb, "to reserve")
- NOUN: "Hand me that book." (`book` = noun, "a written work")

The same surface form `book` has different POS tags in different contexts. The goal of POS tagging is to **resolve such ambiguities** by choosing the proper tag for the context.

**Penn Treebank tagset (Marcus et al., 1993):** 36 primary POS tags, including:
- `NN` — singular noun, `NNS` — plural noun, `NNP` — singular proper noun, `NNPS` — plural proper noun
- `VB` — base verb, `VBD` — past tense, `VBG` — gerund/present participle, `VBN` — past participle, `VBP` — non-3rd-sg present, `VBZ` — 3rd-sg present
- `JJ` — adjective, `JJR` — comparative, `JJS` — superlative
- `RB` — adverb, `IN` — preposition/subordinating conjunction, `DT` — determiner, `CD` — cardinal number, `PRP` — personal pronoun

**Python (TextBlob):**
```python
from textblob import TextBlob
text = 'Google is looking at buying U.K. startup for $1 billion'
TextBlob(text).tags
# [('Google', 'NNP'), ('is', 'VBZ'), ('looking', 'VBG'),
#  ('at', 'IN'),    ('buying', 'VBG'), ('U.K.', 'NNP'),
#  ('startup', 'NN'), ('for', 'IN'),    ('1', 'CD'),
#  ('billion', 'CD')]
```

**Methods for POS tagging (memorise — asked in 2024-style questions):**
1. **Hidden Markov Models (HMM)** — generative, uses transition + emission probabilities.
2. **Maximum Entropy Markov Models (MEMM)** — discriminative, conditional probability.
3. **Conditional Random Fields (CRF)** — discriminative, models the entire label sequence jointly.
4. **RNNs, LSTMs, Transformers** — recent deep-learning approaches (BiLSTM-CRF was the SOTA before BERT).

**Evaluation metrics:**
- **Accuracy** — overall fraction of correctly tagged tokens.
- **Macro-F1** — gives equal importance to each tag class, useful when tag distribution is skewed (e.g., `NN` is far more common than `SYM`).

### B.12 Named Entity Recognition (NER)

NER locates and classifies named entities in text into predefined categories such as **person, organisation, location, time expression, quantity, monetary value, percentage**. While POS tags are assigned to individual words, a named entity is often an entire multi-word phrase: "Marie Curie" (person), "New York City" (location), "Stanford University" (organisation).

**Python (spaCy):**
```python
import spacy
nlp = spacy.load('en_core_web_sm')
text = 'Google is looking at buying U.K. startup for $1 billion'
for ent in nlp(text).ents:
    print("Entity:", ent.text)
# Entity: Google
# Entity: U.K.
# Entity: $1 billion
```

Visualisation with `displaCy`:
```python
from spacy import displacy
displacy.render(nlp(text), style="ent", jupyter=True)
```

### B.13 Other Optional Pre-processing Steps

1. **Dependency parsing** — assigns a syntactic structure to a sentence by linking each word to its head (governor). Useful for relation extraction and sentence simplification.
2. **Coreference resolution** — connecting tokens that refer to the same entity. Example: "Marie Curie … she … her" all refer to the same person.
3. **Triplet extraction** — extracting (subject, verb, object) triplets from a sentence. Useful for building knowledge graphs.
4. **Relation extraction** — a broader form of triplet extraction where entities can have multiple, typed relationships (e.g., `born_in(Marie Curie, Warsaw)`).

**All-in-one spaCy pipeline:**
```python
import spacy, pandas as pd
nlp = spacy.load('en_core_web_sm')
text = 'Google is looking at buying U.K. startup for $1 billion'
doc = nlp(text)
pd.DataFrame([[t.text, t.is_stop, t.lemma_, t.pos_] for t in doc],
             columns=['Token','is_stop_word','lemma','POS'])
```
When `nlp` is called on text, spaCy first tokenises it into a `Doc` object, then runs the default pipeline: **tagger → parser → entity recognizer**. Each component returns the processed `Doc`, which is passed to the next.

### B.14 Regular Expressions *(PYQ 2024 Q1(A), 3 marks)*

A **regular expression (RE or regex)** is a sequence of characters that defines a search pattern. In NLP, regex is widely used for pattern-matching tasks such as email extraction, URL detection, phone-number normalisation, and date parsing. Python's `re` module supports the standard regex syntax.

**Question (2024 Q1-A):** Design a regex to detect email addresses from:
> "I am a student with email id abc@xyz.com and my friend's email is abc.def@xyz.co.in."

**Model answer:**

The local part (before `@`) can contain letters, digits, dots, underscores, percent, plus, hyphen. The domain part (after `@`) can contain letters, digits, dots, and hyphens. A country-code TLD may be two parts (`.co.in`).

```python
import re
text = "I am a student with email id abc@xyz.com and my friend's email is abc.def@xyz.co.in."
pattern = r'[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}(?:\.[A-Za-z]{2,})*'
re.findall(pattern, text)
# Output: ['abc@xyz.com', 'abc.def@xyz.co.in']
```

**Explanation of the regex (3-mark depth):**
- `[A-Za-z0-9._%+-]+` — local part: one or more letters, digits, dots, underscores, percent, plus, or hyphen.
- `@` — literal "@".
- `[A-Za-z0-9.-]+` — domain name: letters, digits, dots, hyphens.
- `\.[A-Za-z]{2,}` — TLD: a dot followed by at least 2 letters.
- `(?:\.[A-Za-z]{2,})*` — optional additional country-code TLDs (e.g., `.in`, `.uk`).

### B.15 Speech Processing Fundamentals *(critical — tested every year)*

Although professor's mid-sem email says "Unit 1 (Introduction and Pre-processing)", the original Unit 1 syllabus (visible on slide 2 of Week 1 PPT) explicitly includes **Basics of Speech Processing, Place and Manner of Articulation, Word Boundary Detection, Argmax-based computations, HMM and Speech Recognition**. **Both PYQs (2024 and 2025) test these topics heavily**, so they must be prepared.

#### B.15.1 Place and Manner of Articulation *(PYQ 2024 Q2(A), 2025 Q3(e))*

**Place of articulation** = *where* in the vocal tract a speech sound is constricted. The major places are:

| Place | Description | Example consonants (English) |
|---|---|---|
| **Bilabial** | Both lips | /p/, /b/, /m/ |
| **Labio-dental** | Lower lip + upper teeth | /f/, /v/ |
| **Dental** | Tongue tip + upper teeth | /θ/ (think), /ð/ (this) |
| **Alveolar** | Tongue tip + alveolar ridge (just behind upper teeth) | /t/, /d/, /s/, /z/, /n/, /l/ |
| **Post-alveolar / Palato-alveolar** | Tongue blade + area just behind alveolar ridge | /ʃ/ (ship), /ʒ/ (measure), /tʃ/ (chip), /dʒ/ (judge) |
| **Palatal** | Tongue body + hard palate | /j/ (yes) |
| **Velar** | Tongue back + soft palate (velum) | /k/, /g/, /ŋ/ (sing) |
| **Glottal** | Vocal folds themselves | /h/, glottal stop /ʔ/ |

**Manner of articulation** = *how* the airstream is constricted:

| Manner | Description | Example |
|---|---|---|
| **Plosive / Stop** | Complete closure then sudden release | /p/, /b/, /t/, /d/, /k/, /g/ |
| **Fricative** | Narrowing produces turbulent airflow | /f/, /v/, /s/, /z/, /ʃ/, /ʒ/, /θ/, /ð/, /h/ |
| **Affricate** | Stop closure released slowly into a fricative | /tʃ/, /dʒ/ |
| **Nasal** | Oral cavity closed; air through nose | /m/, /n/, /ŋ/ |
| **Approximant** | Articulators close but no turbulence | /ɹ/, /l/, /j/, /w/ |
| **Trill / Tap** | Brief vibration of articulator | /r/ (Scottish), /ɾ/ (Spanish "pero") |
| **Lateral** | Airflow around the side of the tongue | /l/ |

Together, place and manner of articulation, plus the voicing distinction (voiced vs. voiceless), uniquely identify a consonant in phonetics. They are the basis of the **International Phonetic Alphabet (IPA)**, which NLP systems use as the alphabet of speech.

#### B.15.2 Word Boundary Detection *(PYQ 2024 Q4(B), 2025 Q2)*

**Definition:** Word boundary detection is the task of segmenting a continuous stream of input (either speech audio or unspaced text) into discrete word units. In speech, the audio signal has no natural pauses between words; in many languages (Chinese, Japanese, Thai), written text has no spaces between words.

**Challenges:**
- In **speech**, boundaries are blurred by coarticulation, assimilation, and speaker rate variation. The acoustic cue for a word boundary is subtle (slight pause, pitch reset, lengthening of the final syllable).
- In **text**, languages without spaces need segmentation dictionaries or statistical models. Even in English, hyphenation ("state-of-the-art") and contractions ("don't") create ambiguity.
- Different languages have different conventions: German compounds words (`Rindfleischetikettierungsüberwachungsaufgabenübertragungsgesetz`); Chinese requires word segmentation as a separate task; Thai has no spaces at all.
- Speaker accents, disfluencies ("uh", "um"), and code-switching (mixing languages) make the task harder.

**Strategies for handling boundary errors:**
1. **Acoustic-phonetic features** — detect pauses, pitch drops, vowel lengthening.
2. **Language-model priors** — use a statistical LM to prefer segmentation that gives higher-probability word sequences (e.g., "the cat" is more probable than "theca t").
3. **Dictionary lookup** — match segmentations against a lexicon.
4. **Sub-word models** — fall back to BPE / SentencePiece so the model never has to commit to a hard boundary.
5. **Transformer-based end-to-end ASR** (Whisper, Conformer) — learn boundaries implicitly.

#### B.15.3 Argmax Computation *(PYQ 2024 Q1(C), 4 marks)*

**The Argmax principle:** When we have a noisy input $X$ (e.g., a speech signal, or a sequence of word embeddings) and want to find the most probable *hidden* sequence $W^*$ (e.g., the words spoken, or the POS tags), we use:

$$W^* = \arg\max_W P(W \mid X)$$

Using Bayes' rule:
$$P(W \mid X) = \frac{P(X \mid W) \cdot P(W)}{P(X)} \propto P(X \mid W) \cdot P(W)$$

So:
$$W^* = \arg\max_W P(X \mid W) \cdot P(W)$$

Where:
- $P(X \mid W)$ = **acoustic model** (likelihood of observing signal $X$ given word sequence $W$).
- $P(W)$ = **language model** (probability of the word sequence $W$).
- For text-only NLP (POS tagging, NER), $P(X \mid W)$ becomes the **emission probability** (e.g., HMM emission).

**Bigram Argmax for sentence prediction (PYQ 2024 Q1(C)):**
For sentence "The cat chased the mouse" using a bigram LM, the most probable word at each position is the one that maximises $P(w_k \mid w_{k-1})$. Given a small candidate set per position (e.g., the top-3 likely words from the acoustic model), compute the product of bigram probabilities for every candidate sequence and pick the argmax.

$$\hat{W} = \arg\max_W \prod_{k=1}^{n} P(w_k \mid w_{k-1})$$

**Worked pattern:**
- Given candidates: $w_1 \in \{$"The"$\}$, $w_2 \in \{$"cat"$, "bat", "rat"$\}$, $w_3 \in \{$"chased"$, "ate"$\}$, ...
- For each candidate sequence $W = (w_1, w_2, w_3, w_4, w_5)$, compute $P(W) = \prod_k P(w_k \mid w_{k-1})$.
- Return $\hat{W}$ maximising $P(W)$.

#### B.15.4 HMM for Speech Recognition *(PYQ 2024 Q3(B), 2025 Q2 OR)*

**Hidden Markov Model (HMM)** is a doubly stochastic process: an underlying Markov chain of hidden states generates observable outputs through emission probabilities. For speech recognition, the hidden states are *phonemes* (or sub-phonetic HMM states such as the 3-state left-to-right HMM with onset / nucleus / coda), and the observations are *acoustic feature vectors* (typically MFCCs or Mel-spectrograms computed every 10 ms).

**Three fundamental problems of HMM (Jurafsky & Martin):**
1. **Evaluation** — given HMM $\lambda = (A, B, \pi)$ and observation sequence $O$, compute $P(O \mid \lambda)$. Solved by the **Forward algorithm**.
2. **Decoding** — given HMM $\lambda$ and observation $O$, find the most likely state sequence $Q^*$. Solved by the **Viterbi algorithm**.
3. **Learning** — given observation $O$, estimate HMM parameters $\lambda$ that maximise $P(O \mid \lambda)$. Solved by the **Baum-Welch algorithm** (a special case of EM).

**Constructing a basic HMM for ASR (5 / 10 mark answer):**
- **States** $S = \{s_1, \ldots, s_N\}$ — one HMM per phoneme (or per word, in a simple system). E.g., for the word "cat" → phonemes /k/ /æ/ /t/ → three HMMs concatenated.
- **Observations** $O = \{o_1, \ldots, o_T\}$ — sequence of acoustic feature vectors (MFCCs).
- **Transition probabilities** $A = [a_{ij}]$ — $a_{ij} = P(s_j \text{ at } t+1 \mid s_i \text{ at } t)$. Speech HMMs are usually **left-to-right** (no backward transitions), so $a_{ij} = 0$ for $j < i$.
- **Emission probabilities** $B = [b_j(o)]$ — $b_j(o) = P(o \mid s_j)$. Historically modelled by Gaussian Mixtures (GMM-HMM systems); modern systems use DNNs (DNN-HMM hybrids) or skip HMMs entirely (CTC / attention-based end-to-end ASR).
- **Initial state distribution** $\pi$ — typically $\pi_1 = 1$ (start at the first state) and $\pi_i = 0$ for $i > 1$.

**Processing an input speech signal (workflow):**
1. **Pre-emphasis** — boost high frequencies (1st-order high-pass filter).
2. **Framing** — chop the signal into 25-ms frames every 10 ms (overlap = 15 ms).
3. **Windowing** — apply Hamming window to each frame to reduce edge effects.
4. **FFT → Mel filterbank → log → DCT** → produce 13-dimensional MFCCs (+ Δ + ΔΔ = 39 features).
5. **Acoustic model scoring** — for each candidate phoneme-state sequence, compute the likelihood of the observed MFCCs given the state (the emission model).
6. **Viterbi decoding** — combine acoustic scores with the language-model prior $P(W)$ to find the most probable word sequence $\hat{W} = \arg\max_W P(O \mid W) \cdot P(W)$.
7. **Output** — the recognised word sequence.

#### B.15.5 Components of Speech Recognition *(PYQ 2024 Q5(A) OR, 6 marks)*

A full ASR system has these components:

1. **Acoustic Front-end** — converts raw audio into feature vectors (MFCC / Mel / log-Mel filterbank). Includes pre-emphasis, framing, windowing, FFT, Mel filterbank, log, DCT.
2. **Acoustic Model** — maps acoustic features to phoneme (or sub-word) probabilities. Classic: GMM-HMM; modern: DNN-HMM, CTC-trained RNN/Transformer, RNN-Transducer.
3. **Pronunciation Model (Lexicon)** — maps each word to its phoneme sequence. E.g., `cat → /k/ /æ/ /t/`. Stored as a lexicon file (e.g., CMU Pronouncing Dictionary).
4. **Language Model** — assigns probability $P(W)$ to word sequences. Classic: n-gram LM; modern: neural LM. Used to disambiguate acoustically similar candidates ("recognise speech" vs "wreck a nice beach").
5. **Decoder** — combines acoustic, pronunciation, and LM scores to find the most probable word sequence via Viterbi search (or A* search).

**Workflow diagram (sketch):**
```
Audio → [Front-end: MFCC] → [Acoustic Model: P(o|s)] →
                                          ↓
                        [Pronunciation Lexicon: word→phonemes]
                                          ↓
                              [Decoder + LM: P(W)]
                                          ↓
                              Recognised text
```

### B.16 Computational Grammar *(PYQ 2024 Q4(A), 2025 Q3(d))*

**Definition (2 marks):** Computational grammar is the formal specification of the syntactic rules of a language in a machine-processable form. It defines which strings of words are grammatically well-formed in a language and which are not, and assigns a structural description (typically a parse tree) to each well-formed string. It is the bridge between linguistics and computation.

**Why is computational grammar necessary for NLP? (5-mark depth, PYQ 2024 Q4-A):**

1. **Structural disambiguation** — many sentences have multiple parse trees. A computational grammar provides a deterministic procedure for choosing the right parse. Example: "I saw the man with the telescope" — did I use a telescope, or did the man have one? The grammar resolves this.
2. **Anaphora resolution** — to resolve "she" → "Marie" we need a syntactic structure that connects the pronoun to its antecedent.
3. **Machine translation** — reordering subject-verb-object across languages requires a parse tree (e.g., English SVO vs. Japanese SOV).
4. **Information extraction** — extracting (subject, verb, object) triplets requires knowing which noun is the subject and which is the object.
5. **Question answering** — answering "who did what to whom?" requires syntactic roles.

**Types of grammars used in NLP:**
- **Regular grammars** (Type-3, Chomsky hierarchy) — equivalent to finite-state automata; used in tokenisation, morphology.
- **Context-Free Grammars (CFG)** (Type-2) — production rules like `S → NP VP`; used in constituency parsing.
- **Context-Sensitive Grammars** (Type-1) — handle agreement; rarely used directly.
- **Unification-based grammars** (HPSG, LFG) — feature structures + unification; linguistically rich.
- **Dependency grammars** — words linked by head-dependent relations; used by spaCy, Universal Dependencies.

### B.17 Data Attributes & File Formats *(PYQ 2024 Q5(B), Q5(B) OR)*

#### B.17.1 Types of Data Attributes

| Type | Description | Examples | Operations |
|---|---|---|---|
| **Nominal** (categorical, qualitative) | Unordered categories. | Eye colour {brown, blue, green}; POS tag {NN, VB, JJ}; language {en, hi, fr}. | =, ≠ |
| **Ordinal** | Ordered categories, but differences meaningless. | Education {high-school < bachelor < master < PhD}; rating {1★–5★}. | =, ≠, <, > |
| **Interval-scaled** | Numeric, equal intervals, no true zero. | Temperature in °C / °F; calendar year. | =, ≠, <, >, +, − |
| **Ratio-scaled** | Numeric, equal intervals, true zero exists. | Length, weight, time duration, word frequency, TF-IDF score. | =, ≠, <, >, +, −, ×, ÷ |

**Examples (2-mark each):**
- Nominal: `POS = 'NN'`
- Ordinal: `difficulty = 'hard'`
- Interval-scaled: `pub_year = 1998` (the zero point is arbitrary; year 0 doesn't mean "no time")
- Ratio-scaled: `word_count = 350` (0 means "no words"; 700 words = exactly 2× 350 words)

#### B.17.2 File Formats for Corpora — JSON vs CSV *(PYQ 2024 Q5(B) OR, 2+2 marks)*

| Aspect | CSV (Comma-Separated Values) | JSON (JavaScript Object Notation) |
|---|---|---|
| Structure | Flat tabular (rows × columns) | Hierarchical (nested key-value, arrays) |
| Schema | Implicit (header row) | Self-describing |
| Data types | All values are strings by default | Strings, numbers, booleans, null, arrays, objects |
| Readability | Good for tabular data; loses structure for nested | Excellent for nested / mixed data |
| Size | Smaller | Larger (keys repeated per record) |
| Comments | Not supported | Not supported natively |
| Streaming | Easy (row-by-row) | Harder (must parse entire structure) |
| Best for | Tabular corpora (word lists, frequency tables) | Nested corpora (dialogues, documents with metadata, JSON-LD) |

**CSV example:**
```csv
word,POS,frequency
the,DT,7000
cat,NN,150
```

**JSON example:**
```json
{"sentence": "The cat sat.",
 "tokens": [{"text":"The","pos":"DT"},{"text":"cat","pos":"NN"},{"text":"sat","pos":"VBD"}],
 "lang": "en"}
```

#### B.17.3 Speech file formats — MP3 vs FLAC *(PYQ 2024 Q4(B) OR, 5 marks)*

| Aspect | MP3 (MPEG-1 Audio Layer III) | FLAC (Free Lossless Audio Codec) |
|---|---|---|
| Compression type | **Lossy** — discards psycho-acoustically irrelevant data | **Lossless** — perfect reconstruction guaranteed |
| Bitrate | 32–320 kbps (typical: 128 kbps) | ~700–1000 kbps (CD-quality) |
| File size (1 min CD audio) | ~1 MB | ~5–8 MB |
| Quality | Lossy, artefacts at low bitrate | Bit-identical to original |
| Licensing | Patented (historically; now mostly expired) | Royalty-free, open-source |
| Use case | Streaming, podcasts, music distribution | Archival, speech research, NLP training corpora |
| **Advantages** | Small size, universal support, ideal for transmission | Perfect quality, fast seeking, MD5 checksums for integrity |
| **Disadvantages** | Quality loss, generation loss on re-encoding | Larger file size, less bandwidth-efficient |

**For NLP / speech research:** always prefer **FLAC** (or WAV) for training corpora, because lossy compression can corrupt acoustic features (MFCCs) and degrade ASR accuracy. MP3 is acceptable only for end-user delivery.

### B.18 Datasets for NLP: Text Classification vs Machine Translation *(PYQ 2024 Q5(A), 6 marks)*

| Aspect | Text classification dataset | Machine translation dataset |
|---|---|---|
| Structure | Documents + labels | Sentence-aligned bilingual pairs |
| Labels | Single (or multi-) label per document | Target-language sentence (the "label" is itself a sequence) |
| Corpus nature | One language; bag-of-words / TF-IDF sufficient | Two (or more) languages; word alignment needed |
| Attributes / features | Sparse lexical features (word counts, n-gram counts, embeddings) | Source + target embeddings, alignment matrices, attention weights |
| Evaluation | Accuracy, Precision / Recall / F1 | BLEU, METEOR, chrF, COMET |
| Size | Often 10K – 1M documents | Often 1M – 100M sentence pairs |
| Pre-processing | Tokenisation, stop-word removal, stemming, TF-IDF | Tokenisation, BPE sub-word segmentation, Bilingual dictionary, alignment |
| Example corpora | IMDB reviews, 20 Newsgroups, AG News | Europarl, WMT, OPUS, Tatoeba |

The **nature of the corpus and attributes changes** because the two tasks have fundamentally different objectives: classification reduces a variable-length document to a single label, whereas MT maps one sequence to another sequence of (generally) different length. This demands different feature representations, different loss functions (cross-entropy vs. sequence-level NLL), and different evaluation metrics.

---

## Section C — Unit 2: Vectorization & N-gram Language Models

### C.1 Text Representation in NLP (Overview)

**Text representation** is the technique used in NLP to transform raw text into numerical features that capture information needed for computational processing and learning. Machine-learning models cannot operate on raw strings; they need vectors. The Week 4 PPT classifies text representation methods into two broad families:

**1. Discrete text representation:**
- **One-Hot Encoding** — each word → a binary vector with a single 1.
- **Bag of Words (BoW)** — count of each vocabulary word in a document.
- **TF-IDF** — BoW weighted by inverse document frequency to down-weight common words.

**2. Distributed word representation:**
- **Word2Vec** — learns dense embeddings via Skip-Gram or CBOW (Continuous Bag-Of-Words).
- **GloVe (Global Vectors)** — embeddings learned from global co-occurrence statistics.
- **FastText** — extension of Word2Vec that learns embeddings for sub-word n-grams (handles OOV).

### C.2 One-Hot Encoding

Each word in the vocabulary $V$ is represented by a binary vector of size $|V|$ with a single `1` at the index of that word and `0` everywhere else.

$$\text{onehot}(w_i) = [0, 0, \ldots, 1, \ldots, 0] \quad (\text{1 at position } i)$$

**Properties:**
- Vector dimension = $|V|$ (often 50,000 – 500,000) — very high-dimensional.
- All vectors are **orthogonal** — $\text{onehot}(w_i) \cdot \text{onehot}(w_j) = 0$ for $i \neq j$.
- There is **no natural notion of similarity** between one-hot vectors — `cat` and `dog` are as dissimilar as `cat` and `electron`.

**Limitations (the motivation for distributed representations):**
- Massive dimensionality → sparse vectors → memory and compute waste.
- No semantic similarity.
- Cannot handle OOV words.

### C.3 Co-occurrence Matrix & Cosine Similarity *(numerical topic — Week 5 PPT)*

**Co-occurrence matrix $C$** — for a corpus, define a context window of size $k$ (typically symmetric: $k$ words on each side). For every target word $w$ and context word $c$, $C_{w,c}$ = number of times $w$ and $c$ co-occur within the window across the whole corpus.

**Worked example (Week 5 PPT):**

Toy corpus:
```
"data science drives insight"
"data analysis drives insight"
```

Window size = 1 (one word left + one word right). The co-occurrence matrix is:

|       | data | science | analysis | drives | insight |
|---|:---:|:---:|:---:|:---:|:---:|
| **data**    | 0 | 1 | 1 | 0 | 0 |
| **science** | 1 | 0 | 0 | 1 | 0 |
| **analysis**| 1 | 0 | 0 | 1 | 0 |
| **drives**  | 0 | 1 | 1 | 0 | 2 |
| **insight** | 0 | 0 | 0 | 2 | 0 |

The row for each word is its **co-occurrence vector**.

**Cosine similarity:**

$$\text{cosine}(\mathbf{u}, \mathbf{v}) = \frac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\| \, \|\mathbf{v}\|} = \frac{\sum_i u_i v_i}{\sqrt{\sum_i u_i^2} \sqrt{\sum_i v_i^2}}$$

Cosine similarity measures the **angle** between two vectors, ignoring their magnitude. Range: $[-1, 1]$; for non-negative count vectors, range is $[0, 1]$.

**Worked computation (Week 5 PPT):**

$$\mathbf{v}_{\text{science}} = (1, 0, 0, 1, 0)$$
$$\mathbf{v}_{\text{analysis}} = (1, 0, 0, 1, 0)$$

$$\text{cosine}(\mathbf{v}_{\text{science}}, \mathbf{v}_{\text{analysis}}) = \frac{1\cdot1 + 0 + 0 + 1\cdot1 + 0}{\sqrt{1^2+1^2} \cdot \sqrt{1^2+1^2}} = \frac{2}{\sqrt{2}\cdot\sqrt{2}} = \frac{2}{2} = 1.0$$

**Key insight:** even though `science` and `analysis` never directly co-occur in the corpus, they share identical contexts (`data`, `drives`), so their cosine similarity is 1.0 — they are perfect synonyms in this toy distributional semantic space.

### C.4 Raw Co-occurrence Counts — Issues & PMI

**Problem:** Raw co-occurrence counts suffer from **frequency bias**: common words (`the`, `is`, `and`) dominate matrix entries without contributing informative semantic context. A frequent word co-occurs with *everything*, so it cannot discriminate.

**Solution — Pointwise Mutual Information (PMI):** PMI quantifies whether two words co-occur significantly more often than expected by random chance:

$$\text{PMI}(w, c) = \log_2 \frac{P(w, c)}{P(w) \cdot P(c)} = \log_2 \frac{C(w, c) \cdot N}{C(w) \cdot C(c)}$$

where $N = \sum_{i,j} C(w_i, c_j)$ is the total sum of co-occurrence counts, $C(w)$ is the marginal count of word $w$, and $C(w, c)$ is the joint co-occurrence count.

**Interpretation:**
- $\text{PMI} > 0$ → words co-occur more than chance (positively associated).
- $\text{PMI} = 0$ → independent.
- $\text{PMI} < 0$ → co-occur less than chance (negatively associated).

**Problem with PMI:** As $P(w, c) \to 0$, $\text{PMI} \to -\infty$. Negative PMI values are noisy and statistically unreliable (a single co-occurrence produces a huge negative PMI). **Solution: PPMI** (Positive PMI):

$$\text{PPMI}(w, c) = \max(0, \text{PMI}(w, c))$$

All negative PMI values are clamped to 0.

### C.5 PPMI Worked Example (Week 5 PPT)

Using the same toy corpus as Section C.3:

Total co-occurrences: $N = 2 + 2 + 2 + 4 + 2 = 12$ (sum of all entries in matrix).

Marginal counts (row sums): $C(\text{data}) = 2, C(\text{science}) = 2, C(\text{analysis}) = 2, C(\text{drives}) = 4, C(\text{insight}) = 2$.

**PMI for selected pairs:**

| Pair $(w, c)$ | $C(w, c)$ | $C(w)$ | $C(c)$ | $\frac{C(w,c) \cdot N}{C(w) \cdot C(c)}$ | $\text{PMI} = \log_2(\cdot)$ | $\text{PPMI}$ |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| (data, science) | 1 | 2 | 2 | $\frac{1 \cdot 12}{2 \cdot 2} = 3$ | $\log_2 3 \approx 1.585$ | 1.585 |
| (data, analysis) | 1 | 2 | 2 | 3 | 1.585 | 1.585 |
| (science, drives) | 1 | 2 | 4 | $\frac{1 \cdot 12}{2 \cdot 4} = 1.5$ | $\log_2 1.5 \approx 0.585$ | 0.585 |
| (analysis, drives) | 1 | 2 | 4 | 1.5 | 0.585 | 0.585 |
| (drives, insight) | 2 | 4 | 2 | $\frac{2 \cdot 12}{4 \cdot 2} = 3$ | 1.585 | 1.585 |
| (non-co-occurring pairs) | 0 | — | — | 0 | $-\infty$ | **0** (clamped) |

**Final PPMI matrix:**

|       | data | science | analysis | drives | insight |
|---|:---:|:---:|:---:|:---:|:---:|
| **data**    | 0 | 1.585 | 1.585 | 0 | 0 |
| **science** | 1.585 | 0 | 0 | 0.585 | 0 |
| **analysis**| 1.585 | 0 | 0 | 0.585 | 0 |
| **drives**  | 0 | 0.585 | 0.585 | 0 | 1.585 |
| **insight** | 0 | 0 | 0 | 1.585 | 0 |

**Key outcomes:**
- **Semantic synonymy:** $\mathbf{v}_{\text{science}} = (1.585, 0, 0, 0.585, 0)$ and $\mathbf{v}_{\text{analysis}} = (1.585, 0, 0, 0.585, 0)$ are identical vectors — cosine similarity = 1.0 — because they share identical statistical contexts.
- **Frequency adjustment:** Even though `drives` co-occurs twice with `insight` ($C=2$) and only once with `science` ($C=1$), the higher overall frequency of `drives` ($C=4$) adjusts the associations proportionally (1.585 vs 0.585).

### C.6 Bag of Words (BoW)

BoW represents each document as a vector of word counts, ignoring word order. The vector length = vocabulary size $|V|$.

$$\text{BoW}(d) = [c(w_1, d), c(w_2, d), \ldots, c(w_{|V|}, d)]$$

**Limitations:** sparse, no semantic similarity, no word order, frequent words dominate.

### C.7 TF-IDF *(numerical topic — Week 5 PPT)*

While PMI measures word-word association, **TF-IDF (Term Frequency – Inverse Document Frequency)** weights words relative to **document context** in a term-document matrix.

$$\text{TF-IDF}(t, d, D) = \text{TF}(t, d) \times \text{IDF}(t, D)$$

- $\text{TF}(t, d)$ — frequency of term $t$ in document $d$.
- $D$ — entire corpus (collection of all documents).
- $\text{IDF}(t, D)$ — down-weights words appearing in every document; elevates rare, highly discriminative keywords.

**Plain IDF:**
$$\text{IDF}(t, D) = \log \frac{|D|}{|\{d \in D : t \in d\}|}$$

**Problem:** If a term appears in *every* document, plain $\text{IDF} = \log 1 = 0$, killing the weight entirely. Also, $\log \frac{|D|}{0}$ can blow up if a term appears in no document.

**Sklearn's smoothed IDF (memorise this formula):**
$$\text{IDF}(t, D) = \ln\left(\frac{1 + |D|}{1 + |\{d : t \in d\}|}\right) + 1$$

Then **L2-normalise** every document vector after computing TF-IDF.

**Sklearn example (Week 5 PPT):**

```python
from sklearn.feature_extraction.text import TfidfVectorizer
sentences = [
    'The stock price of google jumps on the earning data today',
    'Google plunge on China Data!'
]
vectorizer = TfidfVectorizer(stop_words='english')
TFIDF = vectorizer.fit_transform(sentences)
print(vectorizer.get_feature_names_out())
# ['china' 'data' 'earning' 'google' 'jumps' 'plunge' 'price' 'stock' 'today']
print(TFIDF.shape)   # (2, 9)
print(TFIDF.toarray())
```

**Output:**
```
[[0.       0.29017 0.40782 0.29017 0.40782 0.       0.40782 0.40782 0.40782]
 [0.57615  0.40994 0.       0.40994 0.       0.57615  0.       0.       0.     ]]
```

**Verifying with theory (Week 5 PPT):**

Document 1 ("The stock price of google jumps on the earning data today") — after stop-word removal (`the, of, on`) and lowercasing, the unique content tokens are: `stock, price, google, jumps, earning, data, today` (7 tokens, each appearing once).

- **TF** for each of these tokens = 1.
- **Plain IDF:** `data` and `google` appear in both documents → $\text{IDF} = \log(2/2) = 0$. The other 5 tokens appear in 1 document → $\text{IDF} = \log(2/1) = \log 2 \approx 0.693$ → after `+1` smoothing: $\text{IDF}_{\text{sklearn}} = \ln(3/2)+1 \approx 0.4055 + 1 = 1.4055$.
- **Unnormalised TF-IDF:** `data, google` = $1 \times 1.0000 = 1.0000$; `earning, jumps, price, stock, today` = $1 \times 1.4055 = 1.4055$.
- **L2 norm:** $\|\mathbf{v}_1\|_2 = \sqrt{2 \cdot 1.0^2 + 5 \cdot 1.4055^2} = \sqrt{2 + 9.877} = \sqrt{11.877} \approx 3.4463$.
- **Normalised TF-IDF:**
  - `data, google`: $1.0 / 3.4463 \approx 0.2902$ ✓
  - `earning, jumps, price, stock, today`: $1.4055 / 3.4463 \approx 0.4078$ ✓
  - `china, plunge`: 0 (absent) ✓

Document 2 ("Google plunge on China Data!") — tokens: `google, plunge, china, data`.
- TF for each = 1.
- Unnormalised TF-IDF: `google, data` = 1.0; `plunge, china` = 1.4055.
- L2 norm: $\sqrt{2 \cdot 1.0^2 + 2 \cdot 1.4055^2} = \sqrt{2 + 3.9507} \approx 2.4394$.
- Normalised:
  - `china, plunge`: $1.4055 / 2.4394 \approx 0.5762$ ✓
  - `google, data`: $1.0 / 2.4394 \approx 0.4099$ ✓

The theoretical values match the sklearn output — confirming the smoothed IDF + L2 normalisation formula.

### C.8 N-gram Language Models *(core numerical topic)*

**Language Model (LM)** — a model that predicts the next upcoming word. Formally, an LM assigns a probability to each potential next word, giving a probability distribution over the vocabulary, and (by extension) a probability to a whole sentence.

**Why predict the next word?** Because it is the foundational task of language understanding — used in autocomplete, grammar / spell checking, speech recognition, machine translation, and is the training objective of LLMs (autoregressive next-token prediction).

**General LM goal — two equivalent formulations:**
- Probability of a sentence: $P(W) = P(w_1, w_2, \ldots, w_n) = P(w_{1:n})$
- Probability of the next word: $P(w_n \mid w_1, w_2, \ldots, w_{n-1}) = P(w_n \mid w_{1:n-1})$

### C.9 The Chain Rule of Probability

$$P(w_1, w_2, \ldots, w_n) = \prod_{k=1}^{n} P(w_k \mid w_1, \ldots, w_{k-1})$$

**Example (Week 6-7 PPT):**
$$P(\text{"The water of Walden Pond"}) = P(\text{The}) \cdot P(\text{water} \mid \text{The}) \cdot P(\text{of} \mid \text{The water}) \cdot P(\text{Walden} \mid \text{The water of}) \cdot P(\text{Pond} \mid \text{The water of Walden})$$

**The problem:** Long conditioning histories are impossible to compute because sequences never repeat identically in finite text — the count $C(w_1, \ldots, w_{k-1})$ is almost always zero for long prefixes.

### C.10 Markov Approximation — N-gram Models

**Approximate the context by looking back only $N - 1$ words:**

| Model | $N$ | Formula |
|---|:---:|---|
| **Unigram** | 1 | $P(W) \approx \prod_{k=1}^n P(w_k)$ |
| **Bigram** | 2 | $P(W) \approx \prod_{k=1}^n P(w_k \mid w_{k-1})$ |
| **Trigram** | 3 | $P(W) \approx \prod_{k=1}^n P(w_k \mid w_{k-2}, w_{k-1})$ |
| **N-gram** | $N$ | $P(W) \approx \prod_{k=1}^n P(w_k \mid w_{k-N+1:k-1})$ |

**Example — "I love natural language processing":**
- Unigrams: `["I", "love", "natural", "language", "processing"]`
- Bigrams: `["I love", "love natural", "natural language", "language processing"]`
- Trigrams: `["I love natural", "love natural language", "natural language processing"]`

### C.11 Maximum Likelihood Estimation (MLE)

Estimate probabilities from relative frequency counts in a training corpus:

| Model | MLE Formula |
|---|---|
| Unigram | $P_{\text{MLE}}(w_k) = \dfrac{C(w_k)}{N_{\text{total}}}$ |
| Bigram | $P_{\text{MLE}}(w_k \mid w_{k-1}) = \dfrac{C(w_{k-1}, w_k)}{C(w_{k-1})}$ |
| Trigram | $P_{\text{MLE}}(w_k \mid w_{k-2}, w_{k-1}) = \dfrac{C(w_{k-2}, w_{k-1}, w_k)}{C(w_{k-2}, w_{k-1})}$ |
| N-gram | $P_{\text{MLE}}(w_k \mid w_{k-N+1:k-1}) = \dfrac{C(w_{k-N+1:k})}{C(w_{k-N+1:k-1})} = \dfrac{C(w_{k-N+1:k})}{\sum_w C(w_{k-N+1:k-1}, w)}$ |

**Sentence boundaries:** augment the sequence with `<s>` (start) and `</s>` (end) markers, then apply the chain rule. The probability of the entire sentence becomes:

$$P(W) = \prod_{k=1}^{n+1} P_{\text{MLE}}(w_k \mid w_{k-N+1:k-1})$$

where the $(n+1)$-th token is `</s>`, and $w_0, w_{-1}, \ldots$ are set to `<s>`.

**In practice:** compute in **log-space** to prevent numerical underflow (products of many small probabilities underflow to zero):

$$\log P(W) = \sum_{k=1}^{n+1} \log P_{\text{MLE}}(w_k \mid w_{k-N+1:k-1})$$

### C.12 N-gram Worked Example (Bigram MLE, Week 6-7 PPT)

**Training corpus:**
```
<s> I am Sam </s>
<s> Sam I am </s>
<s> I do not like green eggs </s>
```

**Counts:**
- $C(\text{<s>}) = 3$
- $C(\text{I}) = 3$
- $C(\text{am}) = 2$
- $C(\text{Sam}) = 2$
- $C(\text{<s>, I}) = 2$
- $C(\text{I, am}) = 2$
- $C(\text{am, Sam}) = 1$
- $C(\text{Sam, </s>}) = 1$

**Computations:**

$$P(\text{am} \mid \text{I}) = \frac{C(\text{I, am})}{C(\text{I})} = \frac{2}{3} \approx 0.667$$

$$P(\text{Sam} \mid \text{<s>}) = \frac{C(\text{<s>, Sam})}{C(\text{<s>})} = \frac{1}{3} \approx 0.333$$

### C.13 Evaluating N-gram LMs — Perplexity

Two evaluation methodologies:

1. **Extrinsic (in-vivo) evaluation** — put each model in a real downstream task (MT, ASR), measure accuracy, compare. Expensive and time-consuming but most reliable.
2. **Intrinsic (in-vitro) evaluation** — measure the model's predictive power on unseen held-out text. The standard intrinsic metric is **perplexity**.

**Perplexity** = the inverse probability of the test set, normalised by the number of tokens $n$:

$$\text{PP}(W) = P(W)^{-1/n} = \left(\prod_{k=1}^{n} P(w_k \mid w_{k-N+1:k-1})\right)^{-1/n} = \sqrt[n]{\frac{1}{\prod_{k=1}^{n} P(w_k \mid w_{k-N+1:k-1})}}$$

**Interpretation:** Perplexity is the **effective branching factor** — the average number of equally-likely words the model is choosing between at each step. Lower perplexity = better model. Probability range is $[0, 1]$; perplexity range is $[1, \infty]$.

**Critical requirements for fair comparison (Week 6-7 PPT):**
1. **Identical vocabulary** — including `<UNK>` handling.
2. **Identical tokenisation & test set** — same `<s>`, `</s>` markers, same token boundaries.

### C.14 Cross-Entropy & Log-Perplexity

Because product probabilities underflow, perplexity is computed in **log-space** via average negative log-likelihood, called **cross-entropy $H(W)$** (in bits, base 2):

$$H(W) = -\frac{1}{n} \sum_{k=1}^{n} \log_2 P(w_k \mid w_{k-N+1:k-1})$$

$$\text{PP}(W) = 2^{H(W)}$$

### C.15 Perplexity Worked Example — Bigram (Week 6-7 PPT)

Using the same training corpus as Section C.12.

**Test sequence:** `<s> I am Sam </s>`
**Tokens to predict:** $w_1 = \text{I}, w_2 = \text{am}, w_3 = \text{Sam}, w_4 = \text{</s>}$
**Number of test tokens:** $n = 4$

**Step 1 — Bigram probabilities (MLE):**

| Step | Bigram | Count | Denominator | Probability |
|:---:|---|:---:|:---:|:---:|
| 1 | $P(\text{I} \mid \text{<s>})$ | $C(\text{<s>, I}) = 2$ | $C(\text{<s>}) = 3$ | $2/3 \approx 0.66667$ |
| 2 | $P(\text{am} \mid \text{I})$ | $C(\text{I, am}) = 2$ | $C(\text{I}) = 3$ | $2/3 \approx 0.66667$ |
| 3 | $P(\text{Sam} \mid \text{am})$ | $C(\text{am, Sam}) = 1$ | $C(\text{am}) = 2$ | $1/2 = 0.50000$ |
| 4 | $P(\text{</s>} \mid \text{Sam})$ | $C(\text{Sam, </s>}) = 1$ | $C(\text{Sam}) = 2$ | $1/2 = 0.50000$ |

**Step 2 — Sentence probability:**
$$P(W) = \frac{2}{3} \times \frac{2}{3} \times \frac{1}{2} \times \frac{1}{2} = \frac{4}{36} = \frac{1}{9} \approx 0.11111$$

**Step 3 — Perplexity (direct formula), $n = 4$:**
$$\text{PP}(W) = P(W)^{-1/4} = \left(\frac{1}{9}\right)^{-1/4} = 9^{1/4} = \sqrt{3} \approx 1.732$$

**Step 4 — Cross-entropy method (verification):**

| Bigram | $\log_2 P$ |
|---|---|
| $\log_2(2/3)$ | $\approx -0.58496$ |
| $\log_2(2/3)$ | $\approx -0.58496$ |
| $\log_2(1/2)$ | $= -1.00000$ |
| $\log_2(1/2)$ | $= -1.00000$ |

$$H(W) = -\frac{1}{4}\left(-0.58496 - 0.58496 - 1.00000 - 1.00000\right) = -\frac{1}{4}(-3.16992) \approx 0.79248 \text{ bits/word}$$

$$\text{PP}(W) = 2^{H(W)} = 2^{0.79248} = \sqrt{3} \approx 1.732 \quad \checkmark$$

### C.16 Perplexity Worked Example — Trigram (Week 6-7 PPT)

For trigram models, we add a second `<s>` marker at the start so each sentence has two start markers (giving every trigram enough context).

**Trigram-augmented training corpus:**
```
<s> <s> I am Sam </s>
<s> <s> Sam I am </s>
<s> <s> I do not like green eggs </s>
```

**Test:** `<s> <s> I am Sam </s>` — same 4 tokens to predict ($w_1 = \text{I}, w_2 = \text{am}, w_3 = \text{Sam}, w_4 = \text{</s>}$), $n = 4$.

**Trigram probabilities:**

| Step | Trigram | Count | Denominator | Probability |
|:---:|---|:---:|:---:|:---:|
| 1 | $P(\text{I} \mid \text{<s>, <s>})$ | $C(\text{<s>,<s>,I}) = 2$ | $C(\text{<s>,<s>}) = 3$ | $2/3 \approx 0.66667$ |
| 2 | $P(\text{am} \mid \text{<s>, I})$ | $C(\text{<s>,I,am}) = 1$ | $C(\text{<s>,I}) = 2$ | $1/2 = 0.50000$ |
| 3 | $P(\text{Sam} \mid \text{I, am})$ | $C(\text{I,am,Sam}) = 1$ | $C(\text{I,am}) = 2$ | $1/2 = 0.50000$ |
| 4 | $P(\text{</s>} \mid \text{am, Sam})$ | $C(\text{am,Sam,</s>}) = 1$ | $C(\text{am,Sam}) = 1$ | $1/1 = 1.00000$ |

**Sentence probability:**
$$P(W) = \frac{2}{3} \times \frac{1}{2} \times \frac{1}{2} \times 1 = \frac{2}{12} = \frac{1}{6} \approx 0.16667$$

**Perplexity (direct formula, $n = 4$):**
$$\text{PP}(W) = \left(\frac{1}{6}\right)^{-1/4} = 6^{1/4} \approx 1.565$$

**Cross-entropy method:**

| Trigram | $\log_2 P$ |
|---|---|
| $\log_2(2/3)$ | $-0.58496$ |
| $\log_2(1/2)$ | $-1.00000$ |
| $\log_2(1/2)$ | $-1.00000$ |
| $\log_2(1)$ | $0.00000$ |

$$H(W) = -\frac{1}{4}(-0.58496 - 1 - 1 + 0) = -\frac{1}{4}(-2.58496) \approx 0.64624 \text{ bits/word}$$

$$\text{PP}(W) = 2^{0.64624} \approx 1.565 \quad \checkmark$$

**Interpretation:** The trigram model achieves lower perplexity (1.565 vs 1.732 for bigram) because the additional word of history resolves ambiguity (e.g., knowing with certainty that `</s>` follows `am Sam`). **Holding the test set constant, lower perplexity = better language model.**

### C.17 Data Sparsity Problem in N-gram LMs

Human language has a massive, combinatorial vocabulary. Even huge text corpora contain only a tiny fraction of all valid word combinations. As a result, a large majority of perfectly natural, grammatical N-grams never appear in the training corpus, receiving an empirical count of zero: $C(w_{k-N+1:k-1}, w_k) = 0$.

**Two catastrophic consequences:**
1. **Sequence probability collapse:** Because $P(W) = \prod_k P(w_k \mid \ldots)$, a single unseen N-gram drives the entire product to zero: $P(W) = 0$.
2. **Perplexity explosion:** $\log_2 0 \to -\infty$ → cross-entropy $\to \infty$ → $\text{PP}(W) \to \infty$.

A count of zero does not mean a phrase is impossible — it simply means the training sample was not large enough to observe it.

### C.18 Solutions to Sparsity

1. **Smoothing (Discounting)** — reallocate probability mass from high-frequency N-grams to unseen events. Examples: Laplace (Add-1), Add-$m$ (Lidstone), Good-Turing.
2. **Back-off & Interpolation** — fall back to or blend with lower-order models (trigram → bigram → unigram) where counts are denser.
3. **Continuous / Neural Representations** — modern neural LMs (RNNs, Transformers) represent words in dense continuous vector spaces (embeddings) where semantically similar contexts share statistical strength instead of relying on exact string matches.

### C.19 Smoothing — Laplace (Add-1)

**Laplace smoothing** pretends that every possible N-gram in the vocabulary has been observed one extra time.

**Bigram Laplace formula:**
$$P_{\text{Laplace}}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + |V|}$$

where $|V|$ is the vocabulary size.

**Why add $|V|$ to the denominator?** To maintain a valid probability distribution: $\sum_{w_k \in V} P(w_k \mid w_{k-1}) = 1$:

$$\sum_{w_k \in V} \frac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + |V|} = \frac{\sum_{w} C(w_{k-1}, w) + \sum_{w} 1}{C(w_{k-1}) + |V|} = \frac{C(w_{k-1}) + |V|}{C(w_{k-1}) + |V|} = 1$$

### C.20 Smoothing — Add-$m$ (Lidstone)

**Problem with Laplace:** Adding an entire virtual count of 1 is far too aggressive when $|V|$ is large (e.g., 50,000). It shifts an overwhelming amount of probability mass from observed data to unseen pairs, severely degrading model accuracy.

**Add-$m$ smoothing** replaces the integer 1 with a fractional pseudo-count $m$ (typically $0 < m < 1$, e.g., $m = 0.05$ or $m = 0.1$):

$$P_{\text{Add-}m}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + m}{C(w_{k-1}) + m|V|}$$

**Tuning $m$:** treated as a hyper-parameter, tuned on a validation (held-out) set to minimise perplexity before evaluating on the test set.

**Behaviour:**
- As $m \to 0$: approaches pure MLE.
- As $m \to 1$: becomes standard Laplace smoothing.

### C.21 Branching Factor

The **branching factor** in an N-gram LM is the number of plausible next words the model is trying to choose among given a preceding history $w_{k-N+1}, \ldots, w_{k-1}$. Because language distributions are non-uniform, the branching factor is measured as an **effective branching factor**, which is mathematically identical to perplexity.

**Why perplexity = branching factor?**

- **Uniform case (worst):** $|V| = 10{,}000$ words, each equally likely with $P(w) = 1/10{,}000$.
  - $H = -\log_2(1/10{,}000) = \log_2 10{,}000 \approx 13.29$ bits
  - $\text{PP} = 2^H = 10{,}000$ → effective branching factor = 10,000 (model is blindly choosing).

- **Skewed case (realistic):** Model concentrates high probability on a few words; residual on a few others.
  - $H < 13.29$ bits, $\text{PP} < 10{,}000$ → effective branching factor is smaller (model is "more certain").

### C.22 Back-off vs Interpolation

Both address data sparsity by combining evidence from higher-order N-grams (richer context, but sparse) with lower-order N-grams (weaker context, but denser counts).

#### C.22.1 Linear Interpolation

Always blends probability estimates from **all orders**, regardless of whether the higher-order N-gram was observed:

$$P_{\text{interp}}(w_k \mid w_{k-2}, w_{k-1}) = \lambda_3 P_{\text{MLE}}(w_k \mid w_{k-2}, w_{k-1}) + \lambda_2 P_{\text{MLE}}(w_k \mid w_{k-1}) + \lambda_1 P_{\text{MLE}}(w_k)$$

with $\sum_{j=1}^{3} \lambda_j = 1$ and $\lambda_j \geq 0$.

**Setting the weights:**
- **Static weights:** fixed $\lambda_1, \lambda_2, \lambda_3$ tuned on a held-out validation set (often using the **Expectation-Maximization (EM)** algorithm) to minimise validation perplexity.
- **Context-dependent weights:** let $\lambda$ depend on context frequency. If the history $(w_{k-2}, w_{k-1})$ appears frequently in training, $\lambda_3$ is set higher; if rare, $\lambda_3$ is downscaled in favour of lower-order estimates.

#### C.22.2 Back-off (Katz)

Uses the **highest-order N-gram if it has sufficient evidence**; falls back to lower-order models only when the higher-order count is zero (or below a threshold).

$$P_{\text{BO}}(w_k \mid w_{k-2}, w_{k-1}) = \begin{cases} P^*(w_k \mid w_{k-2}, w_{k-1}) & \text{if } C(w_{k-2}, w_{k-1}, w_k) > 0 \\ \alpha(w_{k-2}, w_{k-1}) \cdot P_{\text{BO}}(w_k \mid w_{k-1}) & \text{if } C(w_{k-2}, w_{k-1}, w_k) = 0 \end{cases}$$

where:
- $P^*(w_k \mid w_{k-2}, w_{k-1}) = \dfrac{C(w_{k-2}, w_{k-1}, w_k) - d}{C(w_{k-2}, w_{k-1})}$ is the **discounted** probability (discount parameter $d$ typically $0 < d < 1$). Discounting frees up probability mass for the lower-order fallback.
- $\alpha(w_{k-2}, w_{k-1})$ is the **back-off weight / normalisation factor** ensuring the leftover mass sums to 1:
  $$\alpha(w_{k-2}, w_{k-1}) = \frac{1 - \sum_{w: C(w_{k-2}, w_{k-1}, w) > 0} P^*(w \mid w_{k-2}, w_{k-1})}{\sum_{w: C(w_{k-2}, w_{k-1}, w) = 0} P_{\text{BO}}(w \mid w_{k-1})}$$

#### C.22.3 Difference (memorise for viva)

| Aspect | Interpolation | Back-off |
|---|---|---|
| When are lower orders used? | Always (blended) | Only when higher-order count = 0 |
| Higher-order probabilities modified? | No (just weighted) | Yes (discounted to free mass) |
| Computation | Cheaper (one formula) | Slightly more complex |
| Typical algorithm | Jelinek-Mercer (static), Bellereo (context-dep.) | Katz back-off, Kneser-Ney |

### C.23 Laplace Smoothing Worked Example (Week 8-9 PPT)

Using the same training corpus as before:
```
<s> I am Sam </s>
<s> Sam I am </s>
<s> I do not like green eggs </s>
```

**Vocabulary:** $\{<s>, </s>, \text{I}, \text{am}, \text{Sam}, \text{do}, \text{not}, \text{like}, \text{green}, \text{eggs}\}$ → $|V| = 10$.

**Unigram counts:**
| $w$ | $C(w)$ |
|---|:---:|
| `<s>` | 3 |
| `</s>` | 3 |
| I | 3 |
| am | 2 |
| Sam | 2 |
| do | 1 |
| not | 1 |
| like | 1 |
| green | 1 |
| eggs | 1 |

**Relevant bigram counts:**

| Bigram | Count |
|---|:---:|
| `<s>, I` | 2 |
| `<s>, Sam` | 1 |
| `I, am` | 2 |
| `I, do` | 1 |
| `am, Sam` | 1 |
| `am, </s>` | 1 |
| `Sam, </s>` | 1 |
| `Sam, I` | 1 |
| (all others) | 0 |

**Test sequence:** `<s> I am Sam </s>` — predict 4 tokens ($w_1 = \text{I}, w_2 = \text{am}, w_3 = \text{Sam}, w_4 = \text{</s>}$), $n = 4$.

**Step 1 — Laplace-smoothed bigram probabilities ($|V| = 10$):**

| Step | $P(w_k \mid w_{k-1}) = \dfrac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + 10}$ | Value |
|:---:|---|:---:|
| 1 | $P(\text{I} \mid \text{<s>}) = \dfrac{2+1}{3+10} = \dfrac{3}{13}$ | $\approx 0.23077$ |
| 2 | $P(\text{am} \mid \text{I}) = \dfrac{2+1}{3+10} = \dfrac{3}{13}$ | $\approx 0.23077$ |
| 3 | $P(\text{Sam} \mid \text{am}) = \dfrac{1+1}{2+10} = \dfrac{2}{12} = \dfrac{1}{6}$ | $\approx 0.16667$ |
| 4 | $P(\text{</s>} \mid \text{Sam}) = \dfrac{1+1}{2+10} = \dfrac{2}{12} = \dfrac{1}{6}$ | $\approx 0.16667$ |

**Step 2 — Sentence probability:**
$$P(W) = \frac{3}{13} \times \frac{3}{13} \times \frac{1}{6} \times \frac{1}{6} = \frac{9}{169 \times 36} = \frac{9}{6084} = \frac{1}{676} \approx 0.00148$$

**Step 3 — Perplexity (direct formula, $n = 4$):**
$$\text{PP}(W) = P(W)^{-1/4} = \left(\frac{1}{676}\right)^{-1/4} = 676^{1/4} = \sqrt{26} \approx 5.099$$

**Step 4 — Cross-entropy method (verification):**

| Bigram | $\log_2 P$ |
|---|---|
| $\log_2(3/13)$ | $\approx -2.11547$ |
| $\log_2(3/13)$ | $\approx -2.11547$ |
| $\log_2(1/6)$ | $\approx -2.58496$ |
| $\log_2(1/6)$ | $\approx -2.58496$ |

$$H(W) = -\frac{1}{4}(-2.11547 - 2.11547 - 2.58496 - 2.58496) = -\frac{1}{4}(-9.40086) \approx 2.35022 \text{ bits/word}$$

$$\text{PP}(W) = 2^{2.35022} \approx 5.099 \quad \checkmark$$

**Interpretation:** The model exhibits an effective branching factor of ~5.10 on this test sequence. (Compare this to the unsmoothed bigram PP of 1.732 — Laplace smoothing has *increased* perplexity, because it shifted probability mass away from observed bigrams to unseen ones. This is the well-known drawback of Add-1 smoothing for sparse N-gram LMs, and motivates the use of Add-$m$ with small $m$ or Kneser-Ney smoothing in practice.)

---

## Section D — Numerical Practice Problems (Master Set)

This section collects every numerical pattern that the professor has either already asked in 2024/2025 or has explicitly included in the Week 2-9 PPTs. **The professor's email says "Questions will be based on numericals, analyticals, logicals and justifications"** — and 2025 had *no* numericals, so one of these is almost certain to appear.

### D.1 BPE Merges — Practice Variant

**Problem.** Given the training corpus below, perform exactly 6 BPE merges.

| Word | Frequency |
|---|---:|
| read | 3 |
| reads | 2 |
| reader | 2 |
| reading | 2 |
| unread | 1 |
| readers | 1 |

(Answer is the table in Section B.8.4 — re-derive it without looking.)

**Test on new words:** `readable`, `reread`, `unreader`. (Answers in B.8.4.)

### D.2 Cosine Similarity

**Problem.** Using the co-occurrence matrix in Section C.3, compute:
- $\text{cosine}(\mathbf{v}_{\text{data}}, \mathbf{v}_{\text{analysis}})$
- $\text{cosine}(\mathbf{v}_{\text{drives}}, \mathbf{v}_{\text{analysis}})$
- $\text{cosine}(\mathbf{v}_{\text{insight}}, \mathbf{v}_{\text{analysis}})$

**Answers:**

- $\mathbf{v}_{\text{data}} = (0, 1, 1, 0, 0),\ \mathbf{v}_{\text{analysis}} = (1, 0, 0, 1, 0)$ → dot = $0 \cdot 1 + 1 \cdot 0 + 1 \cdot 0 + 0 \cdot 1 + 0 \cdot 0 = 0$ → **cosine = 0**.
- $\mathbf{v}_{\text{drives}} = (0, 1, 1, 0, 2),\ \mathbf{v}_{\text{analysis}} = (1, 0, 0, 1, 0)$ → dot = 0 → **cosine = 0**.
- $\mathbf{v}_{\text{insight}} = (0, 0, 0, 2, 0),\ \mathbf{v}_{\text{analysis}} = (1, 0, 0, 1, 0)$ → dot = $0 \cdot 1 + 0 + 0 + 2 \cdot 1 + 0 = 2$.
  - $\|\mathbf{v}_{\text{insight}}\| = \sqrt{4} = 2$; $\|\mathbf{v}_{\text{analysis}}\| = \sqrt{2}$.
  - **cosine** $= \dfrac{2}{2 \cdot \sqrt{2}} = \dfrac{1}{\sqrt{2}} \approx 0.707$.

### D.3 PPMI Matrix Computation

**Problem.** Using the toy corpus in Section C.3, compute the full PPMI matrix (full solution in Section C.5).

**Quick formula recap:**
$$\text{PMI}(w, c) = \log_2 \frac{C(w, c) \cdot N}{C(w) \cdot C(c)}, \quad \text{PPMI}(w, c) = \max(0, \text{PMI}(w, c))$$

### D.4 TF-IDF Computation (2 documents)

**Problem.** For the two documents in Section C.7, re-derive the sklearn-style TF-IDF matrix using:
$$\text{IDF}(t, D) = \ln\left(\frac{1 + |D|}{1 + \text{df}(t)}\right) + 1, \quad \text{TF-IDF}(t, d) = \text{TF}(t, d) \cdot \text{IDF}(t, D)$$

then L2-normalise each document vector.

**Expected normalised values** (full derivation in C.7):
- Doc 1: `data, google` = 0.2902; `earning, jumps, price, stock, today` = 0.4078; `china, plunge` = 0.
- Doc 2: `china, plunge` = 0.5762; `data, google` = 0.4099; all others = 0.

### D.5 Bigram MLE Probability + Perplexity

**Problem.** Given the training corpus in Section C.12 and test sequence `<s> I am Sam </s>`:
1. Compute the four bigram MLE probabilities.
2. Compute $P(W)$.
3. Compute PP(W) directly and via cross-entropy.

**Answers:** see Section C.12–C.15. $P(W) = 1/9 \approx 0.1111$; $\text{PP}(W) = \sqrt{3} \approx 1.732$; $H(W) = 0.79248$ bits/word.

### D.6 Trigram MLE Probability + Perplexity

**Problem.** Repeat D.5 using a trigram model (augment training corpus with an extra `<s>` per sentence).

**Answers:** see Section C.16. $P(W) = 1/6 \approx 0.1667$; $\text{PP}(W) = 6^{1/4} \approx 1.565$; $H(W) = 0.64624$ bits/word.

### D.7 Laplace (Add-1) Smoothing + Perplexity

**Problem.** For the corpus in Section C.23, with $|V| = 10$, compute the Laplace-smoothed bigram probabilities and perplexity on `<s> I am Sam </s>`.

**Answers:** see Section C.23.
- $P(\text{I} \mid \text{<s>}) = P(\text{am} \mid \text{I}) = 3/13 \approx 0.23077$.
- $P(\text{Sam} \mid \text{am}) = P(\text{</s>} \mid \text{Sam}) = 1/6 \approx 0.16667$.
- $P(W) = 1/676 \approx 0.00148$.
- $\text{PP}(W) = 676^{1/4} = \sqrt{26} \approx 5.099$.
- $H(W) \approx 2.35022$ bits/word.

### D.8 Argmax for Bigram Decoding (PYQ 2024 Q1-C pattern)

**Problem.** Given candidates $w_2 \in \{\text{cat, bat, rat}\}$ and bigram counts $C(\text{the, cat}) = 50,\ C(\text{the, bat}) = 5,\ C(\text{the, rat}) = 3$, and $C(\text{the}) = 200$, find the most probable continuation after "the".

**Solution:** Compute $P(w_2 \mid \text{the}) = C(\text{the}, w_2) / C(\text{the})$.
- $P(\text{cat} \mid \text{the}) = 50/200 = 0.25$
- $P(\text{bat} \mid \text{the}) = 5/200 = 0.025$
- $P(\text{rat} \mid \text{the}) = 3/200 = 0.015$

$\arg\max = \text{cat}$. The most probable sequence is "the cat …".

### D.9 Branching Factor Calculation

**Problem.** A language model has $|V| = 10{,}000$ words. On a test set of $n = 100$ tokens, the average per-token probability is $P = 10^{-3}$. Compute the cross-entropy and perplexity.

**Solution:**
- $H = -\log_2(10^{-3}) = 3 \cdot \log_2 10 \approx 3 \times 3.3219 \approx 9.966$ bits/word.
- $\text{PP} = 2^{H} = 2^{9.966} \approx 10^3 = 1000$.

The effective branching factor is 1000, much smaller than the vocabulary size 10,000 — the model has learned that most words are very unlikely given their contexts.

---

## Section E — PYQ Solutions (2024 & 2025)

### E.1 2024 Mid-sem — Full Solutions (50 marks, 2 hours)

#### Q1 (A) — Regex for email detection [3 marks]

**Sentence:** `"I am a student with email id abc@xyz.com and my friend's email is abc.def@xyz.co.in."`

**Regex:** `[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}(?:\.[A-Za-z]{2,})*`

**Python:**
```python
import re
text = "I am a student with email id abc@xyz.com and my friend's email is abc.def@xyz.co.in."
pattern = r'[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}(?:\.[A-Za-z]{2,})*'
re.findall(pattern, text)
# ['abc@xyz.com', 'abc.def@xyz.co.in']
```

**Explanation (worth ~1.5 marks of the 3):**
- `[A-Za-z0-9._%+-]+` → local part (letters, digits, dots, underscores, %, +, -)
- `@` → literal "@"
- `[A-Za-z0-9.-]+` → domain name
- `\.[A-Za-z]{2,}` → top-level domain (≥ 2 letters)
- `(?:\.[A-Za-z]{2,})*` → optional country-code TLDs (e.g., `.in`, `.uk`)

#### Q1 (B) — POS tagging with example [1 + 2 marks]

**Definition (1 mark):** POS tagging is the process of assigning a grammatical category — noun, verb, adjective, adverb, etc. — to each word in a sentence. The goal is to resolve ambiguities (e.g., `book` can be a noun or verb depending on context).

**Example (2 marks):** Sentence: "Google is looking at buying U.K. startup for $1 billion"

| Token | POS tag (Penn Treebank) | Meaning |
|---|---|---|
| Google | NNP | Singular proper noun |
| is | VBZ | Verb, 3rd-sing present |
| looking | VBG | Verb, gerund / present participle |
| at | IN | Preposition |
| buying | VBG | Verb, gerund |
| U.K. | NNP | Singular proper noun |
| startup | NN | Singular noun |
| for | IN | Preposition |
| 1 | CD | Cardinal number |
| billion | CD | Cardinal number |

```python
from textblob import TextBlob
TextBlob('Google is looking at buying U.K. startup for $1 billion').tags
```

#### Q1 (C) — Argmax for "The cat chased the mouse" bigram [4 marks]

**Setup:** Given a bigram LM, the most probable word sequence $\hat{W}$ maximises:

$$\hat{W} = \arg\max_W \prod_{k=1}^{n} P(w_k \mid w_{k-1})$$

**Step 1 — Identify candidate tokens at each position** (typical exam pattern: a small candidate set is given per slot, with a small acoustic-model likelihood $P(\text{obs} \mid w)$). Let us denote:

- $w_1$: only "The" is plausible.
- $w_2 \in \{$"cat", "bat", "rat"$\}$ (acoustic confusion set).
- $w_3 \in \{$"chased", "ate"$\}$.
- $w_4$: only "the" is plausible.
- $w_5 \in \{$"mouse", "house"$\}$.

**Step 2 — Pull bigram probabilities** from the training corpus (or a given LM table). For illustration:

| Bigram | $P$ |
|---|:---:|
| $P(\text{cat} \mid \text{the})$ | 0.05 |
| $P(\text{bat} \mid \text{the})$ | 0.005 |
| $P(\text{rat} \mid \text{the})$ | 0.003 |
| $P(\text{chased} \mid \text{cat})$ | 0.10 |
| $P(\text{ate} \mid \text{cat})$ | 0.05 |
| $P(\text{chased} \mid \text{bat})$ | 0.02 |
| $P(\text{ate} \mid \text{bat})$ | 0.10 |
| $P(\text{the} \mid \text{chased})$ | 0.30 |
| $P(\text{the} \mid \text{ate})$ | 0.20 |
| $P(\text{mouse} \mid \text{the})$ | 0.04 |
| $P(\text{house} \mid \text{the})$ | 0.06 |

**Step 3 — Enumerate candidate sequences and compute $P(W)$ for each.**

E.g., sequence `"The cat chased the mouse"`:
$$P = 0.05 \times 0.10 \times 0.30 \times 0.04 = 6.0 \times 10^{-5}$$

Sequence `"The cat ate the mouse"`:
$$P = 0.05 \times 0.05 \times 0.20 \times 0.04 = 2.0 \times 10^{-5}$$

Sequence `"The bat chased the house"`:
$$P = 0.005 \times 0.02 \times 0.30 \times 0.06 = 1.8 \times 10^{-6}$$

**Step 4 — Take argmax.** The maximum is achieved by `"The cat chased the mouse"`. This is exactly what we expected, and demonstrates how the LM disambiguates acoustically confusable candidates by preferring high-probability bigrams.

#### Q2 (A) — Place and manner of articulation [5 marks]

(Full content in Section B.15.1. For a 5-mark answer, write the definition of each, list the major places (8) and manners (6) with one example each, and include the voicing distinction.)

#### Q2 (B) — Stemming vs Morphological Analysis [2.5 + 2.5 marks]

(Full content in Section B.10. For 2.5 marks each: define + 1 example for each, then a contrast paragraph.)

#### Q3 (A) — Word tokenisation on `"Natural language processing is a field of computer science."` [5 marks]

(Full model answer in Section B.8.2.)

#### Q3 (B) — HMM model for speech recognition [5 marks]

(Full content in Section B.15.4. For 5 marks, draw the architecture: states (phonemes), observations (MFCCs), transition matrix $A$, emission model $B$, initial $\pi$, and describe the Viterbi decoding workflow.)

#### Q4 (A) — Computational grammar [5 marks]

(Full content in Section B.16. For 5 marks, define + 5 reasons why it's necessary + a CFG example like `S → NP VP`, `NP → Det N`.)

#### Q4 (B) — Word boundary detection [5 marks]

(Full content in Section B.15.2. For 5 marks, define + list challenges (4) + strategies (5) + an example in Chinese/Japanese.)

#### OR — Q4 (A) — Preprocessing pipeline on `"NLP is an exciting field of artificial intelligence."` [5 marks]

Apply each preprocessing step:

1. **Tokenisation (whitespace then NLTK `word_tokenize`):**
   - Whitespace: `['NLP', 'is', 'an', 'exciting', 'field', 'of', 'artificial', 'intelligence.']`
   - `word_tokenize`: `['NLP', 'is', 'an', 'exciting', 'field', 'of', 'artificial', 'intelligence', '.']`
2. **Lowercasing:** `['nlp', 'is', 'an', 'exciting', 'field', 'of', 'artificial', 'intelligence', '.']`
3. **Stop-word removal:** `['nlp', 'exciting', 'field', 'artificial', 'intelligence']` (removed: is, an, of)
4. **Stemming (Snowball):** `['nlp', 'excit', 'field', 'artifici', 'intellig']` (stems may not be real words)
5. **Lemmatisation (spaCy):** `['nlp', 'exciting', 'field', 'artificial', 'intelligence']` (all words already in lemma form here)
6. **POS tagging:** `nlp/NN, exciting/JJ, field/NN, artificial/JJ, intelligence/NN`
7. **Vectorisation (BoW or TF-IDF):** final numerical vector ready for ML.

#### OR — Q4 (B) — MP3 vs FLAC [5 marks]

(Full content in Section B.17.3. For 5 marks, draw the comparison table; mention lossy vs lossless, bitrate, file size, use case; recommend FLAC for NLP training corpora.)

#### Q5 (A) — Text classification vs MT datasets [6 marks]

(Full content in Section B.18. For 6 marks, draw the comparison table; explain how the nature of the corpus and attributes changes.)

#### Q5 (B) — Nominal vs Ordinal + Interval-scaled + Ratio-scaled [2 + 2 marks]

(Full content in Section B.17.1. Provide one NLP-relevant example for each: nominal = POS tag, ordinal = difficulty level, interval = publication year, ratio = word count.)

#### OR — Q5 (A) — Components of speech recognition with workflow [6 marks]

(Full content in Section B.15.5. For 6 marks, list the 5 components (front-end, acoustic model, pronunciation lexicon, LM, decoder), then draw the workflow diagram.)

#### OR — Q5 (B) — JSON vs CSV with example [2 + 2 marks]

(Full content in Section B.17.2. Comparison table + a small CSV example + a small JSON example, ideally of the same data for direct comparison.)

---

### E.2 2025 Mid-sem — Full Solutions (25 marks, 60 minutes)

> This is the paper format you should expect this year.

#### Q1 — Components of NLP system + differences [5 marks]

**Answer** (full content in Section B.5):

A complete NLP system has five components:

1. **Lexical Analysis (Tokenisation)** — breaks raw text into tokens (words, sub-words, punctuation). Input: raw text. Output: tokens.
2. **Syntactic Analysis (Parsing)** — analyses grammar and produces a parse tree showing how words combine into phrases. Input: tokens. Output: parse tree.
3. **Semantic Analysis** — extracts the meaning of the sentence: word-sense disambiguation, semantic roles. Input: parse tree. Output: meaning representation.
4. **Discourse / Pragmatic Analysis** — handles context outside the sentence: coreference resolution, conversational implicature. Input: sentences. Output: resolved references, intentions.
5. **Application Layer** — task-specific (sentiment classifier, MT engine, QA, etc.).

**Differences** (the crux of the question):

| Component | Level | Input → Output |
|---|---|---|
| Lexical | Word | raw text → tokens |
| Syntactic | Sentence | tokens → parse tree |
| Semantic | Sentence | parse tree → meaning |
| Discourse / Pragmatic | Document | sentences → resolved references |
| Application | Task | any of the above → task output |

Each component answers a different question ("What are the units?", "Is it grammatical?", "What does it mean?", "What was intended?", "What should I do?"), and they build on each other sequentially.

#### Q2 — Word boundary detection challenges OR HMM in ASR [10 marks]

**Option A — Word boundary detection challenges with examples:**

(Full content in Section B.15.2. For 10 marks, structure as: definition (2) + challenges in speech (3) + challenges in text (3) + examples across languages (1) + strategies to handle errors (1).)

Key points to cover:
- **In speech:** no acoustic pauses between words; coarticulation; assimilation; speaker rate variation; disfluencies; code-switching. Example: English "did you" → "didja"; Hindi-English code-switching.
- **In text:** languages without spaces (Chinese, Japanese, Thai); compound words (German `Rindfleischetikettierungsüberwachungsaufgabenübertragungsgesetz`); hyphenation (`state-of-the-art`); contractions (`don't`). Example: Chinese "我喜欢自然语言处理" must be segmented as "我 / 喜欢 / 自然 / 语言 / 处理".
- **Strategies:** acoustic-phonetic features (pauses, pitch reset, vowel lengthening); LM priors; dictionary lookup; sub-word models (BPE, SentencePiece); end-to-end Transformer ASR (Whisper, Conformer).

**Option B — HMM in ASR with example:**

(Full content in Section B.15.4. For 10 marks, structure as: definition (2) + three HMM problems (2) + construction of HMM for ASR with states/observations/A/B/π (3) + workflow of processing speech signal (2) + worked example (1).)

The worked example should describe: a 3-state left-to-right HMM for the phoneme /ae/ (onset / nucleus / coda); transition matrix with self-loops and forward transitions only; emissions modelled by a Gaussian over MFCC vectors; Viterbi decoding finds the most probable phoneme sequence given MFCC observations; combined with the LM, this gives the most probable word sequence.

#### Q3 — Define the following (2 marks each):

**(a) Tokenization** — The fundamental NLP process of breaking a stream of text into smaller units called tokens using a set of predetermined rules. A token may be a word, sub-word, character, or punctuation mark. Example: `"Hello, world!"` → `['Hello', ',', 'world', '!']`.

**(b) Stemming** — A heuristic process that reduces a word to its base form (called a stem) by stripping suffixes and prefixes using fixed rules. The output stem need not be a real word. Example (Snowball stemmer): `running → run`, `studies → studi`.

**(c) Morphological Analysis** — The process of breaking a word into its constituent morphemes (the smallest meaning-bearing units of a language), considering the grammatical role of each morpheme (root, prefix, suffix, plural marker, tense marker, etc.). Example: `unhappiness` = `un-` (negative prefix) + `happy` (root) + `-ness` (nominalising suffix). It uses linguistic knowledge and is more sophisticated than stemming.

**(d) Computational Grammar** — The formal specification of the syntactic rules of a language in a machine-processable form. It defines which strings of words are grammatical and assigns each a structural description (parse tree). Example: a CFG rule `S → NP VP` says a sentence is a noun phrase followed by a verb phrase.

**(e) Place and Manner of Articulation** — In phonetics, **place** of articulation is *where* in the vocal tract a consonant is constricted (e.g., bilabial for /p/, /b/, /m/; alveolar for /t/, /d/, /s/; velar for /k/, /g/). **Manner** of articulation is *how* the airstream is constricted (e.g., plosive /p/, /t/, /k/; fricative /f/, /s/; nasal /m/, /n/). Together with voicing, they uniquely identify a consonant.

---

## Section F — Python Code Snippets (Quick Reference)

These are the exact library calls that have appeared in the Week 2-3 PPTs. Memorise the import + the one-liner; you may be asked to "write code for …" in a 5-mark question.

### F.1 Tokenisation

```python
# Whitespace tokenizer (NLTK)
from nltk.tokenize import WhitespaceTokenizer
tokens = WhitespaceTokenizer().tokenize("Hello, world! This is NLP.")
# ['Hello,', 'world!', 'This', 'is', 'NLP.']

# Word tokenizer (NLTK Punkt — handles punctuation)
from nltk.tokenize import word_tokenize
tokens = word_tokenize("Hello, world! This is NLP.")
# ['Hello', ',', 'world', '!', 'This', 'is', 'NLP', '.']

# Download punkt model (one-time)
import nltk
nltk.download('punkt')
```

### F.2 Stop-word Removal

```python
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize

text = "S&P and NASDAQ are the two most popular indices in US"
tokens = word_tokenize(text)
sw = set(stopwords.words('english'))
clean = [w for w in tokens if w.lower() not in sw]
# ['S', '&', 'P', 'NASDAQ', 'two', 'popular', 'indices', 'US']
```

### F.3 Stemming (Snowball)

```python
from nltk.stem.snowball import SnowballStemmer
from nltk.tokenize import word_tokenize

stemmer = SnowballStemmer('english')
text = "It's a Stemming testing"
parsed = word_tokenize(text)
out = [(w, stemmer.stem(w)) for w in parsed if w.lower() != stemmer.stem(w)]
# [('Stemming', 'stem'), ('testing', 'test')]
```

### F.4 Lemmatisation (TextBlob)

```python
from textblob import TextBlob

text = "This world has a lot of faces"
parsed = TextBlob(text).words
out = [(w, w.lemmatize()) for w in parsed if w != w.lemmatize()]
# [('has', 'ha'), ('faces', 'face')]   -- (TextBlob's default lemmatiser is imperfect)
```

### F.5 POS Tagging (TextBlob)

```python
from textblob import TextBlob

text = 'Google is looking at buying U.K. startup for $1 billion'
TextBlob(text).tags
# [('Google','NNP'), ('is','VBZ'), ('looking','VBG'), ('at','IN'),
#  ('buying','VBG'), ('U.K.','NNP'), ('startup','NN'),
#  ('for','IN'), ('1','CD'), ('billion','CD')]
```

### F.6 NER (spaCy)

```python
import spacy
nlp = spacy.load('en_core_web_sm')

text = 'Google is looking at buying U.K. startup for $1 billion'
for ent in nlp(text).ents:
    print("Entity:", ent.text)
# Entity: Google
# Entity: U.K.
# Entity: $1 billion

# Visualise
from spacy import displacy
displacy.render(nlp(text), style="ent", jupyter=True)
```

### F.7 All-in-one Pipeline (spaCy)

```python
import spacy, pandas as pd
nlp = spacy.load('en_core_web_sm')

text = 'Google is looking at buying U.K. startup for $1 billion'
doc = nlp(text)
pd.DataFrame([[t.text, t.is_stop, t.lemma_, t.pos_] for t in doc],
             columns=['Token', 'is_stop_word', 'lemma', 'POS'])
```

### F.8 TF-IDF (sklearn)

```python
from sklearn.feature_extraction.text import TfidfVectorizer

sentences = [
    'The stock price of google jumps on the earning data today',
    'Google plunge on China Data!'
]
vectorizer = TfidfVectorizer(stop_words='english')
TFIDF = vectorizer.fit_transform(sentences)

print(vectorizer.get_feature_names_out())
print(TFIDF.shape)
print(TFIDF.toarray())
```

### F.9 N-gram LM Counting (sklearn)

```python
from sklearn.feature_extraction.text import CountVectorizer

corpus = ["I am Sam", "Sam I am", "I do not like green eggs"]
vectorizer = CountVectorizer(ngram_range=(2, 2))  # bigrams
X = vectorizer.fit_transform(corpus)
print(vectorizer.get_feature_names_out())
print(X.toarray())
```

---

## Section G — Formula Cheat Sheet (Memorise Verbatim)

### G.1 Probability & Bayes

| Name | Formula |
|---|---|
| Chain rule | $P(w_1, \ldots, w_n) = \prod_k P(w_k \mid w_1, \ldots, w_{k-1})$ |
| Bayes' rule | $P(W \mid X) = \dfrac{P(X \mid W) P(W)}{P(X)}$ |
| Argmax decoding | $\hat{W} = \arg\max_W P(X \mid W) P(W)$ |

### G.2 N-gram MLE

| Model | Formula |
|---|---|
| Unigram MLE | $P(w_k) = \dfrac{C(w_k)}{N_{\text{total}}}$ |
| Bigram MLE | $P(w_k \mid w_{k-1}) = \dfrac{C(w_{k-1}, w_k)}{C(w_{k-1})}$ |
| Trigram MLE | $P(w_k \mid w_{k-2}, w_{k-1}) = \dfrac{C(w_{k-2}, w_{k-1}, w_k)}{C(w_{k-2}, w_{k-1})}$ |
| N-gram MLE | $P(w_k \mid w_{k-N+1:k-1}) = \dfrac{C(w_{k-N+1:k})}{C(w_{k-N+1:k-1})}$ |

### G.3 Perplexity & Cross-Entropy

| Quantity | Formula |
|---|---|
| Perplexity (direct) | $\text{PP}(W) = P(W)^{-1/n} = \left(\prod_k P(w_k \mid \ldots)\right)^{-1/n}$ |
| Cross-entropy | $H(W) = -\dfrac{1}{n} \sum_k \log_2 P(w_k \mid \ldots)$ |
| PP from H | $\text{PP}(W) = 2^{H(W)}$ |

### G.4 Smoothing

| Method | Formula |
|---|---|
| Laplace (Add-1) bigram | $P_{\text{Lap}}(w_k \mid w_{k-1}) = \dfrac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + |V|}$ |
| Add-$m$ bigram | $P_{\text{Add-}m}(w_k \mid w_{k-1}) = \dfrac{C(w_{k-1}, w_k) + m}{C(w_{k-1}) + m|V|}$ |
| Linear interpolation (trigram) | $P = \lambda_3 P_3 + \lambda_2 P_2 + \lambda_1 P_1, \quad \sum \lambda_i = 1$ |
| Katz back-off | $P_{\text{BO}} = P^*$ if $C > 0$, else $\alpha \cdot P_{\text{BO}}(\text{lower order})$ |

### G.5 Vectorisation

| Method | Formula |
|---|---|
| Cosine similarity | $\cos(\mathbf{u}, \mathbf{v}) = \dfrac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\| \, \|\mathbf{v}\|}$ |
| PMI | $\text{PMI}(w, c) = \log_2 \dfrac{C(w, c) \cdot N}{C(w) \cdot C(c)}$ |
| PPMI | $\text{PPMI}(w, c) = \max(0, \text{PMI}(w, c))$ |
| TF-IDF (basic) | $\text{TF-IDF}(t, d) = \text{TF}(t, d) \times \text{IDF}(t)$ |
| IDF (basic) | $\text{IDF}(t) = \log \dfrac{|D|}{\text{df}(t)}$ |
| Sklearn smoothed IDF | $\text{IDF}(t) = \ln\left(\dfrac{1 + |D|}{1 + \text{df}(t)}\right) + 1$ |
| L2 normalisation | $\hat{\mathbf{v}} = \dfrac{\mathbf{v}}{\|\mathbf{v}\|_2}$ |

### G.6 HMM

| Quantity | Formula |
|---|---|
| Forward probability | $\alpha_t(j) = \sum_i \alpha_{t-1}(i) a_{ij} b_j(o_t)$ |
| Viterbi recursion | $V_t(j) = \max_i V_{t-1}(i) a_{ij} b_j(o_t)$ |
| HMM parameters | $\lambda = (A, B, \pi)$ |

### G.7 Entropy & Branching Factor

| Quantity | Formula |
|---|---|
| Entropy | $H = -\sum_x p(x) \log_2 p(x)$ |
| Branching factor (uniform) | $|V|$ when $p(w) = 1/|V|$ for all $w$ |
| Effective branching factor | $\text{PP}(W)$ |

---

## Section H — Last-Minute Revision Checklist (Morning of the Exam)

### H.1 Definitions You Must Be Able to Give in 1-2 Sentences

- [ ] NLP
- [ ] Tokenisation (token vs type)
- [ ] Stop word
- [ ] Stemming (vs lemmatisation)
- [ ] Lemmatisation
- [ ] Morpheme / Morphological analysis
- [ ] POS tagging (8 basic parts of speech, Penn Treebank has 36 tags)
- [ ] Named Entity Recognition (NER)
- [ ] One-hot encoding
- [ ] Bag of Words
- [ ] TF-IDF
- [ ] PMI / PPMI
- [ ] Cosine similarity
- [ ] N-gram language model (unigram, bigram, trigram)
- [ ] Maximum Likelihood Estimation (MLE)
- [ ] Perplexity
- [ ] Cross-entropy
- [ ] Branching factor
- [ ] Data sparsity
- [ ] Smoothing (Laplace / Add-$m$ / Good-Turing)
- [ ] Back-off (Katz)
- [ ] Linear interpolation
- [ ] BPE (Byte-Pair Encoding)
- [ ] OOV word
- [ ] Place of articulation (8 places — bilabial, labio-dental, dental, alveolar, post-alveolar, palatal, velar, glottal)
- [ ] Manner of articulation (6 manners — plosive, fricative, affricate, nasal, approximant, lateral)
- [ ] Hidden Markov Model (3 problems: evaluation, decoding, learning)
- [ ] Viterbi algorithm
- [ ] Argmax decoding equation
- [ ] Computational grammar (CFG, dependencies)
- [ ] Word boundary detection
- [ ] Components of an NLP system (5: lexical, syntactic, semantic, discourse/pragmatic, application)
- [ ] Components of speech recognition (5: front-end, acoustic model, lexicon, LM, decoder)
- [ ] Nominal / Ordinal / Interval / Ratio data attributes
- [ ] CSV vs JSON
- [ ] MP3 vs FLAC

### H.2 Numerical Procedures You Must Be Able to Execute End-to-End

- [ ] **BPE:** Given a corpus, perform k merges (Section B.8.4, D.1).
- [ ] **Cosine similarity:** Given two vectors, compute (Section C.3, D.2).
- [ ] **PMI / PPMI:** Given a co-occurrence matrix, compute (Section C.5, D.3).
- [ ] **TF-IDF:** Given 2-3 documents, compute sklearn-style TF-IDF + L2 normalise (Section C.7, D.4).
- [ ] **Bigram MLE probability:** Given a corpus and a test sentence, compute $P(W)$ (Section C.12-C.15, D.5).
- [ ] **Bigram perplexity:** Both direct formula and via cross-entropy (Section C.15, D.5).
- [ ] **Trigram MLE + perplexity:** Same, with `<s> <s>` augmentation (Section C.16, D.6).
- [ ] **Laplace smoothing:** Compute smoothed bigram probs + perplexity (Section C.23, D.7).
- [ ] **Argmax decoding:** Given candidates per slot and bigram counts, pick the most probable sequence (Section D.8).

### H.3 Final 15-Minute Skim

1. Section A.3 — strategic prediction.
2. Section C.7 — TF-IDF worked example.
3. Section C.15 — bigram perplexity worked example.
4. Section C.16 — trigram perplexity worked example.
5. Section C.23 — Laplace smoothing worked example.
6. Section B.8.4 — BPE worked example.
7. Section G — formula cheat-sheet.

### H.4 Exam Hall Tips

- **Write the formula first, then plug in numbers.** Partial credit is almost always given for the correct formula.
- **For 2-mark definitions:** keep it to 2 lines + 1 small example. Do not write a paragraph.
- **For 5/10-mark answers:** structure your answer with explicit sub-headings (Definition, Formula, Example, Diagram, Advantages, Disadvantages). Examiners scan for these.
- **Always include the `</s>` token** when computing perplexity (n includes `</s>` but excludes the initial `<s>`).
- **For BPE merges:** if there's a tie, the PPT convention is "choose the leftmost pair from the word `read` if possible; otherwise alphabetical." Mention this if relevant.
- **For TF-IDF:** state explicitly whether you're using the basic IDF or the sklearn smoothed IDF. The numbers differ.
- **For Laplace:** always include $|V|$ in the denominator — forgetting it is the #1 source of mistakes.
- **Time check at 30 minutes:** you should have completed ~12 marks worth of questions. If you're behind, skip the optional OR option and focus on the one you started.

---

## Appendix — Source Material Acknowledgement

This preparation guide is built from the following source materials provided by Dr. Jigar Shah (PDEU, ICT) and shared via the course repository:

1. **PPTs (Weeks 1-9):** All slides converted to text via `pdftotext -layout`.
   - `NLP_Unit1_Week1.pdf` — Introduction to NLP, tasks, paradigms, timeline, syllabus.
   - `NLP_Unit1_Week2.pdf` — Tokenisation, whitespace tokeniser, sub-word (BPE) algorithm.
   - `NLP_Unit1_Week3.pdf` — Stop-word removal, stemming, lemmatisation, POS tagging, NER, BPE worked example.
   - `NLP_Unit2_Week4.pdf` — Text representation overview, one-hot encoding limitations.
   - `NLP_Unit2_Week5.pdf` — Co-occurrence matrix, cosine similarity, PMI/PPMI, TF-IDF worked example.
   - `NLP_Unit2_Week6_7.pdf` — N-gram LMs, chain rule, Markov approximation, MLE, perplexity worked examples.
   - `NLP_Unit2_Week8_9.pdf` — Data sparsity, Laplace/Add-$m$ smoothing, back-off, interpolation, branching factor.
2. **Previous Year Question Papers:**
   - `nlp2024midsem.png` — 2024 mid-sem (50 marks, 2 hours).
   - `nlp2025midsem.png` — 2025 mid-sem (25 marks, 60 minutes) — the format you will face.
   - `nlmpyq.md` — text transcription of both PYQs.

### Cross-References to Original PPT Slides

Every numerical example in this guide comes directly from the Week 2-9 PPTs. If you want to revisit the original slide for any worked example, the mapping is:

| Topic in this guide | Source PPT |
|---|---|
| BPE worked example (Section B.8.4) | `NLP_Unit1_Week3.pdf`, slides 18-21 |
| Co-occurrence matrix & cosine (Section C.3) | `NLP_Unit2_Week5.pdf`, slides 2-3 |
| PPMI worked example (Section C.5) | `NLP_Unit2_Week5.pdf`, slides 5-7 |
| TF-IDF worked example (Section C.7) | `NLP_Unit2_Week5.pdf`, slides 8-12 |
| Bigram MLE + perplexity (Section C.12-C.15) | `NLP_Unit2_Week6_7.pdf`, slides 11-15 |
| Trigram perplexity (Section C.16) | `NLP_Unit2_Week6_7.pdf`, slides 16-17 |
| Laplace smoothing worked example (Section C.23) | `NLP_Unit2_Week8_9.pdf`, slides 19-26 |
| Back-off & interpolation formulas (Section C.22) | `NLP_Unit2_Week8_9.pdf`, slides 27-29 |
| Branching factor (Section C.21) | `NLP_Unit2_Week8_9.pdf`, slides 13-16 |

---

*Best of luck for the exam. Trust the process: read every section once, work every numerical twice, and skim the cheat-sheet the morning of.*
