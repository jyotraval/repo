# SEPM Mid-Sem Study Prep (23IC401T)
### Software Engineering and Project Management — Semester VII

Built from: `week 1`, `Unit-I_SDLC` (parts 1–3), `SCM_UNIT_II`, `SEPM_NOTES_UNIT-I`, `Assignment_1_SEPM` (IA-1 question list), your own handwritten IA-1 answers (`23BIT131_SEPM_IA_1`), and the **2024** & **2025** mid-sem question papers.

---

## 0. How the mid-sem actually looks (from the 2 papers you gave me)

| | **2025 Mid-Sem** | **2024 Mid-Sem** |
|---|---|---|
| Total marks | 25 | 50 |
| Duration | 1 hour | 2 hours |
| Section A | 5×1 mark, answer all | 5×1 mark, answer all |
| Section B | 3×10 marks, **answer any 2** | 4×15 marks, **answer any 3** |

**Pattern to notice:** both papers draw Section A from short definitions/one-liners, and Section B is always built from the *same three buckets*:
1. **Process/Life-cycle models** (waterfall, spiral, RAD, prototyping)
2. **Requirements Engineering / SRS**
3. **Software Configuration Management + Software Quality Assurance**

This has repeated **two years in a row**, so it is overwhelmingly likely to repeat again. The 2025 paper even has a typo where Que-1(e) repeats Que-1(a) verbatim ("What is meant by Software and Software Engineering?") — so don't be thrown off if a question looks duplicated.

### 🎯 Highest-probability Section B questions (study these FIRST, in this order)
1. Classical Waterfall Model — draw + explain phases (asked both years)
2. Iterative Waterfall + Spiral Model — activities in each phase (2024)
3. Waterfall / RAD / Prototyping — explain all three (2024)
4. Requirements engineering — main activities + SRS characteristics (both years, different wording)
5. Software Configuration Management + its principal activities (2025) / + SQA (2024)

### 🎯 Highest-probability Section A one-liners (know a crisp 1–2 line answer)
- What is Software / Software Engineering?
- Prime objective of Software Engineering
- Challenges in software / Software crisis
- Task regions (quadrants) of the Spiral model
- What is CMM used for?
- What is SRS review?
- What is software prototyping?
- What is software quality and how is it measured?
- Define "process" in the context of software quality

---

## 1. Foundations — Software & Software Engineering

**Software** is more than a program: it is a collection of executable code, associated libraries, and documentation. When built for a specific requirement, it is called a **software product**.

**Software Engineering (IEEE definition):** *"The application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software; that is, the application of engineering to software."*

**Prime objective of Software Engineering:** to develop high-quality software that is
- **reliable** — works correctly and consistently
- **maintainable** — easy to modify and enhance
- **cost-effective** — delivered within time and budget
- meets the **user's requirements and expectations**

### Software Crisis / Challenges in software
Software products often:
- Fail to meet user requirements
- Are expensive
- Are difficult to alter, debug, and enhance
- Are delivered late
- Use resources non-optimally

**Contributing factors:** larger/more complex problems, poor project management, lack of adequate SE training, increasing skill shortage, low productivity improvement.

> Standish Group Report (classic stat to quote): only ~28% of projects are fully successful; ~49% are delayed/over-budget; ~23% are cancelled.

### Characteristics of good software
- **Operational:** budget, usability, efficiency, correctness, functionality, dependability, security, safety
- **Transitional:** portability, interoperability, reusability, adaptability
- **Maintenance:** modularity, maintainability, flexibility, scalability

### Handling complexity: Abstraction & Decomposition
Software engineering uses two techniques to fight the exponential growth of effort with program size:
- **Abstraction** — simplify a problem by omitting irrelevant details; focus on one aspect at a time (also called *model building*). Example: a map is an abstraction of a country.
- **Decomposition** — break a complex problem into smaller, largely *independent* parts, solve each separately, then combine. (Classic analogy: breaking a bundle of sticks is hard; breaking them one at a time is easy.)

---

## 2. Software Life Cycle / Process Models

A **software life cycle model (SDLC / process model)** is a descriptive and diagrammatic representation of the software life cycle. It:
- identifies all activities in product development,
- establishes an ordering among activities,
- divides the life cycle into phases,
- defines **entry and exit criteria** for every phase (a phase is "complete" only when its exit criteria are satisfied — these are called **milestones**).

Without a life cycle model, teams fall into chaos (the classic **99% complete syndrome**, where progress can't be honestly tracked).

---

### 2.1 Classical Waterfall Model ⭐ (asked in both papers)

**Definition:** The simplest and most intuitive SDLC model. It is a **linear and sequential** approach where each phase must be completed before the next begins. Also called the *classical life cycle model*.

**Schematic diagram (draw this exactly):**

```
Feasibility Study
        │
        ▼
Requirements Analysis & Specification
        │
        ▼
      Design
        │
        ▼
 Coding & Unit Testing
        │
        ▼
Integration & System Testing
        │
        ▼
     Maintenance
```
(Drawn as descending steps/a "waterfall" — each box flows only downward into the next.)

**Phases explained:**
1. **Feasibility Study** — determine if developing the software is *financially* and *technically* feasible. Roughly understand: input data, processing needed, output data, constraints. Ends with a Go/No-Go decision after cost-benefit analysis.
   - Feasibility has 3 dimensions: **Technical, Economic (cost/benefit), Schedule** feasibility.
2. **Requirements Analysis & Specification** — two sub-activities:
   - *Requirements gathering & analysis* — collect data from customer (interviews/discussions), remove inconsistencies/ambiguities/incompleteness.
   - *Requirements specification* — organize into the **SRS document** (see Section 3).
3. **Design** — transform SRS into a structure suitable for implementation. Two approaches: **Traditional** (structured analysis via DFD + structured design) and **Object-Oriented** (identify objects, their relationships, refine to detailed design).
4. **Coding & Unit Testing** — each module coded, unit tested (tested standalone), and documented.
5. **Integration & System Testing** — modules integrated in planned steps (not "big bang"); after full integration, **system testing** checks the system against the SRS. Includes α-testing (by dev team), β-testing (by friendly customers), and acceptance testing (by the customer).
6. **Maintenance** — consumes the *most* effort of all phases (dev : maintenance ≈ 40:60). Three types:
   - **Corrective** — fix undiscovered bugs
   - **Perfective** — improve/enhance functionality
   - **Adaptive** — port to a new environment/OS/platform

**Shortcoming:** it is *idealistic* — assumes no defects are ever introduced, so it has no mechanism to go back and fix errors. This is purely theoretical; not used as-is in practice. → leads to the **Iterative Waterfall Model**.

---

### 2.2 Iterative Waterfall Model ⭐ (asked 2024)

Fixes the classical model's flaw by adding **feedback paths** between phases, so defects found later can be traced back and corrected.

- **Phase containment of errors:** the principle that errors should ideally be detected in the *same phase* they were introduced — the later a defect is found, the more expensive it is to fix (design defect found in testing requires redoing design + code + test).
- This is the **most widely used** life ccycle model; nearly every other model derives from it.

**Strengths:** easy to understand/use even for inexperienced staff; clear milestones; requirements stability; strong management control (plan, staff, track).

**Deficiencies:** all requirements must be known upfront; can give false impression of progress; integration is "one big bang" at the end; little chance for customer to preview the system.

**When to use:** requirements are well known and stable, technology is understood, team has experience with similar projects.

*(Related but not directly asked so far: the **V-Model** — a waterfall variant that pairs every development phase with a matching testing/validation phase, run in parallel. Good for high-reliability/safety-critical systems. Weakness: doesn't handle iteration or late requirement changes well.)*

---

### 2.3 Prototyping Model ⭐ (asked 2024)

A **derivative of the waterfall model**. Before real development starts, a **prototype** — a toy implementation with limited functionality, low reliability, and inefficient performance — is built using shortcuts (dummy/inefficient functions, table look-ups instead of real computation).

**Diagram (flow):**
```
Requirements Gathering → Quick Design → Build Prototype
        ▲                                    │
        │                                    ▼
  Refine Requirements ◄──── Customer Evaluation of Prototype
                                              │
                                   (customer satisfied?)
                                              │
                                              ▼
                          Design → Implement → Test → Maintain
```

**Why prototype?**
- Learning by doing — useful when requirements are only partially known
- Improves communication & user involvement
- Reduces documentation & maintenance cost
- Illustrates input/output formats, screens, dialogs to the customer
- Resolves technical uncertainties (e.g., response time, algorithm efficiency) before committing
- "You can't get it right the first time" — plan to throw the prototype away

**Advantages:** more usable software, better-accommodated user needs, higher design quality, easier maintenance, often lower overall cost (avoids expensive late redesign).
**Disadvantages:** can be expensive for some projects; risk of over-engineering.

---

### 2.4 Evolutionary Model (a.k.a. Successive Versions / Incremental Model)

Build a simple working **core** first, then add functionality in successive iterations until the full system is built. Each iteration is like a "mini waterfall."

**Diagram idea:** Initial Requirements → Specification → Development → Validation → (loop back with refined requirements) → Initial version → Intermediate versions → Final version.

**Applications:** large projects divisible into modules; object-oriented development.
**Advantages:** users can experiment with a partial system early; core modules get tested thoroughly, reducing final errors; better handling of changing requirements.
**Disadvantages:** hard to split the problem into customer-acceptable increments; process can feel unpredictable/intangible if not planned well.

---

### 2.5 Spiral Model ⭐ (task regions asked 2025)

Proposed by **Boehm (1988)**. Represented as a spiral with several loops; each loop = one phase of the process (innermost loop = feasibility, next = requirements, next = design, etc. — not fixed). Each loop is split into **four sectors/quadrants** — these are the **"task regions"**:

| Quadrant | Task Region | What happens |
|---|---|---|
| 1 | **Objective Setting** | Identify objectives of the phase; examine risks associated with them; find alternate solutions |
| 2 | **Risk Assessment & Reduction** | Detailed analysis of each identified risk; steps taken to reduce it (e.g., build a prototype if requirements risk exists) |
| 3 | **Development & Validation** | Develop and validate the next level of the product |
| 4 | **Review & Planning** | Review results with the customer; plan the next iteration around the spiral |

**Key facts:**
- It is a **risk-driven** model.
- Called a **meta-model** because it subsumes all other models: a single loop = waterfall model; it uses an evolutionary approach where iterations = evolutionary levels; and it uses prototyping as a risk-reduction mechanism.
- Best suited for **large, technically challenging, high-risk** projects. Too complex for small/ordinary projects.

---

### 2.6 RAD Model (Rapid Application Development) ⭐ (asked 2024)

Also called the *rapid prototyping model*. Goal: **decrease time & cost**, and accommodate change requests early — before heavy investment is made.

**Core idea:** make only short-term plans (each iteration = a **time box**) and reuse existing code heavily.

**Methodology per iteration:**
1. A quick-and-dirty prototype for selected functionality is built.
2. Customer evaluates it and gives feedback.
3. Prototype is refined based on feedback.
→ Achieved fast via visual development tools, reusable components, standard APIs.

**Suitable for:** custom products for 1–2 customers; performance/reliability not critical; system splittable into independent modules.
**Unsuitable for:** few reusable/plug-in components available; high performance/reliability required; no precedent for a similar product; system can't be modularized.

**Comparisons (favorite exam angle — know these):**
- **RAD vs Prototyping:** in plain prototyping the prototype is usually *thrown away* (used to gain insight/feedback); in RAD the prototype *evolves into the final deliverable software*.
- **RAD vs Iterative Waterfall:** iterative waterfall develops all functionality together and doesn't easily accommodate change; RAD develops incrementally via heavy reuse and takes customer feedback after every iteration — but waterfall gives better documentation and higher quality/reliability than RAD.
- **RAD vs Evolutionary Model:** both are incremental, but RAD increments are "quick and dirty" prototypes in short cycles, while evolutionary-model increments are systematically developed (mini-waterfalls) and are comparatively larger/longer.

---

### 2.7 Agile Models (lower priority — syllabus topic, not yet in either PYQ, but know the basics)

Proposed to overcome waterfall's rigidity. Requirements are broken into small increments developed over 1–4 weeks.

**Agile Manifesto values:** Individuals & interactions *over* processes & tools; Working software *over* comprehensive documentation; Customer collaboration *over* contract negotiation; Responding to change *over* following a plan.

- **Extreme Programming (XP):** pair programming, continuous testing, frequent small releases, refactoring, user stories.
- **Scrum:** sprints (fixed time-boxed iterations), daily stand-ups, product backlog, Scrum Master/Product Owner roles.

Techniques: **user stories** (simpler than use cases), **spikes** (small exploratory programs), **refactoring**.

---

## 3. Requirements Engineering & SRS ⭐ (asked both years)

### 3.1 Requirements Engineering Process (standard model — draw this diagram)

> Note: your slides cover the *content* of this phase in depth but don't include one single labelled "process" diagram — the diagram below is the standard, widely-taught version. Use it for the "explain with a diagram" question.

```
 ┌──────────────────┐
 │ Feasibility Study │
 └─────────┬──────────┘
           ▼
 ┌──────────────────────────────┐
 │ Requirements Elicitation &    │◄───┐
 │ Analysis (gather from users,  │    │ (loop until
 │ resolve ambiguity/conflicts)  │    │ requirements
 └─────────┬──────────────────────┘    │ are clear/
           ▼                          │ validated)
 ┌──────────────────────────────┐    │
 │ Requirements Specification    │    │
 │  → produces the SRS document  │    │
 └─────────┬──────────────────────┘    │
           ▼                          │
 ┌──────────────────────────────┐    │
 │ Requirements Validation       │────┘
 │ (review SRS with customer)    │
 └─────────┬──────────────────────┘
           ▼
 ┌──────────────────────────────┐
 │ Requirements Management       │
 │ (handle change requests later)│
 └────────────────────────────────┘
```

**Explain each stage in 1 line when writing the answer:**
- **Feasibility study** — is it worth doing at all (technical/financial)?
- **Elicitation & analysis** — gather raw requirements via interviews/discussions with users; remove contradictions, since each user has only a *partial* view of the system.
- **Specification** — organize the clarified requirements into the formal SRS document.
- **Validation** — check the SRS is complete, consistent, and matches what the customer actually wants (formal review/walkthrough).
- **Management** — handle evolving requirements/change requests over the project's life.

### 3.2 SRS Document — Parts

1. **Functional requirements** — the functionalities the system must provide. Each function fᵢ transforms input data into output data (a "black box" transformation).
   - Example: `F1: Search Book` → Input: author's name → Output: book details + location.
2. **Non-functional requirements** — qualities that aren't expressible as functions: maintainability, portability, usability, etc.
3. **Goals of implementation** — general guidance for future trade-offs: future revisions, new devices to support, reusability concerns.

### 3.3 Properties of a Good SRS Document ⭐ (frequently asked as "desirable characteristics")

| Property | Meaning |
|---|---|
| **Concise** | Unambiguous, consistent, complete — no verbose/irrelevant description |
| **Structured** | Well organized so it's easy to understand and modify (SRS is revised often) |
| **Black-box view** | Describes *what* the system should do, not *how* — external behaviour only |
| **Conceptual integrity** | Shows a unified, coherent view so it's easy to read |
| **Response to undesired events** | Specifies acceptable behaviour for exceptional/error conditions |
| **Verifiable** | Every requirement must be checkable — you can prove whether an implementation meets it or not |

### 3.4 Problems if there is no SRS document
- System won't be implemented according to actual customer needs.
- Developers won't know if what they're building is what's actually required.
- Very difficult for maintenance engineers to work without understanding documented requirements.
- No baseline to check requirements are complete/consistent → **SRS review**: a formal walkthrough/technical review of the SRS (by customer + development team) conducted before design begins, to catch ambiguity, inconsistency, and incompleteness early (cheapest point to fix them).

---

## 4. Umbrella Activities — Software Configuration Management (SCM) ⭐

**Definition:** SCM is an activity executed **throughout the system life cycle** to control changes to software products and life-cycle artifacts (plans, programs, specifications, documents/manuals, procedures, data). Each such artifact is a **configuration item (CI)**.

### The Two Principal Activities of Configuration Management

1. **Configuration Identification** — deciding which artifacts (configuration items) need to be tracked; giving each a unique name, type, version info, and organizing the relationships between them; building a software library/database to store and track them. This defines the *scope* of what is controlled.
2. **Configuration Control** — systematically controlling and managing changes made to identified configuration items via a formal **change control process**, so nothing changes silently or without review.

*(Your slides also frame SCM as four connected steps — worth mentioning as elaboration: **Identify → Control → Audit → Report**, all supported by a software library.)*

- **Audit** — verifies changes have been properly implemented (checklist-driven, usually by the QA group).
- **Status reporting** — keeps all stakeholders informed about what changed, when, why, and by whom.

### Supporting concepts (good for extra marks)
- **Baseline** — a milestone/point in development after which any change must go through a formal change-control procedure. A configuration item becomes a baseline after passing formal review (code review, doc review, etc.), then it enters the project software library.
- **Version control:**
  - *Version* — item created by modifying an earlier version (linear, e.g. bug fixes)
  - *Branch* — a concurrent, independent development path
  - *Variant* — different configurations meant to coexist (e.g., same software for Windows vs Linux)
- **SCM Change control process:** change request submitted → change control authority evaluates/approves → item is checked-out, modified, checked-in after QA → item made available for release. (Uncontrolled rapid change leads to chaos — this is *why* SCM exists.)
- **SCM benefits:** reduces effort to manage change (↑ productivity), better integrity/security (↑ quality), generates process information (↑ management control), maintains a development database (better record-keeping).

---

## 5. Umbrella Activities — Software Quality Assurance (SQA) ⭐

**Definition (E.H. Bersoff):** *"Quality assurance consists of those procedures, techniques, and tools applied by professionals to ensure that a product meets or exceeds pre-specified standards during its development cycle."*

- SQA must be **planned and systematic** (it doesn't just happen) and **built into** the development process; continuous improvement is the overall goal.

### SQA as an Umbrella Activity — draw this diagram
SQA sits at the centre and connects to:
- **Software Configuration Management**
- **Testing**
- **Formal Technical Reviews**
- **Standards and Procedures**
- **Metrics and Measurement**
- **Methods and Tools**

### Why SQA pays off
Cost to find/fix a defect rises steeply the later it's caught: cheapest at Requirements, rises through Design → Code → Test → System Test → Field Use (can be 80–130× more expensive in the field than at requirements stage). This is the core justification for doing SQA early.

### What is Software Quality? (asked both years)
- **Customer's viewpoint** → meets specifications
- **Developer's viewpoint** → easy to maintain, test, etc.
- Quality ≠ just "no bugs + meets spec." Other attributes matter: safety, security, reliability, resilience, robustness, understandability, testability, adaptability, modularity, complexity, portability, usability, reusability, efficiency, learnability.
- **How it's measured:** select critical quality attributes early and track them using **metrics** — e.g. **control metrics** (effort, elapsed time) and **predictor metrics** (internal attributes like cyclomatic complexity used to predict external attributes like maintainability).

### Principles of SQA
1. There's a set of standards/quality attributes the product must meet (a goal exists).
2. We can measure product quality (a way exists to check conformance).
3. We track quality attribute values (we can assess how we're doing).
4. We feed quality info back into the process to improve future products.

### Software Standards
- **Product standards** — define characteristics all product artifacts should have.
- **Process standards** — define how the software process should be conducted.
- Why they matter: capture best practices, provide a framework for SQA, ensure continuity of project work.

### The four P's of software development (context for SQA)
**People, Process, Project, Product** — quality is achieved through education/training (people), a defined process template with measurement/feedback (process), management/monitoring (project), and testing/measurement (product).

---

## 6. CMM — SEI Capability Maturity Model ⭐ (both "use of CMM" and "list the levels" have appeared)

**Use of CMM:** it helps a software organization **assess and improve the maturity of its software development process** — moving from ad-hoc/chaotic practices toward disciplined, measured, continuously-improving ones.

**The 5 Maturity Levels:**

| Level | Name | Characteristic |
|---|---|---|
| 1 | **Initial** | Ad hoc / chaotic; no formal procedures, no cost estimates, no real project plans |
| 2 | **Repeatable** | Basic project controls in place; intuitive methods used; can repeat earlier successes |
| 3 | **Defined** | Development process is formally defined and institutionalized org-wide |
| 4 | **Managed** | Process is measured quantitatively; a process database exists |
| 5 | **Optimizing** | Continuous process improvement via feedback and rigorous defect-cause analysis/prevention |

Quick mnemonic: **I-R-D-M-O** (Initial, Repeatable, Defined, Managed, Optimizing).

---

## 7. Extra Short-Answer Topics from your IA-1 (may resurface in mid-sem)

These came from your official `Assignment_1_SEPM` IA-1 question list — same professor's question style, so treat them as fair game:

**Process vs. Method**

| Process | Method |
|---|---|
| A set of activities performed in a specific order to achieve a goal | Specific techniques/tools/procedures used to perform the activities in a process |
| Broader / macro-level view | Detailed / micro-level view |
| Defines overall workflow and phases of development | Defines *how* to do the work |
| Examples: Waterfall, Agile, Spiral | Examples: UML, DFD, Testing techniques |

**Verification vs. Validation**

| Verification | Validation |
|---|---|
| Answers: *"Are we building the product right?"* | Answers: *"Are we building the right product?"* |
| Checks product against specifications/standards | Checks product against actual user needs/intended use |
| Done via reviews, inspections | Done via system testing, user testing |
| Mostly static — no code execution | Dynamic — involves executing the code |

**Software Process** — a set of related activities, methods, practices, and work products used to develop, operate, and maintain software; provides a structured way to manage development and ensure quality within time/cost constraints.
Important features: an *ordered set of activities*, defined *inputs & outputs*, clear *roles & responsibilities*, *milestones & deliverables* for tracking progress, *repeatable & measurable*, *adaptable*.

**Two characteristics of software as a product**
- Software is **engineered/developed, not manufactured** — unlike hardware, there's no physical assembly; cost is dominated by intellectual/creative effort.
- Software is **portable** — the same code can move across platforms (unlike physical hardware).

**System Modeling** — the process of creating a simplified representation of a real-world system to understand, analyze, and design its structure, behaviour, and components *before* actual implementation.

**Factors to consider during system modeling:** define system boundary; identify inputs & outputs; identify major components/subsystems; specify data & control flow; consider performance, reliability & security requirements; model system behaviour; validate the model against user requirements.

**System Engineering Hierarchy** — a structured view showing abstraction levels from highest to lowest:
```
System → Subsystem → Component → Module → Object/Class
```
(System = complete system; Subsystem = major part of the system; Component = small functional unit; Module = implementation unit; Object/Class = basic building block.) Ensures proper decomposition, modularity, and manageability during system development.

**Functions of Data Architecture** — data integration (unify data from multiple sources); data storage (define how data is stored/organized for efficient access); data modeling (structure data to ensure consistency, reduce redundancy); data quality & governance (accuracy, consistency, security, compliance); access & performance (optimize retrieval, support analytics/real-time processing); scalability & flexibility (handle growing data volume, adapt to new business needs/tech).

---

## 8. Diagrams You Should Practice Drawing (neat sketches score CO marks!)

1. Classical Waterfall Model (linear phase list, Section 2.1)
2. Iterative Waterfall Model (same phases + feedback arrows going *backward*)
3. Prototyping Model (loop: gather → quick design → build → evaluate → refine, then → real waterfall)
4. Spiral Model (spiral with 4 labelled quadrants)
5. Requirements Engineering Process (Section 3.1)
6. SQA "umbrella" diagram (Section 5)
7. System Engineering Hierarchy triangle (Section 7)

---

## 9. Full Text of Past Papers (for reference)

### 2025 Mid-Sem (25 marks, 1 hour) — CO1, CO2, CO3
**Section A (all compulsory, 1 mark each)**
a) What is meant by Software and Software Engineering?
b) Define process in the context of software quality?
c) List the task regions in the Spiral model.
d) What is the use of CMM?
e) What is meant by Software and Software Engineering? *(repeated as printed)*

**Section B (answer any 2, 10 marks each)**
a) Draw the schematic diagram to represent the Classical waterfall model in the SDLC.
b) Explain requirements engineering processes with a suitable diagram.
c) What is meant by software configuration management? Explain the two principal activities of configuration management.

### 2024 Mid-Sem (50 marks, 2 hours) — CO1, CO2, CO3
**Section A (all compulsory, 1 mark each)**
a) What are the challenges in software?
b) What is the prime objective of software engineering?
c) What is known as SRS review?
d) What is meant by software prototyping?
e) What is software quality and how do we measure it?

**Section B (answer any 3, 15 marks each)**
a) Explain the iterative waterfall and spiral model for the software life cycle and discuss various activities in each phase.
b) Explain the following: (i) waterfall model (ii) RAD model (iii) Prototyping model.
c) Explain the main activities used in requirements engineering. What are the desirable characteristics of good SRS documents? Explain with an example.
d) What is meant by software configuration management? Explain software quality assurance.

---

## 10. Suggested Revision Plan

**Pass 1 — Core models (do first, highest weight):** Sections 2.1–2.6 — be able to draw every diagram from memory and state 3–4 bullet points per model (definition, phases/steps, advantages, disadvantages/when to use).

**Pass 2 — Requirements & SRS:** Section 3 — memorize the 6 SRS properties and be able to explain the RE process diagram end-to-end with a small example (like the ATM withdraw-cash or library search example from your notes).

**Pass 3 — Umbrella activities:** Sections 4–6 — SCM's two principal activities, SQA's umbrella diagram + quality attributes, CMM's 5 levels. These two topics (SCM + SQA) have appeared in **every single Section B** so far — do not skip.

**Pass 4 — Section A speed round:** Go through Section 0's bullet list and the IA-1 table (Section 7) and time yourself writing 1–2 line answers for each — Section A is easy marks if you're fast and precise.

**Pass 5 — Mock test:** Attempt the 2024 paper cold (50 marks / 2 hrs) under time pressure, then check yourself against this guide.

Good luck! 🎓
