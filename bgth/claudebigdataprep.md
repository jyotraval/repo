# Big Data Analytics and Computing — Mid-Sem Study Prep
**Course Code:** 20IC404T | Semester VII

This guide is built entirely from your uploaded material: `Unit 1_Part 1.pdf` (Intro to Big Data + HDFS), `Unit 1 Map reduce.pdf`, `UNIT 1 YARN.pdf`, `Unit 1 Hbase.pdf`, `hbase lab work.pdf`, `UNIT 1 HIVE.pdf`, and your **2024 + 2025 mid-sem question papers**.

---

## 0. How This Exam Behaves (Pattern Analysis)

| | 2024 Mid-Sem | 2025 Mid-Sem |
|---|---|---|
| Max Marks | 50 | 25 |
| Duration | 2 hrs | 1 hr |
| Structure | 3 big questions, all with sub-parts, one OR choice | 3 questions, sub-parts, one OR choice |
| Topics hit | 5 V's, Hadoop Ecosystem/HDFS R-W, Spark vs MapReduce, RDDs, Transformations/Actions, Pig vs SQL vs Hive, PySpark DataFrame ops, Scala `reduceByKey` walkthrough | Combiner, Checkpointing, HBase vs RDBMS, Schema-on-Read vs Write, Hive external table DDL+DML, YARN components/workflow OR HDFS architecture+write process |

**Key takeaway:** Both papers are drawn from the *same* Unit-1 slide deck topics — HDFS, MapReduce, YARN, HBase, Hive — with 2024 additionally pulling in **Spark/PySpark** (not in your uploaded slides, but very likely testable again — covered in Section 7 below from standard theory). Expect this term's paper to mix **conceptual short-answers (2-5 marks)**, **one HiveQL/PySpark coding question**, and **one big 10-mark "explain architecture + workflow" question with an OR**.

### 🎯 Highest-yield topics (asked almost every time)
1. HDFS Architecture (NameNode/DataNode/Secondary NameNode) + Read/Write process
2. MapReduce phases + Combiner
3. YARN components + workflow
4. Hive: Managed vs External tables, DDL/DML, Schema-on-Read
5. HBase vs RDBMS, HBase architecture
6. 5 V's of Big Data
7. Spark RDDs, transformations/actions, Spark vs MapReduce

---

## 1. Big Data Fundamentals

### 1.1 What is Big Data?
Gartner's definition: **"Big data" is high-volume, high-velocity and high-variety information assets that demand cost-effective, innovative forms of information processing for enhanced insight and decision making.**

Big data = data that **exceeds the processing capacity of conventional database systems** — too big, moves too fast, or doesn't fit your existing DB structures.

**Life cycle:** Generate → Gather → Store → Organize → Analyze → Visualize (>90% of Big Data is unstructured).

### 1.2 The 5 V's (asked in both papers — memorize solid definitions + one example each)

| V | Meaning | Example |
|---|---|---|
| **Volume** | Sheer scale of data generated (KB → YB scale). ~181 ZB generated in 2025. | Facebook photo storage, YouTube uploads |
| **Velocity** | Speed at which data is generated & must be processed. Traditional data = drop of water; Big Data = flowing river. | Stock market feeds, sensor streams, fraud detection |
| **Variety** | Different forms — structured (tables), semi-structured (XML/JSON), unstructured (text, video), streaming, graph data | Social media posts + sensor logs + transaction tables together |
| **Veracity** | Truthfulness/quality/believability of data; Big Data is messy, has noise & bias | Wikipedia data (less authoritative) vs a `.gov` site (authoritative) |
| **Value** | The actual *usable insight* extracted — the whole point of doing Big Data analytics | Turning raw clickstream into a recommendation engine |

> **Exam answer template:** "Define each V in 1 line + why it matters for Big Data Analytics specifically (not just databases in general) + one real example." 5 marks = roughly 1 mark per V with a one-line justification.

### 1.3 Types of Data Analytics
1. **Descriptive** – What happened? (reports, dashboards, historical)
2. **Diagnostic** – Why did it happen? (root-cause, correlations)
3. **Predictive** – What is likely to happen? (forecasting)
4. **Prescriptive** – What action should we take? (optimization, simulation)

### 1.4 Operational vs Analytical Big Data

| Feature | Operational Big Data | Analytical Big Data |
|---|---|---|
| Question | "What is happening right now?" | "What happened, why, and what will happen?" |
| Focus | Real-time, low latency | Long-term trends & strategic insight |
| Data flow | Continuous transaction processing | Batch/stream/micro-batch |
| DB type | NoSQL, distributed OLTP | Data Warehouses, Data Lakes, OLAP |
| Latency | Milliseconds–seconds | Seconds–hours |

### 1.5 Why Hadoop? (Motivation)
Big data storage is hard because: data volumes are massive, all kinds of hardware/network failures happen, and probability of failure **increases** with more machines. The philosophy is **Divide and Conquer**: divide work across machines → combine results.

**5 Motivation Questions → HDFS answers:**
1. Data too big for one machine → **store across multiple machines**
2. High-end machines too expensive → **run on commodity hardware**
3. Commodity hardware fails → **software handles failure intelligently**
4. What if the machine storing data fails? → **replicate the data**
5. How do distributed machines coordinate? → **Master-Slave architecture**

---

## 2. Hadoop Ecosystem & HDFS

### 2.1 What is Hadoop?
Hadoop = open-source **framework for distributed storage + parallel processing** of large datasets across clusters using commodity hardware, designed to detect/handle failures at the application layer.

**3 (+1) core components:**
1. **HDFS** – storage unit
2. **MapReduce** – processing unit
3. **YARN** – resource management unit
4. **Hadoop Common** – shared utilities/libraries

### 2.2 Hadoop Ecosystem (draw this — asked as a 10-mark diagram question)
```
                    Hadoop Ecosystem
┌─────────────────────────────────────────────────────┐
│  Query/Scripting: PIG, HIVE   │  ML: Mahout, Spark MLlib │
│  Search/Index: Solr, Lucene   │  NoSQL DB: HBase          │
│  Coordination: Zookeeper      │  Scheduling: Oozie        │
│  Ingestion: Flume, Sqoop      │  Provisioning: Ambari     │
├─────────────────────────────────────────────────────┤
│           Processing: MapReduce  │  YARN (resource mgmt)   │
├─────────────────────────────────────────────────────┤
│                  Storage: HDFS                        │
└─────────────────────────────────────────────────────┘
```
- **HDFS** – Hadoop Distributed File System (storage)
- **YARN** – Yet Another Resource Negotiator (resource management)
- **MapReduce** – programming-based data processing
- **PIG, HIVE** – query-based data processing services (SQL-like)
- **HBase** – NoSQL database
- **Mahout, Spark MLlib** – machine learning libraries
- **Solr, Lucene** – searching & indexing
- **Zookeeper** – cluster coordination/management
- **Oozie** – job scheduling
- **Flume, Sqoop** – data ingestion (log data / RDBMS data respectively)
- **Ambari** – provision, monitor, maintain the cluster

### 2.3 HDFS — Architecture (Master-Slave)

HDFS is the **open-source version of Google File System (GFS)**, built for **write-once-read-many (WORM)** access to very large files on commodity hardware.

**Two main components:**

| Component | Role |
|---|---|
| **NameNode** (Master) | Manages the **file system namespace/metadata**: file names, permissions, directory hierarchy, and the mapping of blocks → DataNodes. Does **NOT** store actual data. Maintains **FsImage** (full metadata snapshot) and **EditLog** (recent changes log). |
| **DataNode** (Slave/Worker) | Stores the **actual data blocks**, serves client read/write requests, performs block creation/deletion/replication as instructed by NameNode. Sends **heartbeats** (every ~3s) and **block reports** (every ~6hrs) to NameNode. |
| **Secondary NameNode** | **NOT a backup/standby.** Its job is **checkpointing** — periodically merges FsImage + EditLog to prevent the EditLog from growing too large and to speed up NameNode restart. |

**Blocks:** Files are split into fixed-size blocks — default **128 MB** (configurable). Why blocks instead of whole files? (a) a file can be bigger than one disk, (b) fixed size = easy to manage, (c) easy to replicate & load-balance.

**Replication:** Default replication factor = **3**.
- 1st replica → local rack
- 2nd replica → a remote rack
- 3rd replica → same remote rack, different DataNode
- (More replicas placed randomly; ≤2 replicas per rack as far as possible)

#### 2.3.1 HDFS Write Process (step-by-step — HIGH YIELD, asked in 2025 paper)
1. **Client contacts NameNode** to request file creation; NameNode checks permissions and namespace, records the new file metadata.
2. NameNode returns a **list of DataNodes** to host each block's replicas (chosen by a replica-placement algorithm, respects rack awareness & replication factor).
3. Client streams the file in **packets** to the **first DataNode (DN1)**.
4. **Pipeline replication:** DN1 forwards each packet to DN2, DN2 forwards to DN3 → forms pipeline **Client → DN1 → DN2 → DN3**.
5. **Acknowledgement (ACK)** flows backward: DN3 → DN2 → DN1 → Client, confirming each block is safely written.
6. Once all blocks are written and acknowledged, the client calls `close()`; NameNode commits the file as complete in its metadata.
7. If any DataNode fails mid-pipeline, the pipeline reconfigures automatically to skip the failed node.

**Advantages of pipelined replication:** faster writes (parallel streaming), reduced network congestion (data flows one direction), automatic recovery on DataNode failure.

#### 2.3.2 HDFS Read Process
1. Client asks NameNode for block locations of the requested file.
2. NameNode returns the list of blocks and the DataNodes holding each (sorted by network proximity to the client).
3. Client connects directly to the **nearest DataNode** for each block and streams data.
4. On finishing one block, it moves to the DataNode for the next block, continuing till EOF.
5. If a DataNode is unreachable or a block is corrupt (checksum mismatch), the client transparently retries from another replica.

#### 2.3.3 Heartbeats vs Block Reports

| | Heartbeat | Block Report |
|---|---|---|
| Frequency | Every ~3 seconds | Every ~6 hours |
| Purpose | Confirms DataNode is alive/healthy | Lists all blocks stored on that DataNode |
| Missed → | If not received for ~10.5 min, NameNode marks DataNode **dead** and replicates its blocks elsewhere | Used to verify block-location metadata |

#### 2.3.4 Data Integrity & Safemode
- **Checksum:** HDFS client creates a checksum for every block when writing; verified on read. Mismatch → fetch from another replica.
- **Safemode:** A **read-only** state the NameNode enters automatically at startup (no replication/deletion allowed) because it doesn't persist block-locations on disk — it rebuilds its in-memory block map from incoming DataNode block reports. Exits once ~99.9% of blocks are confirmed present (plus a short extension timer).

#### 2.3.5 Secondary NameNode vs Standby NameNode

| Feature | Secondary NameNode (classic) | Standby NameNode (HA, 2.x+) |
|---|---|---|
| Role | Periodic checkpoint helper | Active hot-standby replica |
| Automatic failover? | ❌ No | ✅ Yes, instant |
| Data freshness | Outdated (only up to last checkpoint) | Real-time synchronized |

#### 2.3.6 Why Checkpointing? (2025 PYQ)
The Primary NameNode keeps metadata in RAM + logs every change to the **EditLog** on disk + periodically snapshots to **FsImage**. Over time the EditLog grows huge, which would make NameNode restart very slow (it must replay the entire log). **Checkpointing** = Secondary NameNode periodically **fetches FsImage + EditLog → merges them in its own memory → uploads the new merged FsImage back → Primary NameNode resets/truncates its EditLog.** This keeps the EditLog small and restart fast, and protects against metadata loss.

#### 2.3.7 HDFS vs Local File System

| | HDFS | Local File System |
|---|---|---|
| ✅ Advantage | Reliably stores very large files (PB-scale) across commodity hardware with built-in fault tolerance via replication | — |
| ⚠️ Limitation | Not efficient for large numbers of **small files**, not designed for low-latency random reads/updates of individual records (write-once, append-mostly) | Great for small files & random access |

#### 2.3.8 Useful HDFS Commands

| Into HDFS | Out of HDFS |
|---|---|
| `hadoop fs -put local_file /hdfs/path/` | `hadoop fs -get /hdfs/file local_dest` |
| `hadoop fs -copyFromLocal local_file /hdfs/path/` | `hadoop fs -copyToLocal /hdfs/file local_dest` |
| `hadoop fs -moveFromLocal local_file /hdfs/path/` (deletes local copy) | `hadoop fs -getmerge /hdfs/folder/* merged_file` |
| `hadoop fs -appendToFile local_file /hdfs/existing_file` | |

---

## 3. MapReduce

### 3.1 Concept
MapReduce = a **programming model for parallel processing of large datasets across a distributed cluster**, split into a **Map phase** and a **Reduce phase**.

**Real-world analogy:** Coins deposit machine — **Mapper** categorizes coins by face value; **Reducer** counts coins of each face value in parallel.

### 3.2 Phases (know these cold)
1. **Map Phase** – input is split; each Map task processes its local split, emits intermediate **`<key, value>`** pairs.
2. **Shuffle & Sort** – intermediate pairs are grouped by key and sorted; values with the **same key go to the same reducer**.
3. **Reduce Phase** – reducers aggregate grouped values → final output, written back to HDFS.

**MapReduce paradigm:**
```
Map(k1, v1)          -> list(k2, v2)
Reduce(k2, list(v2)) -> list(v3)
```

### 3.3 Combiner (2025 PYQ — asked exactly this way)
> **Q: Define the role of the Combiner in a MapReduce job. State the phase after which it is used.**

**Answer:** The **Combiner performs local (mini) aggregation of the Mapper's output on the same node**, before the data is sent across the network to the Reducers. It is essentially a "local reducer."
- **Used right after the Map phase**, on each mapper's own output — before Shuffle & Sort sends data across the network.
- **Benefits:** reduces memory/disk requirement of intermediate data, and drastically **reduces network traffic** between Map and Reduce phases.
- Note: Combiner **cannot replace** the Reducer — the Reducer must still combine records with the same key arriving from *different* mappers.
- Implementation-wise, a Combiner is written exactly like a Reducer.

```
        INPUT      MAP                       SHUFFLE      REDUCE      OUTPUT
                 Map → Combine  ─┐
        Input    Map → Combine  ─┼──►  Shuffle/Sort  ──►  Reduce   ──► Output
        data     Map → Combine  ─┘
```

### 3.4 Architecture — Master/Slave (older Hadoop 1.x terms, still asked conceptually)

| Role | Component | Job |
|---|---|---|
| Master | **Job Tracker** | Coordinates jobs — scheduling, phase coordination, handles failures, monitors progress |
| Master | **Job Client** | Submits jobs |
| Slave | **Task Trackers** | Execute the Map/Reduce tasks |

**Core idea: "Bring Computation to Data"** — instead of moving huge data to code, ship the small code to where data already lives (data locality).

**Workflow:**
1. Client submits job to Job Tracker
2. Job Tracker asks NameNode where the data lives
3. Job Tracker creates an execution plan, assigns work to Task Trackers
4. Task Trackers execute and report progress back to Job Tracker
5. Job Tracker manages phase transitions (map → shuffle → reduce)
6. Job Tracker marks the job finished and updates status

### 3.5 Worked Example: Word Count
**Input:**
```
Deer Beer River
Car Car River
Deer Car Beer
```

**Map phase output** (per mapper): `(Deer,1) (Beer,1) (River,1)` / `(Car,1) (Car,1) (River,1)` / `(Deer,1) (Car,1) (Beer,1)`

**Shuffle & Sort** (group by key): `Beer→[1,1]` `Car→[1,1,1]` `Deer→[1,1]` `River→[1,1]`

**Reduce phase output:** `Beer,2  Car,3  Deer,2  River,2`

**Pseudocode:**
```
Map(key, value):        # key=line number, value=line text
    for each word w in value:
        Emit(w, "1")

Reduce(key, list_of_values):   # key=word, values=list of counts
    result = 0
    for v in values:
        result += ParseInt(v)
    Emit(key, result)
```

**Linux pipe simulation:** `cat input.txt | mapper.py | sort | reducer.py`

### 3.6 Practice Program: Count occurrences of each letter in a text file
(This is the "OR" alternative to the Scala question in the 2024 paper — practice both.)

```
Map(key, value):              # key = line number, value = line of text
    for each character c in value:
        if c.isAlpha():
            Emit(lower(c), 1)

Reduce(key, list_of_values):  # key = a letter, values = list of 1's
    sum = 0
    for v in values:
        sum += v
    Emit(key, sum)
```
Example: input `"hadoop"` → mapper emits `(h,1)(a,1)(d,1)(o,1)(o,1)(p,1)` → after shuffle: `o→[1,1]` → reducer emits `(h,1)(a,1)(d,1)(o,2)(p,1)`.

---

## 4. YARN (Yet Another Resource Negotiator)

### 4.1 Why YARN? (Hadoop 1.0 problem)
In Hadoop 1.0, a single **Job Tracker** did both resource management AND application execution/scheduling — a bottleneck limited to ~4,000 nodes and only supported MapReduce. **YARN splits these responsibilities** into a **Global Resource Manager** + **per-application Application Master**, enabling multiple processing engines (batch, streaming, interactive, graph) to share the same HDFS-backed cluster.

### 4.2 Core Components (10-mark question — explain each + workflow)

| Component | Role |
|---|---|
| **Client** | Submits the application to YARN; monitors job status |
| **Resource Manager (RM)** | The **master** daemon. Two sub-parts: **Scheduler** (pure allocator based on capacity/queues — doesn't monitor or restart tasks) and **Applications Manager** (accepts job submissions, negotiates the first container for the Application Master, restarts AM on failure) |
| **Node Manager (NM)** | The **slave/per-node** daemon — registers with RM, sends heartbeats, monitors CPU/memory usage on its node, creates/monitors/kills containers, manages logs |
| **Application Master (AM)** | **One per application** (e.g. per job). Negotiates containers from RM, works with NodeManagers to launch/monitor tasks, requests new containers if tasks fail |
| **Container** | Unit of resource allocation (RAM+CPU+disk) granted by the scheduler on a node; invoked via a **Container Launch Context (CLC)** |

### 4.3 Application Workflow (the "5+5" question — components + workflow)
1. **Application Submission** – Client submits app (code + config + resource requirements) to Resource Manager.
2. **AM Launch** – RM allocates a container on some Node Manager to launch the Application Master.
3. **AM Registration** – AM registers itself with the RM.
4. **Resource Negotiation** – AM negotiates with RM for containers (CPU, memory) needed for its tasks.
5. **Container Launch Notification** – Once RM allocates containers, AM tells the relevant Node Managers to launch them.
6. **Task Execution** – Application's tasks run inside the allocated containers.
7. **Monitoring & Status Reporting** – Client can query RM or AM for status; AM tracks task progress and reports to RM.
8. **Completion & Deregistration** – AM unregisters with RM once done, releasing resources.

### 4.4 Advantages / Disadvantages

| Advantages | Disadvantages |
|---|---|
| Flexibility — run Spark, Flink, Storm, MapReduce on same cluster | Adds configuration/management complexity |
| Efficient centralized resource management | Resource negotiation adds minor latency overhead |
| High scalability (thousands of nodes) | RM is a potential single point of failure (mitigated by Standby RM, Hadoop 2.4+) |
| Dynamic allocation reduces resource waste | Native support for non-Java languages can be limited |
| Security — Kerberos, SSH, secure transmission | |

---

## 5. HBase

### 5.1 Why HBase? (Limitations of plain Hadoop that motivate it)
Hadoop's MapReduce is built for **batch processing**, not real-time/random access — even a simple lookup requires scanning large portions of data. HBase (like Cassandra, MongoDB, CouchDB, Dynamo) solves this by providing **random real-time read/write access** to huge datasets sitting on HDFS.

### 5.2 What is HBase?
- **Distributed, column-oriented database** built on top of HDFS.
- Open-source, horizontally scalable, modeled on **Google BigTable**.
- Leverages HDFS's fault tolerance; sits on top of HDFS providing random real-time read/write.
- Features: linearly scalable, automatic failure support, consistent reads/writes, integrates with Hadoop, Java client API, cross-cluster data replication.
- Used by: Facebook, Twitter, Yahoo, Adobe (also healthcare genome data, e-commerce logs, sports match history).

### 5.3 Data Model / Key Concepts
- **Row Key** – unique identifier per row; determines sort order.
- **Column Family** – logical grouping of related columns; defined at table creation, hard to change later.
- **Column Qualifier** – specific column name within a family; mutable, can vary per row.
- **Cell** – intersection of (row key, column family, column qualifier) → holds a **value + timestamp** (version).
- **Storage hierarchy:** Table = collection of Rows → Row = collection of Column Families → Column Family = collection of Columns → Cell = actual value + timestamp.

### 5.4 HBase vs Traditional RDBMS (2025 PYQ — "two main differences")

| Feature | HBase | RDBMS |
|---|---|---|
| Data architecture | **Column-oriented** datastore | **Row-oriented** datastore |
| Schema | **Schema-less** — only column families defined upfront, columns added dynamically | **Fixed/rigid schema** required before data is loaded |
| Table structure | Wide, sparse, denormalized tables | Thin, normalized tables |
| Data types | Structured + semi-structured | Structured only |
| Scaling | Built-in **automatic horizontal partitioning** (Regions) | No automatic partitioning — typically **vertical** scaling |

> **Model answer for "give two main differences":** (1) HBase is column-family-oriented and schema-less (only column families fixed, columns/qualifiers dynamic per row), while RDBMS enforces a fixed row/column schema at write time. (2) HBase scales horizontally by automatically splitting tables into Regions across servers, whereas RDBMS traditionally scales vertically and doesn't natively auto-partition.

### 5.5 Architecture — Key Components

| Component | Role |
|---|---|
| **HMaster** | Single active master; manages cluster operations, assigns Regions to RegionServers, handles table creation/deletion/schema changes, monitors RegionServer health, load balancing |
| **RegionServer** | Worker node; handles client read/write requests; hosts **Regions** (horizontal partitions of a table by row-key range); runs on a DataNode |
| **ZooKeeper** | Coordinator — maintains cluster state, facilitates HMaster↔RegionServer communication, detects/recovers from server failure |

*(Region = a logical division of an HBase table containing a sorted range of rows.)*

### 5.6 HBase Shell Command Cheat-Sheet

**General:** `help`, `status`, `version`, `whoami`

**DDL (tables):**
```
create 'emp', 'personal_data', 'professional_data'
list
describe 'emp'
alter 'emp', NAME => 'financial_data'
disable 'emp'   /   enable 'emp'
is_disabled 'emp'   /   is_enabled 'emp'
disable 'emp'; drop 'emp'      -- must disable before drop
```

**DML (data):**
```
put 'emp', 'row1', 'personal_data:name', 'John Doe'
get 'emp', 'row1'
get 'emp', 'row1', {COLUMN => 'personal_data:name'}
scan 'emp'
scan 'emp', {COLUMNS => ['personal_data:name'], LIMIT => 5}
delete 'emp', 'row1', 'personal_data:city'
deleteall 'emp', 'row1'
count 'emp'
truncate 'emp'
incr 'emp', 'row1', 'stats:login_count', 1
```

**Admin/tools:** `major_compact 'table'`, `flush 'table'`, `snapshot 'table','snap_name'`, `restore_snapshot 'snap_name'`

---

## 6. Hive

### 6.1 What is Hive?
Hive is a **data warehousing tool / query engine wrapper built on top of MapReduce**, giving SQL-background users a familiar **HiveQL** language. Developed originally by **Facebook**, later ASF open-sourced it. Hive is **not a relational database** — it's a query engine over data stored in Hadoop-compatible file systems.

### 6.2 Hive vs Pig (2024 PYQ asks Pig/SQL/Hive comparison directly)

| Hive | Pig | SQL (RDBMS) |
|---|---|---|
| Declarative SQL-based language | Procedural data-flow language | Declarative |
| For data analysis & reporting; used by Data Analysts | For programming; used by researchers/programmers | For transactional queries on structured data |
| Operates server-side on the cluster | Operates client-side | Operates on a single relational DB engine |
| Has a dedicated metadata DB (Metastore) | No dedicated metastore | Has catalog/system tables |
| Schema-on-Read | Schema applied at runtime, flexible | Schema-on-Write (strict) |
| Built for Hadoop/petabyte scale, batch (OLAP) | Built for Hadoop, batch ETL-style scripting | Built for GB–TB scale, real-time (OLTP) |
| Slower (translates to MapReduce/Tez jobs) | Similar performance profile to Hive on Hadoop | Fast for small/medium transactional data |

### 6.3 Hive Architecture (know the diagram + each component)
```
   CLI / Web UI / JDBC / ODBC / Thrift  →  Driver (Compiler → Optimizer → Executor)  →  Metastore
                                                     │
                                                     ▼
                                    Hadoop (MapReduce + HDFS): JobTracker/NameNode, DataNode/TaskTracker
```

| Component | Role |
|---|---|
| **Metastore** | Stores metadata — table schema, location, partition info — in a traditional RDBMS (backup replicated regularly) |
| **Driver** | Controller; receives HiveQL, creates sessions, tracks execution lifecycle, collects the final results |
| **Compiler** | Converts HiveQL → Abstract Syntax Tree (AST) → Directed Acyclic Graph (DAG) of MapReduce stages |
| **Optimizer** | Transforms the execution plan (e.g., merges joins) for better performance |
| **Executor** | Executes the DAG's tasks, talks to Job Tracker to schedule them, respects task dependencies |
| **CLI / Web UI / Thrift Server** | User interfaces; Thrift Server allows remote clients (JDBC/ODBC) to connect |

**Working of Hive (numbered flow, good for a diagram-based answer):**
1. Execute Query (CLI/Web UI → Driver)
2. Get Plan (Driver → Compiler, parses/checks syntax)
3. Get Metadata (Compiler → Metastore)
4. Send Metadata (Metastore → Compiler)
5. Send Plan (Compiler → Driver)
6. Execute Plan (Driver → Execution Engine)
7. Execute Job (Execution Engine → JobTracker → TaskTracker, i.e., a MapReduce job runs)
8. Fetch Result (Execution Engine ← DataNodes)
9. Send Results (Execution Engine → Driver)
10. Send Results (Driver → Hive Interface / user)

### 6.4 Hive Metastore — 3 Deployment Modes

| Mode | Description |
|---|---|
| **Embedded** | Metastore service + Hive service in same JVM, uses embedded **Derby DB**. Only **one** Hive session possible at a time. |
| **Local** | Metastore runs in same JVM as Hive service, but the DB (e.g., MySQL) runs in a separate process — supports multiple sessions. |
| **Remote** | Metastore & Hive service run in **separate JVMs**, communicate via Thrift. Clients don't need DB credentials. Scalable. |

### 6.5 Hive vs Traditional RDBMS

| Feature | Hive | RDBMS |
|---|---|---|
| Schema | **Schema-on-Read** (applied at query time) | **Schema-on-Write** (enforced before saving) |
| Data modifications | Optimized for append/batch loads (ACID support in modern Hive but best for batch) | Frequent read/write, optimized for concurrent updates |
| Scale | Petabyte+ | GB–TB |
| Workload | OLAP (batch analytics) | OLTP (live transactions) |
| Latency | Minutes/hours (scans massive data) | Milliseconds (fetches specific records) |
| Scalability | Horizontal, commodity servers | Expensive vertical scaling |

### 6.6 Schema-on-Read vs Schema-on-Write (2025 PYQ — exact wording)
> **Q: What is the core principle of "Schema-on-Read" as used by Hive? How is it different from "Schema-on-Write"?**

**Answer:** In **Schema-on-Write** (traditional RDBMS), the schema is enforced **at load/write time** — if data doesn't conform to the schema, it's rejected before storage. In **Schema-on-Read** (Hive), **Hive does not validate the data when it is loaded** — the schema is applied only **when the data is read/queried**. This makes the initial load extremely fast (no parsing/serializing into an internal format at load time), at the cost of possible errors surfacing only at query time. This is exactly why Hive can point at raw files already sitting in HDFS without any upfront transformation.

### 6.7 Managed (Internal) vs External Tables — CRITICAL, appears every year

| | Managed / Internal Table | External Table |
|---|---|---|
| Storage location | Hive's own warehouse dir: `/user/hive/warehouse/` | Wherever you specify with `LOCATION` |
| On `DROP TABLE` | **Both metadata AND data are deleted** | Only **metadata** is deleted; underlying **data stays in HDFS** |
| Use when | Data is temporary, and you want Hive to fully own the lifecycle | Data is shared with other tools/programs, or must survive table drops |

**Syntax skeleton:**
```sql
CREATE [TEMPORARY] [EXTERNAL] TABLE [IF NOT EXISTS] [db.]table_name
(
  col_name data_type [COMMENT 'comment'], ...
)
[COMMENT 'table_comment']
[PARTITIONED BY (col data_type, ...)]
[CLUSTERED BY (col,...) [SORTED BY (col [ASC|DESC],...)] INTO num_buckets BUCKETS]
[ROW FORMAT row_format]
[STORED AS file_format]
[LOCATION 'hdfs_path']
[TBLPROPERTIES (...)]
[AS select_statement];
```

**CTAS (`CREATE TABLE ... AS SELECT`) restrictions:** result table **cannot** be partitioned, cannot be external, cannot be a list-bucketed table; CTAS always triggers a map job.

### 6.8 🔑 Fully Solved: 2025 PYQ Hive Question (practice this exact pattern)
> Given external table `Book(book_id INT, title STRING, author STRING, price FLOAT)` at `/user/hive/input/`:

**a) Create the table (comma-delimited):**
```sql
CREATE EXTERNAL TABLE Book (
    book_id INT,
    title STRING,
    author STRING,
    price FLOAT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/user/hive/input/';
```

**b) Load data from local file, overwriting previous content:**
```sql
LOAD DATA LOCAL INPATH '/home/cloudera/book_data.txt'
OVERWRITE INTO TABLE Book;
```

**c) Create managed table `ExpensiveBooks` for books priced > 100:**
```sql
CREATE TABLE ExpensiveBooks AS
SELECT * FROM Book
WHERE price > 100;
```
*(No `EXTERNAL` keyword → managed table by default; CTAS satisfies "containing all columns" via `SELECT *`.)*

### 6.9 Partitioning
Splits a table into subdirectories based on column values (e.g., date, department) so queries only scan relevant partitions — **massively reduces I/O**.

| Static Partitioning | Dynamic Partitioning |
|---|---|
| You manually specify the partition value at load time | Partition values are determined automatically from data at **execution time** |
| Requires `hive.mapred.mode = strict` awareness | Requires `SET hive.exec.dynamic.partition=true;` + `SET hive.exec.dynamic.partition.mode=nonstrict;` |
| Faster to load | Slower to load (more overhead), but scales when you don't know values upfront |
| Can be altered | Cannot be altered directly (though partitions can be dropped) |

**Static example:**
```sql
CREATE TABLE table_tab1 (id INT, name STRING, dept STRING, yoj INT)
PARTITIONED BY (year STRING);

LOAD DATA LOCAL INPATH 'clientdata/2009/file2'
OVERWRITE INTO TABLE table_tab1 PARTITION (year='2009');
```

**Dynamic example (6-step recipe — good to memorize as a procedure):**
```sql
-- 1 & 2: put source CSV into HDFS (via hdfs dfs -put)
-- 3: staging table
CREATE TABLE student_src (id INT, name STRING, dept STRING, year STRING)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' STORED AS TEXTFILE;

-- 4: empty partitioned target table
CREATE TABLE student_part (id INT, name STRING, dept STRING)
PARTITIONED BY (year STRING)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';

-- 5: enable dynamic partitioning
SET hive.exec.dynamic.partition = true;
SET hive.exec.dynamic.partition.mode = nonstrict;

-- 6: insert (partition column must be LAST in the SELECT list)
INSERT INTO TABLE student_part PARTITION (year)
SELECT id, name, dept, year FROM student_src;

-- 7: verify
SHOW PARTITIONS student_part;
```

**Advantages:** faster queries on low-volume slices, distributes execution load. **Disadvantages:** too many small partitions creates directory overload; not ideal when partitions are very unevenly sized (e.g. partition by country). → This is exactly why **Bucketing** exists.

### 6.10 Bucketing
Divides data into a **fixed number of files** using a **hash function** on a column — `hash(column) MOD num_buckets` — solving the "uneven partition size" problem.

```sql
SET hive.enforce.bucketing = true;

CREATE TABLE emp_bucket (id INT, dept STRING, salary FLOAT)
CLUSTERED BY (id) INTO 5 BUCKETS
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';

INSERT OVERWRITE TABLE emp_bucket SELECT * FROM emp_demo;
```
Can combine partitioning + bucketing: `PARTITIONED BY (dept STRING) CLUSTERED BY (id) INTO 5 BUCKETS`.

**Advantage — Sampling:**
```sql
-- Bucket sampling
SELECT * FROM T_USER_LOG_BUCKET TABLESAMPLE (BUCKET 1 OUT OF 4 AT USER_ID);
-- Block sampling
SELECT * FROM T_USER_LOG_BUCKET TABLESAMPLE (20 PERCENT);
```

### 6.11 Hive Data Types
- **Primitive:** TINYINT, SMALLINT, INT, BIGINT, FLOAT, DOUBLE, DECIMAL, STRING, VARCHAR, BOOLEAN, BINARY, DATE, TIMESTAMP
- **Complex:** ARRAY, MAP, STRUCT
```sql
CREATE TABLE employees (
  name STRING,
  salary FLOAT,
  subordinates ARRAY<STRING>,
  deductions MAP<STRING, FLOAT>,
  address STRUCT<street:STRING, city:STRING, state:STRING, zip:INT>
);
```
**Implicit conversion** only flows "child → ancestor" up the numeric hierarchy (TINYINT→SMALLINT→INT→BIGINT→FLOAT→DOUBLE); BOOLEAN/BINARY never convert implicitly. Integral literals default to **INT** (unless they exceed INT range, then BIGINT).

### 6.12 Operators & Built-in Functions (quick reference)

**Operators:** Relational (`=`,`!=`,`<`,`<=`,`>`,`>=`,`IS NULL`,`LIKE`,`RLIKE`), Arithmetic (`+ - * / %` and bitwise `& | ^ ~`), Logical (`AND/&&`, `OR/||`, `NOT/!`), Complex (`A[n]` array index, `M[key]` map lookup, `S.x` struct field).

**Common functions:** `round()`, `floor()`, `ceil()`, `concat()`, `substr()`, `upper()/lower()`, `trim()/ltrim()/rtrim()`, `regexp_replace()`, `size()`, `cast(expr AS type)`, `from_unixtime()`, `to_date()`, `year()/month()/day()`.

**Aggregate functions:** `count(*)`, `sum()`, `avg()`, `min()`, `max()` — used with `GROUP BY`; filter aggregated groups with `HAVING` (not `WHERE`).

### 6.13 Joins
```sql
-- INNER JOIN — only matching rows
SELECT c.ID, c.NAME, o.AMOUNT FROM CUSTOMERS c JOIN ORDERS o ON (c.ID = o.CUSTOMER_ID);

-- LEFT OUTER JOIN — all left rows, NULL if no right match
SELECT c.ID, c.NAME, o.AMOUNT FROM CUSTOMERS c LEFT OUTER JOIN ORDERS o ON (c.ID = o.CUSTOMER_ID);

-- RIGHT OUTER JOIN — all right rows, NULL if no left match
SELECT c.ID, c.NAME, o.AMOUNT FROM CUSTOMERS c RIGHT OUTER JOIN ORDERS o ON (c.ID = o.CUSTOMER_ID);

-- FULL OUTER JOIN — all rows from both sides, NULL where unmatched
SELECT c.ID, c.NAME, o.AMOUNT FROM CUSTOMERS c FULL OUTER JOIN ORDERS o ON (c.ID = o.CUSTOMER_ID);
```
Also supported: `LEFT SEMI JOIN`, `CROSS JOIN`.

### 6.14 Views
- **Logical only** — no physical data stored; the SELECT runs each time the view is queried.
- Schema is **frozen at creation**; changes to underlying tables are NOT reflected.
- Read-only — cannot `LOAD`/`INSERT`/`ALTER` data directly through a view.
```sql
CREATE VIEW emp_30000 AS SELECT * FROM employee WHERE salary > 30000;
ALTER VIEW v1 AS SELECT * FROM t2;
DROP VIEW [IF EXISTS] emp_30000;
```

### 6.15 Subqueries — know the restrictions (this trips people up)
- ❌ **NOT supported in the SELECT clause** (scalar/correlated subqueries as expressions) → use a `LEFT JOIN + GROUP BY` instead.
- ✅ **Supported in the FROM clause** — subquery **must be aliased**.
- ✅ **Supported in the WHERE clause** for `IN`/`NOT IN` (single column only) and `EXISTS`/`NOT EXISTS` (needs correlated predicate).

```sql
-- FROM clause subquery (must alias)
SELECT department, avg_salary FROM (
  SELECT department, AVG(salary) AS avg_salary FROM employees GROUP BY department
) AS dept_summary;

-- WHERE clause subquery
SELECT * FROM customer WHERE customer_num IN (
  SELECT DISTINCT customer_num FROM orders WHERE amount > 2000
);
```

### 6.16 Quick MCQ-style self-check (from your slides' "What did you grasp" sections)
- `HAVING` filters rows **after** aggregation (not `WHERE`).
- `ORDER BY` sorts globally; `SORT BY` sorts per-reducer (both are valid "sort" answers).
- Metastore stores metadata **only** — actual data lives in HDFS.
- Enable bucketing via `hive.enforce.bucketing`.
- Hive is best suited for **structured / semi-structured** data with an existing schema layout, not arbitrary unstructured blobs.

---

## 7. Apache Spark & PySpark
*(Not in your uploaded slides, but directly tested in the 2024 paper — standard theory below.)*

### 7.1 Spark vs Hadoop MapReduce (2024 PYQ: growing/streaming dataset scenario)
> **Q: Processing a massive, continuously-growing dataset — Spark or MapReduce?**

**Answer: Spark**, because:

| Dimension | MapReduce | Spark |
|---|---|---|
| Performance | Disk-based between every Map/Reduce stage → slow for iterative/streaming workloads | **In-memory** computation (RDDs cached in RAM) → up to 100x faster for iterative jobs; has native **Spark Streaming/Structured Streaming** for continuously arriving data |
| Fault tolerance | Achieved via **data replication** on disk (HDFS) | Achieved via **RDD lineage graphs** (DAG) — lost partitions are recomputed from lineage rather than read from a replica |
| Ease of use | Verbose Java API, only Map/Reduce primitives | Rich, concise APIs in Scala/Python/Java/R (Spark SQL, DataFrame, MLlib, GraphX) |
| Best fit | Very large one-off batch jobs where memory is limited | Growing/streaming data, iterative algorithms (ML, graph), interactive queries |

**Trade-off to mention:** Spark needs more RAM and can be costlier to provision; MapReduce is simpler/cheaper for pure massive batch jobs where speed isn't critical.

### 7.2 RDDs (Resilient Distributed Datasets)
An RDD is Spark's core abstraction: an **immutable, distributed, partitioned collection of objects** that can be operated on in parallel.
- **Resilient** – fault-tolerant via lineage (can be recomputed if a partition is lost — no need for replication).
- **Distributed** – partitioned across nodes in the cluster.
- **Lazy evaluation** – transformations aren't executed until an action is called, allowing Spark to optimize the execution DAG.
- **Enables parallelism** because each partition can be processed independently and concurrently by a different executor/core, and operations (map, filter, etc.) are applied to each partition in parallel without needing shared/synchronized state.

### 7.3 Transformations vs Actions (5 examples each — 2024 PYQ)

**Transformations** (lazy — return a new RDD, not executed immediately):
| Function | Example |
|---|---|
| `map(func)` | `rdd.map(x => x*2)` — doubles every element |
| `filter(func)` | `rdd.filter(x => x > 10)` — keeps elements > 10 |
| `flatMap(func)` | `rdd.flatMap(line => line.split(" "))` — splits & flattens lines into words |
| `reduceByKey(func)` | `pairs.reduceByKey((a,b) => a+b)` — sums values per key |
| `sortByKey()` | `pairs.sortByKey()` — sorts RDD of (k,v) by key |

**Actions** (eager — trigger execution, return a value to the driver):
| Function | Example |
|---|---|
| `collect()` | `rdd.collect()` — returns all elements as an array to the driver |
| `count()` | `rdd.count()` — number of elements |
| `first()` | `rdd.first()` — first element |
| `take(n)` | `rdd.take(5)` — first 5 elements |
| `reduce(func)` | `rdd.reduce((a,b) => a+b)` — aggregates all elements to one value |

### 7.4 🔑 Fully Solved: 2024 PYQ — Scala `reduceByKey` Walkthrough
```scala
val input = Seq(("Big", 1), ("Data", 3), ("big", 4), ("Big", 4), ("data", 2), ("data", 6))
val input2 = sc.parallelize(input)
val input3 = input2.reduceByKey((x, y) => x + y).collect
```
**Step-by-step:**
1. `input` — a Scala `Seq` of (String, Int) tuples.
2. `sc.parallelize(input)` — distributes this local collection into an **RDD** across the Spark cluster's partitions.
3. `reduceByKey((x, y) => x + y)` — a **transformation**: groups all values sharing the **exact same key** (⚠️ keys are **case-sensitive** — `"Big"` and `"big"` are different keys) and sums them within each group.
   - `"Big"` → 1 + 4 = **5**
   - `"Data"` → **3**
   - `"big"` → **4**
   - `"data"` → 2 + 6 = **8**
4. `.collect` — an **action**: gathers all resulting (key, value) pairs from all partitions back to the driver as an `Array`.

**Output:** `Array((Big,5), (Data,3), (big,4), (data,8))` *(exact order not guaranteed since RDDs are partitioned, but each key's aggregated value is fixed)*.

### 7.5 PySpark DataFrame Ops — 🔑 Fully Solved (2024 PYQ pattern)
> Given `df.columns = ['salary', 'age', 'experience', 'department', 'city']`

```python
# a) Shape of the DataFrame (rows, columns)
print((df.count(), len(df.columns)))

# b) View only 'age' and 'city' columns, show 5 records
df.select('age', 'city').show(5)

# c) Add a column: projected salary after 5 years (assume 5% annual increment)
from pyspark.sql.functions import col
df = df.withColumn('projected_salary_5yr', col('salary') * (1.05 ** 5))

# d) Records for employees in the Finance department
df.filter(df.department == 'Finance').show()
# equivalent: df.where(col('department') == 'Finance').show()

# e) Distinct values in the 'department' column
df.select('department').distinct().show()
```
*(State your assumed growth rate explicitly if the exam doesn't specify one — examiners want to see you handle the missing parameter sensibly.)*

### 7.6 PySpark / Spark SQL Quick Reference
| Task | Code |
|---|---|
| Read CSV | `spark.read.csv('file.csv', header=True, inferSchema=True)` |
| Show schema | `df.printSchema()` |
| Group + aggregate | `df.groupBy('department').avg('salary')` |
| Sort | `df.orderBy('salary', ascending=False)` |
| Drop column | `df.drop('city')` |
| Rename column | `df.withColumnRenamed('age','years')` |
| SQL query | `df.createOrReplaceTempView('t'); spark.sql("SELECT * FROM t")` |

---

## 8. Fully Solved — 2025 Mid-Sem Paper (25 Marks)

**Q1 [2×4=8]**
- a) *Combiner role + phase* → see §3.3
- b) *Why checkpointing?* → see §2.3.6
- c) *HBase vs RDBMS, 2 differences* → see §5.4
- d) *Schema-on-Read vs Schema-on-Write* → see §6.6

**Q2 [7]** Hive `Book` external table → fully solved in §6.8

**Q3 [10] — choose ONE:**
- YARN components + workflow [5+5] → §4.2, §4.3
- **OR** HDFS: (a) NameNode/DataNode responsibilities [4] → §2.3; (b) write-process step-by-step [4] → §2.3.1; (c) one advantage + one limitation vs local FS [2] → §2.3.7

---

## 9. Fully Solved — 2024 Mid-Sem Paper (50 Marks)

**Q1**
1. 5 V's significance [5] → §1.2
2. Hadoop Ecosystem diagram [10] → §2.2 **OR** HDFS read/write operations [10] → §2.3.1 + §2.3.2

**Q2**
1. Spark vs MapReduce for a growing dataset [5] → §7.1
2. Importance of RDDs & parallelism [5] → §7.2
3. 5 transformations + 5 actions with examples [5] → §7.3
4. Pig vs SQL vs Hive comparison [5] → §6.2

**Q3**
1. PySpark DataFrame ops (a–e) [10] → §7.5
2. Scala `reduceByKey` code walkthrough [5] → §7.4 **OR** MapReduce letter-count program [5] → §3.6

---

## 10. Predicted Questions for This Term (practice these!)

Since the paper draws consistently from the same Unit-1 deck, these variations are very plausible:

1. Explain the HDFS architecture with a neat diagram, including the role of the Secondary NameNode. *(§2.3)*
2. Differentiate Managed vs External Hive tables. Write a query to create each. *(§6.7)*
3. Explain the MapReduce execution flow with a word-count example, and state where the Combiner fits in. *(§3.5, §3.3)*
4. Compare Static vs Dynamic partitioning in Hive with an example of each. *(§6.9)*
5. Explain HBase architecture (HMaster, RegionServer, ZooKeeper) and how it differs from HDFS alone. *(§5.5)*
6. Explain the YARN Application Workflow end-to-end for a submitted job. *(§4.3)*
7. Write HiveQL for: create table with partitioning, load data, and query with a `JOIN`. *(§6.9, §6.13)*
8. Explain Heartbeats and Block Reports and what happens when a DataNode fails. *(§2.3.3)*
9. What is bucketing and why/when would you prefer it over partitioning? *(§6.10)*
10. Compare Hive and traditional RDBMS on 4–5 dimensions. *(§6.5)*

---

## 11. Ultimate Last-Night Cheat Sheet

- **HDFS block size:** 128 MB | **Replication factor:** 3 | **Heartbeat:** ~3s | **DataNode dead after:** ~10.5 min silence | **Block report:** ~6 hrs
- **NameNode** = metadata only. **DataNode** = actual data. **Secondary NameNode** = checkpointing, NOT a backup.
- **Combiner** = mini-reducer, runs right after Map, reduces network traffic. Cannot replace Reducer.
- **MapReduce flow:** Map → Shuffle & Sort → Reduce.
- **YARN 5 components:** Client, Resource Manager (Scheduler + Applications Manager), Node Manager, Application Master, Container.
- **HBase 3 components:** HMaster, RegionServer, ZooKeeper.
- **HBase = column-oriented, schema-less (column families only); RDBMS = row-oriented, fixed schema.**
- **Hive Metastore modes:** Embedded (1 session, Derby) / Local (multi-session, separate DB process) / Remote (separate JVM, Thrift).
- **Managed table drop** → deletes data + metadata. **External table drop** → deletes metadata only, data survives.
- **Schema-on-Read** (Hive, validated at query time) vs **Schema-on-Write** (RDBMS, validated at load time).
- **Partitioning** = subdirectories by column value (uneven sizes possible). **Bucketing** = fixed-count hash-based files (even sizes) — use `CLUSTERED BY ... INTO n BUCKETS`.
- **Subqueries:** NOT allowed in SELECT clause; allowed (aliased) in FROM clause; allowed in WHERE for IN/EXISTS.
- **Spark RDD** = immutable, distributed, lazy, fault-tolerant via lineage (not replication).
- **Spark beats MapReduce for:** growing/streaming data, iterative jobs — due to in-memory processing + streaming APIs.
- **HAVING** filters after `GROUP BY`; **WHERE** filters before.

---

## 12. Suggested 3-Day Study Plan

| Day | Focus |
|---|---|
| **Day 1** | Big Data fundamentals (§1) + HDFS architecture & read/write (§2) — these underpin everything else |
| **Day 2** | MapReduce (§3) + YARN (§4) + HBase (§5) — write out the workflows from memory, don't just re-read |
| **Day 3** | Hive DDL/DML/partitioning/bucketing (§6) + Spark/PySpark (§7), then do both full PYQ papers (§8, §9) closed-book, and check against the cheat sheet (§11) |

Good luck — you're well covered on every topic both papers have touched. Focus extra energy on **Hive table creation syntax** and the **HDFS write pipeline**, since those come up as concrete, gradable coding-style questions every single year.
