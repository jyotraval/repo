# NLP Last-Hour Cram Sheet — 20IC403T
*You have ~60 minutes. This is triaged for maximum marks per minute. Skip nothing in bold. Everything here is verified correct — just memorize the pattern and reproduce it.*

**Confirmed scope (per prof's email + actual slides):** Tokenization/BPE, Stemming/Lemmatization, POS, NER (Unit 1) + One-Hot/BoW, TF-IDF, Cosine/PMI, N-gram LMs + Smoothing (Unit 2). **Do NOT waste time on:** speech articulation, HMM speech recognition, word boundary detection, corpus data-types (nominal/ordinal), JSON/CSV formats — these are old-syllabus, not this year's.

---

## ⏱ Minute 0–5: The 60-Second Overview
NLP = making computers understand/generate human language. Pipeline: **raw text → preprocessing (tokenize, clean, normalize) → feature representation (vectorize) → model**. Unit 1 = the left half (cleaning). Unit 2 = the right half (turning words into numbers + predicting word sequences).

---

## ⏱ Minute 5–20: Unit 1 Rapid-Fire (memorize these exact lines)

**Tokenization** = breaking text into tokens using rules. **Token** = instance in text; **Type** = distinct vocab word.

**Whitespace tokenization fails because (say all 5 if asked "issues"):**
1. Splits multi-word names wrong ("New York" → 2 tokens)
2. Leaves punctuation stuck to words ("Hello," )
3. Fails for Chinese/Japanese/Korean (no spaces)
4. Breaks emails/URLs/dates/hyphenated words
5. Causes bad search/retrieval matches

**Fix = Subword tokenization (BPE).** Algorithm in one line: *"Repeatedly merge the most frequent adjacent symbol pair, k times; at test time apply the same merges in the same order; unseen substrings just fall back to individual characters — BPE never fails to tokenize."*

**Morpheme** = smallest meaning unit. "cats" = cat + -s (2 morphemes). "unlikeliest" = un+likely+est.

**Stemming vs Lemmatization — THE differentiation answer:**
> "Stemming crudely chops suffixes using fixed rules and may produce a non-word (e.g. 'testing'→'test', but also 'studies'→'studi'). Lemmatization/morphological analysis uses vocabulary + context to return a real dictionary root (lemma) — e.g. sang/sung/sings all → 'sing'."

**POS tagging** = assign grammatical category per word, resolving ambiguity via context.
- Classic ambiguity example: *"Book that flight"* (VERB) vs *"Hand me that book"* (NOUN).
- Penn Treebank tagset = **36 tags**. Methods: HMM, MaxEnt, CRF, RNN/Transformer.

**NER** = find + classify named entities (Person, Org, Location, Time, Money...).
- Example: *"Sourav Ganguly (PERSON) served as captain of Indian Cricket team (ORG) from Kolkata (LOCATION)"*
- Note: NER tags multi-word phrases; POS tags single words/morphemes.

---

## ⏱ Minute 20–45: Unit 2 — Worked Templates (COPY THIS METHOD IN EXAM)

### Template A: One-Hot / BoW limitations (if asked, write this)
> One-hot: vector dimension = |vocabulary| (huge, sparse). Vectors are **orthogonal** → no similarity notion, treats words as fully independent (v_notebook ≠ v_note + v_book). BoW ignores grammar/word order, only counts frequency.

### Template B: Cosine Similarity + PMI (numerical)
**Steps:** (1) Build co-occurrence matrix (count words within window). (2) Cosine formula: `cos(u,v) = (u·v)/(‖u‖‖v‖)`. (3) PMI: `PMI(w,c)=log2[C(w,c)·N / (C(w)·C(c))]`, PPMI = max(0, PMI).

**Mini worked example:** corpus "dogs chase cats", "dogs chase mice", window=1.
`v_cats=[0,1,0,0]`, `v_mice=[0,1,0,0]` (both only co-occur with "chase") → **cosine = 1.0** (perfect similarity despite never appearing together — that's the whole point of PMI/co-occurrence: shared context = similar meaning).

### Template C: TF-IDF (numerical) — memorize this formula, it's THE one your course uses
```
IDF(t,D) = ln[ (1+N)/(1+df(t)) ] + 1        ← N=total docs, df(t)=docs containing t
TF-IDF(t,d) = TF(t,d) × IDF(t,D)            ← then L2-normalize the whole document vector
```
**Why not plain IDF `log(N/df)`?** Because if a term is in EVERY doc, df=N → log(1)=0 → term gets zero weight forever. The "+1" smoothing fixes this.

**Worked pattern:** term in every doc → IDF≈1.0. Term in only 1 of 2 docs → IDF≈1.4055. Multiply by term count, then divide each doc's vector by its L2 norm (`√Σxᵢ²`) to normalize.

### Template D: N-gram MLE + Perplexity — **the highest-value topic, master this**
**Formulas:**
```
Bigram MLE:   P(wk|wk-1) = C(wk-1,wk) / C(wk-1)
Trigram MLE:  P(wk|wk-2,wk-1) = C(wk-2,wk-1,wk) / C(wk-2,wk-1)
P(sentence) = product of all the conditional MLE terms (use <s>...</s> boundaries!)
Perplexity: PP(W) = P(W)^(-1/n)     where n = number of predicted tokens (incl. </s>)
Cross-entropy check: H(W) = -(1/n)Σlog2 P(...)  ;  PP(W) = 2^H(W)  (should match!)
```
**Fully memorized worked example (bigram, from your slides — reproduce this structure exactly):**

Corpus: `<s> I am Sam </s>` / `<s> Sam I am </s>` / `<s> I do not like green eggs </s>`
Test: `<s> I am Sam </s>`
```
P(I|<s>)=2/3   P(am|I)=2/3   P(Sam|am)=1/2   P(</s>|Sam)=1/2
P(W) = (2/3)(2/3)(1/2)(1/2) = 1/9 ≈ 0.111
n=4 → PP(W) = (1/9)^(-1/4) = 9^(1/4) = 3 ≈ 1.732
```
**Trigram on same data:** `P(W) = (2/3)(1/2)(1/2)(1) = 1/6 ≈ 0.167` → `PP = 6^(1/4) ≈ 1.565`
**Justification line (use this if asked "interpret"):** *"Trigram has lower perplexity because more history removes ambiguity — once you know 'am Sam', '</s>' is certain (prob=1). Lower perplexity = better model."*

### Template E: Data Sparsity + Laplace Smoothing — **2nd highest-value topic**
**The problem in one line:** *"If any single bigram in the test sentence has count 0, the whole product P(W)=0, so perplexity becomes infinite — a zero count means 'unseen', not 'impossible'."*

**Laplace (Add-1) fix:**
```
P_Laplace(wk|wk-1) = [C(wk-1,wk) + 1] / [C(wk-1) + |V|]
```
**Why add |V|?** So probabilities still sum to 1 over the whole vocabulary.

**Worked pattern (|V|=11 from the cat/dog/mat corpus), test sentence hits a zero bigram (sat→`</s>` never seen):**
```
Unsmoothed: P(</s>|sat) = 0/2 = 0  →  P(W)=0 → PP=∞
Laplace:    P(</s>|sat) = (0+1)/(2+11) = 1/13 ≈ 0.077   ← now non-zero!
Full smoothed P(W) ≈ 0.0006 → PP(W) ≈ 6.4
```
**Add-m variant:** same formula but `+m` and `+m|V|` instead of `+1`/`+|V|` (m is tuned, 0<m<1). As m→0 it's plain MLE; as m→1 it's Laplace.

**One-liner for Interpolation vs Backoff (easy 2-3 marks if asked):**
> *"Interpolation always blends probabilities from all N-gram orders (unigram+bigram+trigram) with weights λ summing to 1. Backoff uses the highest order only if it has evidence (count>0), and only falls back to lower orders when count=0, after discounting."*

---

## ⏱ Minute 45–55: Speed-Read Formula Sheet
```
cos(u,v) = u·v / (‖u‖‖v‖)
PMI(w,c) = log2[C(w,c)·N / (C(w)C(c))]         PPMI = max(0, PMI)
IDF(t,D) = ln[(1+N)/(1+df(t))] + 1              TF-IDF = TF × IDF  → L2 normalize
Chain rule: P(w1:n) = P(w1)P(w2|w1)...P(wn|w1:n-1)
Bigram MLE: P(wk|wk-1) = C(wk-1,wk)/C(wk-1)
Perplexity: PP(W) = P(W)^(-1/n) = 2^H(W)
Cross-entropy: H(W) = -(1/n)Σ log2 P(wk|...)
Laplace: P(wk|wk-1) = [C(wk-1,wk)+1]/[C(wk-1)+|V|]
Add-m:   P(wk|wk-1) = [C(wk-1,wk)+m]/[C(wk-1)+m|V|]
Interpolation: P̂ = λ3·P(tri) + λ2·P(bi) + λ1·P(uni),  Σλ=1
```

---

## ⏱ Minute 55–60: If You Get Stuck In The Exam
- **Any definition question** → give: (1) one-line definition, (2) one concrete example, (3) why it matters/where it's used. Partial credit loves this structure.
- **Any numerical you don't fully remember** → write the formula first (guaranteed partial marks), plug in whatever counts you can identify from the given text/corpus, show your working even if the final arithmetic is shaky.
- **"Differentiate X and Y" question** → always give a 2-column comparison + one example each. Never write pure prose for these.
- **If a question smells like old-syllabus (speech/HMM/articulation)** → answer with whatever adjacent Unit 1/2 concept you know (e.g., if asked about HMM, mention it's also used in POS tagging — you did cover that) rather than leaving it blank.

**Go. You've got this.**
