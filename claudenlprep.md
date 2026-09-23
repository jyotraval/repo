# NLP Midsem Prep — 20IC403T
*Built from: your professor's syllabus email, all 7 lecture PPTs (Weeks 1–9), and the 2024 + 2025 previous year question papers.*

---

## ⚠️ READ THIS FIRST — Scope Reality Check

I cross-checked your professor's email against the actual content of all 7 PPT decks and against both PYQ papers. There's an important mismatch you need to know about **before** you spend time on the wrong topics.

**Your professor's email says the midsem covers only:**
- **Unit 1: Introduction and Pre-processing**
- **Unit 2: Vectorization and N-gram LMs**
- "All PPTs up to week 9" (I have exactly these 7 files: Weeks 1,2,3,4,5,6-7,8-9 — so you have 100% of the assigned material)

**What the PPTs actually contain (Weeks 1–9):**
| Week(s) | Actual Content |
|---|---|
| 1 | What is NLP, NLP tasks, NLP paradigms, LLM basics, timeline |
| 2 | Preprocessing pipeline, tokenization, whitespace tokenization issues, subword tokenization, BPE algorithm |
| 3 | Stop words, stemming, lemmatization, POS tagging, NER, dependency parsing/coreference/triplet extraction, full BPE worked example |
| 4 | Text representation overview, One-Hot Encoding, Bag of Words |
| 5 | Co-occurrence matrices, Cosine Similarity, PMI/PPMI, TF-IDF (with worked numericals) |
| 6-7 | N-gram Language Models: chain rule, Markov assumption, MLE, worked bigram/trigram example, Perplexity, Cross-Entropy |
| 8-9 | Data sparsity, Laplace/Add-m smoothing, worked smoothing example, Backoff & Interpolation formulas |

**What this means for the old PYQs:** Both 2024 and 2025 papers test topics like **Place & Manner of Articulation, Word Boundary Detection, HMM for Speech Recognition, and Argmax-based sequence computation as a "speech" topic** — this is because in *those* years, "Unit 1" officially meant "Overview of NLP" (which includes speech processing) and "Unit 2" meant "Corpus and Datasets" (nominal/ordinal data, file formats, corpus types). **Neither of those two old units is what's being taught to you this semester.** Your Unit 2 this year is actually "Feature Representations and Extraction" (vectorization + N-grams) — a completely different unit that used to be Unit 4 material.

**Bottom line — my recommendation:**
- 🟢 **High priority (definitely study):** Tokenization, Stemming/Lemmatization/Morphological Analysis, POS tagging, NER, BPE, One-Hot/BoW, TF-IDF, Co-occurrence/PMI, N-gram LMs, Perplexity, Smoothing/Backoff — **all fully covered below with verified worked examples.**
- 🟡 **Medium priority (revise concept only, low chance):** Argmax-based computation — **still very relevant**, but reframed: it will almost certainly appear as "use argmax to find the most likely word/sequence in a bigram model," which is just N-gram MLE (I cover this fully in Unit 2 below), **not** the old speech-decoding argmax.
- 🔴 **Low/no priority (not in your slides — likely NOT tested):** Place/Manner of Articulation, Word Boundary Detection (speech), HMM for Speech Recognition, MP3/FLAC formats, Corpus attribute types (nominal/ordinal/interval/ratio), JSON vs CSV corpus formats, Computational Grammar as a named topic, Regex for email extraction (I've added a 2-minute primer for this last one just in case, since it's a generically useful and quick topic — see Appendix).
- If your professor announces closer to the exam that these old topics ARE included, come back and ask — but based on the syllabus email and slide content you gave me, they are out of scope.

---

## Table of Contents
1. [Unit 1 — Introduction & Pre-processing](#unit-1)
2. [Unit 2 — Vectorization & N-gram Language Models](#unit-2)
3. [Fully Verified Self-Test Practice Problems](#practice)
4. [PYQ Cross-Reference Table](#pyq-table)
5. [Predicted Question Bank / Mock Paper](#mock)
6. [One-Page Formula Cheat Sheet](#cheatsheet)
7. [Appendix: Regex Quick Primer](#appendix)

---

<a name="unit-1"></a>
## PART 1: UNIT 1 — Introduction & Pre-processing

### 1.1 What is NLP?
**Natural Language** = language that evolved naturally through human use (English, Hindi, etc.), as opposed to a programming language.

**NLP** = the field enabling computers to:
- Understand what we write/speak
- Generate write/speak output
- Interpret, manipulate, and comprehend human language for tasks like translation, summarization, speech-to-text, chatbots.

- **Conventional NLP** = rule-based + statistical approaches.
- **Deep learning–based NLP** = uses neural networks (RNN, CNN, Transformer) to process language.
- **LLM (Large Language Model)** = predicts the most likely next word in a sequence, trained on massive data (GPT, Gemini). Built on the **Transformer** architecture with billions of parameters.

**Common NLP tasks:** Sentiment Analysis, Machine Translation, Text Classification, Text Summarization, Question Answering, Text Entailment, NER, Chatbots, Language Modeling.

**NLP Paradigms** (map problems to ML task types):
| Paradigm | Example tasks |
|---|---|
| Text Classification | Sentiment analysis, news grouping |
| Sequence Labelling | NER, code-mixing detection |
| Text Generation | Machine translation, summarization, chatbots |

### 1.2 NLP Pipeline (Basic Flow)
```
Text Input (unstructured) → Language AI (processes input) → { Text Output (generative) | Embeddings (numeric) | Classification (identify targets) }
```
Input text characteristics: unstructured, free-form, variable length/style/grammar, often noisy (typos, emojis, abbreviations).

**Key libraries:**
| Library | Notes |
|---|---|
| NLTK | Most famous Python NLP library; ships `punkt` tokenizer |
| TextBlob | Built on NLTK; simplifies sentiment/POS/translation |
| spaCy | Fast, production-ready; one "best" algorithm per task |
| Gensim | Unsupervised topic modeling, document similarity |

### 1.3 Tokenization
**Definition:** Breaking a stream of text into smaller units called **tokens**, using a set of predetermined rules.

**Token vs Type:**
- **Token** = an instance of a word in running text.
- **Type** = a distinct element of the vocabulary.
- Example: *"they lay back on the San Francisco grass and looked at the stars and their"* → **15 tokens**, **13 types** (repeated words like "the" and "and" reduce type count).

#### Whitespace Tokenization
Splits on spaces/tabs/newlines. `"Hello, world! This is NLP."` → `['Hello,', 'world!', 'This', 'is', 'NLP.']`

**5 Major Issues (classic exam answer — memorize these):**
1. **Multi-word expressions split incorrectly** — "New York University" → 3 separate tokens, losing entity meaning.
2. **Punctuation stuck to words** — "Hello, world!" → `['Hello,', 'world!']` instead of separating punctuation.
3. **Fails for languages without spaces** — Chinese, Japanese, Korean.
4. **Special constructs broken** — emails (`john.doe@email.com`), URLs, phone numbers, dates, hyphenated words ("state-of-the-art").
5. **Retrieval problems** — searching "York University" wrongly matches "New York University" docs.

**Solution → Subword Tokenization** (BPE, WordPiece, SentencePiece): breaks rare words into meaningful subword units, handles compounds, manages OOV (Out-Of-Vocabulary) words.

#### Morphemes & Subwords
- **Morpheme** = smallest meaning-bearing unit of language. E.g. *fox* = 1 morpheme; *cats* = 2 morphemes (*cat* + *-s* plural); *unlikeliest* = {un-, likely, -est}.
- **Morphology** = study of how words are built from morphemes.
- Sentence segmented into morphemes: *"He work-ed care-ful-ly wash-ing the glass-es"*
- Unseen words are represented via known subword units: *lower* = {low, -er}

#### Byte-Pair Encoding (BPE) — Algorithm (IMPORTANT — numerical favorite)
**Token Learner (Training):**
1. Pre-tokenize corpus into words; append end-of-word symbol `_` to each.
2. Initialize vocabulary = set of all individual characters.
3. Find the most frequent **adjacent pair** of symbols (respecting word boundaries).
4. Merge it into a new symbol, add to vocabulary.
5. Replace all occurrences of that pair in the corpus with the merged symbol.
6. Repeat for *k* merges. (*k* is a hyperparameter — open research question.)

**Token Segmenter (Testing):** Apply the learned merges to new text, **in the same order they were learned**, greedily.

**Worked Example (from your slides):**
| corpus (freq) | word |
|---|---|
| 5 | l o w _ |
| 2 | l o w e s t _ |
| 6 | n e w e r _ |
| 3 | w i d e r _ |
| 2 | n e w _ |

Initial vocab: `_, d, e, i, l, n, o, r, s, t, w`
- Merge 1: most frequent adjacent pair → `(e,r)` → new token `er` (appears in "newer" freq 6 + "wider" freq 3 = 9 times)
- Merge 2: `(er, _)` → `er_`
- (Continues similarly for further merges)

**Second worked example (also from your slides) — read/reads/reader/reading/unread/readers:**
Vocabulary starts as: `_, a, d, e, g, i, n, r, s, u`

| Merge # | Most frequent pair | New token |
|---|---|---|
| 1 | (r, e) | re |
| 2 | (re, a) | rea |
| 3 | (rea, d) | read |
| 4 | (read, _) | read_ |
| 5 | (read, e) | reade |
| 6 | (reade, r) | reader |

**Testing on new/OOV words:** apply merges in the learned order.
- `read` → `read_` (fully known)
- `unreader` → `u n reader_` (falls back to characters for unseen parts)
- `readable` → chars `r e a d a b l e _` → apply merges where possible (`re`→`rea`→`read`) → final: `read a b l e _`. **Key insight:** even though `b` and `l` never appeared in any learned merge, they remain valid because they were in the *initial character vocabulary*. **BPE always falls back to characters for truly unseen substrings — it never fails to tokenize.**
- Decoding: concatenate tokens and remove `_`. E.g. `read_` → "read"; `u n reader_` → "unreader".

**Practical tokenizer recommendations:** spaCy (handles punctuation/contractions/multi-word expressions), NLTK's `word_tokenize()` (Punkt-based), Hugging Face tokenizers (BPE/WordPiece for transformers).

### 1.4 Stop Word Removal
Removing very common words (a, the, is, are) that carry little semantic weight.
```python
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize
text = "S&P and NASDAQ are the two most popular indices in US"
stop_words = set(stopwords.words('english'))
tokens = word_tokenize(text)
result = [w for w in tokens if w not in stop_words]
# Output: ['S', '&', 'P', 'NASDAQ', 'two', 'popular', 'indices', 'US']
```

### 1.5 Stemming vs Lemmatization vs Morphological Analysis (classic differentiation question — 2024 & 2025 both ask this)

| Aspect | Stemming | Lemmatization / Morphological Analysis |
|---|---|---|
| Definition | Reduces word to base/root form by **crudely chopping off** suffixes/prefixes, using fixed rules | Transforms word to its dictionary base form (**lemma**), considering **meaning, context, and grammar** |
| Output validity | Output may **not be a real word** | Output is always a **valid dictionary word** |
| Example | "Stemming"→"stem", "testing"→"test" (Snowball stemmer) | "has"→"ha" *(TextBlob quirk)*, "faces"→"face"; sang/sung/sings → all map to **sing** |
| Method | Purely rule-based suffix stripping | Uses vocabulary + morphological/POS analysis |
| Complexity | Fast, simple, less accurate | Slower, more accurate |

**Key one-liner for exam:** *"Lemmatization is essentially morphological analysis applied to normalization — determining that two surface-different words share the same root/lemma despite different forms (tense, number, etc.), whereas stemming is a blunt rule-based suffix-stripping heuristic that doesn't guarantee a real word."*

**Casing:** lowercase all words (or not) — with pretrained LMs, casing is often the *only* normalization step applied. **Important:** after tokenization/normalization, most pipelines are **irreversible** — you cannot recover the exact original raw text.

### 1.6 POS (Part-of-Speech) Tagging
**Definition:** Assigning a grammatical category (noun, verb, adjective, etc.) to each word in a sentence, based on both its **definition and context**.

**Why it matters:** Machine translation, information extraction, question answering, text-to-speech.

- Classic 8 POS categories (Dionysius Thrax, ~100 BC): noun, verb, pronoun, preposition, adverb, conjunction, participle, article.
- **Ambiguity example (memorize):**
  - VERB: *"Book that flight"*
  - NOUN: *"Hand me that book"*
  - **Goal of POS tagging = resolve this ambiguity by choosing the correct tag for the context.**
- **Penn Treebank tagset**: standard English tagset, **36 primary POS tags** (Marcus et al., 1993).

**Example (TextBlob):**
```
'Google is looking at buying U.K. startup for $1 billion'
→ [('Google','NNP'), ('is','VBZ'), ('looking','VBG'), ('at','IN'),
   ('buying','VBG'), ('U.K.','NNP'), ('startup','NN'), ('for','IN'),
   ('1','CD'), ('billion','CD')]
```

**Methods:** HMM, Maximum Entropy Markov Models, CRF, (Recent: RNN/Transformer).
**Evaluation:** Accuracy, Macro-F1 (equal weight per tag).

### 1.7 Named Entity Recognition (NER)
**Definition:** Locating and classifying named entities in text into predefined categories (Person, Organization, Location, Time, Date, Money, Percent, Facility, Event).

- A named entity is often a **multiword phrase** (unlike POS tags which apply per word/morpheme) — e.g. "Marie Curie", "New York City", "Stanford University".

**Example:**
```
"Sourav Ganguly served as the captain of Indian Cricket team and he is from Kolkata"
→ Sourav Ganguly → PERSON
→ Indian Cricket team → ORGANIZATION
→ Kolkata → LOCATION
```
```python
for entity in nlp(text).ents:
    print("Entity:", entity.text)
# 'Google is looking at buying U.K. startup for $1 billion'
# → Entity: Google | Entity: U.K. | Entity: $1 billion
```

### 1.8 Other Preprocessing Steps (optional but examinable as definitions)
| Step | What it does |
|---|---|
| Dependency Parsing | Assigns syntactic structure showing how words relate to each other |
| Coreference Resolution | Connects tokens referring to the same entity (e.g., "he"/"him" → a named person mentioned earlier) |
| Triplet Extraction | Records subject–verb–object triplets from sentence structure |
| Relation Extraction | Broader form of triplet extraction; entities can have multiple interactions |

**Full spaCy pipeline:** `nlp(text)` → tokenizer → tagger → parser → entity recognizer, each stage passing the processed `Doc` object to the next ("processing pipeline").

---

<a name="unit-2"></a>
## PART 2: UNIT 2 — Vectorization & N-gram Language Models

### 2.1 Text Representation Overview
| Type | Methods |
|---|---|
| **Discrete** | One-Hot Encoding, Bag of Words, TF-IDF |
| **Distributed** | Word2Vec (Skip-gram, CBOW), GloVe, FastText *(mentioned in slide topic list but not covered in numeric depth through week 9 — low priority)* |

### 2.2 One-Hot Encoding
Converts categorical variables (words) into binary vectors. Vector dimension = **vocabulary size**.

Example: Red/Blue/Green →
`v_Red=[1,0,0]`, `v_Blue=[0,1,0]`, `v_Green=[0,0,1]`

**Why needed:** avoids implying false ordinality (e.g., Red=1, Blue=2, Green=3 would wrongly imply Green > Blue > Red).

**Limitations (important — likely to be asked):**
- Large-dimensional **sparse** vector: dimension = vocab size (e.g., 500,000).
- Treats every word as **independent** — no compositionality (`v_notebook ≠ v_note + v_book`).
- Vectors are **orthogonal** — **no natural notion of similarity** between one-hot vectors.

### 2.3 Bag of Words (BoW)
- Treats each document as an unordered "bag" of words.
- **Ignores grammar and word order.**
- Only cares about word **frequency** (or presence).

### 2.4 Overcoming Sparsity: Distributional Meaning
**Key idea:** "The meaning of a word is its use in the language." Words are defined by their **environments** (surrounding words). If two words A, B have nearly identical environments → they are **synonyms**. Each word becomes a vector; similar words are "nearby in semantic space," built automatically from co-occurrence in text.

#### Co-occurrence Matrix + Cosine Similarity (fully worked, verified)
**Toy corpus:** *"data science drives insight"*, *"data analysis drives insight"* — window size = 1 (one word left/right).

| Target\Context | data | science | analysis | drives | insight |
|---|---|---|---|---|---|
| data | 0 | 1 | 1 | 0 | 0 |
| science | 1 | 0 | 0 | 1 | 0 |
| analysis | 1 | 0 | 0 | 1 | 0 |
| drives | 0 | 1 | 1 | 0 | 2 |
| insight | 0 | 0 | 0 | 2 | 0 |

**Cosine Similarity formula:**
```
cos_sim(u, v) = (u · v) / (‖u‖ ‖v‖) = Σuᵢvᵢ / (√Σuᵢ² · √Σvᵢ²)
```
**Worked:** `v_science = [1,0,0,1,0]`, `v_analysis = [1,0,0,1,0]`
```
cos_sim = (1·1+0+0+1·1+0) / (√2 · √2) = 2/2 = 1.0
```
**Interpretation:** "science" and "analysis" never co-occur with each other directly, but map to **identical vectors** (cosine = 1.0) because they share identical contexts (data, drives) → this is exactly the distributional hypothesis in action.

#### PMI / PPMI (Pointwise Mutual Information)
**Problem with raw counts:** common words dominate matrix entries without adding semantic signal.

```
PMI(w,c) = log2[ P(w,c) / (P(w)·P(c)) ] = log2[ C(w,c)·N / (C(w)·C(c)) ]
PPMI(w,c) = max(0, PMI(w,c))     ← negative values clipped to 0
```
where N = total sum of all co-occurrence counts in the matrix.

**Worked (same toy corpus):** N = 2+2+2+4+2 = 12
- PMI(data,science) = log2(1×12 / (2×2)) = log2(3) ≈ **1.585**
- PMI(science,drives) = log2(1×12 / (2×4)) = log2(1.5) ≈ **0.585**
- PMI(drives,insight) = log2(2×12 / (4×2)) = log2(3) ≈ **1.585**
- Non-co-occurring pairs → PMI → −∞ ⟹ **PPMI = 0**

**Key outcome:** even though "drives" co-occurs *twice* with "insight" (raw count 2) vs *once* with "science" (raw count 1), PMI **normalizes for drives' overall higher frequency**, giving different (not just doubled) association scores (1.585 vs 0.585).

#### TF-IDF (fully worked, verified with Python)
```
TF-IDF(t,d,D) = TF(t,d) × IDF(t,D)
```
- TF(t,d) = frequency of term t in document d
- IDF down-weights words common across all documents, elevates rare/discriminative ones.

**Problem:** if a term appears in every document, `IDF = log(1) = 0` (or `log(∞)` if it appears nowhere → undefined). 

**Sklearn's smoothed fix (this is the formula your course uses):**
```
IDF(t,D) = ln[ (1 + N) / (1 + df(t)) ] + 1
```
where N = total docs, df(t) = number of docs containing t. Then **L2-normalize** the final TF-IDF vector per document.

**Verified worked example** (2 documents):
- Doc1: "students learn machine learning"
- Doc2: "students learn deep learning models"

| Term | df | IDF = ln((1+2)/(1+df))+1 |
|---|---|---|
| deep | 1 | 1.4055 |
| learn | 2 | 1.0000 |
| learning | 2 | 1.0000 |
| machine | 1 | 1.4055 |
| models | 1 | 1.4055 |
| students | 2 | 1.0000 |

**Doc1 raw TF-IDF** (each term appears once): learn=1.0, learning=1.0, machine=1.4055, students=1.0
L2 norm = √(1²+1²+1.4055²+1²) = √4.9754 ≈ **2.2306**
Normalized: learn=1/2.2306≈**0.4483**, learning≈**0.4483**, machine=1.4055/2.2306≈**0.6301**, students≈**0.4483**

**Doc2 raw TF-IDF:** deep=1.4055, learn=1.0, learning=1.0, models=1.4055, students=1.0
L2 norm = √(1.4055²+1²+1²+1.4055²+1²) = √6.9508 ≈ **2.6364**
Normalized: deep≈**0.5331**, learn≈**0.3793**, learning≈**0.3793**, models≈**0.5331**, students≈**0.3793**

*(Verified against `sklearn.TfidfVectorizer` — matches exactly.)*

### 2.5 N-gram Language Models
**Language Model (LM):** predicts the probability of upcoming word(s); assigns a probability to a whole sentence.
```
P(W) = P(w1,w2,...,wn) = P(w1:n)          — probability of a sequence
P(wn | w1,...,w(n-1)) = P(wn | w1:n-1)    — probability of next word
```
**Why:** autocomplete, spell/grammar check, speech recognition, machine translation; this is literally how LLMs generate text (autoregressive, left-to-right next-word prediction).

**Chain Rule of Probability:**
```
P(A,B,C,D) = P(A) P(B|A) P(C|A,B) P(D|A,B,C)
P(w1:n) = P(w1) P(w2|w1) P(w3|w1:2) ... P(wn|w1:n-1)
```
**Problem:** long conditioning histories are impossible to compute — sequences never repeat identically in finite text.

**Solution — Markov Approximation** (look back only N−1 words):
| Model | Formula |
|---|---|
| Unigram (N=1) | P(W) ≈ ∏ P(wₖ) |
| Bigram (N=2) | P(W) ≈ ∏ P(wₖ \| wₖ₋₁) |
| Trigram (N=3) | P(W) ≈ ∏ P(wₖ \| wₖ₋₂, wₖ₋₁) |
| General N-gram | P(W) ≈ ∏ P(wₖ \| wₖ₋ₙ₊₁:ₖ₋₁) |

**MLE (Maximum Likelihood Estimation) — how to actually compute these probabilities from a corpus:**
```
Unigram:  P_MLE(wₖ)              = C(wₖ) / N_total
Bigram:   P_MLE(wₖ | wₖ₋₁)       = C(wₖ₋₁, wₖ) / C(wₖ₋₁)
Trigram:  P_MLE(wₖ | wₖ₋₂,wₖ₋₁)  = C(wₖ₋₂,wₖ₋₁,wₖ) / C(wₖ₋₂,wₖ₋₁)
```
**Sentence boundaries:** augment every sentence with `<s>` (start) and `</s>` (end) markers before counting.

#### Worked Example — Bigram vs Trigram MLE (from your slides — memorize the whole flow)
**Training corpus:**
```
<s> I am Sam </s>
<s> Sam I am </s>
<s> I do not like green eggs </s>
```
**Counts:** C(`<s>`)=3, C(I)=3, C(am)=2, C(Sam)=2; C(`<s>`,I)=2, C(I,am)=2, C(am,Sam)=1, C(Sam,`</s>`)=1

**Test sequence:** `<s> I am Sam </s>` (n=4 tokens to predict: I, am, Sam, `</s>`)

**Bigram model:**
```
P(I|<s>)   = 2/3 ≈ 0.66667
P(am|I)    = 2/3 ≈ 0.66667
P(Sam|am)  = 1/2 = 0.50000
P(</s>|Sam)= 1/2 = 0.50000
P(W) = (2/3)(2/3)(1/2)(1/2) = 4/36 = 1/9 ≈ 0.11111
```
**Perplexity (direct formula):** `PP(W) = P(W)^(-1/n)` with n=4:
```
PP(W) = (1/9)^(-1/4) = 9^(1/4) = 3 ≈ 1.732
```
**Via Cross-Entropy (log-space, avoids underflow):**
```
H(W) = -(1/n) Σ log2 P(wₖ|...)
     = -(1/4)(-0.585 -0.585 -1.000 -1.000) ≈ 0.79248 bits/word
PP(W) = 2^H(W) = 2^0.79248 ≈ 1.732   ✓ matches
```

**Trigram model** (training data becomes `<s> <s> I am Sam </s>` etc.):
```
P(I|<s>,<s>)    = 2/3 ≈ 0.66667
P(am|<s>,I)     = 1/2 = 0.50000
P(Sam|I,am)     = 1/2 = 0.50000
P(</s>|am,Sam)  = 1/1 = 1.00000
P(W) = (2/3)(1/2)(1/2)(1) = 2/12 = 1/6 ≈ 0.16667
PP(W) = (1/6)^(-1/4) = 6^(1/4) ≈ 1.565
```
**Conclusion (a great "interpret the result" exam answer):** *Trigram achieves lower perplexity (1.565 vs 1.732) than bigram because the extra word of history resolves ambiguity — e.g., knowing "I am" already makes "Sam" certain, and "am Sam" makes `</s>` certain (prob=1). Lower perplexity = better model (holding the test set constant).*

### 2.6 Evaluating Language Models
| Type | Description |
|---|---|
| **Extrinsic (in-vivo)** | Plug model into a real downstream task (MT, speech recognition), compare accuracy. Expensive, doesn't always generalize. |
| **Intrinsic (in-vitro)** | Test model's raw predictive power on held-out text directly, via **Perplexity**. Cheaper, standard for LM comparison. |

**Perplexity:**
```
PP(W) = P(W)^(-1/n)
```
- Inverse probability of the test set, normalized by number of words n.
- Interpreted as the **effective branching factor** — average number of equally-likely next-word choices the model faces at each step.
- Range: Probability∈[0,1] → Perplexity∈[1,∞]. **Lower perplexity = better model.**
- Requires: identical vocabulary, identical tokenization, identical test set across models being compared (else comparison is invalid).

**Branching factor intuition:**
- Vocabulary |V|=10,000, uniform distribution → H = log2(10,000) ≈ 13.29 bits → PP = 10,000 (worst case, zero context).
- A skewed/informed distribution → H < 13.29 → PP < 10,000 (model is "smarter," fewer effective choices).

### 2.7 The Data Sparsity Problem
- Human language has **combinatorial** vocabulary — most valid N-grams never appear in any finite training corpus → count = 0.
- Since `P(W) = ∏ P(wₖ|...)`, **a single unseen N-gram collapses the entire sentence probability to 0.**
- This makes cross-entropy undefined (`log2(0) → -∞`) and **perplexity → ∞**.
- **A zero count does NOT mean impossible — just means the training sample wasn't large enough.**

**Three solution families:**
1. **Smoothing/Discounting** — reallocate probability mass from seen to unseen N-grams (Laplace, Add-m, Good-Turing).
2. **Backoff & Interpolation** — fall back to / blend with lower-order (denser) models.
3. **Neural embeddings** (RNN/Transformer) — share statistical strength across semantically similar contexts instead of exact string matching. *(conceptual mention only — not numerically covered this year)*

#### Laplace (Add-1) Smoothing
```
P_Laplace(wₖ|wₖ₋₁) = [C(wₖ₋₁,wₖ) + 1] / [C(wₖ₋₁) + |V|]
```
**Why add |V| to denominator?** To keep the distribution valid (sums to 1):
```
Σ_wₖ [C(wₖ₋₁,wₖ)+1] / [C(wₖ₋₁)+|V|] = [C(wₖ₋₁)+|V|] / [C(wₖ₋₁)+|V|] = 1
```

#### Add-m (Lidstone) Smoothing
```
P_Add-m(wₖ|wₖ₋₁) = [C(wₖ₋₁,wₖ) + m] / [C(wₖ₋₁) + m|V|]     (0 < m < 1, e.g. m=0.05)
```
- Laplace's "+1" is too aggressive when |V| is large (e.g. 50,000) — steals too much mass from real data.
- m is a **hyperparameter**, tuned on a **held-out validation set** to minimize perplexity.
- As **m → 0**: approaches pure MLE. As **m → 1**: becomes standard Laplace.

#### Worked Example — Laplace Smoothing Fixes a Zero-Probability Case
Using the same "I am Sam" corpus, |V| = 10 (types: `<s>,</s>,I,am,Sam,do,not,like,green,eggs`).

Test: `<s> I am Sam </s>`. Unsmoothed MLE gives:
```
P(I|<s>)=2/3, P(am|I)=2/3, P(Sam|am)=1/2, P(</s>|Sam)=1/2  → all fine here
```
*(If instead your test word combination has never been seen — e.g. `sat` never followed by `</s>` in some other corpus — MLE gives 0 and PP=∞. That's the whole point of needing smoothing.)*

**With Laplace smoothing (|V|=10):**
```
P(I|<s>)    = (2+1)/(3+10) = 3/13 ≈ 0.23077
P(am|I)     = (2+1)/(3+10) = 3/13 ≈ 0.23077
P(Sam|am)   = (1+1)/(2+10) = 2/12 = 1/6 ≈ 0.16667
P(</s>|Sam) = (1+1)/(2+10) = 2/12 = 1/6 ≈ 0.16667

P(W) = (3/13)(3/13)(1/6)(1/6) = 9/6084 ≈ 0.00148
PP(W) = P(W)^(-1/4) = 676^(1/4) ≈ 5.099
```
**Via cross-entropy:** H(W) ≈ 2.35022 bits/word → PP = 2^2.35022 ≈ **5.099** ✓ matches.

*(Notice: smoothed perplexity (5.099) is much higher than unsmoothed bigram perplexity on the same clean sentence (1.732) — smoothing "spends" some probability mass on protecting against unseen events, so it's less confident even when it didn't need to be. This trade-off is a great analytical/justification point for your exam.)*

### 2.8 Backoff & Interpolation
Both combine high-order (rich context, sparse) and low-order (weak context, dense) N-grams.

**1. Interpolation** — ALWAYS blends all orders, regardless of whether the higher-order N-gram was seen:
```
P̂(wₖ|wₖ₋₂,wₖ₋₁) = λ₃·P_MLE(wₖ|wₖ₋₂,wₖ₋₁) + λ₂·P_MLE(wₖ|wₖ₋₁) + λ₁·P_MLE(wₖ)
                     where λ₁+λ₂+λ₃ = 1, all λⱼ ≥ 0
```
- λ's tuned on held-out validation data (e.g. via Expectation-Maximization) to minimize perplexity.
- Can be **context-dependent**: frequent context → higher λ₃ (trust the higher-order model more); rare context → downweight λ₃.

**2. Backoff** — uses the highest-order N-gram if there's *sufficient evidence*; only falls back when count = 0 (or below threshold). Requires **discounting** the higher-order MLE counts to free up probability mass for the fallback.
```
Katz Backoff (trigram → bigram):
P_BO(wₖ|wₖ₋₂,wₖ₋₁) = P*(wₖ|wₖ₋₂,wₖ₋₁)                    if C(wₖ₋₂,wₖ₋₁,wₖ) > 0
                    = α(wₖ₋₂,wₖ₋₁) · P_BO(wₖ|wₖ₋₁)          if C(wₖ₋₂,wₖ₋₁,wₖ) = 0

where P*(wₖ|wₖ₋₂,wₖ₋₁) = [C(wₖ₋₂,wₖ₋₁,wₖ) - d] / C(wₖ₋₂,wₖ₋₁)   (d = discount, 0<d<1)
      α(wₖ₋₂,wₖ₋₁) = normalization weight ensuring leftover mass is redistributed correctly
```

**Interpolation vs Backoff — one-line differentiator for exam:** *Interpolation always mixes all N-gram orders together; Backoff only drops to a lower order when the higher order has zero evidence.*

---

<a name="practice"></a>
## PART 3: Fresh Self-Test Practice Problems (verified — try them yourself first, then check)

### Practice 1 — BPE
Corpus: `low_`(freq 5), `lower_`(freq 2), `newest_`(freq 6), `widest_`(freq 3). Perform 6 BPE merges.

<details><summary>Click to reveal answer</summary>

Initial vocab: `_, d, e, i, l, n, o, r, s, t, w`

| Merge | Pair | New token |
|---|---|---|
| 1 | (e,s) | es |
| 2 | (es,t) | est |
| 3 | (est,_) | est_ |
| 4 | (l,o) | lo |
| 5 | (lo,w) | low |
| 6 | (e,w) | ew |

Final words: `low_` , `low e r _`, `n ew est_`, `w i d est_`
</details>

### Practice 2 — Bigram MLE + Perplexity
Training corpus:
```
<s> the cat sat on the mat </s>
<s> the dog sat on the log </s>
<s> the cat ate the fish </s>
```
Test sentence: `<s> the dog sat on the mat </s>`. Compute P(W), Perplexity, and Cross-Entropy for a bigram model.

<details><summary>Click to reveal answer</summary>

Vocabulary size |V| = 11. Relevant counts: C(the)=6, C(`<s>`)=3, C(dog)=1, C(sat)=2, C(on)=2, C(mat)=1.
```
P(the|<s>)=3/3=1.0     P(dog|the)=1/6≈0.16667   P(sat|dog)=1/1=1.0
P(on|sat)=2/2=1.0      P(the|on)=2/2=1.0        P(mat|the)=1/6≈0.16667
P(</s>|mat)=1/1=1.0

P(W) = 1×0.16667×1×1×1×0.16667×1 ≈ 0.02778
n = 7
Perplexity = 0.02778^(-1/7) ≈ 1.669
Cross-Entropy ≈ 0.739 bits/word  →  2^0.739 ≈ 1.669 ✓
```
</details>

### Practice 3 — Data Sparsity + Laplace Fix
Using the **same** corpus as Practice 2, test sentence `<s> the cat sat </s>`. Show that plain MLE fails, then fix with Laplace smoothing.

<details><summary>Click to reveal answer</summary>

```
P(the|<s>)=1.0, P(cat|the)=2/6≈0.333, P(sat|cat)=1/2=0.5, P(</s>|sat)=0/2=0  ← ZERO!
→ P(W)=0, Perplexity = ∞
```
**Laplace fix (|V|=11):**
```
P(the|<s>)   = 4/14 ≈ 0.28571
P(cat|the)   = 3/17 ≈ 0.17647
P(sat|cat)   = 2/13 ≈ 0.15385
P(</s>|sat)  = 1/13 ≈ 0.07692
P(W) ≈ 0.00059669
n=4 → Perplexity = P(W)^(-1/4) ≈ 6.398
Cross-Entropy ≈ 2.678 bits/word → 2^2.678 ≈ 6.398 ✓
```
</details>

### Practice 4 — Co-occurrence, Cosine Similarity, PMI
Corpus: *"dogs chase cats"*, *"dogs chase mice"*, window=1. Build the co-occurrence matrix, then find cosine similarity(cats, mice) and PMI(cats, chase).

<details><summary>Click to reveal answer</summary>

|  | cats | chase | dogs | mice |
|---|---|---|---|---|
| cats | 0 | 1 | 0 | 0 |
| chase | 1 | 0 | 2 | 1 |
| dogs | 0 | 2 | 0 | 0 |
| mice | 0 | 1 | 0 | 0 |

`v_cats = [0,1,0,0]`, `v_mice = [0,1,0,0]` → **cosine similarity = 1.0** (identical context: both only co-occur with "chase" — classic distributional synonymy, even though cats and mice never appear next to each other!)

N = 8 total co-occurrences. C(cats)=1, C(chase)=4.
`PMI(cats,chase) = log2(1×8 / (1×4)) = log2(2) = 1.0`
</details>

### Practice 5 — TF-IDF
Docs: D1 = "students learn machine learning", D2 = "students learn deep learning models". Compute the sklearn-smoothed IDF for each term, then the normalized TF-IDF vector for D1.

<details><summary>Click to reveal answer</summary>

IDF = ln((1+2)/(1+df))+1. Terms in both docs (df=2): learn, learning, students → IDF=1.0. Terms in one doc (df=1): deep, machine, models → IDF≈1.4055.

D1 raw scores: learn=1.0, learning=1.0, machine=1.4055, students=1.0
L2 norm = √(1+1+1.9754+1) ≈ 2.2306
**Normalized D1: learn≈0.448, learning≈0.448, machine≈0.630, students≈0.448**
</details>

---

<a name="pyq-table"></a>
## PART 4: PYQ Cross-Reference (2024 & 2025) — What's In Scope Now

| PYQ Question | Year | In scope this year? | Where covered above |
|---|---|---|---|
| Q1(A) Regex for email detection | 2024 | 🔴 Not in slides (see Appendix as backup) | Appendix |
| Q1(B) POS tagging definition + example | 2024 | 🟢 Yes | §1.6 |
| Q1(C) Argmax bigram sequence probability | 2024 | 🟡 Yes, reframed as N-gram MLE | §2.5 |
| Q2(A) Place & manner of articulation | 2024 | 🔴 Not in slides | — |
| Q2(B) Stemming vs morphological analysis | 2024 | 🟢 Yes | §1.5 |
| Q3(A) Word tokenization example | 2024 | 🟢 Yes | §1.3 |
| Q3(B) HMM for speech recognition | 2024 | 🔴 Not in slides | — |
| Q4(A) Computational grammar | 2024 | 🔴 Not in slides | — |
| Q4(B) Word boundary detection (speech) | 2024 | 🔴 Not in slides | — |
| Q4(A)-OR Preprocessing steps on text | 2024 | 🟢 Yes (tokenize/stopword/stem/lemmatize/POS) | §1.3–1.7 |
| Q4(B)-OR MP3 vs FLAC | 2024 | 🔴 Not in slides | — |
| Q5(A) Text classification vs MT dataset differences | 2024 | 🔴 Not in slides (old "Corpus" unit) | — |
| Q5(B) Nominal/ordinal/interval/ratio data | 2024 | 🔴 Not in slides | — |
| Q5(A)-OR Speech recognition components | 2024 | 🔴 Not in slides | — |
| Q5(B)-OR JSON vs CSV corpus formats | 2024 | 🔴 Not in slides | — |
| Q1 Components of NLP system | 2025 | 🟢 Yes | §1.2 |
| Q2 Word boundary detection challenges | 2025 | 🔴 Not in slides | — |
| Q2-OR HMM for speech recognition | 2025 | 🔴 Not in slides | — |
| Q3(a) Tokenization | 2025 | 🟢 Yes | §1.3 |
| Q3(b) Stemming | 2025 | 🟢 Yes | §1.5 |
| Q3(c) Morphological analysis | 2025 | 🟢 Yes | §1.5 |
| Q3(d) Computational grammar | 2025 | 🔴 Not in slides | — |
| Q3(e) Place & manner of articulation | 2025 | 🔴 Not in slides | — |

**Takeaway:** roughly half of each old paper is now off-syllabus. Focus your remaining time entirely on Parts 1–3 above — that's where your marks will actually come from, **plus the entirely new Unit 2 vectorization/N-gram content that never appeared in these old PYQs at all** (TF-IDF, PMI, perplexity, smoothing) — these are prime new-question territory since the professor explicitly renamed Unit 2 this year.

---

<a name="mock"></a>
## PART 5: Predicted Question Bank

Professor's note: *"Questions will be based on numericals, analyticals, logicals and justifications."* Based on this + actual slide content, here's a realistic mock paper in the style of your PYQs:

**Q1.**
(A) Differentiate between stemming, lemmatization, and morphological analysis with an example each. [5]
(B) What is the "token vs type" distinction in tokenization? Given a sentence, count tokens and types. [3]
(C) List and explain any four issues with whitespace tokenization. [4]

**Q2.**
(A) Given a small training corpus, perform BPE for 4 merges, showing the vocabulary after each step. [6]
(B) Explain why BPE can still tokenize an out-of-vocabulary word like "readable" even if some characters never appeared in a learned merge. [4]

**Q3.**
(A) Explain the limitations of One-Hot Encoding. Why do word vectors need a "notion of similarity"? [5]
(B) Given a toy corpus, construct a co-occurrence matrix (window=1) and compute cosine similarity between two given words. [5]

**Q4.**
(A) Derive/state the Chain Rule of Probability and show how the Markov assumption simplifies it to a bigram model. [5]
(B) Given a training corpus and a test sentence, use Argmax/MLE to compute the bigram probability of the sentence, then find its Perplexity. [5]

**OR**

(A) Explain the Data Sparsity problem in N-gram LMs and why a single zero-count N-gram destroys the whole sequence probability. [5]
(B) Given a corpus, apply Laplace (Add-1) smoothing to a test sentence containing an unseen bigram, and compute the smoothed Perplexity. [5]

**Q5.**
(A) Derive the sklearn-smoothed IDF formula and explain why plain IDF fails when a term appears in every document. Compute TF-IDF for a 2-document toy corpus. [6]
(B) Differentiate between Interpolation and Backoff for handling unseen N-grams. [4]

**OR**

(A) Define Perplexity and explain why it is called the "effective branching factor." Compute perplexity for a bigram vs trigram model on the same test sentence and interpret which is better and why. [6]
(B) Differentiate Extrinsic vs Intrinsic evaluation of language models. [4]

*(Practice writing full answers to all of these under time pressure — that alone will cover ~90% of realistic midsem content.)*

---

<a name="cheatsheet"></a>
## PART 6: One-Page Formula Cheat Sheet (final review, night before exam)

```
TOKENIZATION
  Token = instance in text | Type = distinct vocabulary element

BPE
  Merge most frequent adjacent pair each step; OOV → falls back to characters

COSINE SIMILARITY
  cos(u,v) = (u·v) / (‖u‖‖v‖)

PMI / PPMI
  PMI(w,c) = log2[ C(w,c)·N / (C(w)·C(c)) ]      PPMI = max(0, PMI)

TF-IDF (sklearn-style)
  IDF(t,D) = ln[ (1+N)/(1+df(t)) ] + 1
  TF-IDF(t,d) = TF(t,d) × IDF(t,D)     → then L2-normalize per document

CHAIN RULE
  P(w1:n) = P(w1)·P(w2|w1)·P(w3|w1:2)·...·P(wn|w1:n-1)

N-GRAM MLE
  Unigram:  P(wk) = C(wk)/N_total
  Bigram:   P(wk|wk-1) = C(wk-1,wk)/C(wk-1)
  Trigram:  P(wk|wk-2,wk-1) = C(wk-2,wk-1,wk)/C(wk-2,wk-1)

PERPLEXITY
  PP(W) = P(W)^(-1/n)  =  2^H(W)
  H(W) = -(1/n) Σ log2 P(wk|context)      [Cross-Entropy]
  Lower PP = better model. PP ∈ [1,∞].

LAPLACE (ADD-1) SMOOTHING
  P(wk|wk-1) = [C(wk-1,wk)+1] / [C(wk-1)+|V|]

ADD-m (LIDSTONE) SMOOTHING
  P(wk|wk-1) = [C(wk-1,wk)+m] / [C(wk-1)+m|V|]     (m→0: MLE, m→1: Laplace)

LINEAR INTERPOLATION (trigram)
  P̂(wk|wk-2,wk-1) = λ3·P(wk|wk-2,wk-1) + λ2·P(wk|wk-1) + λ1·P(wk)   ; Σλ=1

KATZ BACKOFF
  Use highest order if C>0, else back off (with discount d) to lower order
```

---

<a name="appendix"></a>
## Appendix: Regex Quick Primer (backup, in case old-style questions resurface)

Even though not in this year's slides, this is a 2-minute skill in case a preprocessing-cleaning question needs it.

**Email regex (from 2024 PYQ):**
```
[\w.]+@[\w.]+
```
Applied to: *"I am a student with email id abc@xyz.com and my friend's email is abc.def@xyz.co.in."*
- `\w+` matches word characters (letters/digits/underscore); `.` inside `[\w.]+` allows dots in usernames/domains (e.g. `abc.def`, `xyz.co.in`).
- Matches: `abc@xyz.com`, `abc.def@xyz.co.in`

**A more robust version:** `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}`

---

### Final Checklist Before You Walk In
- [ ] Can you list the 5 whitespace tokenization issues from memory?
- [ ] Can you differentiate stemming / lemmatization / morphological analysis with an example each?
- [ ] Can you run a BPE merge table by hand for a new 4-5 word toy corpus?
- [ ] Can you build a co-occurrence matrix and compute cosine similarity by hand?
- [ ] Can you compute PMI/PPMI for a pair of words?
- [ ] Can you compute TF-IDF using the smoothed IDF formula, including L2 normalization?
- [ ] Can you compute bigram/trigram MLE probability, then Perplexity via BOTH the direct formula and cross-entropy, for a new test sentence?
- [ ] Can you explain WHY a zero-count bigram breaks perplexity, and fix it with Laplace smoothing by hand?
- [ ] Can you state the difference between Interpolation and Backoff in one sentence?
- [ ] Do you understand Extrinsic vs Intrinsic evaluation?

Good luck! You have very complete lecture material — the main risk this exam is wasting time on old speech-processing PYQ topics that your professor has explicitly moved off this year's syllabus. Trust the email + slides over the old papers.
