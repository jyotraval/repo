# NLP Mid-Sem — Last Hour Cramming Guide

> **Assumption:** You've done nothing all week. You have 60 minutes.
> **Exam format:** 25 marks · 60 min · 3 questions (2025 pattern)
> **Question style:** Numericals, analyticals, logicals, justifications

---

## ⏰ How to Spend This Hour (do not deviate)

| Time | What to do | Section |
|---|---|---|
| **0:00–0:05** | Read this whole file once, end-to-end. Don't try to memorize yet. | All |
| **0:05–0:20** | Memorize the **7 numericals** in Section 2. These are the marks. | §2 |
| **0:20–0:35** | Memorize the **PYQ-pattern answers** in Section 3. | §3 |
| **0:35–0:45** | Memorize the **definitions** in Section 4 (2-mark questions). | §4 |
| **0:45–0:55** | Memorize the **formula sheet** in Section 5. | §5 |
| **0:55–1:00** | Read the **exam-hall strategy** in Section 6. Calm down. | §6 |

**Rule #1:** Skip everything else. Do not open the textbook. Do not open ChatGPT.
**Rule #2:** The exam is 25 marks in 60 min. **1 mark = 2.4 minutes.** A 10-mark Q gets 24 min. Don't overrun.
**Rule #3:** Numericals carry ~50% of the marks. They are the difference between 8/25 and 18/25. Do them.

---

## 1. 🎯 What Will Almost Certainly Be Asked

Based on professor's email ("numericals, analyticals, logicals, justifications") + 2024+2025 PYQs + Week 1-9 PPTs:

### Almost certain (high probability)
1. **One numerical** — most likely **bigram perplexity** or **Laplace smoothing** (both have step-by-step examples in the PPTs).
2. **Word boundary detection OR HMM in ASR** (10-mark question — appeared in both 2024 and 2025).
3. **Five 2-mark definitions** — tokenisation, stemming, morphological analysis, computational grammar, place/manner of articulation (exactly 2025 Q3).

### Likely
4. **Components of NLP system** (5 marks — asked in 2025 Q1).
5. **BPE numerical** (perform k merges on a small corpus).

### Possible
6. **TF-IDF computation** (worked example in Week 5 PPT).
7. **Argmax computation** (2024 Q1-C pattern).
8. **Regex for email** (2024 Q1-A pattern).

---

## 2. 🔢 The 7 Numericals (Memorize These)

### 2.1 Bigram MLE Probability + Perplexity ⭐ MOST LIKELY

**Training corpus (memorize this — it's the PPT example):**
```
<s> I am Sam </s>
<s> Sam I am </s>
<s> I do not like green eggs </s>
```

**Counts you'll need:**
```
- $C(\text{<s>}) = 3$, $C(\text{I}) = 3$, $C(\text{am}) = 2$, $C(\text{Sam}) = 2$
- $C(\text{<s>, I}) = 2$, $C(\text{I, am}) = 2$, $C(\text{am, Sam}) = 1$, $C(\text{Sam, </s>}) = 1$
```

**Test sequence:** `<s> I am Sam </s>` → predict 4 tokens ($w_1$=I, $w_2$=am, $w_3$=Sam, $w_4$=`</s>`). So **n = 4**.

**Step 1 — Bigram MLE:**
$$P(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k)}{C(w_{k-1})}$$

| $w_k$ | $w_{k-1}$ | Numerator | Denominator | $P$ |
|---|---|---|---|---|
| I | `<s>` | $C(\text{<s>,I})=2$ | $C(\text{<s>})=3$ | $2/3 \approx 0.667$ |
| am | I | $C(\text{I,am})=2$ | $C(\text{I})=3$ | $2/3 \approx 0.667$ |
| Sam | am | $C(\text{am,Sam})=1$ | $C(\text{am})=2$ | $1/2 = 0.5$ |
| `</s>` | Sam | $C(\text{Sam,</s>})=1$ | $C(\text{Sam})=2$ | $1/2 = 0.5$ |

**Step 2 — Sentence probability:**
$$P(W) = \frac{2}{3} \times \frac{2}{3} \times \frac{1}{2} \times \frac{1}{2} = \frac{4}{36} = \frac{1}{9} \approx 0.1111$$

**Step 3 — Perplexity (direct formula):**
$$\text{PP}(W) = P(W)^{-1/n} = \left(\frac{1}{9}\right)^{-1/4} = 9^{1/4} = \sqrt{3} \approx \mathbf{1.732}$$

**Step 4 — Cross-entropy (alternative method):**
$$H(W) = -\frac{1}{n} \sum_k \log_2 P(w_k \mid w_{k-1})$$

| $\log_2 P$ | Value |
|---|---|
| $\log_2(2/3)$ | $-0.585$ |
| $\log_2(2/3)$ | $-0.585$ |
| $\log_2(1/2)$ | $-1.0$ |
| $\log_2(1/2)$ | $-1.0$ |

$$H(W) = -\tfrac{1}{4}(-0.585 - 0.585 - 1 - 1) = \tfrac{3.17}{4} \approx 0.7925 \text{ bits/word}$$
$$\text{PP}(W) = 2^{H(W)} = 2^{0.7925} \approx 1.732 \quad \checkmark$$

** mnemonic for the answer: "1/9, √3, 1.732" **

---

### 2.2 Laplace (Add-1) Smoothing + Perplexity ⭐ SECOND MOST LIKELY

**Same corpus.** Vocabulary $V = \{<s>, </s>, I, am, Sam, do, not, like, green, eggs\}$ → **|V| = 10**.

**Formula:**
$$P_{\text{Lap}}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + |V|}$$

**Step 1 — Smoothed bigram probabilities (|V|=10):**

| $w_k \mid w_{k-1}$ | Formula | Value |
|---|---|---|
| $P(\text{I} \mid \text{<s>})$ | $\frac{2+1}{3+10} = \frac{3}{13}$ | $\approx 0.2308$ |
| $P(\text{am} \mid \text{I})$ | $\frac{2+1}{3+10} = \frac{3}{13}$ | $\approx 0.2308$ |
| $P(\text{Sam} \mid \text{am})$ | $\frac{1+1}{2+10} = \frac{2}{12} = \frac{1}{6}$ | $\approx 0.1667$ |
| $P(\text{</s>} \mid \text{Sam})$ | $\frac{1+1}{2+10} = \frac{2}{12} = \frac{1}{6}$ | $\approx 0.1667$ |

**Step 2 — Sentence probability:**
$$P(W) = \frac{3}{13} \times \frac{3}{13} \times \frac{1}{6} \times \frac{1}{6} = \frac{9}{6084} = \frac{1}{676} \approx 0.00148$$

**Step 3 — Perplexity:**
$$\text{PP}(W) = \left(\frac{1}{676}\right)^{-1/4} = 676^{1/4} = \sqrt{26} \approx \mathbf{5.099}$$

**Step 4 — Cross-entropy check:**
- $\log_2(3/13) \approx -2.1155$
- $\log_2(1/6) \approx -2.585$
- $H = -\tfrac{1}{4}(-2.1155 - 2.1155 - 2.585 - 2.585) = \tfrac{9.401}{4} \approx 2.350$ bits/word
- $\text{PP} = 2^{2.350} \approx 5.099$ ✓

**Mnemonic: "1/676, √26, 5.099"**
- Note: Laplace PP (5.099) > unsmoothed PP (1.732) because smoothing shifted mass to unseen bigrams. This is a known drawback — motivates Add-$m$ with small $m$.

---

### 2.3 Trigram MLE + Perplexity (Third most likely)

For trigram, augment training corpus with **double `<s>`**:
```
<s> <s> I am Sam </s>
<s> <s> Sam I am </s>
<s> <s> I do not like green eggs </s>
```

Test: `<s> <s> I am Sam </s>` — predict same 4 tokens, $n = 4$.

**Trigram MLE:** $P(w_k \mid w_{k-2}, w_{k-1}) = \frac{C(w_{k-2}, w_{k-1}, w_k)}{C(w_{k-2}, w_{k-1})}$

| $w_k \mid (w_{k-2}, w_{k-1})$ | Num | Den | $P$ |
|---|---|---|---|
| $P(\text{I} \mid \text{<s>,<s>})$ | $C(\text{<s>,<s>,I})=2$ | $C(\text{<s>,<s>})=3$ | $2/3 \approx 0.667$ |
| $P(\text{am} \mid \text{<s>,I})$ | $C(\text{<s>,I,am})=1$ | $C(\text{<s>,I})=2$ | $1/2 = 0.5$ |
| $P(\text{Sam} \mid \text{I,am})$ | $C(\text{I,am,Sam})=1$ | $C(\text{I,am})=2$ | $1/2 = 0.5$ |
| $P(\text{</s>} \mid \text{am,Sam})$ | $C(\text{am,Sam,</s>})=1$ | $C(\text{am,Sam})=1$ | $1/1 = 1.0$ |

$$P(W) = \frac{2}{3} \times \frac{1}{2} \times \frac{1}{2} \times 1 = \frac{1}{6} \approx 0.1667$$

$$\text{PP}(W) = \left(\frac{1}{6}\right)^{-1/4} = 6^{1/4} \approx \mathbf{1.565}$$

**Cross-entropy:**
- $\log_2(2/3) = -0.585$, $\log_2(1/2) = -1$, $\log_2(1/2) = -1$, $\log_2(1) = 0$
- $H = -\tfrac{1}{4}(-0.585 - 1 - 1 + 0) = \tfrac{2.585}{4} \approx 0.6462$ bits/word
- $\text{PP} = 2^{0.6462} \approx 1.565$ ✓

**Mnemonic: "1/6, 6^(1/4), 1.565"** — trigram PP (1.565) < bigram PP (1.732) because more context resolves ambiguity.

---

### 2.4 BPE Merges (perform exactly k merges)

**Corpus (memorize):**

| Word | Freq |
|---|---:|
| read | 3 |
| reads | 2 |
| reader | 2 |
| reading | 2 |
| unread | 1 |
| readers | 1 |

**Initial vocab** = `{_, a, d, e, g, i, n, r, s, u}` (the unique chars in the corpus, plus `_` end-of-word marker).

**Step 1:** Append `_` to each word: `read_`, `reads_`, `reader_`, `reading_`, `unread_`, `readers_`.

**Step 2:** Count adjacent pairs weighted by frequency. The 6 merges in order:

| Merge # | Most frequent pair | New token |
|:---:|---|---|
| 1 | (r, e) | `re` |
| 2 | (re, a) | `rea` |
| 3 | (rea, d) | `read` |
| 4 | (read, _) | `read_` |
| 5 | (read, e) | `reade` |
| 6 | (reade, r) | `reader` |

**Final vocab** = 10 chars + 6 merged tokens = 16 tokens.

**Test on new words (apply merges in order):**

| Test word | Initial chars | Final BPE tokens | In training? |
|---|---|---|---|
| read | `r e a d _` | `read_` | Yes |
| reader | `r e a d e r _` | `reader _` | Yes |
| readers | `r e a d e r s _` | `reader s _` | Yes |
| reading | `r e a d i n g _` | `read i n g _` | Yes |
| unread | `u n r e a d _` | `u n read_` | Yes |
| **readable (OOV)** | `r e a d a b l e _` | `read a b l e _` | No |
| **reread (OOV)** | `r e r e a d _` | `re read_` | No |
| **unreader (OOV)** | `u n r e a d e r _` | `u n reader _` | No |

**Decode:** concatenate tokens, remove `_`. E.g., `read a b l e _` → `readable`. ✓

**Key insight:** BPE never produces an OOV token — it falls back to characters (`b`, `l` in `readable` are in the initial char vocab).

---

### 2.5 TF-IDF (sklearn-style, 2 documents) — possible

**Documents (after stop-word removal):**
- D1: `stock price google jumps earning data today` (7 tokens, each freq 1)
- D2: `google plunge china data` (4 tokens, each freq 1)

Vocabulary: `{china, data, earning, google, jumps, plunge, price, stock, today}` → |V|=9.

**Smoothed IDF (sklearn formula):**
$$\text{IDF}(t) = \ln\left(\frac{1 + |D|}{1 + \text{df}(t)}\right) + 1$$

With $|D| = 2$:
- `data, google` appear in both docs → df=2 → IDF = $\ln(3/3)+1 = 0 + 1 = 1.0$
- `earning, jumps, price, stock, today` (only D1), `china, plunge` (only D2) → df=1 → IDF = $\ln(3/2)+1 \approx 0.4055 + 1 = 1.4055$

**TF-IDF (unnormalized):**
- D1: `data, google`=1×1.0=1.0; `earning, jumps, price, stock, today`=1×1.4055=1.4055
- D2: `data, google`=1.0; `china, plunge`=1.4055

**L2 normalize:**
- $\|\mathbf{v}_1\| = \sqrt{2(1.0)^2 + 5(1.4055)^2} = \sqrt{2 + 9.877} \approx 3.4463$
- Normalized D1: `data, google`=1.0/3.4463≈**0.2902**; others=1.4055/3.4463≈**0.4078**
- $\|\mathbf{v}_2\| = \sqrt{2(1.0)^2 + 2(1.4055)^2} \approx 2.4394$
- Normalized D2: `data, google`≈**0.4099**; `china, plunge`≈**0.5762**

**Mnemonic:** Doc1 has 5 words at 0.4078 and 2 at 0.2902. Doc2 has 2 at 0.5762 and 2 at 0.4099.

---

### 2.6 Cosine Similarity + PPMI (less likely but possible)

**Toy corpus:**
```
"data science drives insight"
"data analysis drives insight"
```
Window size 1 → co-occurrence matrix:

| | data | science | analysis | drives | insight |
|---|:---:|:---:|:---:|:---:|:---:|
| data | 0 | 1 | 1 | 0 | 0 |
| science | 1 | 0 | 0 | 1 | 0 |
| analysis | 1 | 0 | 0 | 1 | 0 |
| drives | 0 | 1 | 1 | 0 | 2 |
| insight | 0 | 0 | 0 | 2 | 0 |

**Total:** $N = 12$. Marginals: $C(\text{data})=C(\text{science})=C(\text{analysis})=C(\text{insight})=2$, $C(\text{drives})=4$.

**PMI:** $\text{PMI}(w,c) = \log_2 \frac{C(w,c) \cdot N}{C(w) \cdot C(c)}$, then **PPMI = max(0, PMI)**.

| Pair | $C(w,c)$ | $C(w)\cdot C(c)$ | Ratio | PMI | PPMI |
|---|:---:|:---:|:---:|:---:|:---:|
| (data, science) | 1 | 4 | 3 | 1.585 | 1.585 |
| (data, analysis) | 1 | 4 | 3 | 1.585 | 1.585 |
| (science, drives) | 1 | 8 | 1.5 | 0.585 | 0.585 |
| (drives, insight) | 2 | 8 | 3 | 1.585 | 1.585 |
| (non-co-occurring) | 0 | — | 0 | $-\infty$ | 0 |

**Cosine similarity (key example):**
- $\mathbf{v}_{\text{science}} = (1, 0, 0, 1, 0)$, $\mathbf{v}_{\text{analysis}} = (1, 0, 0, 1, 0)$
- $\cos = \frac{1+1}{\sqrt{2}\sqrt{2}} = \frac{2}{2} = \mathbf{1.0}$ (perfect synonymy via shared context)

---

### 2.7 Argmax Computation (2024 Q1-C pattern)

**Equation (memorize — write this first!):**
$$\hat{W} = \arg\max_W P(X \mid W) \cdot P(W) = \arg\max_W \prod_k P(w_k \mid w_{k-1})$$

**Pattern:** Given candidates per slot, compute $P(W) = \prod_k P(w_k \mid w_{k-1})$ for each candidate sequence, pick the argmax.

**Worked pattern for "The cat chased the mouse":**
- Slot 1: only "The"
- Slot 2 ∈ {cat, bat, rat}
- Slot 3 ∈ {chased, ate}
- Slot 4: only "the"
- Slot 5 ∈ {mouse, house}

Compute bigram product for each combination, pick the highest. Typical answer: "The cat chased the mouse" because $P(\text{cat} \mid \text{the})$, $P(\text{chased} \mid \text{cat})$, $P(\text{the} \mid \text{chased})$, $P(\text{mouse} \mid \text{the})$ are all high.

**For Bayes' ASR version:** $P(W \mid X) \propto P(X \mid W) \cdot P(W)$ → acoustic model × language model.

---

## 3. 📝 PYQ-Style Answers (10-mark questions)

### 3.1 HMM in Speech Recognition (10 marks) — asked in 2025 Q2 OR

**Definition (2 marks):** HMM is a doubly stochastic model — an underlying Markov chain of hidden states generates observable outputs through emission probabilities. In ASR, **hidden states = phonemes** (or sub-phonetic states like onset/nucleus/coda), **observations = acoustic feature vectors (MFCCs)** computed every 10 ms.

**Three fundamental problems (2 marks):**
1. **Evaluation:** Given $\lambda=(A,B,\pi)$ and $O$, find $P(O \mid \lambda)$ → **Forward algorithm**
2. **Decoding:** Given $\lambda$ and $O$, find most likely state sequence → **Viterbi algorithm**
3. **Learning:** Estimate $\lambda$ from $O$ → **Baum-Welch (EM)**

**HMM parameters (3 marks):**
- States $S=\{s_1,\ldots,s_N\}$ — one HMM per phoneme; for word "cat" → 3 HMMs for /k/ /æ/ /t/
- Transition matrix $A=[a_{ij}]$ — $a_{ij}=P(s_j \text{ at } t+1 \mid s_i \text{ at } t)$. Speech HMMs are **left-to-right** ($a_{ij}=0$ for $j<i$)
- Emission matrix $B=[b_j(o)]$ — $b_j(o)=P(o \mid s_j)$. Classic: GMM; modern: DNN
- Initial $\pi$ — usually $\pi_1=1, \pi_i=0$ for $i>1$

**Workflow (3 marks):**
1. Pre-emphasis → framing (25ms every 10ms) → windowing (Hamming)
2. FFT → Mel filterbank → log → DCT → 13-dim MFCC (+Δ+ΔΔ = 39 features)
3. Acoustic model scores $P(o \mid s)$ for each candidate state
4. Viterbi decoder combines acoustic scores + LM prior $P(W)$:
$$\hat{W} = \arg\max_W P(O \mid W) \cdot P(W)$$
5. Output the recognized word sequence

**Example:** For input audio of "cat" → MFCC frames → 3-state HMMs for /k/ /æ/ /t/ concatenated → Viterbi finds best path → lexicon maps /k/æ/t/ → "cat" → LM confirms high probability → output "cat".

---

### 3.2 Word Boundary Detection (10 marks) — asked in 2024 Q4(B) and 2025 Q2

**Definition (2 marks):** Word boundary detection is the task of segmenting a continuous stream of input (speech audio or unspaced text) into discrete word units. In speech, audio has no natural pauses between words; in many languages (Chinese, Japanese, Thai), text has no spaces.

**Challenges in speech (2 marks):**
- No acoustic pauses between words; coarticulation blurs boundaries
- Speaker rate variation, accents, disfluencies ("uh", "um")
- Code-switching (mixing languages)

**Challenges in text (2 marks):**
- Languages without spaces: Chinese, Japanese, Thai, Korean
- Compound words: German `Rindfleischetikettierungsüberwachungsaufgabenübertragungsgesetz`
- Hyphenation: `state-of-the-art`, contractions: `don't`
- Different conventions: German compounds; Chinese needs segmentation as a separate task

**Examples (2 marks):**
- English speech: "did you" → "didja" (acoustic merger)
- Chinese text: `我喜欢自然语言处理` → must segment as `我 / 喜欢 / 自然 / 语言 / 处理`
- Hindi-English code-switching in speech

**Strategies to handle errors (2 marks):**
1. **Acoustic-phonetic features** — detect pauses, pitch drops, vowel lengthening
2. **Language-model priors** — prefer high-probability word sequences
3. **Dictionary lookup** — match segmentations against lexicon
4. **Sub-word models** — BPE / SentencePiece (avoid hard boundaries)
5. **End-to-end ASR** — Whisper, Conformer (learn boundaries implicitly)

---

### 3.3 Components of NLP System (5 marks) — asked in 2025 Q1

**Five components** with their input → output:

| # | Component | Input | Output |
|:---:|---|---|---|
| 1 | **Lexical Analysis (Tokenisation)** | Raw text | Tokens |
| 2 | **Syntactic Analysis (Parsing)** | Tokens | Parse tree |
| 3 | **Semantic Analysis** | Parse tree | Meaning representation |
| 4 | **Discourse / Pragmatic Analysis** | Sentences | Resolved references, intentions |
| 5 | **Application Layer** | Any of above | Task output (label, translation, answer) |

**Differences (the key part of the answer):**
- Lexical answers "What are the units?"
- Syntactic answers "Is it grammatical? How structured?"
- Semantic answers "What does it mean?"
- Pragmatic answers "What was intended in context?"
- Application answers "What should I do with this?"

Each component builds on the previous one sequentially.

---

### 3.4 Components of Speech Recognition (6 marks) — asked in 2024 Q5(A) OR

**Five components:**
1. **Acoustic Front-end** — converts raw audio into MFCC features (pre-emphasis, framing, windowing, FFT, Mel filterbank, log, DCT)
2. **Acoustic Model** — maps features to phoneme probabilities. Classic: GMM-HMM; modern: DNN-HMM, CTC-trained RNN/Transformer, RNN-Transducer
3. **Pronunciation Model (Lexicon)** — maps each word to its phoneme sequence (e.g., `cat → /k/ /æ/ /t/`). Stored as CMU Pronouncing Dictionary
4. **Language Model** — assigns $P(W)$ to word sequences. Classic: n-gram; modern: neural LM
5. **Decoder** — combines all three scores, finds $\hat{W} = \arg\max_W P(O \mid W) \cdot P(W)$ via Viterbi/A* search

**Workflow:**
```
Audio → [Front-end: MFCC] → [Acoustic Model: P(o|s)]
                                ↓
              [Pronunciation Lexicon: word → phonemes]
                                ↓
                    [Decoder + LM: P(W)]
                                ↓
                       Recognized text
```

---

### 3.5 Regex for Email Extraction (3 marks) — asked in 2024 Q1(A)

**Pattern:** `[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}(?:\.[A-Za-z]{2,})*`

```python
import re
text = "I am a student with email id abc@xyz.com and my friend's email is abc.def@xyz.co.in."
pattern = r'[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}(?:\.[A-Za-z]{2,})*'
re.findall(pattern, text)
# ['abc@xyz.com', 'abc.def@xyz.co.in']
```

**Explanation:**
- `[A-Za-z0-9._%+-]+` → local part (letters, digits, dots, _, %, +, -)
- `@` → literal @
- `[A-Za-z0-9.-]+` → domain name
- `\.[A-Za-z]{2,}` → TLD (≥2 letters)
- `(?:\.[A-Za-z]{2,})*` → optional country TLD (.in, .uk)

---

### 3.6 POS Tagging with Example (3 marks) — asked in 2024 Q1(B)

**Definition (1 mark):** POS tagging assigns a grammatical category (noun, verb, adjective, etc.) to each word in a sentence. Goal: resolve ambiguities (`book` = noun or verb depending on context).

**Example (2 marks):**
Sentence: "Google is looking at buying U.K. startup for $1 billion"

| Token | Tag | Meaning |
|---|---|---|
| Google | NNP | Singular proper noun |
| is | VBZ | Verb, 3rd-sing present |
| looking | VBG | Verb, gerund |
| at | IN | Preposition |
| buying | VBG | Verb, gerund |
| U.K. | NNP | Singular proper noun |
| startup | NN | Singular noun |
| for | IN | Preposition |
| 1 | CD | Cardinal number |
| billion | CD | Cardinal number |

Penn Treebank has 36 POS tags. Methods: HMM, MEMM, CRF, RNNs, Transformers.

---

## 4. 📖 2-Mark Definitions (Memorize — exactly 2025 Q3)

> These 5 definitions appeared in 2025 Q3. They will very likely appear again this year.

### (a) Tokenization
The fundamental NLP process of breaking a stream of text into smaller units called **tokens** using a set of predetermined rules. A token may be a word, sub-word, character, or punctuation.
**Example:** `"Hello, world!"` → `['Hello', ',', 'world', '!']`
**Token vs Type:** "they lay back on the San Francisco grass" has **15 tokens** but **13 types** (some words repeat).

### (b) Stemming
A heuristic process that reduces a word to its base form (the **stem**) by stripping suffixes and prefixes using fixed rules. The stem need not be a real word.
**Example (Snowball stemmer):** `running → run`, `studies → studi`, `Stemming → stem`, `testing → test`.

### (c) Morphological Analysis
The process of breaking a word into its constituent **morphemes** (smallest meaning-bearing units), considering the grammatical role of each (root, prefix, suffix, plural marker, tense marker). Uses linguistic knowledge; more sophisticated than stemming.
**Example:** `unhappiness` = `un-` (negative prefix) + `happy` (root) + `-ness` (nominalizing suffix). `cats` = `cat` + `-s` (plural).

### (d) Computational Grammar
The formal specification of the syntactic rules of a language in a machine-processable form. It defines which strings of words are grammatical and assigns each a structural description (parse tree).
**Example (CFG rule):** `S → NP VP` (a sentence is a noun phrase + verb phrase).
**Why necessary:** structural disambiguation, anaphora resolution, machine translation, information extraction.

### (e) Place and Manner of Articulation
- **Place** = *where* in the vocal tract a consonant is constricted: bilabial (/p/,/b/,/m/), labio-dental (/f/,/v/), dental (/θ/,/ð/), alveolar (/t/,/d/,/s/,/n/,/l/), post-alveolar (/ʃ/,/tʃ/), palatal (/j/), velar (/k/,/g/,/ŋ/), glottal (/h/).
- **Manner** = *how* the airstream is constricted: plosive (/p/,/t/,/k/), fricative (/f/,/s/,/ʃ/), affricate (/tʃ/,/dʒ/), nasal (/m/,/n/,/ŋ/), approximant (/ɹ/,/l/,/j/,/w/), lateral (/l/).
- Together with **voicing** (voiced vs voiceless), they uniquely identify a consonant.

---

### Bonus 2-mark definitions (might appear)

**Stop word** — commonly used word filtered out before processing because it carries little discriminative info. Examples: `a, the, is, are, in, on, of, and, to`.

**Lemmatisation** — sophisticated process that transforms a word to its base dictionary form (lemma), considering meaning, context, and POS. Output is always a real word.
**Example:** `studies → study`, `running → run` (verb) / `running` (noun), `better → good`.

**Named Entity Recognition (NER)** — locating and classifying named entities (persons, organizations, locations, times, quantities) in text. Often multi-word: "Marie Curie" (person), "New York City" (location).

**OOV (Out-of-Vocabulary)** — a word the model never saw during training. BPE/SentencePiece handle OOV by falling back to sub-word units.

**Morpheme** — the smallest meaning-bearing unit of a language. `cats` = `cat` (root) + `-s` (plural morpheme). `unlikeliest` = `{un-, likely, -est}`.

**Cosine similarity** — measures the angle between two vectors: $\cos(\mathbf{u},\mathbf{v}) = \frac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\| \|\mathbf{v}\|}$. Range $[-1, 1]$; for count vectors, $[0, 1]$.

**Perplexity** — inverse probability of test set, normalized by length: $\text{PP}(W) = P(W)^{-1/n} = 2^{H(W)}$. Interpretation: effective branching factor. Lower = better.

**Cross-entropy** — average negative log-likelihood (in bits): $H(W) = -\frac{1}{n} \sum_k \log_2 P(w_k \mid \ldots)$. Lower = better.

**Smoothing** — reallocating probability mass from observed N-grams to unseen ones to avoid zero probabilities. Methods: Laplace (Add-1), Add-$m$ (Lidstone), Good-Turing.

**Back-off** — if higher-order N-gram count is 0, fall back to lower-order (trigram → bigram → unigram).

**Interpolation** — always blend all orders: $P = \lambda_3 P_3 + \lambda_2 P_2 + \lambda_1 P_1$, where $\sum \lambda_i = 1$.

---

## 5. 📐 Formula Cheat Sheet (Memorize Verbatim)

### N-gram MLE
| Model | Formula |
|---|---|
| Unigram | $P(w_k) = \dfrac{C(w_k)}{N_{\text{total}}}$ |
| Bigram | $P(w_k \mid w_{k-1}) = \dfrac{C(w_{k-1}, w_k)}{C(w_{k-1})}$ |
| Trigram | $P(w_k \mid w_{k-2}, w_{k-1}) = \dfrac{C(w_{k-2}, w_{k-1}, w_k)}{C(w_{k-2}, w_{k-1})}$ |

### Chain Rule
$$P(w_1, \ldots, w_n) = \prod_{k=1}^n P(w_k \mid w_1, \ldots, w_{k-1})$$

### Markov Approximation
$$P(W) \approx \prod_k P(w_k \mid w_{k-N+1:k-1})$$

### Perplexity (direct)
$$\text{PP}(W) = P(W)^{-1/n} = \left(\prod_k P(w_k \mid \ldots)\right)^{-1/n}$$

### Cross-entropy
$$H(W) = -\frac{1}{n} \sum_{k=1}^n \log_2 P(w_k \mid \ldots)$$

### PP from H
$$\text{PP}(W) = 2^{H(W)}$$

### Laplace (Add-1)
$$P_{\text{Lap}}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + |V|}$$

### Add-$m$ (Lidstone)
$$P_{\text{Add-}m}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + m}{C(w_{k-1}) + m|V|}$$

### Linear Interpolation (trigram)
$$P = \lambda_3 P_3 + \lambda_2 P_2 + \lambda_1 P_1, \quad \sum \lambda_i = 1, \lambda_i \geq 0$$

### Katz Back-off
$$P_{\text{BO}} = \begin{cases} P^*(w_k \mid \ldots) & \text{if } C > 0 \\ \alpha \cdot P_{\text{BO}}(w_k \mid \text{lower order}) & \text{if } C = 0 \end{cases}$$

### Cosine Similarity
$$\cos(\mathbf{u}, \mathbf{v}) = \frac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\| \|\mathbf{v}\|} = \frac{\sum_i u_i v_i}{\sqrt{\sum u_i^2} \sqrt{\sum v_i^2}}$$

### PMI
$$\text{PMI}(w, c) = \log_2 \frac{P(w, c)}{P(w) P(c)} = \log_2 \frac{C(w, c) \cdot N}{C(w) \cdot C(c)}$$

### PPMI
$$\text{PPMI}(w, c) = \max(0, \text{PMI}(w, c))$$

### TF-IDF
$$\text{TF-IDF}(t, d) = \text{TF}(t, d) \times \text{IDF}(t)$$
$$\text{IDF}_{\text{basic}}(t) = \log \frac{|D|}{\text{df}(t)}$$
$$\text{IDF}_{\text{sklearn}}(t) = \ln\left(\frac{1 + |D|}{1 + \text{df}(t)}\right) + 1$$

### L2 Normalization
$$\hat{\mathbf{v}} = \frac{\mathbf{v}}{\|\mathbf{v}\|_2}$$

### Argmax Decoding (Bayes / ASR)
$$\hat{W} = \arg\max_W P(W \mid X) = \arg\max_W P(X \mid W) \cdot P(W)$$

### Bayes' Rule
$$P(W \mid X) = \frac{P(X \mid W) P(W)}{P(X)}$$

### Viterbi Recursion
$$V_t(j) = \max_i V_{t-1}(i) \cdot a_{ij} \cdot b_j(o_t)$$

### HMM Parameters
$$\lambda = (A, B, \pi)$$
- $A$ = transition matrix, $B$ = emission matrix, $\pi$ = initial state distribution

### Entropy
$$H = -\sum_x p(x) \log_2 p(x)$$

---

## 6. 🎯 Exam Hall Strategy (Read This Last)

### 6.1 Time Allocation (60 min, 25 marks)

| Question type | Marks | Time |
|---|:---:|:---:|
| 5 short Q's (definitions) | 5 × 2 = 10 | 12 min |
| 1 conceptual Q (10 marks) | 10 | 24 min |
| 1 numerical Q (10 marks) | 10 | 20 min |
| Buffer / revision | — | 4 min |
| **Total** | **25** | **60 min** |

### 6.2 The 7 Golden Rules

1. **Numerical first, theory second.** If a numerical is worth 10 marks and a definition is worth 2 marks, do the numerical first. Numericals have more partial-credit slack.

2. **Write the formula BEFORE plugging in numbers.** Even if your arithmetic is wrong, the formula gets you 50% of the marks.

3. **For 2-mark definitions:** keep it to 2 lines + 1 small example. Do not write a paragraph. The examiner is scanning for the keyword + the example.

4. **For 5/10-mark answers:** use sub-headings explicitly (Definition → Formula → Example → Diagram → Advantages → Disadvantages). Examiners scan for these.

5. **Always include `</s>` in perplexity.** n includes `</s>` but excludes the initial `<s>`. This is the #1 source of mistakes.

6. **For Laplace:** always include $|V|$ in the denominator. Forgetting it = -2 marks instantly.

7. **If you're stuck on a numerical for >5 min, move on.** Come back if time permits. Don't sacrifice 8 marks of theory for 2 marks of arithmetic.

### 6.3 Numerical Answer Patterns (Memorize these 4 numbers!)

| Numerical | $P(W)$ | $\text{PP}(W)$ | $H(W)$ bits/word |
|---|:---:|:---:|:---:|
| Bigram MLE | 1/9 ≈ 0.111 | **√3 ≈ 1.732** | 0.7925 |
| Trigram MLE | 1/6 ≈ 0.167 | **6^(1/4) ≈ 1.565** | 0.6462 |
| Bigram + Laplace | 1/676 ≈ 0.00148 | **√26 ≈ 5.099** | 2.350 |
| (Trigram < Bigram PP) | — | 1.565 < 1.732 | — |

If the question gives you the exact same training corpus as above (the "I am Sam" corpus), these answers are correct verbatim. If the corpus differs, apply the same method — the structure of the answer is identical.

### 6.4 Quick Concept Recall (5 min before exam)

- **NLP** = make computers understand + generate human language.
- **5 components of NLP system** = Lexical → Syntactic → Semantic → Pragmatic → Application.
- **5 components of ASR** = Front-end → Acoustic model → Lexicon → LM → Decoder.
- **5 preprocessing steps** = Tokenise → Lowercase → Stop-word removal → Stem/Lemmatize → Vectorize.
- **3 HMM problems** = Evaluation (Forward) → Decoding (Viterbi) → Learning (Baum-Welch).
- **3 solutions to data sparsity** = Smoothing → Back-off/Interpolation → Neural embeddings.
- **Penn Treebank** has **36 POS tags**.
- **8 places of articulation** = bilabial, labio-dental, dental, alveolar, post-alveolar, palatal, velar, glottal.
- **6 manners of articulation** = plosive, fricative, affricate, nasal, approximant, lateral.
- **Argmax equation** = $\hat{W} = \arg\max_W P(X \mid W) \cdot P(W)$.
- **Lower perplexity = better model.**
- **Laplace smoothing INCREASES perplexity** (a known drawback).
- **Trigram PP < Bigram PP** because more context resolves ambiguity.
- **BPE never produces OOV** — falls back to characters.
- **MP3 = lossy, FLAC = lossless.** Use FLAC for NLP training.
- **CSV = flat tabular, JSON = nested hierarchical.**

### 6.5 Final Breath

You've got this. The exam is 25 marks. Even if you only nail:
- All 5 definitions (10 marks)
- 1 conceptual (10 marks)
- Half of the numerical (2-3 marks)

...that's already 22-23/25. **Focus on the definitions and the conceptual questions first** — they are the most reliable marks. The numerical is bonus.

**Breathe. Read each question twice. Write the formula first. Move on if stuck.**

Good luck. 🍀

---

*End of last-hour cramming guide. Total reading time: ~15 minutes if skimmed, ~30 minutes if studied.*
