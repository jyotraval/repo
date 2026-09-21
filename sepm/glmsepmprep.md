# SEPM — Mid-Semester Exam Study Prep 📘

**Course:** Software Engineering & Project Management (SEPM)
**Course Code:** 23IC401T  |  **Department:** ICT, PDEU
**Mid-Sem Coverage:** Unit-I (Software Process Models & Requirements Engineering) + Unit-II (Umbrella Activities: SCM, SQA, Risk Management)
**Prepared from:** Professor's lecture notes (SEPM_NOTES_UNIT-I.pdf, Unit-I_SDLC.pdf/1/2, week 1.pdf, SCM_UNIT_II.pdf), 2024 & 2025 mid-sem PYQs (image + text), and IA-1 assignment. Gaps in professor's notes (Risk Management, detailed Scrum/XP, V&V) supplemented from standard SE textbooks (Pressman, Rajib Mall, Sommerville) — clearly marked with a 📚 icon.

---

## 0. How to Use This Document

1. **First pass (Day 1):** Read the *PYQ Analysis* (§2) and *Exam Strategy* (§3) to understand what matters most. Then read *Unit-I notes* (§4) end-to-end — don't memorise yet, just understand.
2. **Second pass (Day 2):** Read *Unit-II notes* (§5). Then attempt *Model Answers for PYQs* (§6) WITHOUT looking at the answer, then compare.
3. **Day 3 (revision):** Skim *Quick Revision Cards* (§7) — these are 1-liners for last-day cramming. Draw every diagram at least twice on paper.
4. **Exam day morning:** Re-read §3 (Exam Strategy), §7 (Quick Cards), and §8 (Last-Minute Tips).

> ⚠️ **Drawing diagrams is non-negotiable.** The PYQ explicitly says "Writing appropriate … drawing neat sketches/schematics wherever required is an integral part of the answer." Every model answer below includes a *diagram description* — practise drawing it.

---

## 1. Syllabus (Mid-Sem Scope)

### Unit-I — Software Process Models and Software Requirements Engineering (10 hrs)

- Software Product, Software crisis
- Handling complexity through **Abstraction and Decomposition**
- Overview of software development activities
- **Process Models:** Classical waterfall, Iterative waterfall, Prototyping, Evolutionary, Spiral, RAD
- **Agile Models:** Extreme Programming (XP), Scrum
- **Requirements Engineering:** Process, SRS, functional vs non-functional, desirable characteristics of good SRS

### Unit-II — Umbrella Activities (10 hrs)

- **Software Configuration Management (SCM):** Process and activities, Configuration audit, Metrics in SCM, Tools & automation
- **Software Quality Assurance (SQA):** Quality Control vs Quality Assurance, Tools, Measures of SQA Success
- **Risk Management:** Risk Management Cycle, Risk Identification, Quantification, Monitoring, Mitigation, Metrics in Risk Management

---

## 2. PYQ Analysis (2024 + 2025 Mid-Sem)

### 2.1 Exam Pattern

| Year | Total Marks | Duration | Section A | Section B |
|------|-------------|----------|-----------|-----------|
| **2025** | **25** | 1 hour | Que-1 (5 sub-parts × 1 mark) — answer all | Que-2 (3 sub-parts × 10 marks) — answer **any 2** |
| **2024** | **50** | 2 hours | Que-1 (5 sub-parts × 1 mark) — answer all | Que-2 (4 sub-parts × 15 marks) — answer **any 3** |

**What this means for your 2026 mid-sem:** Expect a hybrid pattern. Likely 25–50 marks, 1–2 hours. Section A will always have five 1-mark questions (definitions / one-liners). Section B will offer choices — you must answer 2–3 long-answer questions (10–15 marks each). **Always prepare 3 of the 4 long-answer topics deeply**, so you have a safety margin in the choice.

### 2.2 Frequency Analysis — Topics in PYQs

| Topic | 2024 | 2025 | Total hits | Priority |
|------|------|------|------------|----------|
| Software & Software Engineering (definition, objectives, challenges) | Q1a, Q1b | Q1a, Q1e | **4** | 🔥🔥🔥 Must-know |
| Process Models (waterfall / iterative / spiral / RAD / prototyping) | Q2a, Q2b | Q2a | **3** | 🔥🔥🔥 Must-know |
| Requirements Engineering + SRS | Q1c, Q2c | Q2b | **3** | 🔥🔥🔥 Must-know |
| Software Configuration Management (SCM) | Q2d | Q2c | **2** | 🔥🔥🔥 Must-know |
| Software Quality / Quality Assurance | Q1e, Q2d | Q1b | **3** | 🔥🔥 Must-know |
| Spiral Model — task regions | — | Q1c | **1** | 🔥🔥 Must-know (easy 1-mark) |
| CMM | — | Q1d | **1** | 🔥 Must-know (easy 1-mark) |
| Software Prototyping | Q1d | — | **1** | 🔥 Must-know |
| SRS Review | Q1c | — | **1** | 🔥 Must-know |

### 2.3 Section-A Question Bank (1-mark questions asked so far)

1. What is meant by Software and Software Engineering? (asked **twice** in 2025!)
2. Define process in the context of software quality.
3. List the task regions in the Spiral model.
4. What is the use of CMM?
5. What are the challenges in software?
6. What is the prime objective of software engineering?
7. What is known as SRS review?
8. What is meant by software prototyping?
9. What is software quality and how do we measure it?

### 2.4 Section-B Question Bank (long-answer questions asked so far)

1. Draw the schematic diagram of the Classical Waterfall Model in the SDLC. (2025 — 10 marks)
2. Explain requirements engineering processes with a suitable diagram. (2025 — 10 marks)
3. What is meant by software configuration management? Explain the two principal activities of configuration management. (2025 — 10 marks)
4. Explain the iterative waterfall and spiral model for the software life cycle and discuss various activities in each phase. (2024 — 15 marks)
5. Explain: (i) Waterfall model, (ii) RAD model, (iii) Prototyping model. (2024 — 15 marks)
6. Explain the main activities used in requirements engineering. What are the desirable characteristics of good SRS documents? Explain with an example. (2024 — 15 marks)
7. What is meant by software configuration management? Explain software quality assurance. (2024 — 15 marks)

### 2.5 Predicted Topics for 2026 Mid-Sem (High Confidence)

Based on the 2-year pattern, **at least 2 of the following 4 long-answer questions will appear** in some form:

1. **Process Models comparison** (waterfall + iterative + spiral + RAD + prototyping) — almost guaranteed.
2. **Requirements Engineering + SRS characteristics** — almost guaranteed.
3. **SCM with two principal activities** — almost guaranteed.
4. **SQA — definition, QC vs QA, activities, metrics** — high probability.

Plus **Risk Management** is in the syllabus and hasn't appeared in either PYQ — strong candidate for either a 1-mark (define risk) or a 10-mark (explain risk management cycle).

---

## 3. Exam Strategy & Topic Priority

### 3.1 The 6 "Must-Master" Topics (95% confidence at least 4 of these appear)

| # | Topic | Marks Potential | Notes |
|---|-------|-----------------|-------|
| 1 | **Classical + Iterative Waterfall Model** (diagram + phases + adv/disadv) | 10–15 | Practise drawing the schematic from memory |
| 2 | **Spiral Model** (task regions + diagram) | 1–15 | Task regions = 4 quadrants — memorise verbatim |
| 3 | **Requirements Engineering** (process + SRS characteristics) | 10–15 | SRS = black-box; 6 desirable characteristics |
| 4 | **SCM** (definition + two principal activities) | 10–15 | Config Identification + Config Control |
| 5 | **SQA** (definition + QC vs QA + activities + metrics) | 10–15 | Cost-of-defect curve; FTR |
| 6 | **Software & SE definition** (very short, asked twice!) | 1 | One-liner; do not skip |

### 3.2 Time Allocation for a 25-mark / 1-hour exam

- Section A (5 × 1 = 5 marks): **8–10 minutes total** (~2 min per question).
- Section B (2 × 10 = 20 marks): **50 minutes** (~25 min per long answer).
- Leave 2 minutes at end to check numbering + attach any sheets.

### 3.3 Time Allocation for a 50-mark / 2-hour exam

- Section A (5 × 1 = 5 marks): **10 minutes total**.
- Section B (3 × 15 = 45 marks): **100 minutes** (~33 min per long answer).
- Leave 10 minutes to review + complete diagrams.

### 3.4 How to write a 10/15-mark answer

1. **Opening definition** (1–2 lines): *"X is defined as …"*
2. **Diagram** (always, if applicable): neatly labelled, use a ruler. Box for entities, arrows for flow.
3. **Phases / Activities / Steps**: bullet list with one-line description of each.
4. **Advantages**: 4–5 bullets.
5. **Disadvantages**: 4–5 bullets.
6. **When to use / Application**: 2–3 bullets.
7. **Closing line**: summarising when the model is preferred.

A 15-mark answer needs ~2 full pages (400–500 words + diagram). A 10-mark answer needs ~1.5 pages (250–350 words + diagram).

### 3.5 Choice Strategy for Section B

In 2025, you must answer 2 of 3 (Q2a, Q2b, Q2c). In 2024, 3 of 4 (Q2a–d). The safest strategy is to **prepare 3 topics deeply + 1 topic lightly** so you always have a margin.

- **Strongly recommended trio**: (1) Process Models, (2) Requirements Engineering + SRS, (3) SCM + SQA.
- **Light backup**: Risk Management (for 1-mark or as a 10-mark replacement).

---

## 4. UNIT-I — Software Process Models & Requirements Engineering

### 4.1 Software & Software Engineering

#### 4.1.1 Definition of Software

**Software is more than just program code.** A *program* is an executable code that serves some computational purpose. **Software** is a collection of (i) executable programming code, (ii) associated libraries, and (iii) documentations. When software is made for a specific customer's requirement, it is called a **software product**.

Engineering, in general, is all about developing products using well-defined, scientific principles and methods.

#### 4.1.2 Software Engineering — Definition

**Software Engineering is an engineering branch associated with the development of a software product using well-defined scientific principles, methods and procedures.** The outcome is an efficient and reliable software product.

**IEEE definition:** *"Software engineering is the application of a systematic, disciplined, quantifiable approach to the development, operation and maintenance of software; that is, the application of engineering to software."*

It is also viewed as a **systematic collection of past experience** arranged in the form of methodologies and guidelines. Small programs can be written informally without SE principles, but for large software products these principles are absolutely necessary to achieve good quality software cost-effectively.

#### 4.1.3 Prime Objective of Software Engineering (Assignment Q1; 2024 PYQ Q1b)

To produce **efficient and reliable software products in a cost-effective manner** using systematic, disciplined and quantifiable methods — i.e., to deliver a quality product **within time and budget** that meets customer requirements.

#### 4.1.4 Software Engineering Paradigm (Assignment Q2)

A *software-engineering paradigm* is a chosen combination of **process model + methods + tools** used to develop software. Different paradigms suit different problem types — there is no single "best" paradigm.

#### 4.1.5 Need / Importance of Software Engineering (Assignment Q6)

The need arises because of the **high rate of change in user requirements and environment**:

- **Large software** — as size grows, engineering discipline is needed (just like building a wall vs. building a house — the latter needs an architect's blueprint).
- **Scalability** — without a scientific basis it is easier to re-create software than to scale an existing one.
- **Cost** — hardware has become cheap; software cost stays high if proper process is not followed.
- **Dynamic nature** — software must adapt continuously to changing environment; SE helps manage this.
- **Quality management** — better process ⇒ better-quality software product.

#### 4.1.6 Software Characteristics / Attributes (Assignment Q8)

A software product is judged on three grounds:

| Category | Attributes |
|----------|-----------|
| **Operational** (how well it works in operations) | budget, usability, efficiency, correctness, functionality, dependability, security, safety |
| **Transitional** (important when moved to another platform) | portability, interoperability, reusability, adaptability |
| **Maintenance** (capability to maintain in a changing environment) | modularity, maintainability, flexibility, scalability |

#### 4.1.7 Software Crisis (2024 PYQ — challenges in software)

It is often the case that software products: **fail to meet user requirements, are expensive, are difficult to alter/debug/enhance, are delivered late, and use resources non-optimally.**

**Standish Group Report**: only ~28% of projects are successful; ~49% are delayed or over cost; ~23% are cancelled.

**Factors contributing to the crisis:**
- Larger problems
- Poor project management
- Lack of adequate training in software engineering
- Increasing skill shortage
- Low productivity improvements

**Cost shift**: In 1960 hardware dominated cost; by 2018 software dominates (e.g., laptop ≈ ₹45,000 vs. Rational suite floating license ≈ ₹6,03,200). Despite this, software is preferred because it is **easier/faster to develop and change, and consumes no space, weight, or power**. But more complexity ⇒ harder to change ⇒ more changes ⇒ more complexity (vicious cycle).

**Symptoms of software crisis:**
- Late delivery of software
- Cost overruns
- Poor quality
- Unmaintainable code
- Cancelled projects
- Failure to meet user requirements

**Challenges in software (2024 Q1a):**
- Increasing size & complexity of software
- Changing user requirements
- Tight schedules & cost pressures
- Lack of trained personnel
- Difficulty in measuring/estimating software
- Difficulty in coordinating large teams
- Legacy systems needing maintenance

**Solutions offered by SE:** abstraction & decomposition, structured/standardised methods, process models, metrics, CASE tools, quality assurance, formal methods.

#### 4.1.8 Software Quality (2024 PYQ Q1e; 2025 Q1b "process in context of software quality")

**Bersoff's definition (Quality Assurance):** *"those procedures, techniques, and tools applied by professionals to ensure that a product meets or exceeds pre-specified standards during its development cycle."*

**Two angles of viewing quality:**
- **Customer's viewpoint** → meets specifications.
- **Developer's viewpoint** → easy to maintain, test, etc.

**Quality is not just meeting specifications & removing defects** — other quality attributes include: safety, security, reliability, resilience, robustness, understandability, testability, adaptability, modularity, complexity, portability, usability, reusability, efficiency, learnability.

**Critical quality attributes must be selected early** in development and planned for how to achieve them.

**Process in the context of software quality (2025 Q1b):**
A *process* is a set of activities, methods, practices and transformations used to develop and maintain software and associated products. In the context of software quality, the process defines *how* software is developed — and a well-defined process is the foundation of repeatable quality. Without a disciplined process, quality is left to chance.

---

### 4.2 Handling Complexity: Abstraction & Decomposition

#### 4.2.1 Why Complexity Matters

A small program (few variables) is within an individual's grasp. As the number of independent variables grows, it exceeds human cognitive limits — effort grows **exponentially** with size. The **exploratory (build-and-fix) style** breaks down for non-trivial projects: a "dirty" program is written, bugs are fixed as noticed; results in unmaintainable code and is unusable in team development.

#### 4.2.2 Abstraction

- **Definition**: Simplify a problem by **omitting irrelevant details**; focus on only one aspect and ignore the rest. Also called **model building**.
- **Why used**: To reduce the complexity a human must handle at any one time. (Example: use a map of a country instead of visiting every house; biological taxonomy: Kingdom→Phylum→Species instead of examining every organism.)
- **Hierarchy of abstractions**: For complex problems a *single* level of abstraction is inadequate; a *hierarchy of models* is built — each layer abstracts the layer below and is implemented by the layer above. Example: Architectural design → High-level design → Detailed design — each is an abstraction layer.

#### 4.2.3 Decomposition

- **Definition**: Divide a complex problem into many small independent parts; solve each separately; combine solutions.
- **Why used**: Each small part is easier to grasp and solve. A bundle of sticks is hard to break together but easy one-by-one. Book chapters (organised) vs. mixed-up text.
- **Constraint**: Arbitrary decomposition does **not** help — the parts must be **more or less independent**. If highly interrelated, complexity reduction is not realised.

#### 4.2.4 How They Help

Together, abstraction & decomposition "flatten" the exponential effort-vs-size curve to nearly **linear**, allowing large software to be developed by humans. They underpin every SE activity:

- SRS — black-box abstraction (specify *what*, not *how*).
- Design — architectural decomposition → detailed design.
- Coding — modules / functions.
- Testing — unit / integration / system.
- Maintenance — modular code is easier to fix.

---

### 4.3 Software Development Activities (Overview)

The **software life cycle** is a series of identifiable stages a software product undergoes during its lifetime. Major activities (any life cycle model contains them, possibly in different orders):

1. **Feasibility study** — determine whether the project is financially & technically worthwhile.
2. **Requirements analysis & specification** — understand exact customer requirements, document them in SRS.
3. **Design** — transform SRS into a structure suitable for implementation (architecture, high-level, detailed).
4. **Coding & unit testing** — translate design into source code; each module unit-tested.
5. **Integration & system testing** — integrate modules in a planned manner; α-test, β-test, acceptance test.
6. **Maintenance** — corrective (fix bugs), perfective (enhance), adaptive (port to new environment).

**Relative effort (typical):** maintenance ≈ 60% (max); among development phases, testing ≈ max. Development-to-maintenance effort ratio ≈ **40:60**.

**Project deliverables — myth vs. reality:** Myth = only the working program is the deliverable. Reality = documentation of all aspects is required for operation and maintenance.

---

### 4.4 Software Process / Process Models — Overview

#### 4.4.1 What is a Process?

A **process** is a **set of activities, methods, practices and transformations** used to develop and maintain software and associated products (Assignment Q5 — distinguish process vs. method: a *process* sequences and manages activities across the life cycle; a *method* provides techniques for performing one activity).

#### 4.4.2 What is a Process Model / Life Cycle Model / SDLC?

A software life cycle model (also called process model or SDLC) is a **descriptive and diagrammatic representation of the software life cycle**:
- Identifies all activities undertaken during product development.
- Establishes a precedence ordering among activities.
- Divides the life cycle into phases.
- Defines entry/exit criteria for every phase.
- A phase can start only when entry criteria are satisfied; it is complete only when exit criteria are met.

#### 4.4.3 Important Features of a Process (Assignment Q7)

- Defines activities and their ordering.
- Defines entry/exit criteria for each phase.
- Provides milestones for tracking progress.
- Enables systematic, disciplined development.
- Helps identify inconsistencies, redundancies, omissions.
- Helps tailor the process to specific projects.

#### 4.4.4 Why Needed?

Without a model, team members have no shared understanding of *when* to do *what* ⇒ chaos and project failure. Without entry/exit criteria and milestones, project managers fall prey to the **"99% complete syndrome"** — they cannot objectively track progress. A model provides requirements stability during development and facilitates strong management control (plan, staff, track).

#### 4.4.5 Software Process Activities (Generic — Sommerville)

1. **Software specification** — define functionality & constraints.
2. **Software development & design** — design & implement to meet spec.
3. **Software validation** — verify it does what customer wants.
4. **Software evolution** — evolve to meet changing needs.

#### 4.4.6 SEI Capability Maturity Model (CMM) (Assignment Q9; 2025 PYQ Q1d — "What is the use of CMM?")

**Use of CMM:** The CMM is intended to help a software organization **improve** its software development processes. Its focus is on **process improvement** — guiding organisations from ad-hoc, chaotic development to a measured, optimised, continuously-improving process.

**5 Levels of CMM:**

| Level | Name | Characteristic |
|-------|------|----------------|
| **1** | **Initial** (ad hoc) | No formal procedures, no cost estimates, no project plans, no management mechanism to ensure procedures are followed. |
| **2** | **Repeatable** (intuitive) | Basic project controls in place; intuitive methods used. |
| **3** | **Defined** (qualitative) | Development process is defined and institutionalised across the organisation. |
| **4** | **Managed** (quantitative) | Process is measured; a process database is established. |
| **5** | **Optimizing** | Improvement feedback data is used; rigorous defect-cause analysis and prevention. |

**Important notes:**
- A Level 1 organisation *can* still get ISO 9000 certification (certification is easy and can be a marketing ploy).
- A Level 2 organisation has significant advantage in obtaining ISO 9000 certification.
- A Level 3 organisation would have little difficulty in obtaining ISO 9000 certification.
- Even excellent developers (e.g., space-shuttle software) attain only around Level 3–4.

**People Capability Maturity Model (PCMM)** — improves knowledge and skills of people:
- L1 Initial — no training, staff talent not critical.
- L2 Repeatable — basic work practices; recruiting, growth, training to fill skill gaps.
- L3 Defined — tailor practices to organisation's business; skills-based compensation.
- L4 Managed — mentoring, team-building, quantitative competence goals.
- L5 Optimizing — best practices for team & individual improvement.

---

### 4.5 Classical Waterfall Model (2025 PYQ Q2a — 10 marks)

#### 4.5.1 Phases (in order)

1. Feasibility study
2. Requirements analysis & specification
3. Design
4. Coding & unit testing
5. Integration & system testing
6. Maintenance

#### 4.5.2 Schematic Diagram — How to Draw It

Draw a vertical stack of six rectangular boxes (top-to-bottom), one per phase, with downward arrows between them. Surround the stack with a large rounded-rectangle labelled **"Software Life Cycle"** along its left side, with sub-labels alongside each box: *Conceptualize / Specify / Design / Code / Test / Deliver / Maintain / Retire*.

```
┌─────────────────────────────────────┐
│  Software Life Cycle                │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  1. Feasibility Study       │    │
│  └──────────────┬──────────────┘    │
│                 ↓                   │
│  ┌─────────────────────────────┐    │
│  │ 2. Requirements Analysis    │    │
│  │    & Specification (SRS)    │    │
│  └──────────────┬──────────────┘    │
│                 ↓                   │
│  ┌─────────────────────────────┐    │
│  │ 3. Design                   │    │
│  └──────────────┬──────────────┘    │
│                 ↓                   │
│  ┌─────────────────────────────┐    │
│  │ 4. Coding & Unit Testing   │    │
│  └──────────────┬──────────────┘    │
│                 ↓                   │
│  ┌─────────────────────────────┐    │
│  │ 5. Integration & System     │    │
│  │    Testing                  │    │
│  └──────────────┬──────────────┘    │
│                 ↓                   │
│  ┌─────────────────────────────┐    │
│  │ 6. Maintenance              │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
```

#### 4.5.3 Activities in Each Phase

- **Feasibility study**: visit client, understand input/output data & processing needs; examine alternative solutions; perform **cost-benefit analysis (CBA)** covering development, set-up, operational costs vs. quantifiable & non-quantifiable benefits; check economic, technical & schedule feasibility; Go/No-Go decision; produce a *business case* (executive summary, project background, business opportunity, costs, benefits, risks).
- **Requirements analysis & specification**: requirements gathering (interviews, discussions with users/analysts) → analysis (remove inconsistencies, anomalies, incompleteness) → specification in SRS.
- **Design**: transform SRS into a structure suitable for implementation. Two approaches: traditional (structured analysis + structured design) and object-oriented.
- **Coding & unit testing**: each module coded and unit-tested (tested in isolation for efficient debugging) and documented.
- **Integration & system testing**: integrate modules in a planned, incremental manner; system testing comprises **α-testing** (by dev team), **β-testing** (by friendly customers), **acceptance testing** (by customer after delivery). Goal: ensure conformance to SRS.
- **Maintenance**: ~60% of total life-cycle effort. Three types — *corrective* (fix residual bugs), *perfective* (enhance functionality), *adaptive* (port to new environment).

#### 4.5.4 Advantages

- Simplest and most intuitive model; easy to understand and use, especially by inexperienced staff.
- Milestones (phase entry/exit) are well understood.
- Provides requirements stability during development.
- Facilitates strong management control (plan, staff, track).
- Good documentation produced; serves as reference for maintenance.

#### 4.5.5 Disadvantages / Shortcomings

- Idealistic: assumes **no defects are introduced** in any phase — impossible in practice.
- Defects are usually detected much later (e.g., design defect found in coding/testing); later detection ⇒ higher rework cost.
- **All requirements must be known up-front** — but ~40% of requirements change after project start (Capers Jones data on 8000 projects).
- Gives a false impression of progress (**99% complete syndrome**).
- Integration is one big bang at the end.
- Little opportunity for customer to preview the system.
- Cannot accommodate change requests during development.
- Heavy-weight process.

> **Frederick Brooks quote:** *"…the assumption that one can specify a satisfactory system in advance, get bids for its construction, have it built, and install it… this assumption is fundamentally wrong…"*

#### 4.5.6 When to Use

- Requirements are well known and stable.
- Technology is understood.
- Development team has experience with similar projects.

> **Important tip:** Even when an iterative/agile model is actually followed, **documents should reflect a classical waterfall structure** to facilitate comprehension (mathematical-proof analogy: present a clean deductive chain even if discovery was messy).

---

### 4.6 Iterative Waterfall Model (2024 PYQ Q2a — 15 marks)

#### 4.6.1 What it is / Why Iterative

Classical waterfall assumes no defects — but engineers commit errors in almost every phase. The iterative waterfall adds **feedback paths** so that when a defect is detected in a later phase, engineers can go back to the phase where it occurred and rework. The principle of detecting errors as close to their point of introduction as possible is called **phase containment of errors** — earlier detection ⇒ much cheaper correction.

#### 4.6.2 Diagram Description

Same vertical stack as classical waterfall (Feasibility → Requirements → Design → Coding → Testing → Maintenance), but with **upward feedback arrows** from each lower phase back to one or more previous phases (e.g., Testing → Design, Testing → Requirements, Coding → Design, Design → Requirements).

```
Feasibility  ←─────── Requirements
    ↓                   ↑
Requirements ←────── Design
    ↓                   ↑
   Design   ←────── Coding
    ↓                   ↑
   Coding   ←────── Integration & Testing
    ↓
   Maintenance
```

#### 4.6.3 Activities in Each Phase

Same activities as classical waterfall — the difference is the explicit feedback loop allowing rework. The first working model appears early. Each phase produces a deliverable (SRS, design document, code, test reports) that can be reviewed before moving on.

#### 4.6.4 Advantages

- Working model available at a very early stage ⇒ easier to find functional/design flaws early.
- Finding issues early enables corrective measures within limited budget.
- Most widely used model in practice (almost every other model is derived from it).
- Produces good documentation and reliable software.
- Simple to understand and use.

#### 4.6.5 Disadvantages

- Suitable **only for well-understood problems**.
- Not suitable for very large projects or for projects subject to many risks.
- Does not facilitate accommodating change requests during development.
- Applicable mainly to large and bulky software projects — hard to break a small system into serviceable increments.

#### 4.6.6 When to Use

- Requirements well understood and stable.
- Technology is mature.
- Team experienced with similar projects.
- Documentation quality & high reliability are important.

---

### 4.7 Prototyping Model (2024 PYQ Q2b-iii, Q1d)

#### 4.7.1 What is Software Prototyping? (2024 Q1d)

A **prototype** is a *toy implementation* of the system with **limited functional capabilities, low reliability, and inefficient performance**. It is usually built using several shortcuts (e.g., inefficient, inaccurate or dummy functions, table look-up instead of actual computation).

#### 4.7.2 Need for a Prototype

- Illustrate input data formats, messages, reports, interactive dialogues to customer.
- Gain better understanding of customer needs (UI behaviour, screen layouts, output formats).
- Impossible to get the product right the first time ⇒ plan to throw away the first version.
- Examine technical issues (response time of a hardware controller, efficiency of a sorting algorithm) — prototype may be the only way to resolve them.

#### 4.7.3 When to Use

- User requirements are not complete.
- Technical issues are not clear.
- Especially popular for user-interface development.

#### 4.7.4 Types of Prototypes

- **Throwaway prototype** (rapid/throwaway prototyping): built with shortcuts, used to clarify requirements, then discarded; experience guides actual development. The notes focus on this.
- **Evolutionary prototype**: prototype is refined iteratively into the final product (covered under Evolutionary Model — see §4.8).

#### 4.7.5 Diagram / Steps

1. Requirements gathering →
2. Quick design →
3. Build prototype →
4. Customer evaluation of prototype →
5. Refine requirements (loop back to step 2 if not satisfied) →
6. Customer satisfied? →
7. Implement (Design → Code → Test → Maintain) the actual system using the waterfall model.

```
  Requirements Gathering
            ↓
       Quick Design
            ↓
    Build Prototype  ←────┐
            ↓              │
   Customer Evaluation ────┘ (if not satisfied)
            ↓ (satisfied)
  Refine Requirements
            ↓
  Design → Code → Test → Maintain
```

After prototype approval, the requirements analysis & specification phase becomes *redundant* — the final working prototype serves as an *animated requirements specification*.

#### 4.7.6 Advantages

- Resulting software is usually **more usable**.
- User needs better accommodated.
- Design is of higher quality.
- Resulting software easier to maintain.
- Overall development cost usually **lower** for systems with unclear requirements or unresolved technical issues (avoids massive redesign costs of late change requests).

#### 4.7.7 Disadvantages

- For some projects it is **expensive**.
- Susceptible to **over-engineering** — designers add sophistications they couldn't put in the prototype.
- Prototype code is usually thrown away (wasted effort, though experience is gained).

---

### 4.8 Evolutionary Model

#### 4.8.1 Definition

Also called **successive versions model** or **incremental model**. A simple working version is built first; subsequently it undergoes functional improvements and new functions are added in successive versions till the desired system is built. Recognises the reality of changing requirements.

#### 4.8.2 Steps

1. Develop **core modules** of the software first.
2. Build an **initial skeletal version**.
3. Refine into increasing levels of capability (iterations).
4. Each iteration: develop → validate → integrate → validate system → deliver.
5. Add new functionality (or enhance existing) in successive versions.
6. Multiple versions until the final version.
7. Each iteration is a short mini-project (often a mini-waterfall), 2–6 weeks long; many iterations (e.g., 10–15) typical.

#### 4.8.3 Diagram Description

A timeline: *Initial rough requirements → Initial specification → Initial version → Development → Intermediate versions (multiple) → Validation → Final version*. An iterative loop overlays development/validation to show the increments.

```
Initial Requirements → Initial Spec → V1 (core) → V2 (+features) → V3 (+features) → … → Vn (final)
                          ↑                              │
                          └────────── Feedback ──────────┘
```

#### 4.8.4 Applications

- Large projects where modules can be identified for incremental implementation.
- Customers want to start using core features rather than wait for full software.
- Object-oriented development (system can be partitioned into object units).
- Foundation of agile techniques; basis for Rational Unified Process (RUP) and Extreme Programming.

#### 4.8.5 Advantages

- Users get a chance to experiment with partially developed system early.
- Helps find exact user requirements ⇒ software more likely to meet them.
- Core modules tested thoroughly ⇒ fewer errors in final delivery.
- Better management of complexity (develop one increment at a time).
- Better management of changing requirements.
- Customer feedback incorporated efficiently.
- Training can start on an earlier release.
- Frequent releases allow quick fixing of unanticipated problems.
- Customer trauma of adopting an entirely new system is reduced (gradual introduction).
- No large upfront capital outlay.

#### 4.8.6 Disadvantages / Problems

- Process is **intangible** — no regular, well-defined deliverables.
- Process is **unpredictable** — hard to manage (scheduling, workforce allocation).
- Systems are **poorly structured** — continual changes degrade software structure.
- Systems **may not converge** to a final version.
- Difficult to divide the problem into several versions acceptable to the customer that can be incrementally implemented and delivered.

---

### 4.9 Spiral Model (2024 PYQ Q2a; 2025 PYQ Q1c — "List the task regions")

#### 4.9.1 Definition / Who Proposed

Proposed by **Barry Boehm in 1988**. The diagram looks like a **spiral with many loops**; the exact number of loops is not fixed. Each loop = a phase of the software process (innermost ≈ feasibility, next ≈ requirements, next ≈ design, etc.). There are no fixed phases; the team decides how to structure the project into phases.

#### 4.9.2 Task Regions / Quadrants (CRITICAL — 2025 Q1c asks to "List" them)

Each loop is split into **four sectors (quadrants)**:

| Quadrant | Name | Activities |
|----------|------|-----------|
| **1st** | **Objective Setting** | Identify the objectives of the phase; examine the risks associated with these objectives; find alternative solutions possible. |
| **2nd** | **Risk Assessment and Reduction** | Detailed analysis of each identified project risk; steps are taken to reduce the risk. Example: if there is a risk that requirements are inappropriate, a prototype may be developed. |
| **3rd** | **Development and Validation** | Develop and validate the next level of the product after resolving risks. |
| **4th** | **Review and Planning** | Review results achieved so far with the customer; plan the next iteration around the spiral. Progressively more complete version of software gets built with each iteration. |

**Definition of risk** (used in Spiral): *"any adverse circumstance that might hamper successful completion of a software project."*

#### 4.9.3 Diagram Description — How to Draw

Draw a spiral originating at the centre and unwinding outward (like a snail shell). Divide it into 4 quadrants using two perpendicular axes (one horizontal, one vertical). Label the four quadrants clockwise from top-right:
- **Top-right (Q1):** Objective Setting
- **Bottom-right (Q2):** Risk Assessment & Reduction
- **Bottom-left (Q3):** Development & Validation
- **Top-left (Q4):** Review & Planning

As the spiral moves outward, the **radius = cumulative cost** and the **angle = progress through the quadrant**.

```
                 Q1: Objective Setting
                         │
            ┌────────────┼────────────┐
            │      /     │     \      │
            │    /       │       \    │  ← spiral grows outward
            │  /         │         \  │     (radius = cost)
            │/           │           \│
   ─────────┼────────────┼────────────┼─────────
            │\           │           /│
            │  \         │         /  │
            │    \       │       /    │
            │      \     │     /      │
            └────────────┼────────────┘
   Q3: Development        │      Q2: Risk Assessment
   & Validation           │      & Reduction
                         │
                  Q4: Review & Planning
```

#### 4.9.4 Spiral Model as a Meta-Model

The spiral model **subsumes all other models**:
- A single-loop spiral represents the **waterfall model**.
- An evolutionary approach over multiple loops represents the **evolutionary model**.
- Uses **prototyping** as a risk-reduction mechanism.
- Retains the step-wise approach of the waterfall model.

**Risk handling is inherently built in** — this is its distinguishing feature. The model enables understanding and reacting to risks during each iteration.

#### 4.9.5 Advantages

- Best for **technically challenging** software products prone to **several kinds of risks**.
- Risk-driven — risks are explicitly identified and reduced each iteration.
- Combines best features of waterfall + prototyping + evolutionary.
- Customer review at the end of each loop ensures feedback.

#### 4.9.6 Disadvantages

- Much **more complex** than other models — deters its use in ordinary projects.
- Requires **risk-assessment expertise** — if team is not experienced, the model degenerates into something else.
- Number of loops is not fixed — hard to plan and schedule.
- Heavy management overhead.

#### 4.9.7 When to Use

- Technically challenging, large-scale projects with many uncertainties and risks.
- Projects where requirements are expected to change.
- Long-lived projects that need continuous risk management.

---

### 4.10 RAD Model — Rapid Application Development (2024 PYQ Q2b-ii)

#### 4.10.1 Definition / Full Form

RAD = **Rapid Application Development**; sometimes called the *rapid prototyping model*.

**Major aims:**
- Decrease the time taken and cost incurred to develop software.
- Facilitate accommodating change requests as early as possible — before large investments have been made in development and testing.

#### 4.10.2 Underlying Principle

To reduce development time & cost yet stay flexible: **make only short-term plans and make heavy reuse of existing code**.

#### 4.10.3 Methodology / Phases

1. Plans are made **one increment at a time** — the time planned for each iteration is called a **time box**.
2. Each iteration enhances the implemented functionality a little.
3. During each iteration:
   - Develop a **quick-and-dirty prototype** for selected functionality.
   - Customer evaluates the prototype and gives feedback.
   - Prototype is refined based on feedback.
   - The prototype **evolves into deliverable software** (unlike throwaway prototyping).
4. Fast creation of working prototypes is achieved through **specialised tools** supporting:
   - Visual style of development
   - Reusable components
   - Standard APIs (Application Program Interfaces)

#### 4.10.4 Diagram Description

Sequence of time-boxes (iterations). Each iteration cycle: *Identify increment → Quick design → Build prototype → Customer evaluation → Refine → Integrate into deliverable*. The prototype is NOT thrown away — it becomes part of the final product.

```
  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
  │  Time Box 1     │  │  Time Box 2     │  │  Time Box 3     │
  │  ─────────      │  │  ─────────      │  │  ─────────      │
  │  Identify       │  │  Identify       │  │  Identify       │
  │  Quick Design   │  │  Quick Design   │  │  Quick Design   │
  │  Build Prototype│  │  Build Prototype│  │  Build Prototype│
  │  Customer Eval  │  │  Customer Eval  │  │  Customer Eval  │
  │  Refine         │  │  Refine         │  │  Refine         │
  └────────┬────────┘  └────────┬────────┘  └────────┬────────┘
           │                    │                    │
           └─────── Final Integrated Product ────────┘
```

#### 4.10.5 RAD vs Prototyping vs Evolutionary vs Iterative Waterfall

| Aspect | Prototyping | RAD | Evolutionary | Iterative Waterfall |
|--------|-------------|-----|--------------|---------------------|
| Prototype disposed? | Yes (throwaway) | No — evolves into product | No — incremental versions | No prototype |
| Increment size | N/A | Small/short | Medium-large | Whole system |
| Quality | High (final build) | Possibly poorer | High (waterfall per increment) | High |
| Documentation | Good | Lighter | Medium | Best |
| Reuse of code | No | Heavy | Light | No |

#### 4.10.6 Advantages

- Dramatically reduced development time.
- Reduced cost.
- Easy accommodation of change requests.
- Heavy reuse of components.

#### 4.10.7 Disadvantages

- Quality & reliability possibly poorer.
- Requires specialised visual development tools & reusable components.
- Not suitable when performance/reliability is critical or system cannot be modularised.
- Project becomes tied to specific tools/vendors.

#### 4.10.8 When to Use

- Quick time-to-market dominates.
- Custom software for a small number of users.
- Modular system; reusable components readily available.
- Performance & reliability not critical.

---

### 4.11 Agile Models

#### 4.11.1 Why Agile

Proposed mid-1990s to overcome waterfall's shortcomings, **primarily to help projects adapt to change requests**. Requirements are decomposed into many small incremental parts developed over **1–4 weeks each**.

#### 4.11.2 Agile Manifesto — 4 Values

1. **Individuals and interactions** over processes and tools.
2. **Working software** over comprehensive documentation.
3. **Customer collaboration** over contract negotiation.
4. **Responding to change** over following a plan.

(That is, while there is value in the items on the right, the items on the **left are valued more**.)

#### 4.11.3 Agile Methodologies (List)

- **XP** (Extreme Programming)
- **Scrum**
- **Unified Process / RUP**
- **Crystal**
- **DSDM**
- **Lean**

#### 4.11.4 Agile Principal Techniques

- **User stories** — simpler than use cases; short descriptions of a feature from the user's perspective.
- **Metaphors** — based on user stories, developers propose a common vision of what is required.
- **Spike** — a small, simple program to explore potential solutions.
- **Refactor** — restructure code without affecting behaviour to improve efficiency, structure, etc.

#### 4.11.5 Agile Nitty-Gritty

- At any time, **only one increment** is planned, developed, deployed at the customer site. No long-term plans are made.
- An iteration may not add significant functionality, but a new release is invariably made at the end of each iteration and delivered to the customer for regular use.

#### 4.11.6 Methodology / Principles

- **Face-to-face communication** favoured over written documents.
- Development team shares a single office space.
- Team size deliberately kept small (**5–9 people**) — most suited to small projects.
- Effectiveness ranking (Cockburn/Ambler): face-to-face at whiteboard > face-to-face conversation > video conversation > phone > videotape > email > audiotape > paper documentation. Richer channels are more effective.
- **Primary measure of progress**: incremental release of working software.
- Frequent delivery — once every few weeks.
- Change requests easily accommodated.
- Close cooperation between customers and developers.

#### 4.11.7 Extreme Programming (XP) 📚

> 📚 Detailed XP coverage is **not in the professor's notes** — supplemented from standard SE textbooks (Pressman / Rajib Mall).

**Definition:** XP is an agile software development methodology designed to deliver high-quality software quickly through disciplined engineering practices, frequent releases, and close customer collaboration. Created by **Kent Beck** in the late 1990s.

**5 Values of XP:**
1. **Communication** — team & customer talk constantly, face-to-face.
2. **Simplicity** — do the simplest thing that could possibly work.
3. **Feedback** — continuous feedback from tests, customer, and team.
4. **Courage** — willing to throw away code, refactor, tell the truth.
5. **Respect** — every member's contribution is valued.

**12 Practices of XP:**
1. **Planning Game** — short releases, frequent iteration planning.
2. **Small Releases** — deploy often (daily/weekly).
3. **Metaphor** — simple shared story of how the system works.
4. **Simple Design** — no premature optimisation; design for today.
5. **Test-Driven Development (TDD)** — write tests before code (Red-Green-Refactor).
6. **Refactoring** — continuously improve code structure.
7. **Pair Programming** — two programmers at one workstation (driver + navigator).
8. **Collective Ownership** — anyone can change any code.
9. **Continuous Integration** — integrate & build multiple times a day.
10. **40-hour Week** — sustainable pace; no burnout.
11. **On-site Customer** — customer available full-time with the team.
12. **Coding Standards** — all code follows common conventions.

**XP Process Flow:** User stories → Release planning → Iteration (1–3 weeks) → TDD + Pair programming → Continuous integration → Small release → Customer feedback → Next iteration.

#### 4.11.8 Scrum 📚

> 📚 Detailed Scrum coverage is **not in the professor's notes** — supplemented from standard SE textbooks.

**Definition:** Scrum is an iterative & incremental agile framework for managing product development, based on **empirical process control** (transparency, inspection, adaptation). Originated in software but applicable to any complex product.

**3 Roles:**
1. **Product Owner (PO)** — represents the customer/stakeholders; owns the Product Backlog; prioritises items by business value.
2. **Scrum Master (SM)** — facilitator/coach; ensures Scrum is understood & enacted; removes impediments; NOT a project manager.
3. **Development Team** — self-organising, cross-functional, 3–9 members; builds the increment.

**3 Artifacts:**
1. **Product Backlog** — prioritised list of all desired features (User Stories) for the product; maintained by PO.
2. **Sprint Backlog** — subset of Product Backlog items selected for the current sprint + plan for delivering them.
3. **Increment / Potentially Shippable Product** — the sum of all completed backlog items across sprints; must meet Definition of Done (DoD).

**5 Events / Ceremonies:**
1. **Sprint** — the container event; time-box of 2–4 weeks; no changes that would endanger the Sprint Goal.
2. **Sprint Planning** — at the start of a sprint (~8 hours max for a 4-week sprint); team selects backlog items & makes a plan.
3. **Daily Scrum (Stand-up)** — 15-minute daily sync; 3 questions — what did I do yesterday? what will I do today? are there impediments?
4. **Sprint Review** — at the end of the sprint; team demos the increment to stakeholders; feedback gathered.
5. **Sprint Retrospective** — after review; team reflects on the sprint (what went well, what didn't, what to improve); continuous improvement.

**Scrum Process Flow:**
```
Product Backlog (PO) → Sprint Planning → Sprint Backlog
                                              ↓
                                ┌───────── Sprint (2–4 wks) ─────────┐
                                │   Daily Scrum (15 min)            │
                                │   Development work                │
                                │   (self-organising team)         │
                                └───────────────┬───────────────────┘
                                                ↓
                                Increment → Sprint Review (demo)
                                                ↓
                                       Sprint Retrospective
                                                ↓
                                       Updated Product Backlog
                                                ↓
                                       Next Sprint...
```

**Advantages of Scrum:**
- Frequent, working software.
- Adapts to changing requirements.
- Customer feedback loop is short.
- High team morale (self-organising).
- Transparency & visibility.

**Disadvantages of Scrum:**
- Daily meetings can become tedious.
- Requires disciplined, experienced team.
- Not suitable for very large teams without scaling (Nexus, SAFe).
- Scope creep risk if PO not strong.

#### 4.11.9 Advantages of Agile (General)

- Customer satisfaction via early & continuous delivery of working software.
- Welcome changing requirements, even late in development.
- Working software delivered frequently (weeks rather than months).
- Close, daily cooperation between business people and developers.
- Projects built around motivated individuals; trust them.
- Face-to-face conversation is the most efficient form of communication.
- Sustainable development pace.
- Continuous attention to technical excellence & good design enhances agility.
- Simplicity — art of maximising work not done — is essential.
- Self-organising teams produce best architectures, requirements, designs.
- Regular reflection & tuning.

#### 4.11.10 Disadvantages of Agile

- Difficult to scale to large projects/teams.
- Requires highly disciplined, motivated, co-located team.
- Light documentation ⇒ hard to maintain long-term or hand over.
- Easy to lose sight of overall product vision.
- Customer must be available & committed throughout.
- Not suitable for safety-critical or high-reliability systems requiring heavy up-front design.

---

### 4.12 Requirements Engineering (2024 Q2c; 2025 Q2b)

#### 4.12.1 Definition

Requirements engineering is the process of **establishing the services the customer requires** from a system and the **constraints** under which it operates and is developed. Conducted by experienced team members called **system analysts**.

#### 4.12.2 Requirements Engineering Process — Activities (2025 Q2b — "Explain RE processes with suitable diagram")

The RE process consists of the following sequential activities (each producing a defined output):

1. **Feasibility Study** — financial & technical feasibility of the project (covered in §4.5.3 above).
2. **Requirements Gathering** — collect relevant data from customer (interviews, discussions, observation, questionnaires, studying existing documents).
3. **Requirements Analysis & Specification** — analyse gathered requirements to remove inconsistencies, anomalies, incompleteness; resolve through further discussions; then organise systematically into the SRS document.
4. **SRS Review / Requirements Validation** — review SRS for correctness, completeness, consistency, etc. Customer's approval is the **exit criterion** for the requirements phase.
5. (Subsequent phases) — Design, Coding, Testing, Maintenance.

#### 4.12.3 Diagram — How to Draw RE Process

```
  Feasibility Study
         ↓
  Requirements Gathering  ←──────────┐
         ↓                            │
  Requirements Analysis & Specification (SRS)
         ↓                            │
       SRS Review  ───────────────────┘ (if changes needed)
         ↓ (approved)
       Design
         ↓
       Coding, Testing, Maintenance...
```

#### 4.12.4 Functional vs Non-Functional Requirements

- **Functional requirements** — describe the *functionalities* required from the system. The system performs a set of high-level functions {f_i}; each function transforms a set of input data (i_i) to a corresponding set of output data (o_i). Example: library system *Search Book* — Input: author name; Output: book details + library location.
- **Non-functional requirements** — deal with characteristics that cannot be expressed as functions — maintainability, portability, usability, reliability, performance, security, etc.
- **Goals of implementation** — general suggestions regarding development (future revisions, new devices to support, reusability issues) that guide trade-offs among design goals but are not immediate requirements.

#### 4.12.5 Requirements Gathering Techniques

- **Interviews** (structured & unstructured) with users and stakeholders.
- **Discussions** with end-users and customers.
- **Questionnaires** (mentioned in syllabus).
- **Observation / on-site visits** (e.g., manager visits the client's main office).
- Studying existing documents, manuals, current system.
- **Prototyping** to elicit clearer requirements.
- Sample dialogues and use-case scenarios.

#### 4.12.6 Requirements Specification — SRS Document

After all ambiguities, inconsistencies and incompleteness are resolved, requirements are systematically organised into the **Software Requirements Specification (SRS) document**. Important components:
- Functional requirements
- Non-functional requirements
- Goals of implementation

#### 4.12.7 SRS Review (2024 Q1c)

Once drafted, the SRS is reviewed by the customer and the development team. The customer's approval is the **exit criterion** for the requirements phase. SRS review checks for: correctness, completeness, consistency, ambiguity, verifiability, modifiability, traceability.

#### 4.12.8 Desirable Characteristics of a Good SRS Document (2024 Q2c)

1. **Concise** — and at the same time unambiguous, consistent, complete. Verbose & irrelevant descriptions reduce readability and increase error possibilities.
2. **Structured** — well-structured ⇒ easy to understand and modify (SRS undergoes several revisions).
3. **Black-box view** — specify *what* the system should do, not *how*; treat the system as a black box (hence SRS is also called *black-box specification*). Specify externally visible behaviour only.
4. **Conceptual integrity** — reader can easily understand.
5. **Response to undesired events** — characterise acceptable responses to exceptional conditions.
6. **Verifiable** — every requirement must be such that it can be determined whether or not it has been met in an implementation.

(Other commonly listed characteristics include **correctness, consistency, completeness, modifiability, traceability** — all covered above.)

#### 4.12.9 Problems Without an SRS Document

- System would not be implemented according to customer needs.
- Developers would not know whether what they are developing is what is required.
- Maintenance engineers would find it very difficult to understand functionality.
- User-document writers cannot write proper user manuals.

#### 4.12.10 Problems With an Unstructured Specification

- Difficult to understand.
- Difficult to modify.
- Conceptual integrity not shown.
- May be ambiguous and inconsistent.

#### 4.12.11 Example Structure of an SRS (ATM Withdraw-Cash)

Functional requirements documented as numbered items (R1, R1.1, R1.2, …) each specifying Input / Output / Processing:

- **R1: Withdraw Cash** — determines account type & number; checks balance; if sufficient, dispenses cash, else error.
  - **R1.1: Select withdraw amount option** — Input: "withdraw amount" option; Output: prompt for account type.
  - **R1.2: Select account type** — Input: user option; Output: prompt to enter amount.
  - **R1.3: Get required amount** — Input: amount (integer, multiples of 100, between 100 and 10,000); Output: cash + printed transaction statement; Processing: debit if balance sufficient, else error.

#### 4.12.12 Decision Tree

A **decision tree** is a graphic view of processing logic in decision-making and the corresponding actions. Edges represent conditions; leaf nodes represent actions.

Example: Library Membership Automation Software (LMS) with three options — New member / Renewal / Cancel membership. Each option has a Decision (what is checked) and an Action (what is done). The tree branches on the chosen option, then on validity checks, terminating in the action.

```
                    ┌─ Valid form? ── Yes ── Create new member
   New Member ──────┤
                    └─ Valid form? ── No ── Show error
   Renewal   ───────...
   Cancel    ───────...
```

#### 4.12.13 Decision Table

A **decision table** represents complex processing logic in **tabular/matrix form**. Upper rows specify conditions to be evaluated; lower rows specify actions to be taken when conditions are satisfied. A column = a **rule** — if condition true, execute corresponding action. Useful when many conditions combine; LMS can be represented as a decision table mapping valid/invalid selection × option type to action.

| Condition \ Rule | R1 | R2 | R3 | R4 | R5 | R6 |
|------------------|----|----|----|----|----|----|
| Option = New      | Y  | Y  | N  | N  | N  | N  |
| Option = Renewal | N  | N  | Y  | Y  | N  | N  |
| Option = Cancel  | N  | N  | N  | N  | Y  | Y  |
| Form valid       | Y  | N  | Y  | N  | Y  | N  |
| **Action**        | Create | Show error | Renew | Show error | Cancel | Show error |

#### 4.12.14 Verification & Validation (V&V) 📚

> 📚 Noted in Assignment Q10 & Q15; not elaborated in professor's notes — supplemented from standard textbooks.

- **Verification** — *"Are we building the product right?"* — checks whether the software meets its specification. Done via **reviews, walkthroughs, inspections** (static techniques) at each phase. Example: design review, code walkthrough.
- **Validation** — *"Are we building the right product?"* — checks whether the software meets customer's actual needs. Done via **testing** (dynamic techniques) on running code. Example: system testing, acceptance testing.

| Aspect | Verification | Validation |
|--------|--------------|------------|
| Question | Building the product right? | Building the right product? |
| Basis | Specification | Customer needs |
| Technique | Static (reviews) | Dynamic (testing) |
| When | Each phase | After development |
| Defect type caught | Process/deviation defects | Product/requirement defects |

---

## 5. UNIT-II — Umbrella Activities

### 5.1 Software Configuration Management (SCM) (2024 Q2d; 2025 Q2c)

#### 5.1.1 Definition

SCM is an **activity executed throughout the system life cycle to control change of products and life-cycle artifacts**. To what do we want to control changes? — *plans, specifications, procedures, programs, documents/manuals, data*.

A **configuration item (CI)** is *an artifact to which we want to control changes*.

#### 5.1.2 Need / Why SCM

- Software is constantly changed (corrective, perfective, adaptive).
- Without control, change = chaos; uncontrolled change rapidly leads to chaos.
- Need integrity, security, traceability of changes.
- Need to communicate change status to all stakeholders.

#### 5.1.3 SCM Process & Activities

The SCM activities are depicted as four sequential activities with feedback and reporting:

1. **Identify** (Configuration Identification)
2. **Control** (Configuration Control — baselines, change control)
3. **Audit** (Configuration Audit)
4. **Report / Support** (Status Reporting + Library support)

These are supported by a **software library** (database) that stores, manages and tracks configuration items.

#### 5.1.4 Two Principal Activities of SCM (CRITICAL — 2025 Q2c)

This is the most-asked sub-question on SCM. Memorise these two verbatim:

##### (a) Configuration Identification

Each configuration item must be **identified and described** with metadata:
- A unique name
- Configuration item type
- Project identifier
- Change and/or version information
- Resources the CI provides or requires
- Pointer to the actual configuration item

Configuration items must be **organised** — relationships between CIs defined (e.g., object diagram `<part-of>` domain model; domain model `<related-to>` use-case model).

Define and construct a **software library (database)** that stores, manages and tracks configuration items.

##### (b) Configuration Control

Concerned with managing changes to CIs after they have been baselined. Implements baselines, version control and change control (see below).

#### 5.1.5 Configuration Audit

- **Audit ensures that changes have been properly implemented.**
- Have the proper steps and procedures been followed? — checked via a checklist.
- Usually done by the Quality Assurance (QA) group if SCM is a formal activity.

#### 5.1.6 Version Control

- A CI usually **evolves** throughout the SE process — it will have several versions.
- An **evolution graph** describes a CI's change history.
- **Version** — configuration item k is obtained by modifying configuration item i; usually result of bug fixes / enhanced functionality; item k supersedes item i; created in linear order.
- **Branch** — a concurrent development path requiring independent configuration management.
- **Variant** — different configurations that are intended to coexist; e.g., Oracle for Windows vs. Oracle for Linux.

#### 5.1.7 Baseline

A **baseline** is a *time/phase in software development (usually a project milestone) after which any changes must be formalised* (e.g., go through a formal change-control procedure).

- A CI must first **pass a set of formal review procedures** (formal code review, documentation review, etc.) to become a baseline.
- It then becomes part of the project software library.
- After baselining, a **"check-out" procedure** is applied to the item — access to and change of the CI is controlled.
- Any modified CI must again go through formal review before it can replace the original baselined item.

#### 5.1.8 Change Control / Change Management Process

1. **STOP** — change request is submitted by users/developers.
2. **Change Control Authority (CCA)** evaluates, decides, and issues an **Engineering Change Order (ECO)** if approved.
3. The configuration item is **checked-out**, changed, **checked-in** after SQA, controlled and versioned.
4. The configuration item is **made available for use** (promotion; release).

Uncontrolled change rapidly leads to chaos — hence the formal flow.

```
  Change Request ──→ CCA ──→ Approved? ── No ──→ Rejected
                              │
                            Yes
                              ↓
                       Check-out CI
                              ↓
                          Modify CI
                              ↓
                          SQA review
                              ↓
                       Check-in CI (new version)
                              ↓
                          Promotion/Release
```

#### 5.1.9 SCM Status Reporting

- Keeps all parties informed and up-to-date on the status of a change.
- Communication mechanism among project members.
- Can determine **who made what changes, when, and why**.

#### 5.1.10 SCM Support — Software Library

A software library provides facilities to **store, label, identify versions, and track the status** of configuration items.

- Used by a **single developer** in their everyday workspace — *check-in / check-out*.
- Used by **other developers** via a *master directory* — tracks **promotions** after SQA.
- Used by **users** — a *software repository* tracks **releases**.

#### 5.1.11 SCM Tools & Automation

- **Version control systems** (RCS, SCCS, CVS, Subversion, Git) — implement check-in/check-out, branching, merging, release tagging.
- **Build tools** (Make, Ant, Maven) — automate compilation/integration.
- **Defect-tracking tools** (Bugzilla, Jira) — automate change requests.
- **Repository / library management tools** — automate baselining & status reporting.

#### 5.1.12 Metrics in SCM

- Number of change requests received / approved / rejected.
- Number of versions / branches / variants per CI.
- Time to process a change request (lead time).
- Defect injection & removal rates per baseline.
- **Software Maturity Index (SMI)** — measures product stability; as SMI → 1, the product stabilises (range 0–1). Defined in IEEE Std 982.1-1988.
- **Design Structure Quality Index (DSQI)** — also 0–1, compares with past designs; low DSQI ⇒ further design work/review needed.

#### 5.1.13 SCM Benefits

- Reduces effort to manage and effect change ⇒ improved productivity.
- Better software integrity and security ⇒ increased quality.
- Generates information about the process ⇒ enhanced management control.
- Maintains a software development database ⇒ better record keeping and tracking.

---

### 5.2 Software Quality Assurance (SQA) (2024 Q2d; Q1e)

#### 5.2.1 Definition

**Bersoff's definition (Quality Assurance):** *"those procedures, techniques, and tools applied by professionals to ensure that a product meets or exceeds pre-specified standards during its development cycle."*

- Essential activity for any business producing products used by others.
- Must be planned and systematic (does not just happen).
- Must be built into the development process (a natural outcome of software engineering).
- Continuous improvement is the overall goal.

#### 5.2.2 SQA as an Umbrella Activity

SQA encompasses (umbrella over):
- **Methods and tools**
- **Formal technical reviews (FTR)**
- **Testing**
- **Standards and procedures**
- **Software configuration management**
- **Quality metrics and measurement**

#### 5.2.3 Quality Control (QC) vs Quality Assurance (QA) — IMPORTANT

| Aspect | Quality Control (QC) | Quality Assurance (QA) |
|--------|----------------------|------------------------|
| Orientation | **Product-oriented** | **Process-oriented** |
| Goal | Find defects in finished product | Prevent defects by improving process |
| Approach | Reactive — inspects & tests | Proactive — defines & audits process |
| When | After development (testing) | Throughout development |
| Example | Test runs, inspections of finished code | Process audits, standards reviews |

**QA aims to *prevent* defects; QC aims to *find* defects.**

#### 5.2.4 Principles of SQA

1. We have a set of **standards and quality attributes** a software product must meet → there is a goal.
2. We can **measure** the quality of a software product → determine conformance to standards. *(key point)*
3. We **track** the values of the quality attributes → assess how well we are doing.
4. We **use the information** about software quality to improve the quality of future products → feedback into the development process.

#### 5.2.5 Why SQA Activities Pay Off — Cost of Defects Across Life Cycle

Cost to find & fix a defect grows **exponentially** across the life cycle (log scale):

| Phase | Relative Cost to Fix |
|-------|---------------------|
| Requirements | 1.00× |
| Design | 1.30×–2.00× |
| Code | 4.00× |
| Test | 10× |
| System test | 13× |
| Field use | 80–130× |

SQA pays off because defects are *cheap to fix* in early phases. Requirements, analysis and design phases introduce **50–60% of all defects**; **Formal Technical Reviews can uncover ~75% of these**.

#### 5.2.6 Software Quality — How Measured (2024 Q1e)

- **Customer's viewpoint** → meets specifications.
- **Developer's viewpoint** → easy to maintain, test, etc.
- Quality is **not just meeting specifications & removing defects** — other attributes: safety, security, reliability, resilience, robustness, understandability, testability, adaptability, modularity, complexity, portability, usability, reusability, efficiency, learnability.
- Critical quality attributes must be selected *early* and planned for.

#### 5.2.7 Software Standards

Why important:
1. Encapsulate **best practices** (acquired through trial & error) → avoids previous mistakes.
2. Provide a **framework** around which to implement the SQA process → ensures best practices are followed.
3. Assist in ensuring **continuity** of project work → reduces learning effort when starting new work.

Two types:
- **Product standards** — define characteristics all product artifacts should exhibit.
- **Process standards** — define how the software process should be conducted.

#### 5.2.8 SQA Activities

- Defining standards and quality attributes.
- Measuring product & process quality (metrics).
- Performing **Formal Technical Reviews (FTR) / walkthroughs** at each phase — requirements walkthroughs, analysis walkthroughs, design walkthroughs, code walkthroughs, test-plan review.
- **Software testing**.
- **Software Configuration Management**.
- **Audits**.
- Collecting & analysing metrics.
- **Statistical Quality Assurance (SQA)** — categorise & determine cause of defects; **80-20 rule**: 80% of defects trace to 20% of causes; isolate & correct that 20%.
- **Formal / clean-room approaches** — proving programs/specifications correct; the **Cleanroom process** combines formal proof + statistical QA.

#### 5.2.9 SQA Tools

- Review checklists, inspection forms.
- Static analysers (cyclomatic-complexity, fan-in/fan-out, length-of-identifiers, depth-of-nesting).
- Test harnesses & coverage analysers.
- Defect-tracking systems.
- Configuration management / version control systems.

#### 5.2.10 Measures of SQA Success

- **Defect density** (defects per KLOC).
- **Defect removal efficiency (DRE)** = defects found internally ÷ (defects found internally + found by customer after delivery).
- **Mean time to failure (MTTF)**.
- Review effectiveness (defects found per review hour).
- Coverage of reviews (~75% of defects can be uncovered by FTR).

#### 5.2.11 Software Reviews / Audits

**Reviews are the principal method of validating the quality of a project.** Schedule of reviews:

- Requirements capture → *requirements walkthroughs* → *analysis walkthroughs*
- Analysis → *design walkthroughs*
- Design → *code walkthroughs*
- Implementation → *test plan review*

Reviews lead to **early discovery of defects**.

#### 5.2.12 Software Metrics

- **metric** — any type of measurement relating to a software system, process or artifact.
- **Control metrics** — used to plan, manage and control the development process (effort, elapsed time, disk usage).
- **Predictor metrics** — used to predict an associated product quality (e.g., cyclomatic complexity predicts ease of maintenance).
  - **External attribute** — discovered only after software is in use (maintainability, reliability, portability, usability).
  - **Internal attribute** — measurable directly from software (cyclomatic complexity, lines of code, # parameters, # error messages, length of user manual).
- Goal: **use internal attributes to predict external attributes**.

#### 5.2.13 Product Quality: Design Quality Metrics

Key attribute = **maintainability**, related to cohesion, coupling, understandability, adaptability — most cannot be measured directly; we infer them from **complexity**:

- **Structural fan-in / fan-out**
  - fan-in = # calls to a component by other components.
  - fan-out = # components called by a component.
  - High fan-in ⇒ high coupling. High fan-out ⇒ calling component has high complexity.
- **Informational fan-in / fan-out** — also considers parameters passed & shared data:
  - **complexity = component-length × (fan-in × fan-out)²** (validated on Unix system; predicts implementation effort).
- **IEEE Standard 982.1-1988** — looks at subsystem properties (number of subsystems, degree of coupling) and database properties (number of attributes & classes); computes **Design Structure Quality Index (DSQI)** in 0–1; compared with past designs.
- **Software Maturity Index (SMI)** — measures stability across releases; as SMI → 1, the product stabilises.

#### 5.2.14 Product Quality: Program Quality Metrics

For implementation components key attributes = **reliability** and **difficulty of implementation**:

- **Halstead's Software Science**
  - n1 = # unique operators; n2 = # unique operands
  - N1 = total # operators; N2 = total # operands
  - L = N1 + N2 (component length)
  - **V = L × log₂(n1 + n2)** (volume in bits)
  - **D = (n1 / 2) × (N2 / n2)** (difficulty)
  - **E = V × D** (effort required to implement)
- **McCabe's Cyclomatic Complexity** — based on control flow; measures logical complexity; indicates testing difficulty. Distinct relationship demonstrated between cyclomatic complexity and # errors in source code, and time to find/fix errors.
- Other: length of code, length of identifiers, depth of conditional nesting.

#### 5.2.15 Process Quality

Unlike manufactured products, software has unique factors affecting quality: software is *designed, not manufactured*; software development is *creative, not mechanical*; individual skills & experience matter; external factors (application novelty, commercial pressure) matter ⇒ software processes are **organisation-specific**; **people & technology may matter more than process**; **insufficient resources always adversely affect quality**.

#### 5.2.16 Process Quality Frameworks

- **ISO 9001 / 9000-3** — *generic quality model* focused on process management; customised to an organisation's quality model; instantiated as organisational quality process; used to develop project quality plans which support project quality management. Certification is easy — can be a marketing ploy.
- **SEI CMM** — see §4.4.6 above.
- **People CMM (PCMM)** — see §4.4.6 above.

#### 5.2.17 Summary of Software Quality

- Quality software **does not just happen**.
- Quality-assurance mechanisms should be **built into** the software development process.
- Developing quality software requires: management support & involvement; gathering & use of software metrics; policies and procedures everyone follows; commitment to following them even when things get rough.
- **Testing is important but not all there is** to obtaining a quality software product.

---

### 5.3 Risk Management 📚

> 📚 Risk Management is in the syllabus (Unit-II) but **NOT covered in any of the professor's supplied notes** (Lecture 38 in the contents but missing from the file). The material below is supplemented from standard SE textbooks (Pressman, Rajib Mall, Sommerville). High probability of appearing in 2026 mid-sem — read carefully.

#### 5.3.1 Definition of Risk

A **risk** is an unwanted event that has negative consequences, OR more formally: *"a potential problem — it might happen, it might not."* In software engineering context (per Spiral Model notes): *"any adverse circumstance that might hamper successful completion of a software project."*

Two key characteristics:
1. **Uncertainty** — the event may or may not happen.
2. **Loss** — if it does happen, there's a negative consequence.

#### 5.3.2 Types of Risks

| Type | Description | Example |
|------|-------------|---------|
| **Project risks** | Affect project schedule or resources | Staff turnover, budget cut |
| **Product risks** | Affect the quality or performance of the software being developed | Use of a new framework, dependency on unreliable 3rd-party component |
| **Business risks** | Affect the organisation developing the software | Building a product no one wants; losing management support |
| **Technology risks** | Arose from the software or hardware technologies | Use of unproven tech, performance shortfalls |

**Boehm's Top 10 Software Risks:**
1. Personnel shortfalls
2. Unrealistic schedules and budgets
3. Developing the wrong software functions
4. Developing the wrong user interface
5. Gold-plating (unnecessary features)
6. Continuing stream of requirements changes
7. Shortfalls in externally furnished components
8. Shortfalls in externally performed tasks
9. Real-time performance shortfalls
10. Straining computer-science capabilities

#### 5.3.3 Risk Management Cycle

Risk management is a continuous, iterative process throughout the project life cycle. The cycle has 4 phases:

1. **Risk Identification** — identify what can go wrong.
2. **Risk Analysis / Quantification** — estimate likelihood & impact.
3. **Risk Planning / Mitigation** — decide how to address each risk.
4. **Risk Monitoring** — track risks throughout project; reassess periodically.

```
       ┌────────────────────────────────┐
       ↓                                │
  Risk Identification ──→ Risk Analysis ──→ Risk Planning ──→ Risk Monitoring ──→ (back to Identification)
```

#### 5.3.4 Risk Identification

**Goal:** Discover risks before they become problems.

**Techniques:**
- **Brainstorming** sessions with project team.
- **Checklists** based on past projects (e.g., Boehm's Top 10).
- **Expert judgement** — interview experienced developers.
- **Risk breakdown structure (RBS)** — hierarchical decomposition: Project → Sub-categories → Individual risks.
- **Use-case / scenario analysis** — what could go wrong in each use case?

**Output:** A **Risk Register** — list of identified risks with descriptions.

#### 5.3.5 Risk Quantification / Analysis

For each identified risk, estimate:
- **Probability (P)** — likelihood of occurrence (0 to 1, or Low/Medium/High).
- **Loss / Impact (L)** — severity if it occurs (cost, schedule, or 1–5 scale).

**Key formula — Risk Exposure (RE):**

> **RE = P(Loss) × Size(Loss)**

Also called **Risk Impact (RI) = Probability × Impact**.

Example: risk of staff loss, P = 0.25, impact = ₹8,00,000 ⇒ RE = ₹2,00,000.

**Risk prioritisation matrix (3×3):**

|              | Low Impact | Medium Impact | High Impact |
|--------------|------------|---------------|-------------|
| **High Prob**  | Medium | High | Critical |
| **Med Prob**   | Low | Medium | High |
| **Low Prob**   | Very Low | Low | Medium |

**Output:** A prioritised risk list — highest RE first.

#### 5.3.6 Risk Mitigation / Resolution Strategies

Five common strategies (RMMM = Risk Mitigation, Monitoring, Management Plan):

1. **Risk Avoidance** — change plans to eliminate the risk. E.g., don't use the unproven technology.
2. **Risk Transfer** — shift risk to another party (outsourcing, insurance, fixed-price contract).
3. **Risk Acceptance** — accept the consequences; do nothing (low-impact risks).
4. **Risk Reduction / Mitigation** — reduce probability or impact. E.g., add more testing, training, prototypes.
5. **Contingency Planning** — prepare a backup plan triggered if the risk occurs.

For each high-priority risk, write a **Risk Information Sheet (RIS)**:
- Risk ID, description
- Probability, impact, RE
- Mitigation plan
- Owner, due date
- Contingency plan

#### 5.3.7 Risk Monitoring

Throughout the project:
- Re-evaluate each risk periodically.
- Track whether mitigation actions are working.
- Identify new risks arising as the project evolves.
- Close out risks that no longer apply.
- Update the Risk Register.

**Milestones / triggers** — predefined conditions that activate the contingency plan.

#### 5.3.8 Metrics in Risk Management

- **Number of risks identified vs. realised** — measures risk identification effectiveness.
- **Risk exposure trends** — is total RE going up or down?
- **Mitigation effectiveness** = (RE_before − RE_after) / RE_before.
- **Risk realisation rate** = # risks that occurred / # risks identified.
- **Cost of risk management** vs. cost of risks realised — ROI of risk management.

---

## 6. Model Answers for PYQs

> These are *model answers* you can adapt. Practise writing them in your own words. Each long-answer follows: Definition → Diagram → Phases/Steps → Advantages → Disadvantages → When to use.

### 6.1 2025 PYQ — Section A (5 × 1 = 5 marks)

#### Que-1 (a) What is meant by Software and Software Engineering?

**Software:** A collection of executable programming code, associated libraries, and documentations — more than just a program; it includes all artifacts produced during development.

**Software Engineering:** An engineering branch associated with the development of a software product using well-defined scientific principles, methods and procedures; the outcome is an efficient and reliable software product. IEEE definition: *"the application of a systematic, disciplined, quantifiable approach to the development, operation and maintenance of software."*

#### Que-1 (b) Define process in the context of software quality.

A **process** is a set of activities, methods, practices and transformations used to develop and maintain software and associated products. In the context of software quality, the process defines *how* software is developed — and a disciplined, well-defined process is the foundation of repeatable quality. Without a sound process, quality is left to chance.

#### Que-1 (c) List the task regions in the Spiral model.

The Spiral model has **4 task regions (quadrants)**:
1. **Objective Setting** — identify objectives, examine risks, find alternatives.
2. **Risk Assessment and Reduction** — analyse and reduce identified risks.
3. **Development and Validation** — develop & validate the next level of the product.
4. **Review and Planning** — review with customer, plan the next iteration.

#### Que-1 (d) What is the use of CMM?

The Capability Maturity Model (CMM), developed by the Software Engineering Institute (SEI), is used to help software organisations **improve** their software development processes. It defines 5 maturity levels (Initial → Repeatable → Defined → Managed → Optimizing) that guide organisations from ad-hoc chaotic development towards a measured, continuously-optimised process.

#### Que-1 (e) What is meant by Software and Software Engineering?

*(Same as Q1a — asked twice in 2025!)*
**Software** = executable code + libraries + documentation.
**Software Engineering** = systematic, disciplined, quantifiable approach to developing, operating, and maintaining software; the application of engineering to software.

### 6.2 2025 PYQ — Section B (2 × 10 = 20 marks)

#### Que-2 (a) Draw the schematic diagram to represent the Classical Waterfall Model in the SDLC. [10 Marks]

**Definition:** The Classical Waterfall Model, proposed by Winston Royce (1970), is the oldest, simplest, and most intuitive life-cycle model. It represents the software development process as a sequential, top-down flow of phases, where each phase must be completed before the next begins.

**Phases (in order):**
1. Feasibility study
2. Requirements analysis & specification (SRS)
3. Design
4. Coding & unit testing
5. Integration & system testing
6. Maintenance

**Schematic Diagram:** *(Draw the 6 stacked boxes from §4.5.2 — see diagram above.)*

**Activities in each phase (brief):**
- **Feasibility study** — visit client; perform cost-benefit analysis; check economic, technical & schedule feasibility; produce business case.
- **Requirements analysis & specification** — gather requirements; analyse for inconsistencies; document in SRS.
- **Design** — transform SRS into a structure suitable for implementation (architecture, high-level, detailed).
- **Coding & unit testing** — code modules; unit-test in isolation; document.
- **Integration & system testing** — integrate modules; α-test (dev team), β-test (friendly customers), acceptance test (customer).
- **Maintenance** — corrective (fix bugs), perfective (enhance), adaptive (port). Consumes ~60% of total life-cycle effort.

**Advantages:**
- Simple and intuitive; easy to understand & use.
- Well-defined milestones (phase entry/exit).
- Requirements stability during development.
- Strong management control (plan, staff, track).
- Good documentation for maintenance.

**Disadvantages:**
- Idealistic — assumes no defects in any phase.
- Defects detected late ⇒ high rework cost.
- All requirements must be known up-front (~40% change after start).
- 99% complete syndrome.
- Big-bang integration at end; no customer preview.
- Cannot accommodate change requests during development.

**When to use:** Requirements well-known & stable; technology understood; team experienced.

#### Que-2 (b) Explain requirements engineering processes with a suitable diagram. [10 Marks]

**Definition:** Requirements Engineering (RE) is the process of **establishing the services the customer requires** from a system and the **constraints** under which it operates and is developed. It is conducted by experienced team members called **system analysts**.

**RE Process — Activities:**
1. **Feasibility Study** — financial & technical feasibility; produce business case (Go/No-Go decision).
2. **Requirements Gathering** — collect data via interviews, discussions, questionnaires, observation, studying existing documents, prototyping.
3. **Requirements Analysis & Specification** — analyse gathered data; remove inconsistencies, anomalies, incompleteness; resolve through further discussions; organise into the SRS document.
4. **SRS Review / Requirements Validation** — review SRS for correctness, completeness, consistency, etc.; customer's approval is the **exit criterion** for the requirements phase.

**Diagram:** *(Draw the flowchart from §4.12.3.)*

**Output:** Software Requirements Specification (SRS) document containing:
- Functional requirements (what the system does — input/output transformations).
- Non-functional requirements (performance, security, usability, portability, etc.).
- Goals of implementation (future revision plans, reusability issues).

**Types of Requirements:**
- **Functional** — services the system must provide (e.g., "withdraw cash" function).
- **Non-functional** — constraints on the system (performance, security, reliability).
- **Goals of implementation** — future-direction suggestions.

**Desirable characteristics of a good SRS** (also asked in 2024 Q2c): Concise, Structured, Black-box view, Conceptual integrity, Response to undesired events, Verifiable (also: Correctness, Consistency, Completeness, Modifiability, Traceability).

#### Que-2 (c) What is meant by software configuration management? Explain the two principal activities of configuration management. [10 Marks]

**Definition of SCM:** Software Configuration Management (SCM) is an **activity executed throughout the system life cycle to control change of products and life-cycle artifacts**. A **configuration item (CI)** is *an artifact to which we want to control changes* — plans, specifications, procedures, programs, documents, data.

**Need for SCM:**
- Software is constantly changed (corrective, perfective, adaptive).
- Without control, change = chaos.
- Need integrity, security, traceability.
- Need to communicate change status to all stakeholders.

**Two Principal Activities of SCM:**

##### (1) Configuration Identification

Each CI must be identified and described with metadata:
- Unique name
- Configuration item type
- Project identifier
- Change and/or version information
- Resources the CI provides or requires
- Pointer to the actual CI

CIs must be **organised** — relationships defined (e.g., *part-of*, *related-to*). Define and construct a **software library (database)** to store, manage, track CIs.

##### (2) Configuration Control

Concerned with managing changes to CIs after they have been **baselined**. A baseline is a milestone after which changes must be formalised. Configuration control implements:
- **Version control** — managing multiple versions, branches, variants of CIs.
- **Change control** — formal process:
  1. Change request submitted.
  2. Change Control Authority (CCA) evaluates & issues Engineering Change Order (ECO) if approved.
  3. CI is checked-out, modified, SQA-reviewed, checked-in.
  4. New version promoted & released.

**Other supporting SCM activities:** Configuration Audit (verify changes implemented correctly; done by QA group), Status Reporting (communicate change status), Library support.

**Benefits of SCM:**
- Reduced change-management effort.
- Improved software integrity & security.
- Enhanced management control.
- Better record keeping & tracking.

### 6.3 2024 PYQ — Section A (5 × 1 = 5 marks)

#### Q1 (a) What are the challenges in software?

- Increasing size & complexity.
- Changing user requirements.
- Tight schedules & cost pressures.
- Lack of trained personnel.
- Difficulty in measuring/estimating software.
- Difficulty in coordinating large teams.
- Legacy systems needing continuous maintenance.

#### Q1 (b) What is the prime objective of software engineering?

To produce **efficient and reliable software products in a cost-effective manner** — to deliver a quality product **within time and budget** that meets customer requirements.

#### Q1 (c) What is known as SRS review?

Once the SRS document is drafted, it is reviewed by the customer and the development team to check for correctness, completeness, consistency, ambiguity, verifiability, modifiability, and traceability. **Customer's approval is the exit criterion** for the requirements phase.

#### Q1 (d) What is meant by software prototyping?

A **prototype** is a *toy implementation* of the system with limited functional capabilities, low reliability, and inefficient performance — built using shortcuts (e.g., dummy functions, table look-ups). It is used to clarify user requirements and resolve technical issues, then typically discarded (throwaway) or refined (evolutionary).

#### Q1 (e) What is software quality and how do we measure it?

**Software quality** is the degree to which a software product meets or exceeds pre-specified standards during its development cycle, viewed from both customer (meets specifications) and developer (easy to maintain/test) perspectives. **Measured via:** defect density (defects/KLOC), defect removal efficiency (DRE), mean time to failure (MTTF), cyclomatic complexity, fan-in/fan-out, Halstead metrics, review effectiveness, and conformance to defined quality attributes (safety, security, reliability, usability, etc.).

### 6.4 2024 PYQ — Section B (3 × 15 = 45 marks)

#### Q2 (a) Explain the iterative waterfall and spiral model for the software life cycle and discuss various activities in each phase. [15 Marks]

This is a comparison question — answer in two parts.

**Part I: Iterative Waterfall Model**

*Definition:* The Iterative Waterfall extends the classical waterfall by adding **feedback paths** so that defects detected in a later phase can be reworked in an earlier phase. This implements **phase containment of errors** — earlier detection ⇒ cheaper correction.

*Phases:* Same 6 phases as classical waterfall — Feasibility → Requirements → Design → Coding → Integration & Testing → Maintenance.

*Diagram:* Vertical stack with upward feedback arrows.

*Activities:* Each phase has the same activities as classical waterfall; the difference is the explicit feedback loop allowing rework.

*Advantages:*
- Working model available early.
- Issues found early ⇒ lower-cost correction.
- Most widely used model in practice.
- Good documentation & reliable software.

*Disadvantages:*
- Suitable only for well-understood problems.
- Not for large/very risky projects.
- Cannot accommodate change requests.

*When to use:* Stable requirements, mature technology, experienced team.

**Part II: Spiral Model**

*Definition:* Proposed by **Barry Boehm (1988)**. A risk-driven meta-model where the project is depicted as a spiral of many loops, each loop = a phase, and each loop is split into 4 task regions (quadrants).

*Task Regions:*
1. **Objective Setting** — identify objectives, examine risks, find alternatives.
2. **Risk Assessment & Reduction** — analyse & reduce identified risks (e.g., via prototyping).
3. **Development & Validation** — develop & validate the next level of the product.
4. **Review & Planning** — review results with customer; plan next iteration.

*Diagram:* Spiral with 4 quadrants; radius = cumulative cost; angle = progress.

*Activities per loop:* Each loop moves the project forward — inner loops ≈ early phases (feasibility, requirements), outer loops ≈ later phases (design, coding, testing).

*Advantages:*
- Best for technically challenging, risky projects.
- Risk-driven — risks explicitly identified & reduced each iteration.
- Combines best of waterfall + prototyping + evolutionary.
- Customer review at end of each loop.

*Disadvantages:*
- More complex than other models.
- Requires risk-assessment expertise.
- Number of loops not fixed — hard to plan.
- Heavy management overhead.

*When to use:* Technically challenging, large-scale, long-lived projects with many risks.

#### Q2 (b) Explain: (i) Waterfall model, (ii) RAD model, (iii) Prototyping model. [15 Marks]

For each model, follow the same template: Definition → Diagram → Phases/Steps → Advantages → Disadvantages → When to use. See §4.5 (Waterfall), §4.10 (RAD), §4.7 (Prototyping) for full content. Spend ~5 marks / ~5 minutes on each.

#### Q2 (c) Explain the main activities used in requirements engineering. What are the desirable characteristics of good SRS documents? Explain with an example. [15 Marks]

*Part I: Main activities of RE* (5–7 marks) — see §4.12.2: Feasibility study, Requirements gathering, Analysis & specification, SRS review.

*Part II: Desirable characteristics of good SRS* (5–6 marks) — see §4.12.8: Concise, Structured, Black-box view, Conceptual integrity, Response to undesired events, Verifiable.

*Part III: Example SRS* (3–4 marks) — use the ATM withdraw-cash example from §4.12.11 (R1, R1.1, R1.2, R1.3 with Input/Output/Processing).

#### Q2 (d) What is meant by software configuration management? Explain software quality assurance. [15 Marks]

*Part I: SCM* (7 marks) — see §5.1: Definition, need, 2 principal activities (Configuration Identification + Configuration Control), baseline, version control, change control, audit, status reporting, benefits.

*Part II: SQA* (8 marks) — see §5.2: Definition, SQA as umbrella activity, QC vs QA, principles, cost-of-defect curve, SQA activities, SQA tools, measures of SQA success (DRE, MTTF, defect density), reviews, metrics (Halstead, McCabe, DSQI, SMI), ISO 9001, CMM.

---

## 7. Quick Revision Cards (Last-Day Cramming)

> Read these the night before the exam. Each card is a 1-liner you should be able to recite from memory.

### Card Set A — Definitions (1-mark gold)

1. **Software** = executable code + libraries + documentation; more than just a program.
2. **Software Engineering (IEEE)** = systematic, disciplined, quantifiable approach to development, operation & maintenance of software.
3. **Prime objective of SE** = produce efficient & reliable software, cost-effectively.
4. **Software Crisis** = projects fail to meet user reqts, delivered late, expensive, unmaintainable (Standish: ~28% success, ~23% cancelled).
5. **Process** = set of activities, methods, practices, transformations to develop & maintain software.
6. **Process Model (SDLC)** = descriptive & diagrammatic representation of the software life cycle.
7. **Abstraction** = simplify by omitting irrelevant details; model building.
8. **Decomposition** = divide problem into independent parts; solve separately.
9. **Software prototype** = toy implementation with limited functionality, low reliability, inefficient performance.
10. **Baseline** = milestone after which changes to a CI must be formalised.
11. **Configuration Item (CI)** = an artifact to which we want to control changes.
12. **SRS** = Software Requirements Specification; black-box specification of the system.
13. **SRS Review** = customer & team review of SRS; customer approval = exit criterion for requirements phase.
14. **Verification** = "Are we building the product right?" (static; reviews).
15. **Validation** = "Are we building the right product?" (dynamic; testing).
16. **Risk** = an unwanted event with uncertainty & loss.
17. **Risk Exposure (RE)** = P(loss) × Size(loss).

### Card Set B — Process Models (10/15-mark gold)

| Model | Key Phrase | When to Use |
|-------|-----------|-------------|
| **Classical Waterfall** | Sequential, top-down, no feedback | Stable requirements, understood technology |
| **Iterative Waterfall** | + feedback paths; phase containment | Well-understood, large projects |
| **Prototyping** | Toy implementation → discard → build real | Unclear requirements, UI development |
| **Evolutionary** | Incremental versions; core first, then add features | Changing requirements, customer wants early use |
| **Spiral (Boehm 1988)** | Risk-driven; 4 quadrants: Objective → Risk → Dev → Review | Technically challenging, risky projects |
| **RAD** | Time boxes; quick-and-dirty prototypes → evolve into product | Fast time-to-market, modular system, reuse |
| **Agile (XP/Scrum)** | Short iterations (1–4 wks); face-to-face; embrace change | Small teams, co-located, customer always available |

### Card Set C — Spiral Task Regions (Memorise verbatim — asked in 2025 Q1c)

1. **Objective Setting**
2. **Risk Assessment & Reduction**
3. **Development & Validation**
4. **Review & Planning**

### Card Set D — CMM 5 Levels

1. **Initial** (ad hoc)
2. **Repeatable** (intuitive)
3. **Defined** (qualitative)
4. **Managed** (quantitative)
5. **Optimizing**

### Card Set E — SRS Desirable Characteristics (2024 Q2c)

1. **Concise**
2. **Structured**
3. **Black-box view** (what, not how)
4. **Conceptual integrity**
5. **Response to undesired events**
6. **Verifiable**

(Also: **Correctness, Consistency, Completeness, Modifiability, Traceability**.)

### Card Set F — SCM Two Principal Activities (2025 Q2c)

1. **Configuration Identification** — name, type, project ID, version, resources, pointer; organise CIs in a software library.
2. **Configuration Control** — manage changes to baselined CIs; version control + change control via CCA & ECO.

### Card Set G — QC vs QA

| QC | QA |
|----|-----|
| Product-oriented | Process-oriented |
| Find defects | Prevent defects |
| Reactive (testing) | Proactive (process audits) |
| After development | Throughout development |

### Card Set H — Risk Management Cycle

1. **Risk Identification** (brainstorm, checklist, RBS)
2. **Risk Analysis/Quantification** (P × L = RE; prioritise)
3. **Risk Planning/Mitigation** (avoid/transfer/accept/reduce/contingency)
4. **Risk Monitoring** (reassess, track, close out)

### Card Set I — Cost of Defect Across Life Cycle

| Phase | Cost |
|-------|------|
| Requirements | 1× |
| Design | 1.3–2× |
| Code | 4× |
| Test | 10× |
| System Test | 13× |
| Field Use | **80–130×** |

### Card Set J — Halstead & McCabe Formulas (SQA metrics)

- **Halstead Volume:** V = L × log₂(n1 + n2), where L = N1 + N2
- **Halstead Difficulty:** D = (n1 / 2) × (N2 / n2)
- **Halstead Effort:** E = V × D
- **McCabe Cyclomatic Complexity:** V(G) = E − N + 2 (or # of decision points + 1)

### Card Set K — Agile Manifesto (4 Values)

1. **Individuals & interactions** over processes & tools.
2. **Working software** over comprehensive documentation.
3. **Customer collaboration** over contract negotiation.
4. **Responding to change** over following a plan.

### Card Set L — Scrum Roles, Artifacts, Events

- **3 Roles:** Product Owner, Scrum Master, Development Team.
- **3 Artifacts:** Product Backlog, Sprint Backlog, Increment.
- **5 Events:** Sprint, Sprint Planning, Daily Scrum, Sprint Review, Sprint Retrospective.

---

## 8. Last-Minute Exam Tips

### 8.1 The Night Before

1. **Re-read §3 (Exam Strategy) and §7 (Quick Cards).** That's it — don't try to learn new material tonight.
2. **Practise drawing 4 diagrams from memory:** Classical Waterfall, Spiral (4 quadrants), RE Process Flow, Change Control Process. If you can draw these in your sleep, half the battle is won.
3. **Memorise these verbatim:** Spiral's 4 task regions; CMM's 5 levels; SRS's 6 desirable characteristics; SCM's 2 principal activities.
4. **Sleep 7+ hours.** A tired brain cannot recall definitions precisely.

### 8.2 In the Exam Hall

1. **Read the question paper fully first (2 minutes).** Mark the questions you'll attempt. Choose your Section-B questions strategically — pick the ones you know best, not the ones that "look short".
2. **Section A (1-mark):** Answer in 2–3 lines max. Don't write paragraphs — examiners deduct for over-writing 1-mark questions.
3. **Section B (10/15-mark):** Always start with a **1-line definition**, then a **neat labelled diagram**, then phases/steps as bullets, then advantages (4–5), then disadvantages (4–5), then when to use.
4. **Diagrams:** Use a ruler. Box for entities, arrow for flow. Label everything. An unlabelled diagram = 0 marks for the diagram.
5. **Time discipline:** If you're stuck on a question for more than its allotted time, MOVE ON. Come back at the end.
6. **Underline key terms** in your answer (definition, phase names, formulas) — helps the examiner spot your answer quickly.
7. **End each long answer cleanly.** Don't add "End of Answer" markers. Just stop after the last point.

### 8.3 Common Mistakes to Avoid

- ❌ Writing the same answer for Q1a and Q1e in 2025 (both ask "Software and Software Engineering") — write *slightly* different angles, e.g., one emphasising the components of software, the other emphasising the IEEE definition.
- ❌ Drawing the Spiral as a circle, not as a spiral — it must look like a spiral unwinding outward.
- ❌ Forgetting to label diagram axes (radius = cost, angle = progress for Spiral).
- ❌ Listing fewer than 4 advantages/disadvantages in 10-mark answers.
- ❌ Not drawing a diagram when the question explicitly says "with suitable diagram".
- ❌ Mixing up Verification (product right) and Validation (right product) — they're easy to swap under stress.
- ❌ Writing Configuration Identification and Configuration Control in wrong order — Identification comes FIRST, then Control.

### 8.4 If You Run Out of Time

If you have 5 minutes and 1 unanswered 10-mark question, write:
1. **Definition** (2 lines)
2. **Diagram** (rough but labelled)
3. **3 bullet points of activities/phases**
4. **2 advantages**
5. **2 disadvantages**

This skeleton can fetch 4–5 marks out of 10, which is far better than 0.

### 8.5 Confidence Boosters

- The exam is **highly pattern-based.** The same 6 topics recur every year. If you've mastered §3 (the 6 must-master topics), you've already secured 70% of the marks.
- **Diagrams are easy marks.** Most students skip them. You won't.
- **Section A is essentially free marks** — memorise the 9 questions in §2.3 and you'll answer any Section A easily.
- **Spiral task regions, CMM levels, SRS characteristics, SCM activities** — these are *list questions*. Lists are the easiest thing to memorise. Do not skip these.

---

## 9. Source Files Used

| File | Use |
|------|-----|
| `repo/spempyqs.md` | PYQs (2024 + 2025) in text form |
| `repo/spem2025mid.png` | 2025 mid-sem paper image (extracted via VLM) |
| `repo/spen2024mid.png` | 2024 mid-sem paper image (extracted via VLM) |
| `repo/SEPM_NOTES_UNIT-I.pdf` | Professor's lecture notes (Lectures 1–14) — covers Unit-I fully |
| `repo/Unit-I_SDLC.pdf`, `Unit-I_SDLC1.pdf`, `Unit-I_SDLC2.pdf` | SDLC lecture slides |
| `repo/week 1.pdf` | Week 1 lecture material |
| `repo/SCM_UNIT_II.pdf` | SCM + SQA + CMM + PCMM + ISO 9001 notes |
| `repo/Assignment_1_SEPM.pdf` | IA-1 assignment questions (topic hints) |
| `repo/23BIT131_SEPM_IA_1.pdf` | Student's IA-1 submission (mostly scanned handwriting — not extractable, not used) |
| 📚 Pressman / Rajib Mall / Sommerville | Risk Management, XP, Scrum, V&V (gaps in professor's notes) |

---

**End of SEPM Mid-Sem Prep — best of luck! 🎯**

*This study guide is ~10,000 words and covers every topic in the mid-sem syllabus with PYQ pattern analysis, model answers, and quick-revision cards. Trust your preparation; you've got this.*

