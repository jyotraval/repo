# Complete Mid-Semester Exam Preparation Kit
**Course Name:** Software Engineering and Project Management (SEPM)  
**Course Code:** 23IC401T | **Duration:** 1 Hour | **Max Marks:** 25 Marks  
**Target Syllabus:** Unit I (Life Cycle Models, Requirements Engineering, Agile, Structured & OO Design) & Unit II (SQA, SCM, Software Metrics, CMM/PCMM)

---

## Part 1: Exam Structure & Scoring Strategy

The 25-mark examination follows a strict format:
* **Section A (5 Marks):** 5 compulsory short-answer questions (1 mark each).  
  *Strategy:* State the exact technical definition, IEEE standard phrasing, or direct bullet points. Keep answers within 2–4 high-impact lines.
* **Section B (20 Marks):** Answer **any 2 out of 3** long-answer questions (10 marks each).  
  *Strategy:* Every 10-mark question requires a clean, labeled schematic diagram, step-by-step phase breakdowns, advantages/disadvantages, and practical industry examples.

```
                  ┌────────────────────────────────────────┐
                  │      25 MARKS MID-SEM EXAM GRID        │
                  ├───────────────────┬────────────────────┤
                  │ Section A: 5 M    │ Section B: 20 M    │
                  │ (5 x 1M = 5 Marks)│ (2 x 10M = 20 Marks│
                  │ Short, crisp defs │ Diagram + Phases + │
                  │ & exact keywords  │ Deep Explanation   │
                  └───────────────────┴────────────────────┘
```

---

## Part 2: High-Yield Section A Rapid-Fire Bank (1-Mark Questions)

### Q1. Define Software and Software Engineering (IEEE Definition).
* **Software:** A collection of executable programming code, associated libraries, configuration files, and related documentation that fulfills specific user requirements.
* **Software Engineering (IEEE):** *"The application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software; that is, the application of engineering to software."*

### Q2. What is the prime objective of software engineering?
To deliver high-quality, reliable, maintainable, and scalable software products cost-effectively and on schedule, utilizing proven scientific principles, methodologies, and systematic processes.

### Q3. Define "Process" in the context of software quality.
A software process is a structured sequence of identifiable activities, practices, methods, and transformations used by an organization to develop and maintain software. In software quality, an institutionalized process ensures consistent product attributes, phase containment of errors, and continuous improvement.

### Q4. List the four task regions (quadrants) of the Spiral Model.
1. **First Quadrant:** Objective Setting (Determine objectives, alternatives, and operational constraints).
2. **Second Quadrant:** Risk Assessment and Reduction (Identify, evaluate risks, and build prototypes).
3. **Third Quadrant:** Development and Validation (Engineer, test, and verify the next-level product).
4. **Fourth Quadrant:** Review and Planning (Customer evaluation of the increment and planning for the next spiral cycle).

### Q5. What is the use of SEI's Capability Maturity Model (CMM)?
CMM provides a structured, 5-level evolutionary roadmap to assess an organization's software development process maturity, establish process controls, and drive continuous software process improvement.

### Q6. What is known as an SRS Review?
An SRS review is a formal technical inspection/walkthrough conducted jointly by system analysts, developers, customers, and domain experts to detect and eliminate ambiguities, contradictions, omissions, and inconsistencies in the Software Requirements Specification document before the design phase begins.

### Q7. What is meant by Software Prototyping?
A prototype is a toy, limited-capability implementation of a software system built rapidly using shortcuts (such as table lookups or dummy modules). It is used to demonstrate user interfaces, clarify unclear requirements, and resolve underlying technical risks.

### Q8. What is Software Quality, and how is it measured?
* **Definition:** Software quality is the degree to which a software system satisfies both its explicit functional requirements and its implicit non-functional quality attributes (maintainability, reliability, usability, efficiency).
* **Measurement:** It is measured through **internal metrics** (e.g., Cyclomatic Complexity, Lines of Code, Halstead's Volume) and **external metrics** (e.g., defect density, mean time to failure [MTTF], customer change-request rate).

### Q9. What are the two fundamental techniques used in SE to handle problem complexity?
1. **Abstraction:** Simplifying a problem by suppressing irrelevant details and concentrating only on aspects relevant to the current objective (model building).
2. **Decomposition:** Dividing a complex system into smaller, highly independent, manageable sub-components that can be solved and verified separately (divide-and-conquer).

### Q10. What is "Phase Containment of Errors"?
The quality engineering principle of detecting and correcting defects in the exact same life cycle phase in which they are introduced, preventing defects from leaking downstream where rectification costs increase exponentially (e.g., $1.0\times$ in Requirements vs. $80\text{–}130\times$ in Field Use).

### Q11. Define System Modeling.
System modeling is the process of constructing abstract graphical, textual, or mathematical representations of a real-world system to analyze its context, behavior, structures, and data flows prior to coding and physical implementation.

### Q12. State the System Engineering Hierarchy.
The hierarchy decomposes systems from the broadest context down to the foundational implementation constructs:
$$\text{System} \longrightarrow \text{Subsystems} \longrightarrow \text{Components} \longrightarrow \text{Modules} \longrightarrow \text{Objects / Classes}$$

### Q13. List the 5 maturity levels of SEI-CMM.
* **Level 1:** Initial (Ad-hoc, chaotic, undisciplined)
* **Level 2:** Repeatable (Basic project tracking and management controls)
* **Level 3:** Defined (Processes documented, standardized, and institutionalized)
* **Level 4:** Managed (Quantitative process measurements and metrics database)
* **Level 5:** Optimizing (Continuous process improvement and defect-cause prevention)

### Q14. Distinguish between a Process and a Method.
* **Process:** A macro-level framework defining the overall life cycle workflow, milestones, phases, deliverables, and entry/exit criteria (e.g., Waterfall, Agile, Spiral).
* **Method:** A micro-level technical procedure, notation, or guideline applied to perform an activity within a process (e.g., UML diagrams, Data Flow Diagrams, Boundary Value Analysis).

### Q15. Define Verification and Validation in one line each (Boehm's aphorism).
* **Verification:** *"Are we building the product right?"* (Checking work products statically against specifications via reviews/walkthroughs).
* **Validation:** *"Are we building the right product?"* (Dynamically executing software to ensure it satisfies user needs and intended operational use).

---

## Part 3: Core Section B Master Blueprints (10-Mark Questions)

---

### Topic 1: Classical Waterfall Model vs. Iterative Waterfall Model

#### 1. Classical Waterfall Model (Theoretical Model)
* **Concept:** Proposed as the earliest, most intuitive sequential SDLC. It divides development into strictly linear, non-overlapping stages. Each phase begins only after the preceding phase completes and meets its exit criteria.

```
  ┌─────────────────────────┐
  │    Feasibility Study    │
  └───────────┬─────────────┘
              ▼
  ┌─────────────────────────┐
  │ Requirements Analysis   │
  │    & Specification      │
  └───────────┬─────────────┘
              ▼
  ┌─────────────────────────┐
  │      System Design      │
  └───────────┬─────────────┘
              ▼
  ┌─────────────────────────┐
  │  Coding & Unit Testing  │
  └───────────┬─────────────┘
              ▼
  ┌─────────────────────────┐
  │  Integration & System   │
  │         Testing         │
  └───────────┬─────────────┘
              ▼
  ┌─────────────────────────┐
  │       Maintenance       │
  └─────────────────────────┘
```

#### Detailed Phase Activities:
1. **Feasibility Study:** Investigates technical, economic (cost/benefit), and operational feasibility. Evaluates whether the product meets business justification (ROI) and team capability. Output: *Feasibility Report*.
2. **Requirements Analysis & Specification:** 
   * *Requirements Gathering & Analysis:* Collect data from stakeholders, resolve contradictions/ambiguities.
   * *Requirements Specification:* Systematically document system features into an SRS (Software Requirements Specification) covering functional, non-functional, and implementation constraints.
3. **Design:** Transforms the SRS into an architectural model and detailed logic. Derives data structures, algorithms, module interfaces, and interaction flows. Divided into *High-Level Design (modules)* and *Detailed Design (algorithms/data structures)*.
4. **Coding & Unit Testing:** Translates module designs into compilable code using a programming language. Each module is tested in total isolation to ensure correct logic.
5. **Integration & System Testing:** Integrates individual units incrementally according to an integration plan. Tests interfaces, end-to-end user journeys, performance, and SRS conformance ($\alpha$-testing, $\beta$-testing, acceptance testing).
6. **Maintenance:** Consumes roughly **60%** of life cycle effort. Divided into:
   * *Corrective Maintenance:* Bug fixes not found during testing.
   * *Perfective Maintenance:* Modifying code to add new user capabilities.
   * *Adaptive Maintenance:* Porting software to new operating environments (OS/hardware).

#### Major Shortcoming:
* **Idealistic & Rigid:** It assumes engineers commit zero errors during design/coding. In practice, defects inevitably surface later, requiring backwards iterations that this model does not support.

---

#### 2. Iterative Waterfall Model (Practical Standard)
To overcome the inability to correct defects discovered downstream, feedback paths are engineered between adjacent phases.

```
  ┌─────────────────────────┐
  │    Feasibility Study    │◄──────┐
  └───────────┬─────────────┘       │
              ▼                     │
  ┌─────────────────────────┐       │
  │ Requirements Analysis   │◄────┐ │
  └───────────┬─────────────┘     │ │ Feedback
              ▼                   │ │ Paths
  ┌─────────────────────────┐     │ │ for Defect
  │      System Design      │◄──┐ │ │ Correction
  └───────────┬─────────────┘   │ │ │
              ▼                 │ │ │
  ┌─────────────────────────┐   │ │ │
  │  Coding & Unit Testing  │◄┐ │ │ │
  └───────────┬─────────────┘ │ │ │ │
              ▼               │ │ │ │
  ┌─────────────────────────┐ │ │ │ │
  │  Integration & System   ├─┴─┴─┴─┘
  │         Testing         │
  └───────────┬─────────────┘
              ▼
  ┌─────────────────────────┐
  │       Maintenance       │
  └─────────────────────────┘
```

* **Feedback Paths:** When defects are identified during integration or unit testing, developers backtrack to earlier stages (e.g., redesigning a component or re-specifying an ambiguous feature).
* **Phase Containment of Errors:** Emphasizes reviews at each stage (SRS review, design review, code walkthroughs) so defects are intercepted early, minimizing rework costs.

---

### Topic 2: Spiral Model (Boehm's Meta-Model & Risk-Driven Development)

* **Origin:** Proposed by Barry Boehm in 1988.
* **Why is it called a Meta-Model?** It encompasses and subsumes other life cycle models. A single-loop spiral represents the Classical Waterfall; multiple loops represent evolutionary/incremental delivery; each cycle incorporates prototyping to eliminate risks.
* **Structure:** Represented as a spiral with a variable number of loops (not fixed). The radius represents cumulative cost; the angular degree represents progress made.

```
                           Quadrant 1:                       Quadrant 2:
                        OBJECTIVE SETTING            RISK ASSESSMENT & REDUCTION
                                      │
                 Determine Objectives,│    Identify Risks,
                 Alternatives, and    │    Evaluate Alternatives,
                 Constraints          │    Resolve through Prototyping
                                      │           . 
                                      │         .   .
                                      │       .       .
               ───────────────────────┼───────.───────.────────►
                                      │     .           .
                                      │    .             .
                 Review Results with  │   .   Develop & Validate
                 Customer, Plan Next  │  .    Next-Level Product
                 Phase / Loop         │ .
                                      │
                           Quadrant 4:                       Quadrant 3:
                        REVIEW & PLANNING             DEVELOPMENT & VALIDATION
```

#### Detailed Quadrant Operations:
1. **First Quadrant (Objective Setting):**
   * Identify specific phase objectives (e.g., performance targets, scope boundaries).
   * Identify operational constraints (budget, deadline, interfaces) and identify alternative execution strategies.
2. **Second Quadrant (Risk Assessment and Reduction):**
   * Detailed analysis of project, technical, and commercial risks.
   * Apply mitigation techniques: if requirements are ambiguous, develop a rapid prototype; if hardware controller speed is unknown, perform simulation benchmark tests.
3. **Third Quadrant (Development and Validation):**
   * Develop and test the chosen increment of the product.
   * If technical risks are cleared via prototyping, execution may follow a standard waterfall or evolutionary cycle for that increment.
4. **Fourth Quadrant (Review and Planning):**
   * Evaluate results achieved to date with the customer.
   * Decide on a **Go/No-Go** checkpoint: if risks are too severe, terminate the project. If viable, plan resource commitments for the next spiral loop.

* **Best Suited For:** Large-scale, high-budget, technically complex, safety-critical, and risk-prone systems.  
* **Drawback:** Demands specialized risk-assessment expertise; excessive overhead for routine, small-scale projects.

---

### Topic 3: Software Prototyping & RAD Models

#### 1. Prototyping Model
* **Mechanism:** When user requirements are ambiguous or technical approaches untried, a throwaway prototype is constructed before full development begins.

```
       ┌───────────────────────────────┐
       │     Requirements Gathering    │
       └──────────────┬────────────────┘
                      ▼
       ┌───────────────────────────────┐
       │         Quick Design          │
       └──────────────┬────────────────┘
                      ▼
       ┌───────────────────────────────┐
  ┌───►│       Build Prototype         │
  │    └──────────────┬────────────────┘
  │                   ▼
  │    ┌───────────────────────────────┐
  │    │      Customer Evaluation      │
  │    └──────────────┬────────────────┘
  │                   ▼
  └─── No ── [Customer Satisfied?]
                      │ Yes
                      ▼
       ┌───────────────────────────────┐
       │ Standard Engineering Lifecycle│
       │ (Design -> Code -> Test -> MT)│
       └───────────────────────────────┘
```

* **Shortcuts Employed:** Inefficient algorithms, mock data lookups, and unoptimized GUI mockups.
* **Fate of the Prototype:** It is thrown away; the experience gained forms the baseline of the verified SRS document.

#### 2. Rapid Application Development (RAD)
* A high-speed adaptation of the linear sequential model where essential features are developed in short, strict **time-boxes** (usually 60–90 days).
* Relies on **heavy reuse** of pre-built code components, commercial off-the-shelf (COTS) libraries, visual graphical modeling tools, and automated code generators.
* Unlike the Prototyping model (where code is thrown away), the RAD prototype iteratively **evolves directly into the production software**.

#### Direct Comparison Matrix: Prototyping vs. RAD vs. Iterative Waterfall

| Parameter | Prototyping Model | RAD Model | Iterative Waterfall |
| :--- | :--- | :--- | :--- |
| **Primary Goal** | Clarify ambiguous requirements & technical risks | Minimize time-to-market using rapid toolsets | Systematic, disciplined engineering |
| **Fate of Prototype** | Thrown away (*throwaway prototype*) | Evolved into the final deliverable | No prototype (final code written directly) |
| **Component Reuse** | Low / Negligible | Very High (APIs, reusable modules) | Moderate |
| **Documentation** | Low during prototyping phase | Low / Minimal (time-constrained) | Very High, formal, and structured |
| **System Quality** | High (since real system built fresh) | Poorer performance and reliability | High quality and reliability |

---

### Topic 4: Requirements Engineering & SRS Document

#### 1. Requirements Engineering Workflow

```
   ┌─────────────────────────────────────────────────────────────┐
   │ 1. Requirements Gathering (Elicitation)                     │
   │    Interviews, questionnaires, domain research, user stories│
   └──────────────────────────────┬──────────────────────────────┘
                                  ▼
   ┌─────────────────────────────────────────────────────────────┐
   │ 2. Requirements Analysis                                    │
   │    Detect & resolve ambiguities, conflicts, incompleteness  │
   └──────────────────────────────┬──────────────────────────────┘
                                  ▼
   ┌─────────────────────────────────────────────────────────────┐
   │ 3. Requirements Specification                               │
   │    Formalization into the standard SRS Document              │
   └──────────────────────────────┬──────────────────────────────┘
                                  ▼
   ┌─────────────────────────────────────────────────────────────┐
   │ 4. Requirements Validation & Review                         │
   │    Formal review meetings, traceability checks, sign-off    │
   └─────────────────────────────────────────────────────────────┘
```

#### 2. Components of an SRS Document
* **Functional Requirements:** Explicit high-level system functions $\{f_i\}$ mapping input data sets $(i_k)$ to output data sets $(o_k)$.
* **Non-Functional Requirements:** Qualitative constraints including system performance, reliability, security, safety, maintainability, and portability.
* **Goals of Implementation:** General guidelines for developers regarding future expansions, target hardware architectures, and planned technology migration paths.

#### 3. Desirable Properties of an SRS Document
1. **Concise:** Free of redundant, wordy, or irrelevant technical discussions.
2. **Unambiguous:** Every requirement has exactly one distinct interpretation.
3. **Consistent:** Requirements do not contradict one another.
4. **Complete:** Specifies all possible inputs, outputs, and system responses under both standard and exceptional conditions.
5. **Black-Box View:** Documents *what* the system must do without stating *how* to implement it algorithmically.
6. **Verifiable:** Every listed requirement must be quantifiable such that a concrete test case can prove its compliance.
7. **Traceable:** Easy to link to design components and code modules through unique identifiers.

#### 4. Practical SRS Example: Automated Teller Machine (ATM)
* **Requirement R1:** *Withdraw Cash Function*
  * **Input:** User ATM card PIN, selection of account type, integer withdrawal amount (must be multiple of 100, $100 \le \text{amount} \le 10,000$).
  * **Processing:** System validates PIN against the core banking server. Verifies account balance $\ge \text{withdrawal amount}$. If satisfied, debits the account and directs the dispenser unit.
  * **Output:** Cash dispensed, printed receipt, and updated balance displayed.
  * **Exception Condition:** If balance is insufficient, eject card, output "Insufficient Funds" error, and abort transaction without debiting.

---

### Topic 5: Software Configuration Management (SCM)

* **Definition:** An umbrella quality control activity executed across the entire software development life cycle to systematically manage, control, audit, and track changes to all project artifacts.
* **Configuration Item (CI):** Any work product placed under configuration control (e.g., project plan, SRS, design documents, source code files, test suite cases, user manuals).

```
                    ┌─────────────────────────┐
                    │ Configuration Item (CI) │
                    └────────────┬────────────┘
                                 │
                     Formal Inspection & Review
                                 │
                                 ▼
                     ┌───────────────────────┐
                     │   BASELINED STATE     │
                     └───────────┬───────────┘
                                 │
                      Locked in Project Library
                                 │
         ┌───────────────────────┴───────────────────────┐
         │ Check-out                                     │
         ▼                                               ▼
┌──────────────────┐                           ┌──────────────────┐
│Developer Sandbox │                           │  Change Control  │
│(Modifications)   │                           │  Board (CCB)     │
└────────┬─────────┘                           └──────────────────┘
         │
    Review & SQA
         │
         ▼ Check-in
┌──────────────────┐
│ New Version (CI) │
└──────────────────┘
```

#### The Two Principal Activities of Configuration Management:

#### 1. Version Control (Work Products Tracking)
* Manages multiple iterations of evolving CIs throughout the life cycle.
* **Key Terminologies:**
  * *Version:* An instance of a CI created by modifying an existing item, usually applied in a linear timeline to incorporate bug fixes or functional extensions ($v1.0 \rightarrow v1.1 \rightarrow v2.0$).
  * *Branch:* An independent development path split off from the main trunk to enable concurrent feature work without destabilizing the mainline codebase.
  * *Variant:* Co-existing versions of a software product tailored for different operational targets (e.g., *Product A for Linux* vs. *Product A for Windows*).
* **Storage Environment:** Managed using a tiered **Software Library** containing:
  1. *Developer Workspace (Private):* Work-in-progress, unreviewed code.
  2. *Master Directory (Controlled):* Formally accepted CIs under active tracking.
  3. *Software Repository (Static):* Baselined, delivered customer release archives.

#### 2. Change Control (Workflow Governance)
* Prevents uncontrolled change, which leads to "project chaos."
* **Step-by-Step Change Control Procedure:**
  1. **Change Request Submission:** A stakeholder or engineer submits a formal Change Request (CR) specifying defect details or required modifications.
  2. **Technical & Business Evaluation:** The Change Control Authority (CCA) / Change Control Board (CCB) evaluates the impact on cost, system stability, and project schedule.
  3. **Engineering Change Order (ECO):** If approved, an ECO is formally issued authorizing the checkout of the baselined CI.
  4. **Check-Out & Modification:** The developer checks out the CI into their local sandbox and modifies it.
  5. **Review, SQA & Check-In:** The modified item undergoes formal technical review and regression testing. Upon passing, it is checked back into the software library with an incremented version number.
  6. **Configuration Audit & Status Reporting:** Verifies that changes match the ECO specification and updates the status log (noting *who changed what, when, and why*).

---

### Topic 6: Software Design — Structured vs. Object-Oriented Design

#### 1. Structured Design
* Employs structured analysis using **Data Flow Diagrams (DFDs)** and translates them into **Structure Charts** via Transform or Transaction Analysis.

```
       DFD SYMBOLS:
   ┌───────────────┐          (  Process  )         ═════════════════
   │External Entity│          (  Bubble   )         ═══ Data Store═══
   └───────┬───────┘          (───────────)         ═════════════════
           │                        ▲
           └────── Data Flow ───────┘
```

* **DFD Balancing:** A critical rule where the aggregate input and output data flows crossing the boundary of a parent process bubble must balance precisely with the incoming and outgoing flows of its decomposed lower-level DFD child diagram.

```
                       BALANCED DECOMPOSITION:

   Level 1:                                 Level 2 (Decomposition of P1):
      d1                                          d1
      ───►(  P1  )───► d2                         ───►( P1.1 )──┐
          (      )                                    (      )  │ d12
                                                                ▼
                                                      ( P1.2 )◄─┘
                                                      (      )───► d2
```

* **Structure Chart Building Blocks:**
  * *Rectangular Box:* Represents a module.
  * *Invocation Arrow:* Represents control flow from caller to callee.
  * *Annotated Small Arrow:* Represents parameter data flow between modules.
  * *Diamond Symbol:* Represents conditional module execution (selection).
  * *Curved Loop Arrow:* Represents repeated execution of subordinate modules (repetition).

#### 2. Modularity Metrics: Cohesion and Coupling

```
                ┌──────────────────────────────────────────────┐
                │          MODULARITY DESIGN GOAL:             │
                │     HIGH COHESION  &  LOW COUPLING           │
                └──────────────────────────────────────────────┘
```

#### Cohesion (Intra-Module Strength): Ranked from Worst (1) to Best (7)
1. **Coincidental (Lowest/Worst):** Modules perform tasks that have no meaningful relationship to each other (random bundling).
2. **Logical:** Elements perform operations of similar logical category (e.g., an error-handling routine that handles all system errors regardless of context).
3. **Temporal:** Tasks are grouped together purely because they execute during the same phase of program execution (e.g., `startup_initialization()`).
4. **Procedural:** Functions are grouped because they follow a specific sequential sequence of execution, although they work on different data.
5. **Communicational:** Functions operate on the same shared input or output data set (e.g., `print_and_save_report()`).
6. **Sequential:** The output of one functional activity forms the direct input to the next internal activity (assembly pipeline).
7. **Functional (Highest/Best):** All elements in the module cooperate to execute exactly one well-defined computational task (e.g., `compute_sine()`).

#### Coupling (Inter-Module Interdependence): Ranked from Worst (1) to Best (5)
1. **Content Coupling (Highest/Worst):** One module directly accesses, points to, or modifies the private code or internal data of another module.
2. **Common Coupling:** Multiple modules share unrestricted read/write access to the same global data space.
3. **Control Coupling:** One module explicitly controls the flow of another by passing control flags/switches.
4. **Stamp Coupling:** Modules share an entire aggregate composite data structure (e.g., passing a complete Record struct when the function only needs one integer field).
5. **Data Coupling (Lowest/Best):** Modules communicate strictly through parameters consisting of primitive data items (e.g., integers, floats).

---

#### 3. Object-Oriented Design: Associations, Aggregation, and Composition

```
  1. ASSOCIATION: Weak, independent relationship (Line)
     ┌──────────────┐                  ┌──────────────┐
     │Library Member│ 1 ──────────── * │     Book     │
     └──────────────┘                  └──────────────┘

  2. AGGREGATION: Shared "has-a" relationship (Hollow Diamond)
     ┌──────────────┐                  ┌──────────────┐
     │  Classroom   │ ◇───────────── * │    Chair     │
     └──────────────┘                  └──────────────┘

  3. COMPOSITION: Strong "part-of" life-cycle binding (Filled Diamond)
     ┌──────────────┐                  ┌──────────────┐
     │   Invoice    │ ◆───────────── * │ Invoice Item │
     └──────────────┘                  └──────────────┘
```

* **Aggregation:** An open/hollow diamond denotes shared ownership. The parts can exist independently of the whole. (If the classroom is decommissioned, the chairs are not destroyed).
* **Composition:** A filled diamond denotes strict exclusive containment. The lifetime of the part is tied directly to the lifetime of the whole. (If the invoice object is deleted, its invoice items are destroyed immediately).

---

### Topic 7: Software Quality Assurance (SQA) & SEI-CMM

#### 1. Bersoff's Definition of SQA
*"Quality assurance consists of those procedures, techniques, and tools applied by professionals to ensure that a product meets or exceeds pre-specified standards during its development cycle."*

#### 2. The 4 P’s of Software Engineering Quality

```
                          ┌─────────────┐
                          │   PEOPLE    │
                          └──────┬──────┘
                                 │ participate
                                 ▼
    ┌─────────────┐  template ┌─────────────┐   result   ┌─────────────┐
    │   PROCESS   ├──────────►│   PROJECT   ├───────────►│   PRODUCT   │
    └─────────────┘           └─────────────┘            └─────────────┘
      (Activities)               (Management)              (Artifacts)
```

1. **People:** The skill, education, training, and experience of the engineering staff.
2. **Process:** The formalized life cycle activities, standards, templates, and methodologies guiding execution.
3. **Project:** Day-to-day managerial supervision, resource allocation, and tracking.
4. **Product:** The tangible deliverables (documents, architectures, code, test suites).

#### 3. Software Metrics Breakdown
* **Control Metrics:** Measure the process flow to guide planning and budget management (e.g., effort expended, person-months, actual cost vs. projected budget).
* **Predictor Metrics:** Measure internal attributes to forecast external quality before product release.
  * *Internal Attribute:* Directly measurable from the codebase itself (e.g., Cyclomatic Complexity, Lines of Code).
  * *External Attribute:* Properties discoverable only after deployment (e.g., maintainability, operational reliability).

#### 4. SEI Capability Maturity Model (CMM) 5-Level Architecture

```
 Level 5: OPTIMIZING   ── Focus on continuous process improvement & defect prevention
         ▲
 Level 4: MANAGED      ── Quantitative measurement & software process database
         ▲
 Level 3: DEFINED      ── Standardized, institutionalized organizational engineering processes
         ▲
 Level 2: REPEATABLE   ── Basic project management, cost/schedule controls
         ▲
 Level 1: INITIAL      ── Ad-hoc, chaotic, heroic efforts, unstandardized
```

* **Level 1 (Initial):** No formalized procedures. Project success relies entirely on exceptional individual efforts. Unpredictable costs and schedules.
* **Level 2 (Repeatable):** Basic project management controls implemented. Past successes can be repeated on similar applications. Tracking of cost, schedule, and baseline functionality.
* **Level 3 (Defined):** The organization has fully documented, standardized, and institutionalized software engineering processes across all departments. Training programs exist.
* **Level 4 (Managed):** Software processes and product quality are measured quantitatively. A comprehensive metrics database is maintained to establish predictability.
* **Level 5 (Optimizing):** Focus is shifted to continuous improvement. Statistical feedback mechanisms and root-cause defect analysis are used to refine and improve the processes.

---

## Part 4: Complete Solutions to Assignment-1 & Previous Year Exams

### Solutions to Internal Assignment-1 (Dr. Deepak Sahu)

#### 1. What is the prime objective of software engineering? (CO1)
The primary objective of software engineering is to systematically build high-quality, reliable, scalable, and maintainable software products within specified timeframes and budgetary allocations, using defined engineering principles and methodologies.

#### 2. Define software engineering paradigm. (CO1)
A software engineering paradigm is an overarching framework of development practices, life cycle models, scientific methods, and structured tools that provides an end-to-end roadmap for building software—from initial requirements gathering through to final post-delivery maintenance.

#### 3. What do you mean by spiral model? (CO1)
The Spiral Model, proposed by Barry Boehm in 1988, is an evolutionary, risk-driven SDLC meta-model. It structures a project into an adaptable number of loops, each split into four quadrants: Objective Setting, Risk Assessment & Reduction (via prototyping), Development & Validation, and Customer Review/Planning.

#### 4. Write a brief note on waterfall model. (CO1)
The Waterfall model is a classical, linear-sequential software process model that moves strictly downhill through consecutive phases: Feasibility Study $\rightarrow$ Requirements Analysis & Specification $\rightarrow$ System Design $\rightarrow$ Coding & Unit Testing $\rightarrow$ Integration & System Testing $\rightarrow$ Maintenance. It is easy to manage due to clear phase milestones, but it does not support defect-correction feedback loops or changing user requirements.

#### 5. Distinguish between process and methods. (CO1)
* **Process:** The macro-level engineering structure and timeline that outlines *what* activities must be executed, their sequence, deliverables, and exit criteria (e.g., Agile, Iterative Waterfall).
* **Method:** The micro-level technical approach, discipline, or notation specifying *how* to perform a particular development task within a process (e.g., Object-Oriented Analysis, DFD creation, White-Box Testing).

#### 6. Give the importance of software engineering. (CO1)
* **Complexity Control:** Leverages abstraction and decomposition to prevent development effort from growing exponentially with program size.
* **High Reliability & Quality:** Replaces undisciplined "build-and-fix" hacking with formal verification and validation activities.
* **Cost & Schedule Containment:** Reduces maintenance effort, which historically accounts for roughly 60% of total lifetime software costs.
* **Team Scalability:** Provides milestones and deliverables so large teams can collaborate without project failure.

#### 7. Define software process. State the important features of a process. (CO2)
* **Definition:** A software process is a collection of activities, methods, practices, and transformations that engineers use to develop and maintain software and its related artifacts.
* **Important Features:**
  1. *Predictability:* Establishes entry and exit criteria for each phase.
  2. *Measurability:* Enables tracking of milestones, cost, and defect counts.
  3. *Repeatability:* Allows an organization to reproduce project successes across different teams.
  4. *Evolutionary Improvement:* Can be tailored and refined through feedback.

#### 8. Write any two characteristics of software as a product. (CO2)
1. **Software is Engineered, Not Manufactured:** Software does not require raw material assembly or factory stamping. Its primary costs reside in intellectual design and development rather than downstream reproduction.
2. **Software Does Not "Wear Out":** Unlike hardware, software does not suffer from mechanical friction or environmental degradation. Failures stem from uncorrected design defects or changing environmental requirements.

#### 9. List the process maturity levels in SEI's CMM. (CO5)
Level 1: Initial | Level 2: Repeatable | Level 3: Defined | Level 4: Managed | Level 5: Optimizing.

#### 10. Distinguish clearly between verification & validation. (CO5)
| Dimension | Verification | Validation |
| :--- | :--- | :--- |
| **Core Question** | *"Are we building the product right?"* | *"Are we building the right product?"* |
| **Activity Type** | Static evaluation (Walkthroughs, reviews, inspections). | Dynamic execution (Functional testing, field validation). |
| **Focus** | Conformance to specifications and standards. | Conformance to user operational needs and expectations. |
| **Execution** | Done without running software code. | Requires running executable builds. |

#### 11. What are the functions of data architecture? (CO2)
1. *Data Integration:* Unifying data sets from heterogeneous business operational sources into a standardized model.
2. *Storage Optimization:* Defining efficient persistence schemas (relational, non-relational) for fast retrieval.
3. *Data Modeling & Integrity:* Specifying entities, relationships, constraints, and dictionaries to eliminate redundancy.
4. *Governance & Security:* Establishing access control rules, encryption, and regulatory compliance policies.

#### 12. Define System Modeling. (CO3)
System modeling is the process of generating abstract visual representations (such as DFDs, Use Case Models, or State Charts) to analyze, communicate, and document the behavioral and structural properties of a system without exposing implementation source code.

#### 13. State the System Engineering Hierarchy. (CO2)
$$\text{System} \longrightarrow \text{Subsystems} \longrightarrow \text{Components} \longrightarrow \text{Modules} \longrightarrow \text{Objects / Classes}$$
*(Decomposes top-level system context down to unit-level modules to ensure structured problem solving).*

#### 14. Mention some of the factors to be considered during System Modeling. (CO3)
* Definition of system boundary and external interfaces.
* Identification of external entities, input data, and output data sets.
* Mapping of data and control flows between processing nodes.
* Identification of non-functional performance and safety constraints.
* Selection of appropriate abstraction levels to keep diagrams readable (3 to 7 bubbles per DFD level).

#### 15. Define Verification & Validation. (CO5)
* **Verification:** The process of evaluating intermediate artifacts (SRS, design docs, code) to ensure they meet the prerequisites established by preceding life cycle phases.
* **Validation:** The process of evaluating the complete, executable software system at the end of the development cycle to verify it meets user requirements and business needs.

---

### Solutions to Mid-Semester Exam 2025 (Course Code: 23IC401T)

#### Section A Answers:
* **Que-1 (a) What is meant by Software and Software Engineering? [1M]**  
  *Refer to Part 2, Q1.*
* **Que-1 (b) Define process in the context of software quality? [1M]**  
  *Refer to Part 2, Q3.*
* **Que-1 (c) List the task regions in the Spiral model. [1M]**  
  *Refer to Part 2, Q4.*
* **Que-1 (d) What is the use of CMM? [1M]**  
  *Refer to Part 2, Q5.*
* **Que-1 (e) What is meant by Software and Software Engineering? [1M]**  
  *(Repeated question on the paper)* Provide the standard IEEE 610.12 definition to secure full credit: Application of a systematic, disciplined, quantifiable approach to development, operation, and maintenance of software.

#### Section B Detailed Answers (10 Marks Each):
* **Que-2 (a) Draw the schematic diagram to represent the Classical waterfall model in the software development life cycle. [10M]**  
  *Answer Plan:*
  1. Draw the linear-sequential downward block diagram (*Part 3, Topic 1*).
  2. Detail all 6 phases: Feasibility Study, Requirements Analysis & Specification, Design, Coding & Unit Testing, Integration & System Testing, Maintenance.
  3. Include the effort distribution breakdown: Maintenance accounts for ~60% of total life cycle effort, and Testing consumes the largest effort among development phases (~40–50%).
  4. Explain its idealistic nature and why it fails in real-world projects (lack of error correction feedback paths).
* **Que-2 (b) Explain requirements engineering processes with a suitable diagram. [10M]**  
  *Answer Plan:*
  1. Draw the 4-stage block diagram (*Part 3, Topic 4*).
  2. Elaborate on Stage 1 (Elicitation: Interviews, workshops), Stage 2 (Analysis: Removing inconsistencies and partial user viewpoints), Stage 3 (Specification: Functional, Non-functional, Goals of Implementation), and Stage 4 (Validation: SRS formal reviews).
  3. List the 7 properties of a quality SRS document (Concise, Unambiguous, Black-box view, Verifiable, etc.).
  4. Provide a practical example (e.g., ATM Cash Withdrawal).
* **Que-2 (c) What is meant by software configuration management? Explain the two principal activities of configuration management. [10M]**  
  *Answer Plan:*
  1. Provide the formal definition of SCM and explain Configuration Items (CIs) and Baselines (*Part 3, Topic 5*).
  2. Draw the CI baseline-to-library state diagram.
  3. Deeply explain Activity 1: **Version Control** (evolution graphs, versions vs. branches vs. variants, and the 3-tier software library: workspace, master directory, repository).
  4. Deeply explain Activity 2: **Change Control** (CR submission, CCB impact assessment, ECO generation, check-out/check-in protocol, SCM audits).

---

### Solutions to Mid-Semester Exam 2024 (Selected Questions)

* **Que-1 (a) What are the challenges in software? [1M]**  
  Exponential complexity growth with size, volatile requirement changes, high cost of defect removal downstream, maintaining legacy code, and managing multi-developer coordination without clear phase controls.
* **Que-1 (c) What is known as SRS review? [1M]**  
  *Refer to Part 2, Q6.*
* **Que-1 (d) What is meant by software prototyping? [1M]**  
  *Refer to Part 2, Q7.*
* **Que-2 (a) Explain iterative waterfall and spiral model with phase activities. [15M]**  
  Combine the detailed write-ups and diagrams of **Iterative Waterfall** (*Part 3, Topic 1*) and **Spiral Model** (*Part 3, Topic 2*).
* **Que-2 (b) Explain: (i) Waterfall model, (ii) RAD model, (iii) Prototyping model. [15M]**  
  Use the three models detailed in *Part 3, Topics 1 and 3*, including the direct comparison table.

---

## Part 5: Last-Minute Exam Cheat Sheet

### 1. Key Formulas & Ratios
* **Effort Distribution Ratio:**  
  $$\text{Development Effort} : \text{Maintenance Effort} \approx 40 : 60$$
* **Relative Cost of Fixing Defects:**  
  Requirements Phase $= 1.0 \times$ | Coding Phase $= 2.0 \times$ | Unit Testing $= 4.0 \times$ | Field Operation $= 80\text{–}130 \times$
* **Halstead's Metric:**  
  $$\text{Length } L = N_1 + N_2 \quad \vert \quad \text{Volume } V = L \times \log_2(n_1 + n_2)$$  
  *(where $n_1, n_2$ are unique operators and operands; $N_1, N_2$ are total operators and operands).*
* **Informational Complexity Metric:**  
  $$\text{Complexity} = \text{Length} \times (\text{Fan-in} \times \text{Fan-out})^2$$

### 2. Modularity Quick Check
* **Cohesion Hierarchy (Worst to Best):**  
  $$\text{Coincidental} < \text{Logical} < \text{Temporal} < \text{Procedural} < \text{Communicational} < \text{Sequential} < \mathbf{Functional}$$
* **Coupling Hierarchy (Worst to Best):**  
  $$\text{Content} > \text{Common} > \text{Control} > \text{Stamp} > \mathbf{Data}$$

### 3. Essential Diagrams Checklist
Review and be ready to reproduce:
* [ ] Classical Waterfall Model (6 sequential downward boxes)
* [ ] Iterative Waterfall Model (with backwards feedback loops)
* [ ] Spiral Model (4 quadrants: Objectives, Risks, Development, Review)
* [ ] Requirements Engineering Process (Elicitation $\rightarrow$ Analysis $\rightarrow$ Specification $\rightarrow$ Validation)
* [ ] SCM Baseline & Change Control Workflow (CR $\rightarrow$ CCB $\rightarrow$ ECO $\rightarrow$ Check-Out $\rightarrow$ Audit $\rightarrow$ Check-In)
* [ ] DFD Balancing Diagram (Level 1 Bubble vs. Level 2 Decomposition)
* [ ] V-Model (Left-hand development stages linked to right-hand testing stages)
