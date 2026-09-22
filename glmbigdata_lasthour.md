# Big Data Mid-Sem — LAST HOUR CRAM GUIDE
### Course Code: 20IC404T • 25 Marks • 1 Hour • You Did Nothing All Year

> **You have 60 minutes. This guide is structured minute-by-minute. Do NOT skip ahead. Follow the order. By minute 60 you'll have just enough to score 18–22 / 25.**

---

## MINUTE 0–2 — TRIAGE: WHAT'S COMING

The 2025 paper had 3 questions. The 2024 paper was 50 marks (also includes Spark/RDD/Pig — usually Unit-2). **Bet 100% on the 2025 pattern** because it's the most recent:

| Q | Marks | Topic | Time in exam |
|---|-------|-------|--------------|
| **Q1** | 8 (4×2) | Combiner • Checkpointing in HDFS • HBase vs RDBMS (2 diffs) • Schema-on-Read vs Write | 10 min |
| **Q2** | 7 | Hive: (a) create external table 3 marks • (b) LOAD OVERWRITE 2 marks • (c) CTAS managed table 2 marks | 15 min |
| **Q3** | 10 | **YARN components + workflow** (5+5) **OR** **HDFS architecture + write pipeline** (4+4+2) | 25 min |

**Strategy:** Master Q1 + Q2 first (15 easy marks), then drill ONE of the Q3 options (YARN is easier — fewer moving parts).

---

## MINUTE 2–10 — Q1a: COMBINER (2 marks)

**Memorize this answer verbatim:**

> The Combiner is a **local reducer** that runs on the output of the Mapper at the same node, **before the Shuffle & Sort phase**, to perform **local aggregation** of intermediate `<key, value>` pairs.
>
> Benefits:
> - Reduces memory and disk requirements of Map tasks.
> - Reduces network traffic between mappers and reducers.
>
> The Combiner's class is the **same as the Reducer's class**. It must be **associative and commutative** because the framework may call it 0, 1, or multiple times per key. It **cannot replace** the Reducer — the Reducer is still needed to aggregate across multiple mappers.

**Pipeline diagram (draw this):**
```
INPUT → MAP → COMBINER → SHUFFLE & SORT → REDUCE → OUTPUT
```

**Phase after which it is used:** After the Map phase, before Shuffle & Sort.

✅ **Done — move to Q1b.**

---

## MINUTE 10–16 — Q1b: WHY CHECKPOINTING IN HDFS (2 marks)

**Memorize:**

> The Primary NameNode keeps metadata in RAM for fast access. It logs every change to an **EditLog** file on disk and periodically saves a snapshot to an **FsImage** file. If the EditLog grows without bound, restarting the NameNode would take hours because every transaction must be replayed.
>
> **Checkpointing solves this:** The **Secondary NameNode** periodically:
> 1. **Fetches** the current FsImage + EditLog from the Primary NameNode.
> 2. **Merges** them in memory to create a new, updated FsImage (a *checkpoint*).
> 3. **Uploads** the new FsImage back to the Primary NameNode.
> 4. The Primary NameNode **truncates** the EditLog.
>
> Result: EditLog stays small → NameNode restart is fast.

**Key fact:** Secondary NameNode is **NOT a backup NameNode** — it cannot take over if Primary fails. (Standby NameNode in HA mode does that.)

✅ **Done — move to Q1c.**

---

## MINUTE 16–22 — Q1c: HBASE vs RDBMS (2 differences, 2 marks)

**Two differences to memorize:**

**Difference 1 — Storage orientation:**
- HBase is **column-oriented** (stores data column-family-wise).
- RDBMS is **row-oriented**.

**Difference 2 — Schema:**
- HBase is **schema-less** (only column families defined upfront; column qualifiers can vary per row).
- RDBMS has a **fixed, rigid schema** (every row must conform; adding a column requires `ALTER TABLE`).

**Bonus (mention if time):**
- HBase is **horizontally scalable** with built-in auto partitioning (regions across RegionServers).
- RDBMS typically scales **vertically** (buy a bigger machine).

**Memory hook:** *"HBase = Column + Schema-less + Horizontal"*

✅ **Done — move to Q1d.**

---

## MINUTE 22–30 — Q1d: SCHEMA-ON-READ vs SCHEMA-ON-WRITE (2 marks)

**Memorize:**

> **Schema-on-Read (Hive's core principle):** Hive does **not verify** the data when it is loaded. The schema is applied **at the time of query (read)**. Data is simply copied as raw files into HDFS; Hive's metastore stores only the schema definition. When a query runs, Hive parses each row on the fly.
>
> **Schema-on-Write (RDBMS):** Schema is enforced **at load time** — the database parses data, validates it against the schema, and serializes it into its internal format before saving. Non-conforming rows are **rejected**.

**Comparison table (write this in the answer):**

| Aspect | Schema-on-Read (Hive) | Schema-on-Write (RDBMS) |
|--------|------------------------|---------------------------|
| Verify at load | No | Yes |
| Load speed | Very fast | Slower |
| Query speed | Slower (parse at query) | Faster |
| Bad rows surface | At query time | At load time |
| Why chosen | Fast initial load; data-format flexibility | Data integrity + transactional safety |

**Why Hive uses Schema-on-Read:** Makes the initial load extremely fast (just copy files into HDFS) — fits the write-once, read-many model of HDFS.

✅ **Q1 DONE — 8 marks secured. Move to Q2.**

---

## MINUTE 30–40 — Q2: HIVE CODE (7 marks)

This is **pure code-memorization** — the easiest 7 marks in the paper.

### Q2a — Create the external `Book` table (3 marks)

**Memorize this query verbatim:**

```sql
CREATE EXTERNAL TABLE IF NOT EXISTS Book (
  book_id INT,
  title   STRING,
  author  STRING,
  price   FLOAT
)
ROW FORMAT DELIMITED
  FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/user/hive/input/';
```

**Why each line:**
- `EXTERNAL` — table is external (Hive doesn't own the data).
- `IF NOT EXISTS` — suppresses warning if table exists.
- `ROW FORMAT DELIMITED FIELDS TERMINATED BY ','` — declares comma as the delimiter.
- `STORED AS TEXTFILE` — plain text storage format.
- `LOCATION '/user/hive/input/'` — points to existing HDFS directory (mandatory for external tables).

### Q2b — Load data, overwriting previous content (2 marks)

```sql
LOAD DATA LOCAL INPATH '/home/cloudera/book_data.txt'
OVERWRITE INTO TABLE Book;
```

**Key points:**
- `LOCAL INPATH` — file is on the **local** filesystem of the Hive client (not HDFS).
- `OVERWRITE` — replaces existing data in the table directory.
- If `OVERWRITE` were omitted, the file would be appended.

### Q2c — Create a new managed table `ExpensiveBooks` with price > 100 (2 marks)

```sql
CREATE TABLE ExpensiveBooks AS
SELECT book_id, title, author, price
FROM Book
WHERE price > 100;
```

**Why this works:**
- `CREATE TABLE … AS SELECT` (CTAS) creates a **managed** (internal) table by default — no `EXTERNAL` keyword.
- The new table inherits column names + types from the SELECT.
- The WHERE clause filters books with `price > 100`.
- Hive runs a MapReduce job to populate the new table.

✅ **Q2 DONE — 7 more marks. Total: 15 / 25. Move to Q3.**

---

## MINUTE 40–55 — Q3: YARN COMPONENTS + WORKFLOW (10 marks)

> Choose YARN over HDFS — it's **5 components + 8 numbered workflow steps**. Easier to memorize than HDFS write pipeline (which has more moving parts).

### Q3 — Explain the purpose of each core component of YARN and the workflow (5 + 5 = 10 marks)

**5 Components (memorize in this order):**

**1. Client**
- The entity that submits an application (e.g., MapReduce job, Spark app) to YARN.
- Communicates with the Resource Manager to request execution and monitor status.
- Acts as the user's interface to launch and manage applications.

**2. Resource Manager (RM)** — the **master** daemon
- Responsible for **global resource assignment and management** across the cluster.
- Two sub-components:
  - **Scheduler** — pure scheduler that allocates containers to applications based on capacity, queues, etc. (Capacity / Fair Scheduler plug-ins). Does **not** monitor applications or restart failed tasks.
  - **Applications Manager** — accepts job submissions, negotiates the first container for the Application Master, and restarts the AM on failures.

**3. Node Manager (NM)** — the **slave** daemon, one per node
- Manages individual nodes; registers with RM and sends heartbeats (node health).
- Monitors resource usage (CPU, memory) on its node.
- Creates, monitors, and kills containers as directed by RM or AM.
- Manages log files.

**4. Application Master (AM)** — one per application
- Negotiates resources (containers) from the RM for its application's tasks.
- Works with Node Managers to launch and monitor tasks inside containers.
- Tracks the status and progress of its application, reports back to RM.
- Requests new containers if tasks fail.

**5. Container**
- A collection of physical resources (RAM, CPU cores, disk) on a single node.
- The **unit of allocation** granted by the scheduler.
- Launched via **Container Launch Context (CLC)** — contains environment variables, security tokens, dependencies.

### Architecture diagram (draw this in the exam)

```
   ┌────────┐
   │ Client │
   └────┬───┘
        │ 1. Submit application
        ▼
   ┌────────────────────────┐
   │   Resource Manager (RM)│  (Master daemon)
   │ ┌─────────┐ ┌────────┐ │
   │ │Scheduler│ │AppsMgr │ │
   │ └─────────┘ └────────┘ │
   └──────────┬─────────────┘
              │ 2. Launch container for AM
              ▼
   ┌─────────────────────────┐
   │  Application Master (AM)│  (per application)
   │  - Negotiates resources │
   │  - Monitors tasks       │
   └──────────┬──────────────┘
              │ 3. Ask NM to launch containers
              ▼
   ┌──────────────────────────┐
   │   Node Manager (NM)      │  (Slave daemon, one per node)
   │   - Manages containers   │
   │   - Heartbeats to RM     │
   └─────┬────────────────────┘
         │
         ▼
   ┌─────────────┐
   │  Container  │   (RAM + CPU + disk)
   └─────────────┘
```

### YARN Application Workflow (8 steps — memorize the verbs)

1. **Application Submission** — Client submits the application (code + config + resource requirements) to the Resource Manager.
2. **Application Master Launch** — RM allocates a container on a Node Manager to launch the Application Master.
3. **AM Registration** — The newly launched AM registers itself with the RM, indicating readiness to manage the application.
4. **Resource Negotiation** — AM negotiates with RM for the necessary containers (CPU, memory) for the application's tasks.
5. **Container Launch Notification** — Once containers are allocated, AM notifies the corresponding Node Managers to launch these containers.
6. **Task Execution** — Application's code and tasks execute inside the allocated containers on the Node Managers.
7. **Monitoring and Status Reporting** — Client monitors status via RM or AM. AM monitors task progress and reports to RM.
8. **Completion and Deregistration** — Upon completion, AM unregisters with RM, releasing allocated resources.

**Memory hook for the 8 verbs:** *"Submit → Launch AM → Register → Negotiate → Notify → Execute → Monitor → Deregister"*

✅ **Q3 DONE — 10 more marks. Total: 25 / 25.**

---

## MINUTE 55–60 — EMERGENCY MEMORY HACKS

### If your brain freezes on Q1 short answers, write these single sentences:

| Question | One-sentence rescue |
|----------|---------------------|
| Combiner | *"Combiner is a local reducer that runs after Map and before Shuffle to reduce network traffic; same class as Reducer; must be associative+commutative."* |
| Checkpointing | *"Secondary NameNode periodically merges FsImage+EditLog into a new FsImage so the EditLog stays small and NameNode restart is fast."* |
| HBase vs RDBMS (2 diffs) | *"1. HBase is column-oriented, RDBMS is row-oriented. 2. HBase is schema-less, RDBMS has rigid schema."* |
| Schema-on-Read | *"Hive verifies schema at query time (Schema-on-Read) vs RDBMS verifies at load time (Schema-on-Write)."* |

### If your brain freezes on Q2 Hive code, write these skeleton queries:

```sql
-- a)
CREATE EXTERNAL TABLE Book (book_id INT, title STRING, author STRING, price FLOAT)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/user/hive/input/';

-- b)
LOAD DATA LOCAL INPATH '/home/cloudera/book_data.txt'
OVERWRITE INTO TABLE Book;

-- c)
CREATE TABLE ExpensiveBooks AS
SELECT * FROM Book WHERE price > 100;
```

### If your brain freezes on Q3 YARN, write these 5 component names + 8 verbs:

**5 Components:** Client, Resource Manager (Scheduler + Apps Mgr), Node Manager, Application Master, Container.

**8 Workflow Verbs:** Submit → Launch AM → Register → Negotiate → Notify → Execute → Monitor → Deregister.

---

## WALK-IN CHECKLIST (60 seconds before the bell)

| Done? | Item |
|-------|------|
| ☐ | ID + hall ticket |
| ☐ | Pen (×2) + pencil + eraser |
| ☐ | Diagram in Q3 drawn first (before writing prose) |
| ☐ | Q1 = 4 short notes × 3-4 lines each (don't over-write) |
| ☐ | Q2 = Hive code with `EXTERNAL`, `ROW FORMAT DELIMITED`, `OVERWRITE`, `CREATE TABLE AS SELECT` |
| ☐ | Q3 = Labelled diagram + 5 components + 8 numbered workflow steps |

---

## DON'T-PANIC RULES

1. **Even if you forget the diagram**, write the 5 components + 8 steps in a numbered list — you'll still score 6–7 / 10.
2. **Even if you forget exact Hive syntax**, write what you remember with `EXTERNAL`, `LOAD`, `OVERWRITE`, `SELECT` — partial credit is generous.
3. **Even if you forget a component name**, describe it: *"the master daemon that allocates resources globally"* = Resource Manager. *"the slave daemon that runs on each node"* = Node Manager.
4. **Draw the diagram FIRST**, then write the prose. Examiners award marks for the diagram.
5. **Time-skip rule:** If Q1c or Q1d is taking >4 minutes, write the 2-difference version above and MOVE ON. Don't lose Q2 + Q3 to perfectionism on Q1.

---

## MEMORY HOOK SUMMARY (recite to yourself in the exam hall)

> **"Combiner-After-Map, Checkpoint-Merges-Log, HBase-Column-Schemaless, Schema-Read-Versus-Write"**

> **"External + Comma + Textfile + Location, Local + Overwrite, CTAS = Managed"**

> **"Client-RM-NM-AM-Container, Submit-Launch-Register-Negotiate-Notify-Execute-Monitor-Deregister"**

> **"YARN Splits JobTracker into RM + AM → multi-engine + scalable"**

---

**You've got this. Walk in, write the diagram first, fill in the prose, hand it in. 25/25 is achievable in 60 minutes if you stick to this plan.**

*End of last-hour cram guide.*
