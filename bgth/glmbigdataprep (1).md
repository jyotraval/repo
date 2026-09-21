# Big Data Analytics and Computing — Mid-Semester Complete Study Prep

> **Course Code:** 20IC404T  •  **Semester:** VII  •  **Exam:** Mid-Semester
> Prepared from: Unit-1 Part-1 (Intro to Big Data), MapReduce, YARN, HBase, HBase Lab, Hive slides + 2024 & 2025 Previous Year Question Papers (PYQs).

---

## How To Use This Guide

1. **Read each concept section** in order — it is built directly from the professor's slides so the terminology matches what was taught.
2. **Memorise the comparison tables** (Hive vs RDBMS, HBase vs RDBMS, Secondary NN vs Standby NN, Hive vs Pig, etc.) — they are exam favourites.
3. **Practise the code snippets** (Hive DDL, HBase shell, MapReduce word-count, Scala `reduceByKey`) by hand. The 2025 paper has a 7-mark Hive coding question; the 2024 paper has a 5-mark Scala/MapReduce code question.
4. **Solve every PYQ** in the model-answer section without looking at the solution first. The 2025 paper (25 marks, 3 questions) is the most representative of what you will get.
5. **Use the Quick-Revision Cheatsheet** at the end for the last 30 minutes before the exam.

---

## Exam Pattern (Based on 2024 + 2025 PYQs)

| Year | Total Marks | Duration | Structure |
|------|-------------|----------|-----------|
| **2025** | **25** | 1 hour | Q1 (8 marks, 4 sub-questions of 2 marks each), Q2 (7 marks, Hive code), Q3 (10 marks, YARN **OR** HDFS) |
| **2024** | **50** | 2 hours | Q1 (5 + 10 = 15, Vs of Big Data + Hadoop ecosystem/HDFS read-write), Q2 (5×4 = 20, Spark vs MapReduce, RDD, transformations/actions, Pig vs SQL vs Hive), Q3 (10 + 5, PySpark DataFrame ops + Scala code/MapReduce) |

### Important observation
- **2025 paper is fully covered by the Unit-1 slides you have** (Big Data intro, HDFS, MapReduce, YARN, HBase, Hive). Every single question maps directly to a slide.
- **2024 paper additionally tests Spark, RDDs, Pig** (which are typically Unit-2 topics). Even though those slides were not given to you, brief notes and a model answer are included in §10 so you can answer them confidently if a similar question reappears.

### Marks-Distribution Strategy (for a 25-mark 2025-style paper)
- **Q1 short notes (8 marks):** 4 facts × 2 marks. Spend ~10 minutes. Write 4-5 lines per sub-question.
- **Q2 Hive code (7 marks):** Spend ~15 minutes. Three small queries. Always write `ROW FORMAT DELIMITED FIELDS TERMINATED BY ','` for CSV.
- **Q3 long answer (10 marks):** Spend ~25 minutes. Draw a diagram for YARN or HDFS architecture — examiners award marks for the diagram. Then explain each component.

---

## UNIT 1.1 — Introduction to Big Data

### 1.1.1 Definition
Big Data is an all-inclusive term that refers to extremely large, very fast, highly diverse and complex data that **cannot be managed with traditional data management tools**. Formally (Gartner's definition):

> *"Big Data is high-volume, -velocity and -variety information assets that demand cost-effective, innovative forms of information processing for enhanced insight and decision making."*

In simple language: Big Data is data that exceeds the processing capacity of conventional database systems — it is too big, moves too fast, or doesn't fit the structures of your database architectures. To gain value from this data, you must choose an alternative way to process it.

### 1.1.2 Life Cycle of Big Data
Big data is mostly (over 90%) unstructured data. The life-cycle stages are:

1. **Generate** – sensors, social media, transactions, logs create data continuously.
2. **Gather** – collect data from disparate sources into a staging area.
3. **Store** – persist in a distributed file system (HDFS) or NoSQL store (HBase).
4. **Organize** – clean, transform, partition, and structure the data.
5. **Analyze** – run queries, ML models, or batch jobs.
6. **Visualize** – present insights via dashboards/reports.

### 1.1.3 The 5 V's of Big Data  *(★ 2024 Q1 — 5 marks)*

| V | What it means | Real-world example |
|---|---------------|--------------------|
| **Volume** | The sheer amount of data — PB / EB scale. ~402.74 million TB generated per day in 2024; ~221 ZB expected in 2026; ~181 ZB generated in 2025; ~90% of the world's data was created in the last two years. | All X-rays in a large hospital ≈ 1 TB; half of all US academic research libraries ≈ 1 PB. |
| **Velocity** | The speed at which data is generated and must be processed. Data flows like a river, not like a drop. Mobile devices + IoT generate data continuously. **Processing must be faster than generation**, otherwise decisions are late → opportunities are lost. | E-promotions sent to your phone based on current location and purchase history; healthcare sensors that must react within seconds to abnormal vital signs. |
| **Variety** | Different *types* of data — structured (RDBMS tables), semi-structured (XML/JSON), unstructured (text, video, audio), graph data, streaming data. | A single app generates form data, text, graph (friends), audio, video — all must be linked together. |
| **Veracity** | Truthfulness / believability / **quality** of data. Big Data is messy. Causes of poor quality: technical error, human error, sensor malfunction, malicious disinformation, urgency (using best-available data). | A .gov site is authoritative; Wikipedia less so. A malfunctioning sensor may report wrong temperature. |
| **Value** | The *business* worth extracted from data. Without value, the other four V's are pointless. Big Data must drive enhanced insight and decision-making. | Uber's surge pricing when your battery is low; oil & gas companies detecting a leaking well in 1 day instead of a $5 M, month-long physical inspection. |

> **Memory hook:** *"Vol-Vol-Var-Ver-Val"* — **Vol**ume, **Vol**ocity (second one is "velocity" — Velo), **Var**iety, **Ver**acity, **Val**ue.

### 1.1.4 Types of Data Analytics
Four types — usually remembered as **DDPP** (Descriptive, Diagnostic, Predictive, Prescriptive):

| Type | Question it answers | Description |
|------|---------------------|-------------|
| **Descriptive** | *What happened?* | Summarises historical data using reports, scorecards, metrics. E.g., identifies customer-product relationships. |
| **Diagnostic** | *Why did it happen?* | Investigates past data deeper to discover root causes, anomalies, correlations. |
| **Predictive** | *What is likely to happen?* | Uses historical patterns to forecast future trends/risks. Turns data into actionable information. |
| **Prescriptive** | *What action should we take?* | Suggests decision options, illustrates implications of each option (optimisation + simulation). |

### 1.1.5 Operational vs Analytical Big Data

| Feature | Operational Big Data | Analytical Big Data |
|---------|----------------------|---------------------|
| Primary question | "What is happening right now?" | "What happened, why, and what will happen?" |
| Core focus | Real-time, low-latency execution | Long-term trends, patterns, strategic insights |
| Data flow | Continuous real-time transaction processing | Batch / stream / micro-batch analytical processing |
| Database type | NoSQL, distributed OLTP | Data warehouses, data lakes, OLAP |
| Typical users | Front-end apps, customers, operational staff | Data scientists, business analysts, executives |
| Latency | Milliseconds to seconds | Seconds / minutes / hours |

They form a continuous feedback loop in modern data architectures — operational systems feed analytical systems, and analytical insights tune operational systems.

### 1.1.6 Big Data Challenges
- **Scaling:** Vertical (buy a bigger machine — expensive, limited) vs Horizontal (add more commodity nodes — cheaper, scales out). Hadoop chose horizontal.
- **Scale of infrastructure:** Power, cooling, rack space, network.
- **Storage of huge files:** Need efficient access, effective use of space, redundancy/failsafe. If 1 disk has 1% failure/yr, what's the chance that 1 of 103 disks fails? (High — therefore replication is needed.)
- **Distributed processing is non-trivial:** Task assignment, failure handling, result exchange, synchronisation.
- **Reliability:** PBs of data across thousands of machines; probability of failure grows with the number of machines.

### 1.1.7 Solution Philosophy: Divide and Conquer
**Divide work → Combine results.** This is the foundational idea behind both HDFS (split files into blocks and distribute) and MapReduce (split processing into Map tasks, then Combine/Reduce results).

---

## UNIT 1.2 — Hadoop & HDFS

### 1.2.1 What is Hadoop?
Hadoop is a **framework** that allows distributed processing of large data sets across clusters of commodity hardware using simple programming models. It is designed to:
- Scale from a single server to thousands of machines.
- Detect and handle failures at the application layer (delivering a highly-available service on top of failure-prone computers).

### 1.2.2 Hadoop's Three Core Components (+ Common)

| Component | Full name | Role |
|-----------|-----------|------|
| **HDFS** | Hadoop Distributed File System | Storage unit |
| **MapReduce** | MapReduce | Processing unit |
| **YARN** | Yet Another Resource Negotiator | Resource management unit |
| Hadoop Common | — | Common utilities that support the other modules |

### 1.2.3 Hadoop Ecosystem  *(★ 2024 Q1 — 10 marks — "Draw and explain")*

> Examiners expect a labelled diagram with at least 8 components and a one-line explanation of each.

```
                 ┌────────────────────────────────────────────┐
                 │              HADOOP ECOSYSTEM               │
                 ├────────────────────────────────────────────┤
   Storage ──►   │  HDFS   (Hadoop Distributed File System)   │
                 │  HBase  (NoSQL column DB on top of HDFS)    │
   Resource──►  │  YARN   (Yet Another Resource Negotiator)   │
   Processing►  │  MapReduce (data processing paradigm)       │
                 │  Spark / Spark MLlib (in-memory + ML)        │
   Query/SQL─►  │  Pig, Hive  (SQL-like / procedural query)    │
                 │  Apache Drill (SQL on Hadoop)               │
   ML ─────►    │  Mahout, Spark MLlib (machine learning)     │
   Search ──►   │  Solr, Lucene (searching and indexing)      │
   Coord ───►   │  Zookeeper (cluster coordination)           │
   Sched ───►   │  Oozie (job scheduling)                     │
   Ingest ───►  │  Flume, Sqoop (data ingestion services)     │
   Manage ───►  │  Ambari (provision / monitor / maintain)    │
                 └────────────────────────────────────────────┘
```

**One-line explanation of each component (memorise these):**
- **HDFS** – distributed, fault-tolerant storage for very large files.
- **YARN** – manages cluster resources (CPU, memory) and schedules jobs.
- **MapReduce** – batch processing framework that splits work into Map → Shuffle/Sort → Reduce.
- **Spark / Spark MLlib** – in-memory data processing; much faster than MapReduce for iterative workloads; MLlib provides ML algorithms.
- **Pig** – procedural data-flow language (Pig Latin) for transforming large datasets.
- **Hive** – data warehouse on top of Hadoop; runs SQL-like queries (HiveQL) translated into MapReduce/Tez jobs.
- **HBase** – NoSQL column-oriented database on HDFS for random real-time read/write.
- **Mahout / Spark MLlib** – machine-learning libraries (classification, clustering, recommendation).
- **Solr / Lucene** – search and indexing engines.
- **Zookeeper** – coordination service: configuration, naming, distributed sync, group services.
- **Oozie** – workflow/job scheduler for Hadoop jobs.
- **Flume** – log/data ingestion into HDFS (streaming sources).
- **Sqoop** – bulk transfer between Hadoop and relational databases.
- **Ambari** – provisioning, monitoring, and managing a Hadoop cluster.

### 1.2.4 HDFS (Hadoop Distributed File System)

**HDFS** is the open-source implementation of Google File System (GFS). It is a distributed file system for storing huge datasets on commodity hardware.

Key facts:
- Stores write-once, read-many (WORM) files.
- Files cannot be modified after creation (appends may be supported if enabled).
- Master-slave architecture (NameNode = master, DataNodes = slaves).
- Blocks are replicated (default replication factor = 3) for fault tolerance and fast parallel reads.
- Default block size = **128 MB** (configurable; older versions used 64 MB, even earlier 64 MB).

### 1.2.5 HDFS Architecture

```
                       ┌─────────────────────┐
                       │      NameNode       │   (Master)
                       │  - Metadata  - Block │
                       │    mapping           │
                       │  - FS Image + Edit Log│
                       └──────────┬──────────┘
                                  │ heartbeats / block reports
        ┌─────────────────────────┼───────────────────────────┐
        │                         │                             │
   ┌────┴──────┐           ┌──────┴─────┐               ┌─────────┐
   │ DataNode 1│           │DataNode 2  │   ...          │DataNode N│ (Slaves)
   │ blk-1,blk2│           │blk-1,blk-3 │               │blk-2,blk3│
   └───────────┘           └────────────┘               └──────────┘

                       ┌──────────────────────┐
                       │ Secondary NameNode  │  (Checkpoint helper)
                       └──────────────────────┘
```

#### NameNode (Master)
- Manages the **file-system namespace**: file names, directory tree, permissions.
- Maintains the mapping of *files → blocks → DataNodes* (metadata).
- **Does NOT store actual data** — only metadata.
- Maintains two on-disk structures:
  - **FsImage** — full snapshot of the metadata since the beginning (master copy).
  - **EditLog** — recent changes to metadata since the last FsImage.
- Manages file operations: open, close, rename.
- Heartbeat mechanism: every 3 s a DataNode sends a heartbeat. If NameNode does not hear from a DataNode for **~10 minutes**, it considers the DataNode dead and replicates its blocks.
- Block Report: each DataNode periodically (default 6 hours) sends a full list of blocks it holds.

#### DataNode (Slave / Worker)
- Stores actual data blocks on local disk.
- Serves client read/write requests.
- Sends heartbeats + block reports to NameNode.
- Performs block creation, deletion, replication as instructed by the NameNode.
- Cluster can have 1 to thousands of DataNodes.

#### Secondary NameNode  *(★ Frequently asked — "Why checkpointing?")*

**NOT a backup NameNode!** It cannot take over if the Primary NameNode fails.

Its job is **checkpointing** — merging the FsImage and EditLog so the EditLog doesn't grow too large:
1. **Fetch** — periodically downloads the current FsImage + EditLog from Primary NN.
2. **Merge** — combines them in its memory to create a new, updated FsImage (a *checkpoint*).
3. **Upload** — sends the new FsImage back to Primary NN.
4. **Reset** — Primary NN replaces old FsImage with new one and truncates the EditLog.

**Why is this needed?** If the EditLog grows unbounded, restarting the NameNode would take hours to replay all transactions. Checkpointing keeps the restart time short.

#### Secondary NameNode vs Standby NameNode

| Feature | Secondary NameNode (Classic) | Standby NameNode (Hadoop 2.x+ HA) |
|---------|-------------------------------|-----------------------------------|
| Role | Helper for periodic checkpointing | Active hot-standby replica |
| Auto failover? | No — cannot take over if Primary fails | Yes — takes over instantly |
| Data freshness | Outdated (only up to last checkpoint) | Real-time synchronised |

#### Why blocks? (Reasons)
- A single file can be larger than one disk.
- Block is fixed size → easy to manage and manipulate.
- Easy to replicate and do fine-grained load balancing.

#### Block replication policy (default factor = 3)
- 1st replica: stored on the **local rack**.
- 2nd replica: stored on a **remote rack** (different DataNode).
- 3rd replica: stored on the **same remote rack** but a different DataNode.
- Additional replicas: random DataNodes, with no more than 2 replicas per rack where possible.

#### Replication Pipeline (write path)
1. Client requests file creation from NameNode.
2. NameNode checks permissions, returns a list of DataNodes `[DN1, DN2, DN3]`.
3. Client writes data to DN1.
4. DN1 forwards each packet to DN2.
5. DN2 forwards to DN3.
6. Once DN3 has the data, it sends an ACK back: DN3 → DN2 → DN1 → Client.
7. Client receives ACK → write successful.

**Advantages of pipelined replication:** faster writes (parallel streaming), reduced network congestion (unidirectional), automatic recovery on DataNode failure.

#### Safemode
- A **read-only** administrative state entered automatically by the NameNode at startup.
- No file system modifications, block replications, or deletions allowed.
- **Why required?** The NameNode does not persist block locations on disk; it rebuilds them from DataNode block reports during startup.
- Exit condition: when **99.9%** of blocks are reported (plus a 30-second extension timer).

#### Data Integrity
- Each block has a checksum stored in a hidden file.
- When a client retrieves data, it verifies the checksum; if it doesn't match, the block is fetched from another replica.

#### Cluster Rebalancing
- A scheme can move data from one DataNode to another if free space falls below a threshold (e.g., on adding new nodes / decommissioning).

#### Common HDFS Commands

| Operation | Command |
|-----------|---------|
| Put local file to HDFS | `hadoop fs -put local_file /hdfs/path/` |
| Same, restricted source | `hadoop fs -copyFromLocal local_file /hdfs/path/` |
| Move (delete local copy) | `hadoop fs -moveFromLocal local_file /hdfs/path/` |
| Append local to HDFS file | `hadoop fs -appendToFile local_file /hdfs/existing_file` |
| Get file from HDFS | `hadoop fs -get /hdfs/file local_destination` |
| Copy to local | `hadoop fs -copyToLocal /hdfs/file local_destination` |
| Merge multiple HDFS files | `hadoop fs -getmerge /hdfs/folder/* merged_local_file` |

### 1.2.6 HDFS Read & Write Operations  *(★ 2024 Q1 OR — 10 marks)*

#### Read Operation — step by step
1. Client opens file → calls `open()` on `DistributedFileSystem`.
2. `DistributedFileSystem` calls NameNode to get **block locations** for the first few blocks of the file. NameNode returns a list of DataNodes (sorted by network proximity to the client) for each block.
3. Client gets a `FSDataInputStream` to read from the closest DataNode.
4. Client calls `read()` repeatedly; the stream reads from the closest DataNode for the current block, then connects to the next DataNode for the next block.
5. When the client is done, it calls `close()`.

**Important:** The client reads directly from DataNodes (not through the NameNode) for actual data. The NameNode only provides metadata.

#### Write Operation — step by step
1. Client creates file → calls `create()` on `DistributedFileSystem`.
2. `DistributedFileSystem` calls NameNode to create a new file entry in the namespace. NameNode returns a list of DataNodes `[DN1, DN2, DN3]` for the first block.
3. Client gets a `FSDataOutputStream` and starts writing data into an internal buffer.
4. Data is streamed in **packets** to DN1.
5. DN1 forwards each packet to DN2 → DN3 (the pipeline).
6. Each DataNode stores the packet and a pipeline of ACKs flows back: DN3 → DN2 → DN1 → Client.
7. When a block is complete (e.g., 128 MB written), the client requests the next block's DataNodes from the NameNode.
8. When the file is closed, the DataNodes report the new blocks to the NameNode.

**Key points to mention:** heartbeats, block reports, replication factor 3, rack-aware placement, checksum verification, pipeline ACKs.

### 1.2.7 HDFS Robustness — Handling Failures
Three common failures HDFS must handle:
- **DataNode failure** — detected via missing heartbeats; NameNode marks the DataNode dead and re-replicates its blocks to maintain replication factor.
- **NameNode failure** — recovered from FsImage + EditLog; in HA mode, Standby NameNode takes over.
- **Network partition** — DataNodes on the wrong side of the partition are marked dead; metadata remains intact.

### 1.2.8 HDFS Advantages & Limitations  *(★ 2025 Q3c — 2 marks)*

**Advantages:**
- **Fault tolerance** — automatic replication + heartbeat monitoring.
- **Scalability** — horizontally scalable to thousands of nodes.
- **Reliability** — checksums, replication, Safemode boot checks.
- **Cost-effective** — runs on commodity hardware.
- **Parallel access** — large blocks enable parallel reads.
- **Data locality** — computation can run where the data lives.

**Limitations:**
- **Not suited for low-latency random access** — optimized for streaming reads (HBase solves this).
- **Single-writer model** — files are write-once-read-many; no arbitrary updates.
- **Small-files problem** — each file's metadata takes ~150 bytes in NameNode RAM; millions of small files exhaust NameNode memory.
- **No POSIX compliance** for many operations.
- **NameNode is a single point of failure** in classic mode (mitigated in HA mode).

### 1.2.9 Brief History of Hadoop
- 2002 — Doug Cutting & Mike Cafarella start Apache Nutch (search engine to index 1 billion pages). Estimated cost: $500K hardware + $30K/month running.
- 2003 — Google publishes GFS paper; Cutting & Cafarella adopt it.
- 2004 — Google publishes MapReduce paper.
- 2006 — Cutting joins Yahoo; Nutch's distributed layer becomes Hadoop (named after his son's toy elephant).
- 2007 — Yahoo tests Hadoop on a 1000-node cluster.
- 2008 — Yahoo releases Hadoop to Apache; Apache successfully tests a 4000-node cluster.
- 2009 — Hadoop sorts 1 PB in <17 hours.

### 1.2.10 Who Uses Hadoop?
- **Meta/Facebook** — user data, photo storage, behavioral analytics.
- **Apple** — Siri voice recognition, iCloud storage backends.
- **Amazon** — recommendation engine, customer analytics.
- **Netflix** — viewing habits, content recommendation, streaming optimization.
- **Visa/Mastercard** — real-time fraud detection from billions of transactions.
- **Uber** — surge pricing, route optimization, demand forecasting.
- **Airbnb** — search metrics, user preference analysis.

---

## UNIT 1.3 — MapReduce

### 1.3.1 Philosophy: Divide & Conquer
- **Divide Work** — break the input into splits and assign each split to a mapper.
- **Combine Results** — shuffle, sort, and reduce intermediate outputs to produce the final result.

**Real-world analogy (Coin Deposit):**
- *Mapper* — categorises coins by face value (one pile per denomination).
- *Reducer* — counts the coins in each pile in parallel.

### 1.3.2 What is MapReduce?
A **programming model** for efficient, parallel processing of large datasets in a distributed manner. Developers write only two functions:

```
Map    (k1, v1)            -> list (k2, v2)         // emits intermediate <key, value> pairs
Reduce (k2, list(v2))     -> list (v3)              // aggregates values for each key
```

The framework handles **everything else**: scheduling, data partitioning, inter-node communication, synchronization, fault tolerance, retries. *All values for the same key are guaranteed to reach the same Reducer.*

### 1.3.3 HDFS vs MapReduce — Role Separation

| Aspect | HDFS | MapReduce |
|--------|------|-----------|
| Purpose | Distributed file **storage** | Distributed data **processing** |
| Functionality | Store & manage data; provide fault tolerance + scalability | Process and analyze data in parallel |
| Layer | Storage layer | Processing layer on top of HDFS |
| Use case | Storing large datasets | Processing those datasets |
| Idea | Bring **data** to multiple machines | Bring **computation** to data (data locality) |

### 1.3.4 MapReduce Architecture: Master-Slave

```
                       ┌──────────────┐
        Job Client ───►│  Job Tracker │◄──── Heartbeats + task status
                       │  (Master)    │      from Task Trackers
                       └──────┬───────┘
                              │
              ┌───────────────┼────────────────┐
              │               │                │
        ┌─────┴─────┐   ┌─────┴─────┐    ┌─────┴─────┐
        │Task Tracker│   │Task Tracker│    │Task Tracker│  (Slaves)
        │  Map|Reduce│   │  Map|Reduce│    │  Map|Reduce│
        └────────────┘   └────────────┘    └────────────┘
              │
        ┌─────▼─────┐
        │  HDFS data │  (blocks local to the node)
        └────────────┘
```

- **Job Client** — submits the job (Mapper + Reducer + Input/Output paths) to the Job Tracker.
- **Job Tracker** — coordinates jobs (scheduling, phase coordination, handles failures, monitors progress). It uses data locality when assigning tasks (assigns a Map task to a Task Tracker that holds the input split).
- **Task Tracker** — executes the Map / Reduce tasks assigned by the Job Tracker, reports progress.
- **Idea:** *"Bring computation to data!"*

### 1.3.5 MapReduce Phases (3 phases)

1. **Map Phase**
   - Input data is split into input splits.
   - Each Map task processes its local split and produces **intermediate key-value pairs**.

2. **Shuffle & Sort Phase** *(framework-managed)*
   - Intermediate pairs from all Map tasks are grouped by key.
   - Keys are sorted so identical keys are contiguous → ensures ordered keys before Reduce.

3. **Reduce Phase**
   - Reducers receive grouped keys + values from shuffle/sort.
   - They aggregate and emit the final output → written back to HDFS.

### 1.3.6 WordCount — Canonical Example

Input:
```
Deer Beer River
Car Car River
Deer Car Beer
```

Pipeline:
```
INPUT            SPLIT          MAP         SHUFFLE/SORT      REDUCE       OUTPUT

Deer Beer River → Deer,1     → Beer  → [1,1]  → Beer,2
                  Beer,1     → Car   → [1,1,1] → Car,3
                  River,1    → Deer  → [1,1]  → Deer,2
Car Car River   → Car,1      → River → [1,1]  → River,2
                 Car,1
                 River,1
Deer Car Beer   → Deer,1
                 Car,1
                 Beer,1
```

- **Map key/value:** Key = line number (offset), Value = words in the line.
- **Intermediate key/value:** Key = word, Value = `1` for each occurrence.
- **Reduce key/value:** Key = word, Value = aggregated count.

### 1.3.7 Mapper / Reducer Pseudocode

```
Map(key, value):
    // key: line number, value: words in line
    for each word w in value:
        Emit(w, "1")

Reduce(key, list_of_values):
    // key: a word, list_of_values: list of "1"s
    result = 0
    for each v in list_of_values:
        result += ParseInt(v)
    Emit(key, result)
```

### 1.3.8 Combiner — Local Aggregation  *(★ 2025 Q1a — 2 marks)*

The Combiner is a **local reducer** that runs at the mapper output, *before* the data crosses the network to reach the Reducer.

**Role:** Performs local aggregation on the `<key, value>` pairs emitted by a single mapper, *reducing the volume of data shipped across the network*.

**Phase after which it is used:** The Combiner runs **after the Map phase** and **before the Shuffle & Sort phase** (or, equivalently, at the start of shuffle).

```
INPUT  →  MAP  →  COMBINER  →  SHUFFLE & SORT  →  REDUCE  →  OUTPUT
```

**Benefits:**
- Reduces memory/disk requirements of Map tasks.
- Reduces network traffic between mappers and reducers.

**Important constraints:**
- The Combiner **must be associative and commutative** because the framework may call it 0, 1, or multiple times per key.
- **The Combiner's class is the same as the Reducer's class** (its `reduce()` method is reused).
- The Reducer **cannot** be removed — it is still required to aggregate across the outputs of multiple mappers (whose combiners ran independently).

**Example:** With input `(Car,1), (Car,1), (River,1)` from a single mapper, the combiner can emit `(Car,2), (River,1)` to reduce data sent to the reducer. The reducer then receives `(Car,2)` from this mapper plus `(Car,1)` from another mapper, producing `(Car,3)`.

### 1.3.9 MapReduce Workflow (Execution Flow)
1. Client submits the job (Mapper + Reducer + input path + output path).
2. Job Tracker splits the input into tasks and assigns them to Task Trackers based on data locality.
3. Task Trackers execute Map tasks on locally stored input splits.
4. Intermediate outputs are **shuffled and sorted** by the framework.
5. Reduce tasks process grouped outputs and produce the final result.
6. Final output is written back to HDFS.

### 1.3.10 Mimicking Hadoop with Linux Pipes (Demo)
A Hadoop job can be mimicked on a single machine using Linux pipes:

```bash
cat input.txt | ./mapper.py | sort | ./reducer.py
```

Output:
```
a           2
and         1
framework   2
hadoop      2
in          1
is          2
java        1
parallel    1
processing  1
simple      1
supports    1
written     1
```

### 1.3.11 MapReduce Program — Count Letter Occurrences  *(★ 2024 Q3 OR — 5 marks)*

> *"Write a simple example of a MapReduce program to count the occurrences of each letter in a text file."*

**Python-style pseudocode (works as mapper.py and reducer.py):**

```python
# mapper.py
import sys
for line in sys.stdin:
    line = line.strip().lower()
    for ch in line:
        if ch.isalpha():        # only letters
            print(f"{ch}\t1")
```

```python
# reducer.py
import sys
from collections import defaultdict

counts = defaultdict(int)
for line in sys.stdin:
    ch, cnt = line.strip().split('\t')
    counts[ch] += int(cnt)

for ch in sorted(counts):
    print(f"{ch}\t{counts[ch]}")
```

**Run:**
```bash
cat input.txt | ./mapper.py | sort | ./reducer.py
```

**Java-style Hadoop MapReduce skeleton:**

```java
public class LetterCount {
  public static class LetterMapper extends Mapper<LongWritable, Text, Text, IntWritable> {
    private final static IntWritable one = new IntWritable(1);
    private Text letter = new Text();
    public void map(LongWritable key, Text value, Context ctx)
        throws IOException, InterruptedException {
      String line = value.toString().toLowerCase();
      for (char c : line.toCharArray()) {
        if (Character.isLetter(c)) {
          letter.set(String.valueOf(c));
          ctx.write(letter, one);
        }
      }
    }
  }
  public static class CountReducer extends Reducer<Text, IntWritable, Text, IntWritable> {
    private IntWritable result = new IntWritable();
    public void reduce(Text key, Iterable<IntWritable> values, Context ctx)
        throws IOException, InterruptedException {
      int sum = 0;
      for (IntWritable v : values) sum += v.get();
      result.set(sum);
      ctx.write(key, result);
    }
  }
  public static void main(String[] args) throws Exception {
    Job job = Job.getInstance(new Configuration(), "letter count");
    job.setJarByClass(LetterCount.class);
    job.setMapperClass(LetterMapper.class);
    job.setCombinerClass(CountReducer.class);   // reuse reducer as combiner
    job.setReducerClass(CountReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
  }
}
```

### 1.3.12 MapReduce Summary
- Mapper, Reducer, and Combiner all act on `<key, value>` pairs.
- Map function gets one record at a time.
- Combiner (if present) works on the output of Map.
- Reducer works on the output of Map (or Combiner, if present).
- Combiner = local-reducer; reduces the output of mappers on the same node.

---

## UNIT 1.4 — YARN (Yet Another Resource Negotiator)

### 1.4.1 What is YARN?
YARN = **Yet Another Resource Negotiator**. Introduced in **Hadoop 2.0** to overcome the limitations of Hadoop 1.0. Originally a "Redesigned Resource Manager," now evolved into a **large-scale distributed operating system for Big Data**.

**Key innovation:** YARN **separates the resource management layer from the data processing layer**, enabling multiple data processing engines (batch, interactive, streaming, graph) to run on data stored in HDFS — not just MapReduce.

### 1.4.2 Why YARN? — The Problem with Hadoop 1.0  *(★ 2025 Q3 — explain the problem)*

**Job Tracker Bottleneck in Hadoop 1.0:**
- A **single Job Tracker** managed both:
  - **Cluster resources** (CPU, memory), and
  - **Application execution** (scheduling, monitoring).
- Limited scalability — clusters couldn't scale beyond ~4,000 nodes.
- Supported **only MapReduce** processing — no way to run Spark / Flink / Storm on the same cluster.

**YARN's Solution:**
- Split the Job Tracker's responsibilities into **two daemons**:
  - **Global Resource Manager** (cluster-wide resource scheduling).
  - **Per-Application Application Master** (manages a single application's lifecycle).

This separation allows better scalability, efficiency, and support for diverse workloads.

### 1.4.3 Key Features of YARN

| Feature | Description |
|---------|-------------|
| **Scalability** | The scheduler in Resource Manager allows Hadoop to manage thousands of nodes. |
| **Compatibility** | YARN supports existing MapReduce apps without disruption — compatible with Hadoop 1.0. |
| **Cluster Utilization** | Supports dynamic allocation → optimized cluster utilization. |
| **Multi-tenancy** | Multiple engines (Spark, Flink, Storm, MapReduce) can run simultaneously on the same cluster. |

### 1.4.4 YARN Architecture — Core Components  *(★ 2025 Q3 — 5+5 marks)*

```
   ┌────────┐
   │ Client │
   └───┬────┘
       │ 1. Submit application
       ▼
   ┌────────────────────────┐
   │   Resource Manager (RM)│  (Master daemon — global)
   │ ┌────────────────────┐ │
   │ │   Scheduler        │ │   - Allocates resources to apps
   │ │   Applications Mgr │ │   - Accepts job submissions, launches AM
   │ └────────────────────┘ │
   └─────────┬──────────────┘
             │ 2. Launch container for AM
             ▼
   ┌─────────────────────────┐
   │  Application Master (AM)│  (Per-application)
   │  - Negotiates resources│
   │  - Monitors tasks       │
   └─────────┬───────────────┘
             │ 3. Ask NM to launch containers
             ▼
   ┌──────────────────────────┐
   │   Node Manager (NM)      │  (Slave daemon — per node)
   │   - Manages containers   │
   │   - Sends heartbeats to  │
   │     Resource Manager     │
   └─────┬────────────────────┘
         │
         ▼
   ┌─────────────┐
   │  Container  │   (RAM + CPU + disk on a node)
   └─────────────┘
```

#### a) Client
The entity that initiates and submits an application (e.g., a MapReduce job, a Spark app) to YARN. Communicates with the Resource Manager to request execution, monitors job status, and may interact with the Application Master for progress updates. It is the user's interface to launch and manage applications on the Hadoop cluster.

#### b) Resource Manager (RM)
The **"master" daemon** of YARN. Responsible for **global resource assignment and management**. Has two sub-components:

- **Scheduler** — A *pure scheduler* that allocates resources to applications based on capacity, queues, etc. (Plug-ins: Capacity Scheduler, Fair Scheduler). It does **not** monitor applications; nor does it restart failed tasks. Its only job is to allocate containers based on available resources and policy.
- **Applications Manager** — Accepts job submissions, negotiates the **first container** for the Application Master, and restarts the AM on failures.

#### c) Node Manager (NM)
The **"slave" daemon** that runs on each node in the cluster. Responsible for managing individual nodes:
- Registers with the Resource Manager and sends heartbeats (node health).
- Monitors resource usage (CPU, memory) on its node.
- Creates, monitors, and kills containers as directed by the RM or AM.
- Manages log files.

#### d) Application Master (AM)
- One AM **per application** (e.g., per MapReduce job).
- Negotiates resources (containers) from the Resource Manager.
- Works with the Node Manager(s) to launch and monitor the application's tasks inside containers.
- Tracks the status and progress of its specific application → reports back to the RM.
- Requests new containers if tasks fail.

#### e) Container
- A collection of physical resources (RAM, CPU cores, disk) on a single node.
- The **unit of allocation** granted by the scheduler.
- Containers are launched via **Container Launch Context (CLC)** — a record containing environment variables, security tokens, dependencies, etc.

### 1.4.5 Application Workflow in YARN  *(★ 2025 Q3 — 5 marks — "workflow")*

1. **Application Submission** — A client submits an application (e.g., MapReduce job, Spark application) to the YARN Resource Manager. The submission includes the application's code, configuration, and resource requirements.
2. **Application Master Launch** — The Resource Manager allocates a container on a Node Manager to launch the Application Master for the submitted application. The AM is responsible for managing the application's execution.
3. **Application Master Registration** — The newly launched AM registers itself with the RM, informing the RM of its presence and readiness to manage the application.
4. **Resource Negotiation** — The AM negotiates with the RM for the necessary containers (CPU, memory) to execute the application's tasks. The RM considers available resources and the application's requirements.
5. **Container Launch Notification** — Once containers are allocated by the RM, the AM notifies the respective Node Managers to launch these containers and execute the application's tasks within them.
6. **Task Execution** — The application's code and tasks are executed inside the allocated containers on the Node Managers.
7. **Monitoring and Status Reporting** — The client can monitor the application's status by contacting either the RM or the AM. The AM also monitors the progress of tasks and container status, reporting this information to the RM.
8. **Application Completion and Deregistration** — Upon completion of all tasks and the application's processing, the AM unregisters itself with the RM, releasing the allocated resources.

### 1.4.6 Advantages & Disadvantages of YARN

**Advantages:**
- **Flexibility** — run Spark, Flink, Storm, and MapReduce on the same cluster.
- **Efficient Resource Management** — centralized control for optimal allocation of CPU, memory, disk.
- **High Scalability** — designed for clusters with thousands of nodes.
- **Improved Performance & Utilization** — dynamically allocates resources, reducing waste.
- **Security** — supports Kerberos authentication, SSH, secure data transmission.

**Disadvantages:**
- **Complexity** — adds a layer of configuration and management overhead.
- **Performance Overhead** — resource negotiation and scheduling introduce minor latency.
- **Potential Single Point of Failure** — the Resource Manager is critical (mitigated by High Availability setups; Standby RM since Hadoop 2.4).
- **Limited Non-Java Support** — while supporting multiple engines, native non-Java support can be limited.

### 1.4.7 YARN vs Hadoop 1.0 JobTracker — Summary

| Aspect | Hadoop 1.0 (JobTracker) | Hadoop 2.0 (YARN) |
|--------|--------------------------|---------------------|
| Resource mgmt + execution | Combined in single JobTracker | Split — RM handles resources; AM handles execution |
| Scalability | ~4,000 nodes max | Thousands of nodes |
| Workload support | MapReduce only | MapReduce, Spark, Flink, Storm, … |
| Cluster utilization | Lower (slot-based) | Higher (dynamic container allocation) |
| Failover | JobTracker failure = cluster down | RM HA via Standby RM (since 2.4) |

### 1.4.8 YARN Summary
- YARN is the central operating system of Hadoop 2.x+ for resource management.
- It enables Hadoop to be a multi-purpose, scalable data processing platform beyond just MapReduce.
- Its architecture (central Resource Manager + per-node Node Managers + per-application Application Masters) provides a robust framework for managing cluster resources efficiently.
- It is the foundation that allows modern data-processing frameworks to thrive on Hadoop.

---

## UNIT 1.5 — HBase (NoSQL on top of HDFS)

### 1.5.1 Why HBase? — Limitations of Hadoop
- Hadoop's core framework, MapReduce, is designed for **batch processing** of large datasets. It is **not suitable for real-time data analysis or streaming data**. Even for the simplest lookup, MapReduce must scan the entire dataset.
- A huge dataset when processed results in another huge dataset, which should also be processed sequentially.
- **A new solution is needed to access any point of data in a single unit of time (random access).**

> **Random Access Databases on top of Hadoop:** HBase, Cassandra, CouchDB, Dynamo, MongoDB — all store huge amounts of data and access it randomly.

### 1.5.2 What is HBase?
HBase is a **distributed column-oriented database built on top of the Hadoop File System**:
- Open-source, **horizontally scalable**.
- Data model similar to **Google's Bigtable** — designed to provide quick random access to huge amounts of structured data.
- Leverages fault tolerance provided by HDFS.
- Part of the Hadoop ecosystem — provides random real-time read/write access to data in HDFS.
- One can store data in HDFS either directly or through HBase. Data consumers read/access data in HDFS randomly using HBase.
- HBase sits on top of HDFS and provides read and write access.

### 1.5.3 Why Choose HBase?
- A table for a popular web app may have **billions of rows**. HBase's row-key index gives sub-millisecond fetches.
- Traditional relational data models fail to meet the performance requirements of very big databases. Apache HBase overcomes these performance and processing limitations.

### 1.5.4 Apache HBase Features
- Linearly scalable.
- Automatic failure support.
- Consistent reads and writes.
- Integrates with Hadoop, both as a source and a destination.
- Easy Java API for clients.
- Provides data replication across clusters.

### 1.5.5 Where to Use HBase
Suitable for scenarios requiring **real-time, random access to large datasets**:
- Time-series storage (IoT, financial data).
- Real-time analytics — fraud detection, social-media analysis.
- Data caching, metadata storage.
- Healthcare — genome sequences and disease history.
- E-commerce — customer search history + analytics + targeted advertising.
- Sports — match details + history for better predictions.
- Used by Facebook, Twitter, Yahoo, Adobe.

### 1.5.6 HBase Key Concepts  *(★ 2025 Q1c — HBase vs RDBMS)*

| Concept | Description |
|---------|-------------|
| **Column-oriented storage** | Data stored by column families → fast retrieval of specific columns. |
| **Row Key** | Unique identifier for each row; primary key; determines the **sort order** of data. |
| **Column Families** | Logical groupings of related columns; defined at table creation; not easily changed. |
| **Column Qualifiers** | Specific identifiers within a column family; **mutable**; can vary between rows. |
| **Cell** | Intersection of {row key, column family, column qualifier}; contains a value + a timestamp (version). |
| **Timestamp / Versioning** | HBase auto-assigns a timestamp to each cell value; multiple versions of the same data can be stored and retrieved. |

**Data hierarchy in HBase:**
- **Table** = collection of rows.
- **Row** = collection of column families.
- **Column family** = collection of columns.
- **Cell / Key-Value** = the actual data value + a timestamp.

**Storage mechanism:**
- Tables are sorted by row.
- Schema defines only column families.
- A table can have multiple column families; each can have any number of columns.
- Subsequent column values are stored contiguously on disk.
- Each cell has a timestamp.

### 1.5.7 HBase vs RDBMS  *(★ 2025 Q1c — 2 marks — Give two main differences)*

| Feature | Apache HBase | Traditional RDBMS |
|---------|--------------|-------------------|
| Data architecture | **Column-oriented datastore** | Row-oriented datastore |
| Schema | **Schema-less** (only column families defined upfront) | Fixed / rigid schema required |
| Table structure | Wide, sparse tables designed for de-normalized data | Thin tables designed for normalised data |
| Data types | Structured + semi-structured data | Structured data only |
| Partitioning & scaling | Built-in automatic partitioning (**horizontally scalable**) | No built-in auto partitioning (vertically scalable) |
| Transactions | Limited (row-level only) | Full ACID |
| Joins | Not native | Native SQL JOINs |

**Two main differences to highlight in the exam:**
1. **Column-oriented vs Row-oriented storage.** HBase stores data column-family-wise, enabling efficient retrieval of specific columns over huge rows. RDBMS stores row-wise, which is efficient for transactional row lookups but poor for analytical column scans.
2. **Schema-less (only column families defined upfront) vs Fixed/Rigid schema.** HBase lets you add new column qualifiers per row without altering table schema, making it ideal for sparse, evolving data. RDBMS requires schema changes (ALTER TABLE) for any new column.

### 1.5.8 HBase Architecture

```
                          ┌──────────────┐
                          │   ZooKeeper │  (Coordinator)
                          │   - tracks   │
                          │   active     │
                          │   HMaster    │
                          └──┬───────────┘
                             │
        ┌────────────────────┼──────────────────────────┐
        │                    │                           │
   ┌────▼─────┐         ┌────▼──────┐                ┌────▼──────┐
   │ HMaster  │         │ Region      │   ...          │ Region     │
   │ (master)│         │ Server 1    │                │ Server N   │
   │          │         │ [Regions]  │                │ [Regions]  │
   └──────────┘         └────────────┘                └────────────┘
                              ▲
                              │ each RegionServer runs on a DataNode
                              ▼
                        ┌──────────────┐
                        │  HDFS / Data │
                        └──────────────┘
```

#### HMaster (Master)
- **Single** master node running at a time.
- Manages cluster operations:
  - Maintains metadata.
  - Assigns **regions** to RegionServers.
  - Handles administrative tasks: table creation, deletion, schema modifications.
  - Monitors RegionServer health, performs load balancing.

> **Region** — a logical division of an HBase table containing a sorted range of rows.

#### RegionServers (Workers)
- Worker nodes; handle read/write requests from clients.
- Host HBase table **regions** (horizontal partitions by row key range).
- Each RegionServer operates on a DataNode within the Hadoop cluster.

#### ZooKeeper (Coordinator)
- Acts as a coordinator.
- Maintains cluster state.
- Facilitates communication between HMaster and RegionServers.
- Handles server failure detection and recovery.
- Tracks active HMaster and RegionServers; provides server failure notifications.

### 1.5.9 HBase Shell — Command Reference

#### 1. General Commands

| Command | Description | Example |
|---------|-------------|---------|
| `help` | Display help info / usage syntax | `help 'create'` |
| `status` | Cluster status (servers, dead servers, avg load) | `status`, `status 'simple'` |
| `version` | HBase version | `version` |
| `whoami` | Current user and roles | `whoami` |

#### 2. DDL Commands

| Command | Syntax | Example |
|---------|--------|---------|
| `create` | `create 'table_name', 'col_family1' [, 'col_family2', ...]` | `create 'emp', 'personal_data', 'professional_data'` |
| `list` | `list ['regex']` | `list`, `list 'e.*'` |
| `describe` | `describe 'table_name'` | `describe 'emp'` |
| `alter` | `alter 'table_name', {NAME => 'col_family', KEY => 'value'}` | `alter 'emp', NAME => 'personal_data', VERSIONS => 3` |
| `disable` | `disable 'table_name'` | `disable 'emp'` |
| `enable` | `enable 'table_name'` | `enable 'emp'` |
| `is_disabled` | `is_disabled 'table_name'` | `is_disabled 'emp'` |
| `is_enabled` | `is_enabled 'table_name'` | `is_enabled 'emp'` |
| `drop` | `drop 'table_name'` (must disable first) | `disable 'emp'` then `drop 'emp'` |

#### 3. DML Commands

| Command | Syntax | Example |
|---------|--------|---------|
| `put` | `put 'table_name', 'row_key', 'col_family:qualifier', 'value'` | `put 'emp', 'row1', 'personal_data:name', 'John Doe'` |
| `get` | `get 'table_name', 'row_key' [, {COLUMNS => ['cf:q']}]` | `get 'emp', 'row1'`, `get 'emp', 'row1', {COLUMN => 'personal_data:name'}` |
| `scan` | `scan 'table_name' [, {LIMIT => n, STARTROW => 'r1', STOPROW => 'r2'}]` | `scan 'emp'`, `scan 'emp', {COLUMNS => ['personal_data:name'], LIMIT => 5}` |
| `delete` | `delete 'table_name', 'row_key', 'col_family:qualifier'` | `delete 'emp', 'row1', 'personal_data:city'` |
| `deleteall` | `deleteall 'table_name', 'row_key'` | `deleteall 'emp', 'row1'` |
| `count` | `count 'table_name' [, INTERVAL => n]` | `count 'emp'` |
| `truncate` | `truncate 'table_name'` | `truncate 'emp'` |
| `incr` | `incr 'table_name', 'row_key', 'cf:q', amount` | `incr 'emp', 'row1', 'stats:login_count', 1` |

#### 4. Tools / Admin Commands
- `major_compact 'table_name'` — initiates a major compaction.
- `flush 'table_name'` — forces a flush of in-memory data to HFile.
- `snapshot 'table_name', 'snapshot_name'` — creates a snapshot.
- `restore_snapshot 'snapshot_name'` — restores a table from a snapshot.

### 1.5.10 HBase Lab — Typical Session

```bash
# Start HBase services
sudo hbase master start
sudo hbase regionserver start

# Open the HBase shell
hbase shell
```

```ruby
hbase(main):001:0> status                           # cluster status
hbase(main):002:0> version                          # HBase version
hbase(main):003:0> whoami                          # current user
hbase(main):004:0> create 'employee', 'personal', 'professional'
hbase(main):005:0> list                              # verify
hbase(main):006:0> describe 'employee'

# Insert rows (each cell is a separate put!)
hbase(main):007:0> put 'employee','1','personal:name','raju'
hbase(main):008:0> put 'employee','1','personal:city','hyderabad'
hbase(main):009:0> put 'employee','1','professional:designation','manager'
hbase(main):010:0> put 'employee','1','professional:salary','50000'

# Read data
hbase(main):011:0> get 'employee','1'
hbase(main):012:0> get 'employee','1', {COLUMN => 'personal:name'}
hbase(main):013:0> scan 'employee'
hbase(main):014:0> scan 'employee', {COLUMNS => ['personal:name'], LIMIT => 5}

# Update — same put syntax, new value
hbase(main):015:0> put 'employee','1','personal:city','Delhi'

# Delete
hbase(main):016:0> delete 'employee','1','personal:city'
hbase(main):017:0> deleteall 'employee','1'

# Count + truncate
hbase(main):018:0> count 'employee'
hbase(main):019:0> truncate 'employee'

# Disable + drop a table
hbase(main):020:0> disable 'employee'
hbase(main):021:0> drop 'employee'

# Multi-table operations (regex)
hbase(main):022:0> disable_all 'raj.*'              # disable all tables starting 'raj'
hbase(main):023:0> drop_all 'raj.*'                 # drop all tables starting 'raj'

hbase(main):024:0> exit
```

**Versions (read multiple versions of a cell):**
```
get 'table_name', 'ROW_KEY', {COLUMN => 'column_family:column', VERSIONS => 3}
```

**Important exam point:** To delete or alter a table, you must **disable** it first. After dropping, the table's metadata is gone; you cannot recover via HBase (the underlying HFiles in HDFS may still exist until cleaned by the master).

### 1.5.11 How is HBase Different from Other NoSQL Models?
- HBase stores data as **key/value pairs in a columnar model** (not as documents like MongoDB or as key-value pairs like Redis/Dynamo).
- All columns are grouped together as **column families**.
- HBase provides a **flexible data model** + **low-latency access** to small amounts of data stored in large datasets.
- HBase on top of Hadoop increases the throughput and performance of the distributed cluster setup.
- Provides faster **random reads and writes** than HDFS alone.

---

## UNIT 1.6 — Hive (Data Warehouse on Hadoop)

### 1.6.1 What is Hive?
**Apache Hive** is a **data warehouse system** built on top of Hadoop for querying and analyzing large datasets stored in HDFS.

- **Query engine wrapper** built on top of MapReduce (or Tez/Spark in modern Hive).
- Treated as the **data warehousing tool** of the Hadoop ecosystem.
- Primarily targeted for **SQL-background users** — provides **HiveQL**, which is similar to SQL.
- Developed by **Facebook**; ASF developed it further; open source. Latest version: 4.2.0.

### 1.6.2 Hive vs Pig  *(★ 2024 Q2.4 — 5 marks)*

| Aspect | Hive | Pig |
|--------|------|-----|
| Language | **Declarative SQL-based** (HiveQL) | **Procedural data-flow** (Pig Latin) |
| Use case | Data analysis + reporting | Programming |
| Users | Data analysts | Researchers + programmers |
| Operates | Server side of a cluster | Client side of a cluster |
| Metadata | Dedicated metadata DB (DDL-driven schema) | No dedicated metadata database |
| Learning curve | Easy for SQL experts | Pig Latin differs significantly from SQL |

### 1.6.3 Features of Hive
- Schema flexibility and evolution.
- Tables can be **partitioned** and **bucketed**.
- Tables are defined directly in the Hadoop file system.
- JDBC/ODBC drivers available.
- Fast and scalable; easy to learn.
- Provides summarisation, analysis, and query of data.
- Supports **external tables** — process data without actually storing it in HDFS.
- Provides a low-level interface to Hadoop.
- Supports **partitioning, bucketing, and indexing** at table level for performance.
- Has a rule-based optimizer for execution plans.

### 1.6.4 Hive Architecture — Major Components

```
   ┌─────────────┐ ┌──────────┐ ┌─────────────────┐
   │ JDBC / ODBC │ │   CLI    │ │  Web Interface  │  ◄── Clients
   └──────┬──────┘ └────┬─────┘ └────────┬────────┘
          │              │                │
          └──────────────┴────────────────┘
                          ▼
                   ┌────────────┐
                   │   Driver   │  ◄── Receives HiveQL
                   │  ┌────────┐│
                   │  │Compiler││
                   │  │Optimizer│
                   │  │Executor ││
                   │  └────────┘│
                   └─────┬──────┘
                         │  metadata ops
                         ▼
                   ┌────────────┐
                   │ Metastore  │  (table schemas, locations, partitions)
                   │  (RDBMS)   │
                   └────────────┘
                         │
                         ▼
                   ┌────────────────────────────┐
                   │       Hadoop (MapReduce    │
                   │       + HDFS + YARN)       │
                   │  JobTracker / NodeManager  │
                   │       Data Node            │
                   └────────────────────────────┘
```

#### Metastore
- Central repository for **metadata** of Hive tables (schema, location).
- Stores **partition metadata** — helps the driver track data distributed over the cluster.
- Metadata is stored in a **traditional RDBMS** (MySQL, PostgreSQL).
- A backup server regularly replicates the data; can be retrieved on data loss.

#### Driver
- Acts like a controller.
- Receives HiveQL statements.
- Creates sessions, monitors the life cycle and progress of execution.
- Stores necessary metadata generated during execution.
- Acts as the collection point of data / query results obtained after the Reduce operation.

#### Compiler
- Compiles the HiveQL query → execution plan.
- Converts the query to an **Abstract Syntax Tree (AST)**.
- After checking compatibility + compile-time errors → converts AST to a **Directed Acyclic Graph (DAG)**.
- The DAG divides operators into MapReduce stages and tasks.

#### Optimizer
- Performs transformations on the execution plan → optimized DAG.
- E.g., converts a pipeline of joins into a single join.
- Splits tasks (e.g., applies a transformation before reduce) for better performance and scalability.

#### Executor
- Executes tasks after compilation and optimization.
- Interacts with the job tracker / YARN RM to schedule tasks.
- Pipelines tasks — dependent tasks run only after prerequisites complete.

#### CLI, UI, Thrift Server
- **CLI** — command-line interface for users to submit queries, instructions, monitor process status.
- **Thrift server** — allows external clients to interact with Hive over a network (similar to JDBC/ODBC).

### 1.6.5 Hive Components (Layered View)

```
┌────────────────────────────────────────────────────┐
│  1. Hive Clients                                   │
│     Thrift Clients  |  JDBC Clients  |  ODBC       │
└────────────────────────────────────────────────────┘
                       ▼
┌────────────────────────────────────────────────────┐
│  2. Hive Services                                  │
│     CLI | Web UI | Hive Server | Hive Driver       │
│          (Compilation → Optimization → Execution)  │
└────────────────────────────────────────────────────┘
                       ▼
┌────────────────────────────────────────────────────┐
│  3. Processing Framework & Resource Mgmt           │
│              MapReduce / Tez   +   YARN             │
└────────────────────────────────────────────────────┘
                       ▼
┌────────────────────────────────────────────────────┐
│  4. Distributed Storage                           │
│                      HDFS                          │
└────────────────────────────────────────────────────┘
                       ▲
┌────────────────────────────────────────────────────┐
│  Metastore (RDBMS)                                 │
└────────────────────────────────────────────────────┘
```

- **Hive Clients:** Thrift clients (any Thrift-supporting language); JDBC clients (Java apps via `apache.hadoop.hive.jdbc.HiveDriver`); ODBC clients.
- **Hive Services:** CLI (default shell), Web Interface (GUI), Hive Server (built on Thrift; "Thrift server"), Hive Driver (receives queries from all interfaces).
- **Processing Framework:** Internally queries execute using Hadoop MapReduce (or Tez/Spark).
- **Distributed Storage:** Hive is installed on Hadoop and uses HDFS data.

### 1.6.6 Working of Hive — Step by Step  *(★ Often asked: explain execution flow)*

```
Internet → Driver → Compiler → Metastore → Driver → Execution Engine
          → JobTracker → TaskTracker (Map|Reduce) → HDFS → Driver → Results
```

1. **Execute Query** — Hive interface (CLI/Web UI) sends query to the Driver (JDBC/ODBC driver).
2. **Get Plan** — Driver takes help of the query compiler, which parses the query to check syntax and produces a query plan.
3. **Get Metadata** — Compiler sends a metadata request to the Metastore.
4. **Send Metadata** — Metastore sends metadata as a response to the compiler.
5. **Send Plan** — Compiler checks requirements and resends the plan to the driver. (Parsing + compiling complete.)
6. **Execute Plan** — Driver sends the execution plan to the execution engine.
7. **Execute Job** — Internally the job is a MapReduce job. The execution engine sends the job to the JobTracker (NameNode), which assigns it to TaskTrackers (DataNodes). The query executes as MapReduce.
   - **7.1 Metadata Ops** — The execution engine can execute metadata operations with the Metastore meanwhile.
8. **Fetch Result** — Execution engine receives results from DataNodes.
9. **Send Results** — Execution engine sends resultant values to the driver.
10. **Send Results** — Driver sends results to Hive Interfaces.

### 1.6.7 Hive Metastore — Modes

The Metastore consists of two fundamental units:
- **Metastore Service** — the software interface handling requests (uses Thrift over the network; manages client access to schemas/locations).
- **Backend Database** — the underlying RDBMS storage (MySQL/PostgreSQL; stores table names, column types, partition details, file storage paths).

| Mode | Description |
|------|-------------|
| **Embedded** | Default. Metastore service + Hive services run in the **same JVM**; uses embedded Derby DB on local FS. **Limitation:** only one Hive session at a time (single Derby DB → single writer). |
| **Local** | Multiple Hive sessions allowed. Metastore service still runs in the same JVM as Hive service; the database (e.g., MySQL) runs in a separate JVM/process (same or remote machine). |
| **Remote** | Metastore and Hive services run in **separate JVMs**. Thrift network APIs are used by different processes. Metastore services scale up based on availability. Clients don't share DB credentials with each Hive user. |

### 1.6.8 Hive vs Traditional RDBMS  *(★ 2025 Q1d — Schema-on-Read vs Schema-on-Write)*

| Feature | Apache Hive | Traditional RDBMS |
|---------|-------------|-------------------|
| Schema management | **Schema on Read** (applies structure during query) | **Schema on Write** (enforces strict structure before saving) |
| Data modifications | Optimized for append (supports ACID transactions in modern Hive, but best for batch loads) | Frequent read/write (highly optimized for concurrent updates/deletes) |
| Data volume scale | Built for **petabyte+** scale | Typically GB to TB |
| Workload type | **OLAP** (batch analytics) | **OLTP** (live applications) |
| Analysis style | Historical batch analysis (scans massive datasets over minutes/hours) | Real-time dynamic analysis (specific records in ms) |
| Scalability | Highly scalable (scales out horizontally via commodity servers) | Expensive to scale (traditionally scales vertically) |

### 1.6.9 Schema-on-Read vs Schema-on-Write  *(★ 2025 Q1d — 2 marks)*

This is the core principle behind how Hive treats data:

- **Schema on Write (RDBMS):** The schema is enforced at **load time**. If the data being loaded doesn't conform to the schema, it is **rejected**. The database parses and serializes data into its internal format before saving. Load is slower; querying is fast because data is already in the right structure.

- **Schema on Read (Hive):** Hive **does NOT verify data when it is loaded**. Instead, the schema is applied when the data is **retrieved (read)**. This makes the initial load extremely fast because data does not have to be parsed or serialized into a database's internal format. The trade-off is that query-time parsing adds overhead, and bad rows surface only at query time.

**Why Hive uses Schema-on-Read:**
- Makes for a **very fast initial load** (just copy raw files into HDFS).
- Lets you re-interpret data with a new schema without reloading — useful when data formats evolve.
- Fits the "write-once, read-many" model of HDFS.

### 1.6.10 Limitations of Hive
- Traditional Hive (prior to 0.14) did not support row-level INSERT/UPDATE/DELETE. Modern Hive supports them via ACID-compliant tables.
- Not designed to replace transactional RDBMS engines — though Hive 3.x+ provides full ACID + transactions with background compaction.
- Strictly **OLAP** — not OLTP. Optimized for high-throughput scans, not real-time access. Queries have **high latency**.
- `NULL` vs `null` — both keywords are treated identically in syntax, but Hive distinguishes a true database NULL (stored as `\N` in text files) from literal strings "NULL" or "null".

### 1.6.11 Hive Data Types

#### Primitive Types
TINYINT, SMALLINT, INT, BIGINT, BOOLEAN, FLOAT, DOUBLE, DECIMAL, STRING, VARCHAR, CHAR, DATE, TIMESTAMP, BINARY.

> Integral literals are assumed to be **INT** by default unless the number exceeds INT range (then it becomes BIGINT) or a postfix is present.

#### Complex Types

| Type | Description | Example |
|------|-------------|---------|
| `STRUCT` | Field-name + value pairs | `STRUCT<email:STRING, phone:STRING>` |
| `ARRAY` | Ordered list of elements | `ARRAY<STRING>` (skills list) |
| `MAP` | Key-value pairs | `MAP<STRING, FLOAT>` (deductions) |
| `UNIONTYPE` | Can hold any one of several types | rare |

**Example table using complex types:**
```sql
CREATE TABLE employees (
  name           STRING,
  salary         FLOAT,
  subordinates   ARRAY<STRING>,
  deductions    MAP<STRING, FLOAT>,
  address        STRUCT<street:STRING, city:STRING, state:STRING, zip:INT>
);
```

### 1.6.12 Implicit Conversion Between Primitive Types
Numeric primitives follow a hierarchy (lowest → highest):
`TINYINT → SMALLINT → INT → BIGINT → FLOAT → DOUBLE`.

- Implicit conversion: child → ancestor (e.g., TINYINT auto-converts to BIGINT or DOUBLE).
- BIGINT can only be converted to FLOAT or DOUBLE, but not vice-versa.
- BOOLEAN and BINARY cannot be implicitly converted to other types.
- DECIMAL can be converted to STRING/VARCHAR only.
- STRING can be converted to VARCHAR, DOUBLE, DECIMAL.
- DATE/TIMESTAMP convert to STRING/VARCHAR.
- **Explicit conversion** uses `CAST(expr AS type)` — returns NULL if conversion fails.

### 1.6.13 Hive Data Model

```
Hive Data Model
├── Database / Directory   (HDFS directory: /user/hive/warehouse/<db>.db)
├── Tables                 (sub-directory inside the database)
├── Partitions             (sub-directory inside the table)
└── Buckets                (files inside a partition)
```

- **Default database** = `default`.
- Default warehouse location = `/user/hive/warehouse` (configurable via `hive.metastore.warehouse.dir`).
- **A database, table, or partition in Hive is just an HDFS directory.**

### 1.6.14 Database DDL Commands

```sql
-- Create
CREATE DATABASE <name>;
CREATE DATABASE IF NOT EXISTS <name>;
CREATE (DATABASE|SCHEMA) [IF NOT EXISTS] db_name
  [COMMENT 'comment']
  [LOCATION 'hdfs_path']
  [WITH DBPROPERTIES ('k'='v', ...)];

-- List / inspect
SHOW DATABASES;
SHOW DATABASES LIKE 'db.*';
DESCRIBE DATABASE db_name;
DESCRIBE DATABASE EXTENDED db_name;

-- Switch / drop
USE db_name;
DROP DATABASE [IF EXISTS] db_name [CASCADE];   -- CASCADE drops databases with tables
```

### 1.6.15 Hive Tables — Internal (Managed) vs External  *(★ 2025 Q2 — 7 marks)*

#### Managed (Internal) Table
- Hive manages the **entire lifecycle** of both metadata and data.
- Data is stored in the warehouse directory by default (`/user/hive/warehouse/`).
- **DROP TABLE → deletes metadata AND data in HDFS.**
- Use when data is temporary / Hive should own the lifecycle.

#### External Table
- Storage is **not managed by Hive** — Hive only manages the metadata.
- The data already exists in HDFS; we just attach a schema on top of it.
- **DROP TABLE → only deletes metadata; data remains in HDFS.**
- Use when:
  - The data is also used outside of Hive (other programs read the files).
  - Data needs to remain in the underlying location even after DROP TABLE.
  - You want to use a custom HDFS location.
  - You want Hive to NOT own data.
  - You are not creating the table based on existing tables (AS SELECT).

### 1.6.16 CREATE TABLE Syntax  *(★ 2025 Q2a — 3 marks)*

```sql
CREATE [TEMPORARY] [EXTERNAL] TABLE [IF NOT EXISTS] [db_name.]table_name (
  column_name data_type [COMMENT 'column_comment'],
  ...
)
[COMMENT 'table_comment']
[PARTITIONED BY (partition_col data_type [COMMENT '...'], ...)]
[CLUSTERED BY (column_name, ...) [SORTED BY (column_name [ASC|DESC], ...)] INTO n BUCKETS]
[SKEWED BY (column_name, ...) ON ((value, ...), ...) [STORED AS DIRECTORIES]]
[
  [ROW FORMAT row_format]
  [STORED AS file_format | STORED BY 'storage.handler.class.name' [WITH SERDEPROPERTIES (...)]]
]
[LOCATION 'hdfs_path']
[TBLPROPERTIES ('k'='v', ...)]
[AS select_statement];
```

| Keyword | Use |
|---------|-----|
| `TEMPORARY` | Session-scoped table. |
| `EXTERNAL` | Data already present in HDFS; only metadata is stored. |
| `IF NOT EXISTS` | Suppress warning if table exists. |
| `COMMENT` | Column-level + table-level comments. |
| `PARTITIONED BY` | Partition columns. |
| `CLUSTERED BY … INTO n BUCKETS` | Bucketing. |
| `SORTED BY` | Part of bucketing. |
| `SKEWED BY` | Query optimization for skewed data. |
| `ROW FORMAT` | Row format — text, ORC, Avro, etc. |
| `STORED AS` | Storage format. |
| `LOCATION` | Required for EXTERNAL tables. |
| `TBLPROPERTIES` | Custom properties. |

### 1.6.17 Data Loading & Insertion

```sql
-- Load data from HDFS
LOAD DATA INPATH '/user/hadoop/employee.csv' INTO TABLE employee;

-- Load from local file system
LOAD DATA LOCAL INPATH '/home/cloudera/Documents/employee.csv' INTO TABLE employee;

-- Overwrite existing data
LOAD DATA LOCAL INPATH '...' OVERWRITE INTO TABLE employee;

-- Insert single row
INSERT INTO TABLE employee VALUES (1, 'Deepak', 30000);

-- Insert from another table
INSERT INTO TABLE employee SELECT * FROM employee_temp;

-- Insert overwrite (replace data)
INSERT OVERWRITE TABLE employee SELECT * FROM employee_temp;
```

### 1.6.18 CTAS — Create Table As Select

```sql
CREATE TABLE new_table AS SELECT col1, col2 FROM existing_table WHERE ...;
```

**Restrictions:**
- Cannot create a partitioned table.
- Cannot create an external table.
- Cannot create a list-bucketing table.
- Triggers a MapReduce job to populate data (even `SELECT *` triggers a job).

### 1.6.19 Partitions  *(★ Frequently asked — concepts and code)*

A method of separating a table into related parts based on column values (date, city, department). Each partition corresponds to a subdirectory in the table's directory in HDFS.

**Why partition?**
- By default a Hive query scans the whole table.
- Partitioning restricts the scan to only the relevant partitions, greatly reducing I/O and query time.

#### Static Partitioning
```sql
CREATE TABLE student_tab (id INT, name STRING, dept STRING, yoj INT)
PARTITIONED BY (year STRING)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';

LOAD DATA LOCAL INPATH 'tab1/clientdata/2009/file2'
OVERWRITE INTO TABLE student_tab PARTITION (year='2009');

LOAD DATA LOCAL INPATH 'tab1/clientdata/2010/file3'
OVERWRITE INTO TABLE student_tab PARTITION (year='2010');
```

To use strict mode (forces partition filtering on every query):
```sql
SET hive.mapred.mode = strict;
```

#### Dynamic Partitioning
Useful when partition column values are known only at execution time. Hive creates partitions on the fly based on the data.

```sql
-- Enable dynamic partition mode
SET hive.exec.dynamic.partition = true;
SET hive.exec.dynamic.partition.mode = nonstrict;

-- Create a staging (non-partitioned) table
CREATE TABLE student_src (
  id INT, name STRING, dept STRING, year STRING
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/user/hive/student_src';

-- Create the partitioned target table (empty)
CREATE TABLE student_part (
  id INT, name STRING, dept STRING
)
PARTITIONED BY (year STRING)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE;

-- Dynamically insert: Hive creates a partition per unique year value
INSERT INTO TABLE student_part PARTITION (year)
SELECT id, name, dept, year FROM student_src;
-- Note: partitioning column must be mentioned LAST in the SELECT.

SHOW PARTITIONS student_part;
```

**Comparison: Static vs Dynamic**

| Aspect | Static | Dynamic |
|--------|--------|---------|
| When is the partition column known? | At load time | At execution time |
| Speed | Faster | Slower (more time to load) |
| ALTER partition | Yes | No (drop is allowed) |
| Source | Existing file with known key | Existing non-partitioned table |

**Partitioning advantages:**
- Distributes execution load horizontally.
- Faster queries with low volume of data per partition.

**Partitioning disadvantages:**
- Possibility of too many small partitions → too many directories.
- Not effective when partitioning produces very unequal sizes (e.g., country — big countries dominate).

### 1.6.20 Bucketing  *(★ Important concept)*

Bucketing is another technique to decompose table data into more manageable parts. It is used when partitioning is not ideal (e.g., for high-cardinality columns like `user_id`).

**Mechanism:** Hash function on a column → modulo by the number of buckets → which bucket file the row goes to.

```
bucket_number = hash(column) MOD number_of_buckets
```

```sql
CREATE TABLE emp_bucket (
  id INT, dept STRING, salary FLOAT
)
CLUSTERED BY (id) INTO 5 BUCKETS
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';

-- Enable bucketing (older Hive)
SET hive.enforce.bucketing = true;

INSERT OVERWRITE TABLE emp_bucket SELECT * FROM emp_demo;
```

**Bucketing with partitioning:**
```sql
CREATE TABLE emp_part_bucket (
  id INT, salary INT
)
PARTITIONED BY (dept STRING)
CLUSTERED BY (id) INTO 5 BUCKETS
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';
```

**Advantages of Bucketing:**
- **Sampling** — quickly query a representative subset of data.
- Speeds up joins (if both tables are bucketed on the join key).
- Equally distributed data files.

**Sampling queries:**
```sql
-- Bucket sampling
SELECT * FROM T_USER_LOG_BUCKET
TABLESAMPLE (BUCKET 1 OUT OF 4 AT user_id);

-- Block sampling (percentage of HDFS blocks)
SELECT * FROM T_USER_LOG_BUCKET
TABLESAMPLE (20 PERCENT);
```

### 1.6.21 Operators in Hive

Four types: **Relational, Arithmetic, Logical, Complex**.

#### Relational Operators
`A=B`, `A != B`, `A<B`, `A<=B`, `A>B`, `A>=B`, `A IS NULL`, `A IS NOT NULL`, `A LIKE B`, `A RLIKE B`, `A REGEXP B`.

```sql
SELECT * FROM employee WHERE id = 1241;
SELECT * FROM emp WHERE department IS NOT NULL;
```

#### Arithmetic Operators
`A+B`, `A-B`, `A*B`, `A/B`, `A%B`, `A&B` (bitwise AND), `A|B` (bitwise OR), `A^B` (XOR), `~A` (NOT).

```sql
SELECT id, dept, sal + 1000 FROM emp;   -- shows salary with 1000 added (does NOT update table)
```

#### Logical Operators
`A AND B`, `A && B`, `A OR B`, `A || B`, `NOT A`, `!A`.

```sql
SELECT * FROM emp WHERE salary > 20000 && dept = 'SRE';
```

#### Complex Operators
- `A[n]` — nth element of array A (0-indexed).
- `M[key]` — value for key in map M.
- `S.x` — field x of struct S.

### 1.6.22 Built-in Functions

| Function | Description |
|----------|-------------|
| `round(double a)` | Rounded BIGINT. |
| `floor(double a)` | Max BIGINT ≤ a. |
| `ceil(double a)` | Min BIGINT ≥ a. |
| `rand()`, `rand(int seed)` | Random number. |
| `concat(string A, string B, ...)` | Concatenate strings. |
| `substr(string A, int start)` / `substr(string A, int start, int length)` | Substring. |
| `upper(string A)`, `ucase(string A)` | Uppercase. |
| `lower(string A)`, `lcase(string A)` | Lowercase. |
| `trim`, `ltrim`, `rtrim` | Trimming. |
| `regexp_replace(string A, string B, string C)` | Replace substrings matching B with C. |
| `size(Map<K.V>)`, `size(Array<T>)` | Number of elements. |
| `cast(expr AS type)` | Type conversion; returns NULL on failure. |
| `from_unixtime(int unixtime)` | Convert seconds since epoch to timestamp string. |
| `to_date(string ts)` | Date part of timestamp. |
| `year(date)`, `month(date)`, `day(date)` | Year/month/day parts. |

### 1.6.23 Aggregate Functions
`count(*)`, `count(expr)`, `count(DISTINCT col)`, `sum(col)`, `avg(col)`, `min(col)`, `max(col)`, `rank()`.

```sql
SELECT count(*) FROM emp;
SELECT avg(DISTINCT price) FROM emp;
SELECT max(price) FROM emp;
SELECT gender, count(DISTINCT userid) FROM emp GROUP BY gender;
```

### 1.6.24 Views

A **view** is a purely **logical construct** (an alias for a query) — **no physical data** behind it.

- Logical data structure used to simplify queries by hiding complexity (subqueries, joins, filters) or by flattening data.
- Unlike RDBMS views, Hive views **do not store data** or a physical table structure.
- Once created, the view's description and schema are **frozen immediately**. Changes to underlying tables (e.g., adding a column) will not be reflected.
- View schema is frozen at creation.
- View is **read-only** — may not be used directly to LOAD/INSERT/ALTER data.
- When an underlying table is dropped or changed, subsequent attempts to query the invalid view will fail.

```sql
-- Create a view that filters rows
CREATE VIEW emp_30000 AS
SELECT * FROM employee WHERE salary > 30000;

-- Create a view that picks columns
CREATE VIEW v2 AS SELECT c1, c3, c7 FROM t1;

-- Create a view that filters + transforms
CREATE VIEW v5 AS
SELECT c1, CAST(c3 AS STRING) c3, CONCAT(c4, c5) c5, TRIM(c6) c6, "Constant" c8
FROM t1;

-- Create a view joining two tables
CREATE VIEW v6 AS
SELECT t1.c1, t2.c2 FROM t1 JOIN t2 ON t1.id = t2.id;

-- Alter view (only metadata changes)
ALTER VIEW [db.]view_name AS select_statement;
ALTER VIEW [db.]view_name RENAME TO [db.]view_name;

-- Drop view (only metadata changes; no data file is touched)
DROP VIEW [IF EXISTS] [db.]view_name;
```

### 1.6.25 Querying — Joins, Sampling, UNION, Subqueries

#### Joins
Hive supports INNER, LEFT OUTER, RIGHT OUTER, FULL OUTER, LEFT SEMI, EQUI, and CROSS joins.

```sql
-- INNER join (only matching rows)
SELECT c.ID, c.NAME, c.AGE, o.AMOUNT
FROM customers c JOIN orders o
ON (c.ID = o.CUSTOMER_ID);

-- LEFT OUTER (all customers; NULL when no order)
SELECT c.ID, c.NAME, o.AMOUNT, o.DATE
FROM customers c LEFT OUTER JOIN orders o
ON (c.ID = o.CUSTOMER_ID);

-- RIGHT OUTER (all orders; NULL when no customer)
SELECT c.ID, c.NAME, o.AMOUNT, o.DATE
FROM customers c RIGHT OUTER JOIN orders o
ON (c.ID = o.CUSTOMER_ID);

-- FULL OUTER (all customers + all orders; NULLs where no match)
SELECT c.ID, c.NAME, o.AMOUNT, o.DATE
FROM customers c FULL OUTER JOIN orders o
ON (c.ID = o.CUSTOMER_ID);
```

#### Sampling (only on bucketed tables)
```sql
-- Bucket sampling
SELECT * FROM T_USER_LOG_BUCKET TABLESAMPLE (BUCKET 1 OUT OF 4 AT user_id);

-- Block sampling
SELECT * FROM T_USER_LOG_BUCKET TABLESAMPLE (20 PERCENT);
```

#### UNION
```sql
INSERT OVERWRITE TABLE target_table
SELECT name, id, category FROM source_table_1
UNION ALL
SELECT name, id, "Category159" AS category FROM source_table_2;

-- Or simply
SELECT key FROM src UNION SELECT key FROM src1 ORDER BY key LIMIT 10;
```

#### Subqueries
| Location | Support |
|----------|---------|
| `SELECT` list | **NOT supported** — Hive forbids scalar/correlated subqueries in the SELECT list. Workaround: use a LEFT JOIN + GROUP BY. |
| `FROM` clause | **Supported.** The subquery MUST be aliased. Columns must have unique names. Supports arbitrary levels; can include UNION. |
| `WHERE` clause | **Supported since Hive 0.13.** Supports `IN / NOT IN` (single column), `EXISTS / NOT EXISTS` (requires correlated predicates). |

```sql
-- FROM clause subquery (aliased)
SELECT department, avg_salary
FROM (
  SELECT department, AVG(salary) AS avg_salary
  FROM employees
  GROUP BY department
) AS dept_summary;

-- WHERE IN subquery
SELECT * FROM customer
WHERE customer_num IN (
  SELECT DISTINCT customer_num FROM orders WHERE amount > 2000
);

-- WHERE EXISTS subquery
SELECT e.emp_id, e.emp_name
FROM employees e
WHERE EXISTS (
  SELECT 1 FROM employee_projects p WHERE e.emp_id = p.emp_id
);
```

#### Sorting: ORDER BY vs SORT BY
- `ORDER BY` — sorts **globally** (single reducer).
- `SORT BY` — sorts **per reducer** (parallel sort, faster but partial ordering).
- `DISTRIBUTE BY` — controls which rows go to which reducer.
- `CLUSTER BY` = `DISTRIBUTE BY` + `SORT BY` on the same columns.

### 1.6.26 Common HQL Keywords Cheat Sheet

| Keyword | Purpose |
|---------|---------|
| `SELECT` | Pick columns. |
| `WHERE` | Filter rows before aggregation. |
| `GROUP BY` | Group rows by column. |
| `HAVING` | Filter rows **after** aggregation. |
| `ORDER BY` | Global sort. |
| `SORT BY` | Per-reducer sort. |
| `DISTRIBUTE BY` | Control row distribution to reducers. |
| `CLUSTER BY` | DISTRIBUTE BY + SORT BY on same columns. |
| `LIMIT` | Restrict number of output rows. |

### 1.6.27 Hive Summary (from slides)
1. Apache Hive is an open source data warehouse system built on top of Hadoop for querying and analyzing large datasets stored in the Hadoop file system.
2. Hive architecture consists of Hive Clients, Hive Services, Compiler, Optimizer, Distributed Storage, etc.
3. Hive metastore is the central repository of Hive metadata.
4. Hive Data Definition Language (DDL) is a subset of Hive SQL statements used for creating, deleting, or altering schema objects.
5. Hive partitions is a method of separating a table into related parts based on column values like date, city, and department.
6. In Hive, views are logical data structures that can be used to simplify queries by hiding complexities such as subqueries, joins, and filters.

---

## PYQ 2025 — Model Answers (25-Mark Paper)

> **Exam hint:** Read each question carefully. The 2025 paper has 3 questions totalling 25 marks. You have 1 hour. Pace yourself: ~10 min on Q1, ~15 min on Q2, ~25 min on Q3.

### Q1 — Answer the following (2 × 4 = 8 marks)

#### Q1a) Define the role of the Combiner in a MapReduce job? State the phase after which it will be used.  *(2 marks)*

**Role of Combiner:**
The Combiner is a **local-reducer** that runs on the **output of the Mapper** at the same node where the mapper ran, before the intermediate `<key, value>` pairs are sent across the network to the Reducer. Its role is to perform **local aggregation** of intermediate keys, which:
- Reduces the **memory and disk** requirements of Map tasks.
- Reduces the **network traffic** between mappers and reducers.

**Phase after which it is used:**
The Combiner runs **after the Map phase and before the Shuffle & Sort phase** (i.e., between Map and Shuffle). The Combiner's class is the same as the Reducer's class. It must be **associative and commutative** because the framework may call it 0, 1, or multiple times per key.

```
INPUT → MAP → COMBINER → SHUFFLE & SORT → REDUCE → OUTPUT
```

**Example:** A mapper emits `(Car,1), (Car,1), (River,1)`. The Combiner can locally aggregate to `(Car,2), (River,1)`, sending less data to the reducer.

---

#### Q1b) Why is checkpointing used in HDFS?  *(2 marks)*

**Purpose of checkpointing in HDFS:**
- The Primary NameNode keeps the active file-system metadata **in RAM** for fast access.
- It logs every change in real-time to an **EditLog** file on disk, and periodically saves a snapshot of the file-system structure to an **FsImage** file.
- If the EditLog grows without bound, restarting the NameNode would require replaying every transaction → could take hours.

**Checkpointing solves this problem:**
The Secondary NameNode periodically:
1. **Fetches** the current FsImage + EditLog from the Primary NameNode.
2. **Merges** them in its own memory to create a new, updated FsImage (called a *checkpoint*).
3. **Uploads** the new FsImage back to the Primary NameNode.
4. The Primary NameNode replaces its old FsImage and **truncates the EditLog**.

**Result:** EditLog stays small → NameNode restart is fast → HDFS reliability improved.

---

#### Q1c) How does HBase's data model differ from a traditional relational database? Give two main differences.  *(2 marks)*

**Difference 1 — Storage orientation:**
- **HBase** uses a **column-oriented data model**. Data is stored column-family-wise (the table schema defines only column families; column qualifiers can be added per row), enabling fast retrieval of specific columns over billions of rows.
- **RDBMS** uses a **row-oriented data model** with a fixed, rigid schema. Every row stores all columns; adding a new column requires `ALTER TABLE`.

**Difference 2 — Schema & scaling model:**
- **HBase** is **schema-less** at the column level (only column families are defined upfront). It is **horizontally scalable** with built-in automatic partitioning (regions distributed across RegionServers).
- **RDBMS** has a **fixed, rigid schema** (every row must conform). It typically scales **vertically** (buy a bigger machine); no built-in automatic partitioning.

*(Optional extra: HBase stores each cell value with a timestamp → supports multiple versions of the same data. RDBMS stores only the latest value.)*

---

#### Q1d) What is the core principle of "Schema-on-Read" as used by Hive? How is it different from "Schema-on-Write"?  *(2 marks)*

**Schema-on-Read (Hive's core principle):**
Hive does **not verify the data when it is loaded**. Instead, the schema is applied **at the time of query (read)**. The data is simply copied into HDFS as raw files; Hive's metastore stores only the schema definition (column names + types + location). When a query runs, Hive reads the raw files, parses each row according to the schema, and applies the query.

**How it differs from Schema-on-Write (RDBMS):**
In Schema-on-Write, the schema is **enforced at load time** — the database parses the data, validates it against the schema, and serializes it into its internal format before saving. If a row does not conform, it is **rejected**.

| Aspect | Schema-on-Read (Hive) | Schema-on-Write (RDBMS) |
|--------|------------------------|---------------------------|
| Verification at load | No | Yes |
| Load speed | Very fast (just file copy) | Slower (parse + serialize) |
| Query speed | Slower (parsing at query time) | Faster (data already structured) |
| Schema evolution | Easy (just change metastore; no reload) | Requires ALTER + reload |
| Bad rows surface when? | At query time | At load time |

---

### Q2 — Hive External Table Query (7 marks)

Given:
```text
External table: Book
Schema:  (book_id INT, title STRING, author STRING, price FLOAT)
HDFS location: /user/hive/input/
Comma-delimited text format.
Local file: /home/cloudera/book_data.txt
```

#### Q2a) Write the Hive Query to create the `Book` table (external, comma-delimited).  *(3 marks)*

```sql
CREATE EXTERNAL TABLE IF NOT EXISTS Book (
  book_id  INT,
  title    STRING,
  author   STRING,
  price   FLOAT
)
COMMENT 'External table storing book records'
ROW FORMAT DELIMITED
  FIELDS TERMINATED BY ','
  LINES TERMINATED BY '\n'
STORED AS TEXTFILE
LOCATION '/user/hive/input/';
```

**Key points to highlight:**
- `EXTERNAL` keyword — table is external, not managed by Hive.
- `ROW FORMAT DELIMITED FIELDS TERMINATED BY ','` — declares comma as the field delimiter.
- `STORED AS TEXTFILE` — declares the storage format as plain text.
- `LOCATION '/user/hive/input/'` — points Hive to the existing HDFS directory (mandatory for external tables).

#### Q2b) Write the command to load data into it from the local file `/home/cloudera/book_data.txt`, overwriting the previous content.  *(2 marks)*

```sql
LOAD DATA LOCAL INPATH '/home/cloudera/book_data.txt'
OVERWRITE INTO TABLE Book;
```

**Key points:**
- `LOCAL INPATH` — file is on the **local** filesystem of the Hive client machine, not HDFS.
- `OVERWRITE` — replaces any existing content in the table directory with the new file.
- If `OVERWRITE` was omitted, the file would be appended (added to existing files in the table directory).

#### Q2c) Write a query to create a new **managed** table `ExpensiveBooks`, containing all columns for books with a price greater than 100.  *(2 marks)*

```sql
CREATE TABLE ExpensiveBooks AS
SELECT book_id, title, author, price
FROM Book
WHERE price > 100;
```

**Why this works:**
- The `CREATE TABLE … AS SELECT` (CTAS) form creates a **managed** (internal) table by default.
- No `EXTERNAL` keyword → managed table.
- The new table's schema is derived from the SELECT — it inherits the column names and types from `Book`.
- The WHERE clause filters books with `price > 100`.
- Hive will run a MapReduce job to populate the new table.

*(Note: CTAS cannot create a partitioned or external table — so this is a perfect use case.)*

---

### Q3 — YARN Workflow OR HDFS Architecture & Write (5 + 5 = 10 marks)

#### OPTION A — Explain the purpose of each core component of Hadoop YARN and the workflow.  *(5 + 5 = 10 marks)*

**Core components of YARN (5 marks):**

1. **Client**
   - The entity that initiates and submits an application (e.g., MapReduce job, Spark application) to the YARN Resource Manager.
   - Communicates with the RM to request execution and monitors job status.
   - May also interact with the Application Master for progress updates.
   - Acts as the user's interface to launch and manage applications on the Hadoop cluster.

2. **Resource Manager (RM)** — the *master* daemon
   - Responsible for **global resource assignment and management** across the cluster.
   - Two sub-components:
     - **Scheduler** — pure scheduler that allocates resources (containers) to applications based on capacity, queues, etc. (Capacity / Fair Scheduler plug-ins). It does **not** monitor applications or restart failed tasks.
     - **Applications Manager** — accepts job submissions, negotiates the **first container** for the Application Master, and restarts the AM on failures.

3. **Node Manager (NM)** — the *slave* daemon (one per node)
   - Manages individual nodes; registers with RM and sends heartbeats (node health).
   - Monitors resource usage (CPU, memory) on its node.
   - Creates, monitors, and kills containers as directed by RM or AM.
   - Manages log files.

4. **Application Master (AM)** — one per application
   - Negotiates resources (containers) from the RM for the application's tasks.
   - Works with Node Managers to launch and monitor the application's tasks within containers.
   - Tracks the status/progress of its application → reports back to RM.
   - Requests new containers if tasks fail.

5. **Container**
   - A collection of physical resources (RAM, CPU cores, disk) on a single node.
   - The **unit of allocation** granted by the scheduler.
   - Invoked via Container Launch Context (CLC) — contains environment variables, security tokens, dependencies.

**YARN Application Workflow (5 marks):**

1. **Application Submission** — Client submits the application (code + configuration + resource requirements) to the Resource Manager.
2. **Application Master Launch** — RM allocates a container on a Node Manager to launch the Application Master for this application.
3. **AM Registration** — The newly launched AM registers itself with the RM, indicating it's ready to manage the application.
4. **Resource Negotiation** — AM negotiates with RM for the necessary containers (CPU + memory) for the application's tasks.
5. **Container Launch Notification** — Once containers are allocated by RM, AM notifies the corresponding Node Managers to launch these containers and execute tasks within them.
6. **Task Execution** — Application's code and tasks execute inside the allocated containers on the Node Managers.
7. **Monitoring and Status Reporting** — Client monitors status via RM or AM. AM monitors task progress and reports to RM.
8. **Completion and Deregistration** — Upon completion, AM unregisters with RM, releasing allocated resources.

---

#### OPTION B — HDFS architecture & write process (10 marks)

**B(a) Two main architectural components of HDFS and their primary responsibilities (4 marks):**

HDFS has a master-slave architecture:

1. **NameNode (Master)**
   - Manages the file-system namespace — file names, directory tree, permissions.
   - Maintains the mapping of *files → blocks → DataNodes* (metadata only).
   - Does NOT store actual data; keeps FsImage (snapshot since beginning) + EditLog (recent changes).
   - Receives heartbeats and block reports from all DataNodes.
   - Performs replication, rebalancing, data integrity checks.

2. **DataNode (Slave / Worker)**
   - Stores actual data blocks on local disk.
   - Serves client read/write requests.
   - Sends heartbeats (every 3 s) and block reports (every 6 h) to NameNode.
   - Performs block creation, deletion, replication as instructed by NameNode.

(*Note: Secondary NameNode is a checkpoint helper, not a backup NameNode.*)

**B(b) Step-by-step write process when a client writes `data.txt` to HDFS (4 marks):**

1. **Client requests file creation** — calls `create()` on the DistributedFileSystem.
2. **NameNode response** — NameNode verifies permissions, creates a new file entry in the namespace, and returns a list of DataNodes `[DN1, DN2, DN3]` for the first block (using rack-aware replica placement).
3. **Pipeline formation** — client establishes a write pipeline: `Client → DN1 → DN2 → DN3`.
4. **Data streaming** — client writes data into an internal buffer; the data is split into packets and streamed to DN1, which immediately forwards each packet to DN2, which forwards to DN3.
5. **Acknowledgments** — once DN3 receives a packet, it sends an ACK back: DN3 → DN2 → DN1 → Client. Only after the client receives the ACK does it consider the packet durable.
6. **Block completion** — when 128 MB (default block size) is written, the client closes the block and requests the next block's DataNodes from the NameNode. Steps 3-5 repeat.
7. **File close** — when all data is written, the client calls `close()`. The DataNodes report the new blocks to the NameNode.
8. **Replication verification** — NameNode checks if all replicas were written; if any DataNode failed mid-pipeline, it re-replicates to maintain the replication factor of 3.

**Key roles of each component in the write process:**
- **NameNode** — provides metadata (block IDs, DataNode list, replication target), records the file in namespace, tracks block locations.
- **DataNodes** — physically store the data blocks, replicate via pipeline, send ACKs.
- **Client** — splits data into packets, manages the write pipeline, closes file.
- **Secondary NameNode** — *not* involved in writes; runs periodically to checkpoint FsImage+EditLog.

**B(c) One key advantage and one key limitation of HDFS over a traditional local file system (2 marks):**

- **Advantage:** **Distributed + fault-tolerant storage** — HDFS splits huge files into blocks (e.g., 128 MB) and replicates each block (default factor 3) across multiple machines, so data survives disk/node failures. A traditional local FS stores the file on a single disk; loss of that disk = permanent data loss.

- **Limitation:** **No low-latency random access** — HDFS is optimized for write-once-read-many **streaming** access; reading a single random record still requires scanning an entire 128 MB block. A traditional local FS, with its in-kernel index structures and page cache, can do millisecond random access. (HBase sits on top of HDFS to provide this random-access capability.)

---

## PYQ 2024 — Model Answers (50-Mark Paper)

> **Note:** The 2024 paper tests Spark, RDDs, and Pig, which are typically Unit-2 topics and were not in the slides you were given. The model answers below include a concise brief for each so you can answer them confidently if a similar question appears.

### Q1.1 — The 5 V's of Big Data  *(5 marks)*

*(Use the table from §1.1.3. Explain each V with examples. Highlight: Volume = ~402M TB/day; Velocity = real-time decisions like e-promotions; Variety = structured + semi-structured + unstructured; Veracity = data quality, sensor malfunction, misinformation; Value = Uber surge pricing, oil & gas leak detection.)*

### Q1.2 — Draw and explain Hadoop ecosystem in detail.  *(10 marks)*

*(Draw the ecosystem diagram from §1.2.3 and explain each of: HDFS, HBase, YARN, MapReduce, Spark, Pig, Hive, Mahout/MLlib, Solr/Lucene, Zookeeper, Oozie, Flume, Sqoop, Ambari. Use the one-line explanations provided in §1.2.3.)*

#### OR — Q1.2 (Alt) — Draw and explain read and write operations performed in HDFS in Hadoop.  *(10 marks)*

*(See §1.2.6 — Read operation (NameNode returns block locations, client reads directly from closest DataNode) and Write operation (client creates file → NameNode returns DataNode list → data pipelined through DN1→DN2→DN3 → ACKs flow back). Provide labelled diagrams for each.)*

### Q2.1 — Spark vs Hadoop MapReduce — which to choose for a massive dataset growing every minute?  *(5 marks)*

**Choice:** Use **Apache Spark** for a massive dataset that is growing every minute.

**Justification (trade-offs):**

1. **Performance** — Spark uses **in-memory processing** through RDDs/Dataset/DataFrame abstractions. It can be **10–100× faster than MapReduce** for iterative algorithms (ML, graph processing) because intermediate results stay in memory between stages, whereas MapReduce writes every intermediate output to disk. For a continuously growing dataset, Spark Streaming / Structured Streaming can process data in micro-batches (sub-second latency), while MapReduce is fundamentally a batch-processing model with high per-job latency.

2. **Fault tolerance** — MapReduce achieves fault tolerance by **re-executing failed tasks** from intermediate outputs on disk. Spark achieves it through **RDD lineage**: each RDD remembers its derivation graph (DAG of transformations), so a lost partition can be recomputed from its parents. This is faster than re-executing an entire job from scratch, but lineage graphs that get very long can become expensive to recompute.

3. **Ease of use** — Spark provides high-level APIs in **Scala, Java, Python (PySpark), and R**, plus a declarative DataFrame/Dataset API and a SQL interface. MapReduce requires writing verbose Mapper/Reducer classes (typically in Java), with manual handling of input formats, combiners, partitioners. Spark is therefore significantly easier for analysts and data scientists.

**Trade-offs (counter-points):**
- MapReduce is more **mature**, easier to **tune** for very large batch jobs, and integrates well with existing Hadoop 1.0 clusters.
- Spark requires **more memory** per node (RAM is the bottleneck) and is less efficient for truly streaming workloads than dedicated streaming engines like Flink.
- For a one-shot batch transformation of a multi-petabyte dataset with no iteration, MapReduce can be sufficient.

**Conclusion:** Because the dataset is *growing every minute* (suggesting real-time or near-real-time analytics) and because Spark is significantly faster for iterative analytics and easier to develop in, **Spark is the right choice**.

### Q2.2 — Importance of RDDs in Apache Spark. How do they enable parallelism?  *(5 marks)*

**What is an RDD?**
An **RDD (Resilient Distributed Dataset)** is the **fundamental abstraction** in Apache Spark — a **read-only, partitioned collection of records** distributed across the cluster. RDDs can be created in two ways:
- **Parallelizing** an existing collection in the driver program (e.g., `sc.parallelize(List(1,2,3))`).
- **Reading** from a file in any storage backed by Hadoop (e.g., `sc.textFile("hdfs://...")`).

**Importance:**
1. **Fault tolerance via lineage** — RDDs remember their parent RDDs and the transformation used to derive them. If a partition is lost (e.g., node failure), it can be **recomputed** from the lineage graph, without expensive data replication.
2. **Lazy evaluation** — transformations (`map`, `filter`, `flatMap`) build up a DAG but do not execute until an action (`collect`, `count`, `save`) is called. This allows Spark to optimize the entire plan before executing.
3. **In-memory storage** — RDD partitions can be cached in memory across operations, dramatically speeding up iterative algorithms (machine learning, graph processing) that reuse the same data.
4. **Immutability** — RDDs are read-only; each transformation returns a new RDD. This makes them safe to share across threads/nodes.
5. **Locality-aware scheduling** — Spark tries to schedule tasks on the nodes where the partitions are stored → minimizes network I/O.

**How RDDs enable parallelism:**
- Each RDD is **divided into partitions** — a logical chunk of data.
- Spark launches **one task per partition** in parallel across the executors in the cluster.
- The scheduler assigns tasks to executors based on **data locality** (prefer the node holding the partition's data).
- Transformations like `map` are applied independently per partition → embarrassingly parallel.
- `reduceByKey` triggers a **shuffle** — partitions are reorganized by key so all values for a key go to the same executor, where the reduce function aggregates them in parallel across keys.

**Example:**
```python
rdd = sc.textFile("hdfs://data.txt")     # partitioned across HDFS blocks
words = rdd.flatMap(lambda line: line.split())
pairs = words.map(lambda w: (w, 1))
counts = pairs.reduceByKey(lambda a, b: a + b)   # shuffle + parallel reduce
counts.collect()
```
- `textFile` creates an RDD partitioned by HDFS blocks (e.g., 100 blocks → 100 partitions → 100 parallel tasks).
- Each task runs `flatMap` + `map` independently on its local partition (data locality → no network I/O).
- `reduceByKey` triggers a shuffle so that all pairs with the same key end up on the same executor → reducers run in parallel across keys.

### Q2.3 — List and explain, with example, any five transformation functions and action functions in Spark.  *(5 marks)*

**Transformations** (return a new RDD; lazy — not executed until an action is called):

| Transformation | Description | Example |
|-----------------|-------------|---------|
| `map(f)` | Apply function `f` to each element → new RDD with one output per input. | `rdd.map(x => x * 2)` → `[2, 4, 6]` for input `[1,2,3]` |
| `filter(f)` | Return a new RDD with only elements where `f` returns true. | `rdd.filter(x => x > 1)` → `[2, 3]` |
| `flatMap(f)` | Like `map`, but each input can produce 0 or more outputs. | `rdd.flatMap(line => line.split(" "))` → splits each line into words |
| `reduceByKey(f)` | Merge values for each key using `f`. (Requires pair RDD.) | `pairs.reduceByKey(_ + _)` → sums values per key |
| `groupByKey()` | Group values for each key → `(K, Iterable[V])`. | `pairs.groupByKey()` |

**Actions** (trigger computation; return a value or write output):

| Action | Description | Example |
|--------|-------------|---------|
| `collect()` | Return all elements of the RDD to the driver as a list. | `rdd.collect()` → `Array(1, 2, 3)` |
| `count()` | Return the number of elements. | `rdd.count()` → `3` |
| `take(n)` | Return the first `n` elements. | `rdd.take(2)` → `Array(1, 2)` |
| `reduce(f)` | Aggregate all elements using a commutative + associative binary function. | `rdd.reduce(_ + _)` → `6` |
| `saveAsTextFile(path)` | Write the RDD's elements to a text file in HDFS/local FS. | `rdd.saveAsTextFile("hdfs://out")` |

### Q2.4 — Compare in detail Pig, SQL, and Hive.  *(5 marks)*

| Aspect | Pig | SQL | Hive |
|--------|-----|-----|------|
| Language type | Procedural data-flow (Pig Latin) | Declarative query (ANSI SQL) | Declarative query (HiveQL, a SQL dialect) |
| Engine | Apache Pig → compiles to MapReduce / Tez | RDBMS query engine | Compiles queries to MapReduce / Tez / Spark jobs on Hadoop |
| Data model | Bags (sets of tuples), Tuples | Relational tables | Tables over HDFS files |
| Schema | Optional (schema can be inline in the script) | Strict, predefined schema | Schema-on-Read (flexible) |
| Use case | Complex data transformations (ETL pipelines); procedural control flow | OLTP + OLAP on relational data | Batch OLAP analytics on large datasets in HDFS |
| Users | Researchers, programmers | DBAs, developers, analysts | Data analysts with SQL background |
| Latency | Medium-high (compiles to MapReduce) | Low (ms for OLTP) | High (minutes-hours) |
| Metadata | No dedicated metadata DB | Catalog in RDBMS | Metastore (RDBMS) |
| Operations | `LOAD`, `FOREACH`, `FILTER`, `GROUP`, `JOIN`, `STORE` | `SELECT`, `INSERT`, `UPDATE`, `DELETE` | `SELECT`, `INSERT`, (limited `UPDATE`/`DELETE` in modern Hive) |
| Joins | Supports joins but verbose | Native, optimised joins | Native joins; supports INNER, LEFT/RIGHT/FULL OUTER, LEFT SEMI |
| Best suited for | Multi-step ETL pipelines where you want explicit control over each step | OLTP, transactional systems where ACID is mandatory | Data-warehouse-style batch analytics on Hadoop |

### Q3.1 — PySpark SQL DataFrame operations (10 marks)

Given: `df.columns = ['salary', 'age', 'experience', 'department', 'city']`

```python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("midsem").getOrCreate()

# (a) Display the shape of the data.
print("Rows:", df.count(), "Columns:", len(df.columns))
# Or in newer PySpark:
print(df.count(), len(df.columns))   # prints "N 5"

# (b) View only the columns age and city, and show 5 records.
df.select("age", "city").show(5)

# (c) Add a new column that stores the projected salary after 5 years.
#     Assume 5% annual growth → projected = salary * (1.05 ** 5)
from pyspark.sql.functions import col, expr
df_proj = df.withColumn("projected_salary_5yr", col("salary") * expr("pow(1.05, 5)"))
# Or simpler:
df_proj = df.withColumn("projected_salary_5yr", col("salary") * 1.2763)
df_proj.show(5)

# (d) Fetch the records for employees working in the Finance department.
df.filter(col("department") == "Finance").show()

# (e) View the distinct values for the column department.
df.select("department").distinct().show()
```

**Explanation of each step:**

a) **Shape:** PySpark DataFrames have no `.shape` attribute like Pandas. The equivalent is `(df.count(), len(df.columns))` — `count()` triggers a job to count rows; `df.columns` is a list of column names. Note: `count()` is an *action* (expensive) — it scans the entire DataFrame.

b) **Select columns + show 5:** `df.select("age", "city")` returns a new DataFrame with only those two columns. `.show(5)` triggers execution and prints the first 5 rows in tabular format.

c) **Add a column:** `withColumn(colName, colExpr)` returns a new DataFrame with an additional column. The expression must be a `Column` object — typically built using `col("salary") * 1.2763` or using `expr("...")` for SQL-style expressions. The original DataFrame is unchanged (immutable).

d) **Filter by department:** `df.filter(col("department") == "Finance")` (or equivalently `df.where("department == 'Finance'")`). Returns a new DataFrame containing only matching rows.

e) **Distinct values:** `df.select("department").distinct().show()` — `select` picks the column, `distinct()` deduplicates, `show()` displays the unique values.

### Q3.2 (Option A) — Scala `reduceByKey` output  *(5 marks)*

```scala
val input  = Seq(("Big", 1), ("Data", 3), ("big", 4), ("Big", 4), ("data", 2), ("data", 6))
val input2 = sc.parallelize(input)
val input3 = input2.reduceByKey((x, y) => x + y).collect
```

**Step-by-step explanation:**

1. `input` is a `Seq[(String, Int)]` — a sequence of (word, count) pairs.
2. `sc.parallelize(input)` converts the Seq into an **RDD** of pairs distributed across the cluster (parallel collection). Because the Seq is small, Spark may use a single partition.
3. `reduceByKey((x, y) => x + y)` is a **transformation** on a pair RDD:
   - Spark first **shuffles** the pairs so that all pairs with the same key are on the same partition.
   - Then for each key, the lambda `(x, y) => x + y` is applied to merge all values for that key into a single value (the sum).
   - The result is a new pair RDD containing one entry per unique key with the sum of its values.
4. `.collect` is an **action** that pulls all partitions of the result back to the driver as a local array.

**Important detail — case sensitivity:** Scala `String` comparison is case-sensitive. So:
- `"Big"` (capital B) is a **different key** from `"big"` (lowercase b).
- `"Data"` (capital D) is a **different key** from `"data"` (lowercase d).

**Aggregation per unique key:**
- `"Big"` → `1 + 4 = 5`
- `"Data"` → `3`
- `"big"` → `4`
- `"data"` → `2 + 6 = 8`

**Final output** (as a Scala `Array`):
```
Array((Big,5), (Data,3), (big,4), (data,8))
```

*(Order may vary depending on partitioning; only the key-value pairs are guaranteed.)*

#### Q3.2 (Option B) — MapReduce program to count letter occurrences  *(5 marks)*

*(See §1.3.11 — Python version using `mapper.py` and `reducer.py`, and the Java Hadoop skeleton.)*

---

## Quick-Revision Cheatsheet (last 30 minutes before exam)

### 1) The 5 V's of Big Data
**Volume** (PB/EB) • **Velocity** (real-time) • **Variety** (structured/semi/unstructured) • **Veracity** (quality) • **Value** (business worth).

### 2) Hadoop Components
- **HDFS** = storage • **MapReduce** = processing • **YARN** = resource mgmt • **Common** = utilities.
- Ecosystem: HDFS, HBase, YARN, MapReduce, Spark, Pig, Hive, Mahout/MLlib, Solr/Lucene, ZooKeeper, Oozie, Flume, Sqoop, Ambari.

### 3) HDFS Quick Facts
- Default block size = **128 MB**. Default replication factor = **3** (1 local rack + 2 remote rack).
- NameNode = metadata (FsImage + EditLog), no data.
- DataNode = actual blocks; heartbeat every **3 s**; block report every **6 h**; dead after ~**10 min** no heartbeat.
- Secondary NameNode = **checkpoint helper**, not a backup! Merges FsImage + EditLog → new FsImage.
- Standby NameNode (HA) = real-time hot standby, takes over instantly if Primary fails.
- Safemode at startup; exits when 99.9% of blocks reported.

### 4) HDFS Write Path (memorize!)
1. Client → NameNode: "create `data.txt`".
2. NameNode → Client: list of DataNodes `[DN1, DN2, DN3]`.
3. Client writes packets to DN1 → DN2 → DN3 (pipeline).
4. ACKs back: DN3 → DN2 → DN1 → Client.
5. Block filled (128 MB) → next block. File closed → DataNodes report blocks to NameNode.

### 5) MapReduce Pipeline
INPUT → MAP → **COMBINER** → SHUFFLE & SORT → REDUCE → OUTPUT
- Combiner = local-reducer; same class as Reducer; runs **after Map, before Shuffle**.
- Combiner must be **associative + commutative** (framework may call 0/1/N times).

### 6) YARN Components (5)
1. **Client** — submits application.
2. **Resource Manager** (master) — Scheduler + Applications Manager.
3. **Node Manager** (slave per node) — manages containers, heartbeats.
4. **Application Master** (per app) — negotiates containers, monitors tasks.
5. **Container** — RAM + CPU + disk allocation unit; launched via CLC.

### 7) YARN Workflow (8 steps)
Submit → Launch AM → AM registers → AM negotiates containers → NMs launch containers → tasks execute → monitoring + status → completion + deregistration.

### 8) HBase Key Concepts
- Column-oriented NoSQL on HDFS.
- **Table → Rows → Column Families → Columns → Cell (value + timestamp)**.
- Row Key = primary identifier + sort order.
- Column Family = defined at table creation; not easily changed.
- Column Qualifier = mutable; varies per row.
- HBase Architecture: **HMaster** (master), **RegionServers** (workers), **ZooKeeper** (coordinator).
- Region = horizontal partition by row-key range.

### 9) HBase vs RDBMS — Two Main Differences
1. **Column-oriented vs Row-oriented storage.**
2. **Schema-less (only column families defined) vs Fixed rigid schema.**

(Also: built-in auto partitioning + horizontal scaling vs no built-in partitioning + vertical scaling.)

### 10) HBase Commands (top 8 to memorize)
| Command | Purpose |
|---------|---------|
| `create 'emp', 'personal', 'professional'` | Create table with column families |
| `put 'emp','1','personal:name','raju'` | Insert a cell |
| `get 'emp','1'` | Read a row |
| `scan 'emp'` | Scan all rows |
| `delete 'emp','1','personal:city'` | Delete a cell |
| `deleteall 'emp','1'` | Delete an entire row |
| `disable 'emp'; drop 'emp'` | Drop a table (must disable first) |
| `count 'emp'` | Count rows |

### 11) Hive Architecture
**Clients (Thrift/JDBC/ODBC/CLI/Web) → Driver → Compiler → Optimizer → Executor → MapReduce/Tez → HDFS**
- **Metastore** stores metadata in an RDBMS (MySQL/PostgreSQL).
- Modes: **Embedded** (single session, Derby) / **Local** (multiple sessions, MySQL same JVM) / **Remote** (separate JVMs, Thrift).

### 12) Hive Schema-on-Read vs Schema-on-Write
| | Schema-on-Read (Hive) | Schema-on-Write (RDBMS) |
|---|---|---|
| Verify at load | No | Yes |
| Load speed | Very fast | Slower |
| Query speed | Slower (parse at query) | Faster |
| Bad rows surface | At query time | At load time |

### 13) Hive Managed vs External Table
| | Managed (Internal) | External |
|---|---|---|
| Owner of data | Hive | You / external |
| DROP TABLE | Deletes metadata + data | Deletes only metadata; data stays |
| Default location | `/user/hive/warehouse/` | Custom HDFS path (LOCATION) |

### 14) Hive Create External Table with Comma Delimiter (the 3-mark query!)
```sql
CREATE EXTERNAL TABLE IF NOT EXISTS Book (
  book_id INT, title STRING, author STRING, price FLOAT
)
ROW FORMAT DELIMITED
  FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/user/hive/input/';
```

### 15) Hive Load from Local with Overwrite
```sql
LOAD DATA LOCAL INPATH '/home/cloudera/book_data.txt'
OVERWRITE INTO TABLE Book;
```

### 16) Hive CTAS (managed table from query)
```sql
CREATE TABLE ExpensiveBooks AS
SELECT book_id, title, author, price
FROM Book
WHERE price > 100;
```

### 17) Hive Partitioning — Static vs Dynamic
- **Static:** partition column known at load time. `LOAD DATA LOCAL INPATH '...' OVERWRITE INTO TABLE t PARTITION (year='2009');`
- **Dynamic:** partition column value discovered at execution time.
  ```sql
  SET hive.exec.dynamic.partition = true;
  SET hive.exec.dynamic.partition.mode = nonstrict;
  INSERT INTO TABLE student_part PARTITION (year)
  SELECT id, name, dept, year FROM student_src;   -- partition col LAST
  ```

### 18) Hive Bucketing
- Mechanism: `bucket = hash(column) MOD num_buckets`.
- `SET hive.enforce.bucketing = true;` (older Hive).
- Speeds up joins + sampling.
- `CREATE TABLE emp_bucket (...) CLUSTERED BY (id) INTO 5 BUCKETS ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';`

### 19) Hive Subqueries
- **SELECT list:** ❌ NOT supported (use LEFT JOIN + GROUP BY instead).
- **FROM clause:** ✅ supported, MUST alias the subquery.
- **WHERE clause:** ✅ supported (IN/NOT IN — single column; EXISTS — needs correlated predicate).

### 20) Hive Joins
- INNER, LEFT OUTER, RIGHT OUTER, FULL OUTER, LEFT SEMI, CROSS.
- LEFT SEMI = efficient IN-style semi-join.

### 21) Spark — Quick Facts (for 2024-style Qs)
- **In-memory processing** via RDDs → 10–100× faster than MapReduce for iterative work.
- **RDD = Resilient Distributed Dataset** — read-only, partitioned, fault-tolerant via lineage, lazy evaluation.
- **Transformations** (lazy): `map`, `filter`, `flatMap`, `reduceByKey`, `groupByKey`, `distinct`, `join`.
- **Actions** (trigger exec): `collect`, `count`, `take(n)`, `reduce(f)`, `saveAsTextFile`.
- **PySpark SQL DataFrame ops**: `select`, `filter`, `withColumn`, `groupBy`, `distinct`, `show`, `count`.
- Spark vs MapReduce: Spark wins on performance (in-memory) + ease of use; MapReduce wins on stability for batch ETL.

### 22) Pig Latin Quick Operators
LOAD → FOREACH (map) → FILTER → GROUP → JOIN → COGROUP → STORE.
Pig vs Hive vs SQL: Pig = procedural ETL; Hive = SQL on Hadoop; SQL = ANSI on RDBMS.

### 23) Scala `reduceByKey` Quick Pattern
```scala
val rdd = sc.parallelize(Seq(("a",1), ("a",2), ("b",3), ("b",4)))
val reduced = rdd.reduceByKey(_ + _).collect
// Array((a,3), (b,7))   -- case-sensitive keys!
```

### 24) MapReduce Letter-Count (minimal Python)
```python
# mapper
for line in sys.stdin:
    for ch in line.strip().lower():
        if ch.isalpha():
            print(f"{ch}\t1")
# reducer
counts = {}
for line in sys.stdin:
    ch, c = line.strip().split('\t')
    counts[ch] = counts.get(ch, 0) + int(c)
for ch, c in sorted(counts.items()):
    print(f"{ch}\t{c}")
```

Run: `cat file.txt | ./mapper.py | sort | ./reducer.py`

---

## Last-Minute Tips

### If asked to "Draw and explain" (10-mark questions):
1. **Always draw a labelled diagram** — examiners award marks for the diagram even if the prose is mediocre.
2. After the diagram, **explain each component** with 1–2 lines, in the order they appear in the workflow.
3. End with a **numbered step-by-step workflow** that ties the components together.

### If asked to "Write a Hive query" (Q2 2025):
- Always specify `ROW FORMAT DELIMITED FIELDS TERMINATED BY ','` for CSV.
- Specify `STORED AS TEXTFILE` if the format is text.
- Use `EXTERNAL` + `LOCATION` for external tables.
- Use `CREATE TABLE … AS SELECT` for managed tables from a query.

### If asked "Why" (2-mark short notes):
- Answer in **3–4 bullet points**.
- First bullet: definition of the thing.
- Second bullet: why it's needed.
- Third bullet: example or trade-off.

### If asked for code:
- Use the **language the question specifies** (Java MapReduce if "Hadoop program", Python if "mapper/reducer", Scala if `sc.parallelize`, HiveQL for Hive, PySpark for DataFrame ops).
- Add brief comments (`//` or `#`) at the start of each major step.
- For Java MapReduce, set the Combiner class to the Reducer class.

### Watch out for traps:
- **HBase disable-then-drop:** you MUST `disable 'table'` before `drop 'table'`.
- **Hive external table drop:** only metadata is deleted, data stays in HDFS.
- **Combiner constraints:** must be associative + commutative; cannot replace reducer.
- **Scala `reduceByKey` case sensitivity:** `"Big"` ≠ `"big"` ≠ `"data"` ≠ `"Data"`.
- **Hive subqueries in SELECT list:** NOT supported — use LEFT JOIN + GROUP BY.
- **Partition column placement in dynamic partition INSERT:** the partition column **must be the last** column in the SELECT.

### Time-management (1-hour 25-mark paper):
| Question | Marks | Time |
|----------|-------|------|
| Q1 (4 × 2 marks) | 8 | 10 min |
| Q2 (Hive code) | 7 | 15 min |
| Q3 (YARN or HDFS) | 10 | 25 min |
| Buffer / revision | — | 10 min |

### Time-management (2-hour 50-mark paper, hypothetical):
| Question | Marks | Time |
|----------|-------|------|
| Q1 (5 + 10 = 15) | 15 | 25 min |
| Q2 (4 × 5 = 20) | 20 | 35 min |
| Q3 (10 + 5 = 15) | 15 | 30 min |
| Buffer / revision | — | 30 min |

### Strategy for the 25-mark 2025 pattern:
- The 2025 paper is **100% covered** by your Unit-1 slides. Topics to drill:
  - Combiner (MapReduce).
  - Checkpointing (Secondary NameNode).
  - HBase vs RDBMS (column vs row, schema-less vs fixed).
  - Schema-on-Read vs Schema-on-Write (Hive).
  - Hive create external table + LOAD + CTAS.
  - YARN components + workflow OR HDFS architecture + write pipeline.
- If you only have 30 min left: **practise Q2 (Hive code) and Q3 (YARN)** until you can write them from memory.

### Strategy if 2024-style 50-mark paper:
- 2024 includes Spark, RDD, Pig (typically Unit-2). Use the brief notes in §10 of this guide.
- If a Spark question appears, the safe template is:
  - "Spark uses in-memory processing via RDDs → 10-100× faster than MapReduce for iterative work."
  - "RDDs are read-only, partitioned, fault-tolerant via lineage, lazy evaluation."
  - List 5 transformations (`map`, `filter`, `flatMap`, `reduceByKey`, `groupByKey`) + 5 actions (`collect`, `count`, `take`, `reduce`, `saveAsTextFile`).

---

## Exam-Day Checklist

| Item | Ready? |
|------|--------|
| ID card + hall ticket | ☐ |
| Pen (blue/black) + spare | ☐ |
| Pencil + eraser (for diagrams) | ☐ |
| Calculator (if allowed) | ☐ |
| Water bottle | ☐ |
| Watch (to track time) | ☐ |
| This study prep | ☐ |

---

## Glossary (alphabetical)

| Term | Meaning |
|------|---------|
| **AM** | Application Master (per-app YARN daemon) |
| **Block** | Fixed-size chunk of HDFS file (default 128 MB) |
| **Block Report** | DataNode → NameNode list of stored blocks (every 6 h) |
| **CLC** | Container Launch Context (env vars + tokens + dependencies) |
| **Combiner** | Local reducer that runs at mapper output (after Map, before Shuffle) |
| **Container** | YARN's unit of resource allocation (RAM + CPU + disk on a node) |
| **DataNode** | HDFS worker that stores blocks |
| **DAG** | Directed Acyclic Graph (Hive compiler's query plan) |
| **EditLog** | NameNode's on-disk log of recent metadata changes |
| **FsImage** | NameNode's full snapshot of metadata since beginning |
| **HBase** | NoSQL column-oriented DB on top of HDFS |
| **Heartbeat** | DataNode → NameNode alive signal (every 3 s) |
| **Hive** | Data warehouse on top of Hadoop; SQL-like (HiveQL) |
| **HMaster** | HBase master node (metadata, schema ops, region assignment) |
| **JDBC** | Java Database Connectivity API |
| **MapReduce** | Programming model: Map → Shuffle/Sort → Reduce |
| **Metastore** | Hive's central metadata repository (in RDBMS) |
| **NameNode** | HDFS master node (metadata, block mapping) |
| **NM** | Node Manager (per-node YARN daemon) |
| **ODBC** | Open Database Connectivity API |
| **OLAP** | Online Analytical Processing (Hive) |
| **OLTP** | Online Transaction Processing (RDBMS) |
| **Oozie** | Hadoop workflow scheduler |
| **Partition (Hive)** | Subdirectory of a table keyed by column values |
| **Partition (Spark RDD)** | Logical chunk of an RDD; one task per partition |
| **Pig** | Procedural data-flow language (Pig Latin) |
| **RDD** | Resilient Distributed Dataset (Spark's core abstraction) |
| **ReduceByKey** | Spark transformation that merges values per key |
| **Region** | Horizontal partition of an HBase table by row-key range |
| **RegionServer** | HBase worker; hosts regions |
| **RM** | Resource Manager (YARN's master daemon) |
| **Safemode** | NameNode's read-only startup state until 99.9% blocks reported |
| **Schema-on-Read** | Hive's principle — schema applied at query time |
| **Schema-on-Write** | RDBMS principle — schema enforced at load time |
| **Secondary NameNode** | Checkpoint helper (NOT a backup NameNode) |
| **Spark** | In-memory distributed data-processing engine |
| **Standby NameNode** | HA hot standby; takes over if Primary fails |
| **Thrift** | Cross-language RPC protocol (used by Hive server) |
| **WORM** | Write-Once, Read-Many (HDFS file model) |
| **YARN** | Yet Another Resource Negotiator (Hadoop 2.x resource mgmt) |
| **ZooKeeper** | Distributed coordination service (used by HBase) |

---

**End of study prep — best of luck for your Big Data Analytics mid-semester exam!**
