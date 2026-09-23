# LAST-HOUR NLP EXAM SURVIVAL CHEAT-SHEET
**Target:** Mid-Sem (25 Marks | 60 Mins)  
**Syllabus:** Unit 1 (Preprocessing & Foundations) + Unit 2 (Vectorization & $N$-gram LMs)  
**Strategy:** Memorize the formula box $\to$ Understand the 4 numerical templates $\to$ Cram the justifications.

---

## 1. FORMULA CHEAT-SHEET (MEMORIZE RIGHT NOW)

### 1. $N$-gram MLE Probabilities
* **Bigram:** $P(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k)}{C(w_{k-1})}$
* **Trigram:** $P(w_k \mid w_{k-2}, w_{k-1}) = \frac{C(w_{k-2}, w_{k-1}, w_k)}{C(w_{k-2}, w_{k-1})}$
* **Sentence Probability:** $P(W) = \prod_{k=1}^n P(w_k \mid \text{context})$

---

### 2. Perplexity ($PP$) & Cross-Entropy ($H$)
* **Cross-Entropy:** $H(W) = -\frac{1}{n} \sum_{k=1}^n \log_2 P(w_k \mid \text{context}) \quad \text{(bits/word)}$
* **Perplexity:** $PP(W) = 2^{H(W)} = P(W)^{-\frac{1}{n}} = \sqrt[n]{\frac{1}{P(W)}}$
* *Calculator Trick:* If you have $\ln(x)$, $\log_2(x) = \frac{\ln(x)}{\ln(2)} \approx \frac{\ln(x)}{0.69315}$.
* *Rule:* **Lower Perplexity = Better Model.** Minimum value is $1$ (perfect certainty).

---

### 3. Smoothing Formulas
* **Laplace (Add-1):** 
  $$P_{\text{Laplace}}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + |V|}$$
* **Add-$m$ (Lidstone) ($0 < m < 1$):** 
  $$P_{\text{Add-}m}(w_k \mid w_{k-1}) = \frac{C(w_{k-1}, w_k) + m}{C(w_{k-1}) + m|V|}$$
* **Linear Interpolation:** 
  $$\hat{P} = \lambda_3 P_{\text{tri}} + \lambda_2 P_{\text{bi}} + \lambda_1 P_{\text{uni}} \quad (\sum \lambda_i = 1)$$
* **Katz Back-off:** 
  $$P_{\text{BO}} = \begin{cases} \frac{C(w_{k-2:k}) - d}{C(w_{k-2:k-1})} & \text{if } C > 0 \\ \alpha \cdot P_{\text{BO}}(w_k \mid w_{k-1}) & \text{if } C = 0 \end{cases}$$

---

### 4. Vectorization: PPMI & TF-IDF
* **PMI:** $\text{PMI}(w, c) = \log_2 \left( \frac{C(w, c) \cdot N}{C(w) \cdot C(c)} \right)$ ($N$ = total matrix co-occurrence sum)
* **PPMI:** $\text{PPMI}(w, c) = \max(0, \text{PMI}(w, c))$
* **Cosine Similarity:** $\cos(\mathbf{u}, \mathbf{v}) = \frac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\| \|\mathbf{v}\|}$
* **Sklearn TF-IDF:** $\text{IDF}(t) = \ln \left( \frac{1 + |D|}{1 + \text{DF}(t)} \right) + 1$
* **$L_2$ Normalization:** $\mathbf{v}_{\text{norm}} = \frac{\mathbf{v}}{\sqrt{\sum v_i^2}}$

---

## 2. THE 4 MUST-KNOW NUMERICAL TEMPLATES (EASY 10–15 MARKS)

### Numerical Template 1: Bigram vs. Trigram Perplexity
**Corpus:** 
1. `<s> I am Sam </s>`  
2. `<s> Sam I am </s>`  
3. `<s> I do not like green eggs </s>`  
**Test Sentence:** `<s> I am Sam </s>` (Tokens to evaluate: $n = 4$: `I`, `am`, `Sam`, `</s>`)

#### Bigram Solution:
1. $P(\text{I} \mid \text{<s>}) = \frac{C(\text{<s>}, \text{I})}{C(\text{<s>})} = \frac{2}{3}$
2. $P(\text{am} \mid \text{I}) = \frac{C(\text{I}, \text{am})}{C(\text{I})} = \frac{2}{3}$
3. $P(\text{Sam} \mid \text{am}) = \frac{C(\text{am}, \text{Sam})}{C(\text{am})} = \frac{1}{2}$
4. $P(\text{</s>} \mid \text{Sam}) = \frac{C(\text{Sam}, \text{</s>})}{C(\text{Sam})} = \frac{1}{2}$
* **$P(W)$:** $\frac{2}{3} \times \frac{2}{3} \times \frac{1}{2} \times \frac{1}{2} = \frac{4}{36} = \frac{1}{9} \approx 0.1111$
* **$PP(W)$:** $\left(\frac{1}{9}\right)^{-\frac{1}{4}} = 9^{0.25} = \sqrt{3} \approx \mathbf{1.732}$

#### Trigram Solution (Add two `<s>`):
1. $P(\text{I} \mid \text{<s>}, \text{<s>}) = \frac{2}{3}$
2. $P(\text{am} \mid \text{<s>}, \text{I}) = \frac{1}{2}$
3. $P(\text{Sam} \mid \text{I}, \text{am}) = \frac{1}{2}$
4. $P(\text{</s>} \mid \text{am}, \text{Sam}) = \frac{1}{1} = 1.0$
* **$P(W)$:** $\frac{2}{3} \times \frac{1}{2} \times \frac{1}{2} \times 1 = \frac{2}{12} = \frac{1}{6} \approx 0.1667$
* **$PP(W)$:** $\left(\frac{1}{6}\right)^{-\frac{1}{4}} = 6^{0.25} \approx \mathbf{1.565}$
* **Analytical Justification:** Trigram achieves lower perplexity ($1.565 < 1.732$) because conditioned on `am Sam`, the sentence ending is known with certainty ($P=1.0$), eliminating uncertainty.

---

### Numerical Template 2: Laplace (Add-1) Smoothed Perplexity
Using the same test sentence: `<s> I am Sam </s>` ($n = 4$), Vocabulary $|V| = 10$.
Formula: $P_{\text{Laplace}} = \frac{C(w_{k-1}, w_k) + 1}{C(w_{k-1}) + 10}$
1. $P(\text{I} \mid \text{<s>}) = \frac{2 + 1}{3 + 10} = \frac{3}{13}$
2. $P(\text{am} \mid \text{I}) = \frac{2 + 1}{3 + 10} = \frac{3}{13}$
3. $P(\text{Sam} \mid \text{am}) = \frac{1 + 1}{2 + 10} = \frac{2}{12} = \frac{1}{6}$
4. $P(\text{</s>} \mid \text{Sam}) = \frac{1 + 1}{2 + 10} = \frac{2}{12} = \frac{1}{6}$
* **$P_{\text{Laplace}}(W)$:** $\frac{3}{13} \times \frac{3}{13} \times \frac{1}{6} \times \frac{1}{6} = \frac{9}{6084} = \frac{1}{676} \approx 0.001479$
* **$PP_{\text{Laplace}}(W)$:** $(676)^{1/4} = \sqrt{26} \approx \mathbf{5.099}$
* **Why did PP increase from 1.732 to 5.099?** Laplace smoothing "steals" probability mass from frequently observed bigrams to give a non-zero budget to unseen bigrams. Because our test sentence only contained known bigrams, their probabilities dropped, raising perplexity.

---

### Numerical Template 3: Byte Pair Encoding (BPE)
**Corpus:** `read` (3), `reads` (2), `reader` (2), `reading` (2), `unread` (1), `readers` (1).
1. Append end-of-word marker `_`:
   - `r e a d _` (3), `r e a d s _` (2), `r e a d e r _` (2), `r e a d i n g _` (2), `u n r e a d _` (1), `r e a d e r s _` (1).
2. Count adjacent pairs (Total occurrences = 11):
   - `(r, e)` = 11, `(e, a)` = 11, `(a, d)` = 11.  
     *(Tie-breaker rule: take the leftmost pair in `read`)*
3. **Merge Sequence:**
   - Merge 1: `(r, e)` $\to$ **`re`**
   - Merge 2: `(re, a)` $\to$ **`rea`**
   - Merge 3: `(rea, d)` $\to$ **`read`**
   - Merge 4: `(read, _)` has count $3 + 1 = 4$ $\to$ **`read_`**
   - Merge 5: `(read, e)` has count $2 + 1 = 3$ $\to$ **`reade`**
   - Merge 6: `(reade, r)` has count $2 + 1 = 3$ $\to$ **`reader`**
4. **OOV Tokenization at Test Time:**
   - Word: `readable` $\to$ Split: `r e a d a b l e _`
   - Apply merges: `read a b l e _`
   - Output tokens: `['read', 'a', 'b', 'l', 'e', '_']`
   - **Justification:** BPE handles OOV words without errors because any unknown word defaults back to its known subwords and atomic character tokens.

---

### Numerical Template 4: Co-Occurrence, Cosine Similarity & PPMI
**Corpus:**  
1. `"data science drives insight"`  
2. `"data analysis drives insight"`  
Context window = 1 (symmetrical: 1 left, 1 right). Total count sum $N = 12$.

#### Raw Counts:
- $C(\text{science}) = 2$ (context: `data`, `drives`) $\to \mathbf{v}_{\text{science}} = [1, 0, 0, 1, 0]$ (over `data, science, analysis, drives, insight`)
- $C(\text{analysis}) = 2$ (context: `data`, `drives`) $\to \mathbf{v}_{\text{analysis}} = [1, 0, 0, 1, 0]$
- **Cosine Similarity:**
  $$\cos(\mathbf{v}_{\text{science}}, \mathbf{v}_{\text{analysis}}) = \frac{1(1) + 0 + 0 + 1(1) + 0}{\sqrt{2}\sqrt{2}} = \frac{2}{2} = \mathbf{1.0}$$
  *Meaning:* They are semantic synonyms because they share identical contexts, even though they never appear next to each other.

#### PPMI Calculation:
$\text{PMI}(w, c) = \log_2 \left(\frac{C(w,c) \cdot 12}{C(w) \cdot C(c)}\right)$
* $\text{PPMI}(\text{data}, \text{science}) = \log_2\left(\frac{1 \times 12}{2 \times 2}\right) = \log_2(3) = \mathbf{1.585}$
* $\text{PPMI}(\text{science}, \text{drives}) = \log_2\left(\frac{1 \times 12}{2 \times 4}\right) = \log_2(1.5) = \mathbf{0.585}$
* $\text{PPMI}(\text{drives}, \text{insight}) = \log_2\left(\frac{2 \times 12}{4 \times 2}\right) = \log_2(3) = \mathbf{1.585}$
* Any pair with count $0 \implies \text{PMI} \to -\infty \implies \text{PPMI} = \mathbf{0}$.

---

## 3. HIGH-PROBABILITY JUSTIFICATIONS & "WHY" QUESTIONS

#### 1. Why does an unseen $N$-gram cause Sequence Collapse & Perplexity Explosion?
* **Collapse:** $P(W) = \prod P(w_k \mid w_{k-1})$. If any unseen $N$-gram has $C=0$, $P_{\text{MLE}} = 0$. One zero makes the whole product $P(W) = 0$.
* **Explosion:** $PP(W) = \left(\frac{1}{P(W)}\right)^{1/n} = \left(\frac{1}{0}\right)^{1/n} \to \infty$. In log space, $\log_2(0) \to -\infty$, driving cross-entropy to $\infty$.

#### 2. Why add $|V|$ to the denominator in Laplace Smoothing?
* We add $1$ to every word's count in the vocabulary $V$. Since there are $|V|$ words:
  $$\sum_{w \in V} [C(w_{k-1}, w) + 1] = C(w_{k-1}) + |V|$$
  To keep the probabilities normalized ($\sum_{w \in V} P = 1$), the denominator must be $C(w_{k-1}) + |V|$.

#### 3. Why is Laplace smoothing bad for large $|V|$ and how does Add-$m$ fix it?
* If $|V| = 50,000$, adding $1$ to every word adds $50,000$ to the denominator. This shifts far too much probability mass from seen words to unseen words, ruining model accuracy.
* **Add-$m$ (Lidstone):** Replaces $1$ with a small fraction $m$ (e.g., $m = 0.05$). As $m \to 0$, it approaches pure MLE; as $m \to 1$, it becomes Laplace.

#### 4. Why does Perplexity equal the "Effective Branching Factor"?
* If you guess uniformly among $K$ equally likely words, $P(w) = 1/K$. Then $PP = 2^{-\log_2(1/K)} = K$.
* For real, non-uniform text, a perplexity of $50$ means the model's uncertainty is equivalent to making a uniform random guess among $50$ words at each step.

#### 5. Why can't One-Hot Encoding represent Semantic Similarity?
* Every word is an independent basis vector ($[1, 0, 0, \dots]$ vs $[0, 1, 0, \dots]$).
* The dot product between any two distinct words is always $\mathbf{0}$ (orthogonal). The model cannot tell that "cat" and "dog" are more related than "cat" and "refrigerator".

#### 6. Why use PPMI instead of raw co-occurrence counts?
* Raw counts are dominated by high-frequency words like *the, is, of*, which co-occur with everything without providing useful semantic context (frequency bias).
* PMI divides by marginal probabilities $P(w)P(c)$, which penalizes frequent words and highlights meaningful associations. We use PPMI ($\max(0, \text{PMI})$) because negative PMI tends to be unreliable on small counts and avoids $\log(0) = -\infty$.

#### 7. Linear Interpolation vs. Katz Back-off: What's the difference?
* **Interpolation:** *Always* blends all orders: $\hat{P} = \lambda_3 P_{\text{tri}} + \lambda_2 P_{\text{bi}} + \lambda_1 P_{\text{uni}}$.
* **Back-off:** Uses the highest-order $N$-gram if it exists ($C > 0$); it *only* falls back to lower orders if the count is zero.

#### 8. Why do models need the exact same vocabulary for fair Perplexity comparison?
* Perplexity measures how well probability mass is distributed across a vocabulary.
* A smaller vocabulary splits probability mass fewer ways, which artificially lowers perplexity. A model with an open vocabulary that replaces many words with `<UNK>` will also get an artificially low perplexity score.

---

## 4. RAPID-FIRE DEFINITIONS (2 MARKS EACH)

| Term | 20-Second Verbatim Exam Answer |
| :--- | :--- |
| **Tokenization** | Splitting a continuous text sequence into discrete units (words, punctuation, or subwords) for computational processing. |
| **Stemming** | A crude, heuristic rule-based technique that strips prefixes and suffixes to find a root stem; often produces non-real words (`caring` $\to$ `car`). |
| **Lemmatization** | Context-aware reduction of a word to its canonical dictionary base form (*lemma*) using vocabulary and grammatical analysis (`caring` $\to$ `care`). |
| **Morpheme** | The smallest meaning-bearing unit in a language (e.g., *unlikeliest* = `un-` + `likely` + `-est`). |
| **Morphological Analysis** | Breaking down words into their constituent morphemes (roots, prefixes, suffixes) to identify syntactic roles like tense, number, and case. |
| **Computational Grammar** | Formal rule systems (e.g., Context-Free Grammars) used by algorithms to parse sentence structures, validate syntax, and resolve ambiguities. |
| **Place of Articulation** | The physical location in the vocal tract where airflow is obstructed during speech production (e.g., *Bilabial*: lips; *Alveolar*: tongue on alveolar ridge). |
| **Manner of Articulation** | The method used to obstruct or release airflow during speech production (e.g., *Stop/Plosive*: complete burst; *Fricative*: turbulent friction). |
| **Nominal vs. Ordinal** | **Nominal:** Categories with no order (e.g., POS tags: `NN`, `VB`). **Ordinal:** Categories with a natural ranking, but unequal intervals (e.g., sentiment ratings: `1-star < 2-star < 3-star`). |
| **Interval vs. Ratio** | **Interval:** Numbers with equal steps, but no absolute zero (e.g., Temperature $^{\circ}\text{C}$, Year). **Ratio:** Numbers with equal steps and a true zero point (e.g., word count, duration in ms). |

---

## 5. SPEECH & PIPELINE QUICK-CRASH (5-MARK QUESTIONS)

### 1. HMM in Speech Recognition
* **Bayes' Rule Decoding:**
  $$\hat{W} = \arg\max_W \underbrace{P(O \mid W)}_{\text{Acoustic Model (HMM)}} \cdot \underbrace{P(W)}_{\text{Language Model ($N$-gram)}}$$
* **Acoustic Model $P(O \mid W)$:** Matches continuous acoustic features ($O$ = MFCC vectors from 25ms audio frames) to phone states using HMM emissions ($B$) and transitions ($A$).
* **Language Model $P(W)$:** Provides the prior probability of word sequences to ensure the output makes grammatical and semantic sense.
* **Decoding Algorithm:** The **Viterbi algorithm** finds the optimal path $\hat{W}$ efficiently.

---

### 2. Word Boundary Detection: Speech vs. Text
* **In Text:** Languages like Chinese, Japanese, and Thai do not use spaces between words. Compound words in German (*Donaudampfschiffahrt*) combine multiple words without spaces.
* **In Speech:** The audio waveform is continuous; **speakers do not pause between words**.
  - *Co-articulation:* The vocal tract moves continuously, blending adjacent sounds (*"did you"* sounds like *"did-jew"*).
  - *Acoustic Ambiguity:* Identical sound streams correspond to different words (*"ice cream"* vs. *"I scream"*, *"recognize speech"* vs. *"wreck a nice beach"*).

---

### 3. Audio Formats: MP3 vs. FLAC
* **MP3:** **Lossy** compression. Discards frequencies based on psychoacoustic models. Smaller files, but loses high-frequency details (like fricatives $/s/, /z/$), which can hurt ASR feature extraction.
* **FLAC:** **Lossless** compression. Retains 100% of original waveform details. Larger files, but preferred for training high-accuracy speech models.

---

### 4. Text Classification vs. Machine Translation Datasets
| Feature | Text Classification | Machine Translation |
| :--- | :--- | :--- |
| **Corpus** | Monolingual text. | Parallel bilingual aligned bitext ($S \leftrightarrow T$). |
| **Task Mapping** | Sequence $\to$ Single discrete label/category. | Sequence $\to$ Generated target sequence. |
| **Metric** | Accuracy, F1-Score. | BLEU, METEOR. |

---

## 6. EXAM-HALL TIME ALLOCATION STRATEGY (60 MINS / 25 MARKS)
* **First 5 Mins:** Scan the paper. Identify the primary numerical (BPE, Perplexity, PPMI, or TF-IDF).
* **Next 25 Mins:** Write out the numericals carefully. Double-check all logs and divisions:
  - $\log_2(1) = 0$
  - $\log_2(2) = 1$
  - $\log_2(3) \approx 1.585$
  - $\log_2(4) = 2$
  - $\log_2(1.5) \approx 0.585$
* **Next 20 Mins:** Answer the analytical / "Why" questions using the core keywords bolded above.
* **Last 10 Mins:** Complete the 2-mark definitions and check for units, formula statements, and proper boundary markers (`<s>`, `</s>`).
