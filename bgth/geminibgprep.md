# Comprehensive Mid-Semester Study & Preparation Guide
**Course Code:** 20IC404T — Big Data Analytics and Computing  
**Target Weightage:** 25 Marks (Mid-Semester Exam Pattern)

---

## Part 1: Mid-Semester Exam Blueprint & Weightage Breakdown

Based on the 2025 Mid-Semester examination pattern, the 25-mark paper is structured as follows:

| Section | Question Type | Target Marks | Typical Content Covered |
| :--- | :--- | :--- | :--- |
| **Q1** | **Short Answer Concepts** (4 questions × 2 marks) | **8 Marks** | Core definitions, component roles, critical differentiators (Combiner, Checkpointing, HBase vs RDBMS, Schema-on-Read vs Write). |
| **Q2** | **Hands-on / Query / Coding Problem** | **7 Marks** | HiveQL practicals (External vs Managed tables, Data Loading, CTAS, Partitioning, Bucketing) or PySpark DataFrame operations. |
| **Q3** | **Long Architectural / Workflow Question** *(With OR choice)* | **10 Marks** (5 + 5) | Full system breakdown: Hadoop YARN architecture & workflow **OR** HDFS Architecture, replication write-pipeline, and design trade-offs. |

---

## Part 2: Fully Solved Past Year Papers

---

### Mid-Semester 2025 (25 Marks) — Model Solutions

#### Q1. Answer the following: [2 × 4 = 8 Marks]

##### a) Define the role of the Combiner in a MapReduce job? State the phase after which it will be used? [2 Marks]
* **Role:** The **Combiner** acts as a *"semi-reducer"* or *local aggregator* that runs on the mapper node. It aggregates intermediate key-value pairs produced by the local Map tasks before they are transmitted across the cluster network. Its primary goals are:
  1. To drastically reduce the volume of data sent across the network to Reducers (minimizes network I/O congestion).
  2. To lower disk I/O and CPU memory pressure on the Reducer nodes.
* **Phase after which it is used:** It is executed **immediately after the Map phase** (on the local mapper node) and **before the Shuffle & Sort phase**.

##### b) Why is checkpointing used in HDFS? [2 Marks]
* The Primary NameNode stores its file system metadata in RAM for microsecond access, while logging all write/edit operations to an `EditLog` file on disk, with periodic snapshots stored in `FsImage`.
* Over time, the `EditLog` grows excessively large. If the NameNode restarts, replaying a huge `EditLog` takes an unacceptably long time, causing extended cluster downtime.
* **Checkpointing** (performed by the Secondary NameNode) downloads the `FsImage` and `EditLog`, merges them into an updated, compact `FsImage` (`fsimage.ckpt`), and uploads it back to the Primary NameNode, which truncates the old `EditLog`. This keeps the `EditLog` small and ensures fast cluster restart/recovery.

##### c) How does HBase's data model differ from a traditional relational database (RDBMS)? Give two main differences. [2 Marks]
1. **Column-Oriented & Sparse vs. Row-Oriented & Dense:**
   * **HBase:** Data is stored contiguously by column families. It is schema-less at the column qualifier level and stores sparse tables efficiently; empty/null cells consume **zero storage**.
   * **RDBMS:** Data is stored sequentially row-by-row with a fixed, rigid schema. Null values occupy storage and schema alterations require table alterations.
2. **Built-in Versioning via Timestamps:**
   * **HBase:** Every cell inherently supports multi-versioning. Multiple values of the same cell are preserved alongside millisecond timestamps (or user-defined version numbers).
   * **RDBMS:** Updates overwrite existing row values in-place unless manually historized using audit tables or triggers.

##### d) What is the core principle of "Schema-on-Read" as used by Hive? How is it different from "Schema-on-Write"? [2 Marks]
* **Core Principle of Schema-on-Read:** Data is stored in raw, native format (text, CSV, ORC, etc.) on HDFS without any format validation upon file upload. The structure (schema) is applied and interpreted **only when a query is executed (at read time)**.
* **Difference from Schema-on-Write:**
  * **Schema-on-Write (Traditional RDBMS):** Data must conform strictly to a predefined schema *before* it is written to the database. If fields are missing, invalid, or mismatched, the database rejects the write operation.
  * **Schema-on-Read (Hive):** Guarantees exceptionally fast and flexible ingestion because files are simply copied into HDFS without parsing. Any mismatched data types at read time evaluate to `NULL` rather than failing the ingestion pipeline.

---

#### Q2. HiveQL Practical Problem [Total: 7 Marks]

Given an external Hive table `Book` with schema:  
`(book_id INT, title STRING, author STRING, price FLOAT)` located at `'/user/hive/input/'`.

##### a) Write the Hive Query to create this table, specifying comma-delimited text format. [3 Marks]
```sql
CREATE EXTERNAL TABLE IF NOT EXISTS Book (
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

##### b) Write the command to load data into it from the local file `'/home/cloudera/book_data.txt'` by overwriting the previous content. [2 Marks]
```sql
LOAD DATA LOCAL INPATH '/home/cloudera/book_data.txt' 
OVERWRITE INTO TABLE Book;
```

##### c) Write a query to create a new managed table, `'ExpensiveBooks'`, containing all columns for books with a price greater than 100. [2 Marks]
```sql
CREATE TABLE ExpensiveBooks AS
SELECT * 
FROM Book
WHERE price > 100.0;
```

---

#### Q3. Long Architectural / Workflow Question [10 Marks]

#### OPTION 1: Hadoop YARN Architecture and Workflow [5 + 5 = 10 Marks]

##### Part A: Purpose of Core Components (5 Marks)

```
                       +-------------------+
                       |      Client       |
                       +---------+---------+
                                 | (Job Submission)
                                 v
                       +-------------------+
                       |  Resource Manager |
                       |  - Scheduler      |
                       |  - Apps Manager   |
                       +----+---------+----+
                            |         |
              +-------------+         +-------------+
              |                                     |
              v                                     v
     +-----------------+                   +-----------------+
     |  Node Manager   |                   |  Node Manager   |
     | +-------------+ |                   | +-------------+ |
     | | AppMaster   | |                   | | Container   | |
     | +-------------+ |                   | | (Task)      | |
     | +-------------+ |                   | +-------------+ |
     | | Container   | |                   | +-------------+ |
     | | (Task)      | |                   | | Container   | |
     | +-------------+ |                   | +-------------+ |
     +-----------------+                   +-----------------+
```

1. **ResourceManager (RM):** The master daemon of the entire cluster. It makes global allocation decisions for all compute resources (CPU cores, memory) across applications. It consists of two sub-components:
   * **Scheduler:** Allocates resources strictly according to queue capacities and policies (e.g., Capacity Scheduler, Fair Scheduler). It does *not* monitor application progress or handle task retries.
   * **ApplicationsManager (ASM):** Accepts incoming job submissions, negotiates the initial container to launch the ApplicationMaster, and restarts the ApplicationMaster if it fails.
2. **NodeManager (NM):** The per-node worker agent daemon. It registers with the ResourceManager, periodically sends heartbeats containing node health metrics, and manages the life cycle of containers running on that physical machine.
3. **ApplicationMaster (AM):** A lightweight, framework-specific coordinator spawned *per application* (one per MapReduce job, Spark application, etc.). It negotiates containers with the ResourceManager and collaborates with NodeManagers to launch, execute, and monitor application tasks.
4. **Container:** The basic unit of physical resource allocation on a NodeManager, dynamically encapsulating a bundle of CPU cores, RAM, and disk storage. Tasks execute inside these isolated boundaries defined by a **Container Launch Context (CLC)**.
5. **Client:** The interface used by external users or scripts to submit applications, track runtime status, and retrieve final logs.

##### Part B: Step-by-Step YARN Application Workflow (5 Marks)
1. **Application Submission:** The Client communicates with the ResourceManager's ApplicationsManager, submitting the job package (application code, configuration, dependencies, and resource specs).
2. **ApplicationMaster Container Allocation:** The RM allocates an initial container on an available NodeManager to host the application's dedicated ApplicationMaster.
3. **ApplicationMaster Launch:** The designated NodeManager allocates the container, launches the ApplicationMaster instance, and starts its process.
4. **ApplicationMaster Registration:** The AM registers itself with the ResourceManager, allowing the client to query the AM directly for status updates.
5. **Resource Negotiation:** The AM calculates resource requirements based on input splits and submits heartbeats to the RM's Scheduler requesting worker containers (specifying node/rack locality, CPU, and memory).
6. **Container Launch on Worker Nodes:** Once the RM grants container leases, the AM contacts the respective NodeManagers, supplying the Container Launch Context (CLC) to start task processes.
7. **Task Execution & Monitoring:** Tasks execute inside their assigned containers. The AM tracks each task's progress, re-requesting containers from the RM if any task crashes.
8. **Completion & Deregistration:** When all tasks finish, the AM sends an unregistration call to the RM, cleans up state, releases all containers back to the cluster pool, and shuts down.

---

#### OPTION 2 (OR): HDFS Architecture, Write Pipeline, and Trade-offs [10 Marks]

##### a) The Two Main Architectural Components of HDFS and Primary Responsibilities (4 Marks)

```
                     +---------------------------------------+
                     |           HDFS NameNode               |
                     |  - Metadata & Directory Namespace     |
                     |  - Block Mapping (File -> Block IDs)  |
                     +-------------------+-------------------+
                                         |
               +-------------------------+-------------------------+
               | (Heartbeats / Block Reports)                      |
               v                                                   v
     +-------------------+                               +-------------------+
     |   DataNode 1      |                               |   DataNode 2      |
     | [B1][B2][B3]      | <==== Replication Pipeline ==> | [B1][B2]          |
     | - Stores Blocks   |                               | - Stores Blocks   |
     | - Serves Reads    |                               | - Serves Reads    |
     +-------------------+                               +-------------------+
```

1. **NameNode (Master Node):**
   * **Namespace Management:** Maintains the file system directory tree, file ownership, permissions, and file-to-block mapping in RAM for fast lookups.
   * **Block Coordination:** Decides how files are sliced into blocks (e.g., 128 MB), assigns blocks to DataNodes, and regulates replication policy.
   * **Cluster Health Monitoring:** Tracks active DataNodes via periodic heartbeats (every 3 seconds) and maintains block inventories via block reports.
2. **DataNode (Worker/Slave Node):**
   * **Block Storage:** Stores the actual file data blocks as separate underlying files on the local Linux ext4/xfs filesystem.
   * **Block Operations:** Creates, reads, writes, and deletes physical data blocks upon direct instruction from the NameNode or Client.
   * **Health & Status Reporting:** Periodically sends heartbeats to confirm operational status and sends Block Reports (every 6 hours) detailing its locally stored blocks.

##### b) Step-by-Step Write Operation Process for a New File (`data.txt`) (4 Marks)
1. **Client Request to NameNode:** The client invokes `DistributedFileSystem.create()` to request the creation of `data.txt`. The NameNode verifies permissions and path availability, creates an entry in its namespace, and returns an `FSDataOutputStream`.
2. **Block Allocation:** When the client starts writing the first 128 MB block, it asks the NameNode for a target list of DataNodes based on rack awareness (e.g., DN1 [local rack], DN2 [remote rack], DN3 [same remote rack, different node]).
3. **Replication Pipeline Construction:** The client opens a direct TCP streaming connection to DN1. DN1 connects to DN2, and DN2 connects to DN3, forming a streaming pipeline:
   $$\text{Client} \longrightarrow \text{DN1} \longrightarrow \text{DN2} \longrightarrow \text{DN3}$$
4. **Pipelined Data Streaming:** The client splits the 128 MB block into small 64 KB packets. It streams packet 1 to DN1; DN1 flushes it to its local disk and immediately forwards packet 1 to DN2, while the client sends packet 2 to DN1.
5. **Reverse Acknowledgment (ACK):** When DN3 completes writing a packet, it sends an ACK upstream to DN2, which forwards it to DN1, and DN1 forwards it to the client.
6. **File Finalization:** Once all blocks are streamed and acknowledged, the client calls `close()` on the output stream. The NameNode commits the file to persistent metadata storage and confirms completion.

##### c) One Key Advantage and One Key Limitation of HDFS (2 Marks)
* **Key Advantage:** **High Fault Tolerance & Scalability on Commodity Hardware:** Data is split into large blocks and replicated across distinct nodes and racks (default replication factor = 3). If a disk or node crashes, the system automatically detects it and replicates data from surviving copies without data loss or service disruption.
* **Key Limitation:** **High Latency / Inefficient for Small Files:** HDFS is optimized for high-throughput batch streaming of very large files (Write-Once, Read-Many / WORM). It cannot handle low-latency interactive random reads/writes (sub-millisecond) and suffers severe memory exhaustion on the NameNode if millions of tiny files are stored.

---

### Solved High-Yield Questions from 2024 Exam Paper (50 Marks)

#### 1. Explain the Significance of all 5 V's of Big Data [5 Marks]
* **Volume:** The massive scale and size of datasets generated every second (terabytes to zettabytes). Traditional relational systems cannot scale vertically to handle this volume; distributed horizontal architectures (like HDFS) are required.
* **Velocity:** The speed at which data is produced, streamed, and needs to be analyzed (e.g., IoT sensors, credit card fraud checks, stock feeds). Processing must often happen in real time before data becomes stale.
* **Variety:** Structural diversity of data types:
  * *Structured:* Relational database tables, CSV files.
  * *Semi-Structured:* JSON, XML, server access logs.
  * *Unstructured:* Audio, video, satellite imagery, text feeds (~80–90% of all real-world data).
* **Veracity:** The trustworthiness, noise, cleanliness, and authenticity of data. Dirty data, sensor calibration drifts, and malicious inputs require data cleansing and validation.
* **Value:** The ultimate business payoff and actionable insights extracted through analytics (e.g., predictive maintenance, fraud prevention, dynamic pricing).

#### 2. Apache Spark vs. Hadoop MapReduce for Rapidly Growing Datasets [5 Marks]
* **Selection:** Choose **Apache Spark**.
* **Justification & Trade-offs:**
  * **Performance:** Spark executes processing **in-memory** using directed acyclic graph (DAG) execution, eliminating the extensive disk read/write spills that occur between Map and Reduce phases in MapReduce. Spark is up to 100× faster in memory and 10× faster on disk. For data growing every minute, Spark Streaming / Structured Streaming provides near real-time, low-latency micro-batching.
  * **Fault Tolerance:** MapReduce provides fault tolerance by persisting every intermediate stage to disk (safe, but slow). Spark achieves fault tolerance through **RDD Lineage Graphs**: if a partition is lost, Spark recomputes only the lost partition from memory using its dependency graph without restarting the whole job.
  * **Ease of Use:** Spark provides expressive, high-level APIs in Python, Scala, Java, and SQL with over 80 high-level operators (`map`, `filter`, `reduceByKey`), compared to MapReduce's verbose, low-level Java boilerplate code.

#### 3. Importance of RDDs in Apache Spark & How They Enable Parallelism [5 Marks]
* **Resilient Distributed Datasets (RDDs):** RDDs are the fundamental abstraction of Apache Spark. They are:
  1. *Resilient:* Fault-tolerant using the RDD Lineage Graph (recomputes lost blocks automatically).
  2. *Distributed:* Data is horizontally partitioned across multiple cluster nodes.
  3. *Dataset:* A collection of partitioned records loaded in-memory.
* **How RDDs Enable Parallelism:**
  * An RDD is partitioned into discrete chunks across cluster worker nodes.
  * Each worker thread/executor processes a single partition concurrently and independently.
  * Spark schedules one task per RDD partition, aligning compute directly with data locality, allowing seamless, linear horizontal scaling.

#### 4. Five Transformation and Five Action Functions in Spark with Examples [5 Marks]
* **Transformations (Lazy evaluation; constructs new RDD from existing RDD):**
  1. `map(func)`: Applies a function to each element.  
     *Example:* `rdd.map(x => x * 2)`
  2. `filter(func)`: Returns elements where the function evaluates to true.  
     *Example:* `rdd.filter(x => x % 2 == 0)`
  3. `flatMap(func)`: Maps each element to 0 or more output items (flattens lists).  
     *Example:* `rdd.flatMap(line => line.split(" "))`
  4. `distinct()`: Returns a new dataset with duplicates removed.  
     *Example:* `rdd.distinct()`
  5. `reduceByKey(func)`: Combines values for each key using an associative reduce function.  
     *Example:* `pairRdd.reduceByKey((a, b) => a + b)`
* **Actions (Eager evaluation; triggers computation graph to return results or write to disk):**
  1. `collect()`: Returns all elements of the RDD to the driver program as an array.  
     *Example:* `rdd.collect()`
  2. `count()`: Returns the total number of elements in the RDD.  
     *Example:* `rdd.count()`
  3. `first()`: Returns the first element of the dataset.  
     *Example:* `rdd.first()`
  4. `take(n)`: Returns an array with the first $n$ elements.  
     *Example:* `rdd.take(5)`
  5. `saveAsTextFile(path)`: Writes elements to a text file in HDFS/local storage.  
     *Example:* `rdd.saveAsTextFile("hdfs://output/data")`

#### 5. Comparison: Apache Pig vs. SQL vs. Apache Hive [5 Marks]

| Feature | Apache Pig | SQL (Traditional RDBMS) | Apache Hive |
| :--- | :--- | :--- | :--- |
| **Language** | Pig Latin (Procedural data-flow) | SQL (Declarative query) | HiveQL (Declarative SQL dialect) |
| **Data Types** | Structured, semi-structured, tuples, bags, maps | Structured schemas only | Structured and semi-structured |
| **Execution** | Compiles to MapReduce/Tez | Direct database query engine | Compiles to MapReduce / Tez / Spark |
| **Schema** | Schema-on-Read / Optional | Strict Schema-on-Write | Schema-on-Read |
| **Primary Audience** | Developers, programmers, data pipeline builders | Database administrators, application devs | Data analysts, business intelligence engineers |
| **Metastore** | No central metadata database | System catalog tables | Dedicated external RDBMS Metastore (MySQL/Derby) |

#### 6. PySpark SQL DataFrame Practical Operations [10 Marks]
Given `df.columns` = `['salary', 'age', 'experience', 'department', 'city']`

```python
from pyspark.sql.functions import col

# a) Display the shape of the data (rows, columns)
print(f"Shape: ({df.count()}, {len(df.columns)})")

# b) View only columns 'age' and 'city', show 5 records
df.select("age", "city").show(5)

# c) Add a new column that stores projected salary after 5 years (assume 10% annual hike or simple multiplier)
df_projected = df.withColumn("projected_salary_5yrs", col("salary") * (1.10 ** 5))
df_projected.show(5)

# d) Fetch records for employees working in the 'Finance' department
df.filter(col("department") == "Finance").show()

# e) View distinct values for the column 'department'
df.select("department").distinct().show()
```

#### 7. Scala Spark Code Step-by-Step Analysis [5 Marks]
```scala
val input = Seq(("Big", 1), ("Data", 3), ("big", 4), ("Big", 4), ("data", 2), ("data", 6))
val input2 = sc.parallelize(input)
val input3 = input2.reduceByKey((x, y) => x + y).collect
```
* **Step 1:** `val input = Seq(...)`  
  Creates an in-memory Scala sequence containing 6 key-value tuples: `("Big", 1), ("Data", 3), ("big", 4), ("Big", 4), ("data", 2), ("data", 6)`.
* **Step 2:** `val input2 = sc.parallelize(input)`  
  Converts the local sequence into a distributed RDD (`input2`) across Spark worker nodes.
* **Step 3:** `input2.reduceByKey((x, y) => x + y)`  
  Groups values having identical keys and merges them by adding them together.  
  *String matching is case-sensitive:*
  * Key `"Big"`: $1 + 4 = 5$
  * Key `"Data"`: $3$
  * Key `"big"`: $4$
  * Key `"data"`: $2 + 6 = 8$
* **Step 4:** `.collect`  
  Triggers an **Action**, computing the DAG and pulling the RDD contents into an Array on the driver node.
* **Final Output:**
```scala
Array((Big, 5), (Data, 3), (big, 4), (data, 8))
```
*(Note: Key order inside the returned array may vary based on cluster partitioning).*

#### 8. MapReduce Letter Count Implementation [5 Marks]

##### Mapper (Python Streaming: `mapper.py`)
```python
import sys

for line in sys.stdin:
    line = line.strip().lower()
    for char in line:
        if char.isalpha():
            print(f"{char}\t1")
```

##### Reducer (Python Streaming: `reducer.py`)
```python
import sys

current_char = None
current_count = 0

for line in sys.stdin:
    char, count = line.strip().split('\t')
    count = int(count)
    
    if current_char == char:
        current_count += count
    else:
        if current_char:
            print(f"{current_char}\t{current_count}")
        current_char = char
        current_count = count

if current_char:
    print(f"{current_char}\t{current_count}")
```
* **Execution Pipe:**
```bash
cat input.txt | python mapper.py | sort | python reducer.py
```

---

## Part 3: Deep Technical Notes by Module

---

### Module 1: Big Data Fundamentals & HDFS Internals

#### 1. The 4 Categories of Data Analytics
```
            +-------------------------------+
            |        PRESCRIPTIVE           |  "How can we make it happen?"
            |  (Optimization & Simulation)  |  (Prescribes optimal actions)
            +---------------+---------------+
                            ^
            +---------------+---------------+
            |          PREDICTIVE           |  "What is likely to happen?"
            |      (Machine Learning)       |  (Forecasts future patterns)
            +---------------+---------------+
                            ^
            +---------------+---------------+
            |          DIAGNOSTIC           |  "Why did it happen?"
            |        (Root Cause)           |  (Drills into anomalies)
            +---------------+---------------+
                            ^
            +---------------+---------------+
            |          DESCRIPTIVE          |  "What happened in the past?"
            |    (Reporting & Dashboards)   |  (Historical reporting)
            +-------------------------------+
```

#### 2. Physical & Logical Layout of HDFS
* **Racks & Switches:** Clusters are organized into physical racks connected through network switches. NameNode uses **Rack Awareness** to avoid placing all replicas in the same rack.
* **Block Abstraction:** Files are split into fixed blocks (default: 128 MB in modern Hadoop; 64 MB in Hadoop 1.0).
  * *Why Blocks?*
    1. Enables a file to be larger than any single physical hard disk in the cluster.
    2. Simplifies storage management (predictable block sizes).
    3. Simplifies replication and fine-grained load balancing across nodes.
* **Replication Strategy (Default Factor = 3):**
  * Replica 1: Placed on a DataNode in the local rack as the client.
  * Replica 2: Placed on a DataNode in a different, remote rack.
  * Replica 3: Placed on a different DataNode within the same remote rack.

#### 3. Heartbeats vs. Block Reports
* **Heartbeat:** Sent every **3 seconds**. Communicates node survival, remaining disk capacity, and active data transfers. If no heartbeat arrives for **10.5 minutes** ($10 \times \text{heartbeat interval} + \text{check time}$), the node is declared dead and its blocks are scheduled for re-replication.
* **Block Report:** Sent every **6 hours**. Contains a complete list of all physical blocks stored on that DataNode, allowing the NameNode to rebuild its block-to-node location mapping.

#### 4. HDFS Safemode
* **What is Safemode?** A read-only administrative state entered automatically during NameNode startup. File modifications, writes, and block replications are prohibited.
* **Why Required?** The NameNode does *not* persist block locations to disk (it only saves namespace and file-to-block IDs). It must wait for DataNodes to register and submit their Block Reports to rebuild the memory mapping.
* **Exit Condition:** When the NameNode verifies that **99.9%** of all data blocks satisfy the minimum replication factor, it waits for a **30-second extension timer** and then automatically exits Safemode.

---

### Module 2: Hadoop YARN Architecture

#### 1. Why Hadoop 1.0 Failed to Scale (JobTracker Bottleneck)
* In Hadoop 1.0, the **JobTracker** had dual responsibilities:
  1. Cluster Resource Management (monitoring free slots across nodes).
  2. Application Execution & Monitoring (tracking map/reduce tasks, handling retries).
* Scalability hit an architectural ceiling at ~4,000 nodes and 40,000 concurrent tasks.
* Clusters were strictly hardcoded for MapReduce—other engines (Spark, GraphX, Storm) could not share the HDFS infrastructure.

#### 2. The YARN Paradigm Shift
* **Separation of Concerns:** YARN decouples the resource management layer from the processing layer.
  * *ResourceManager* handles cluster resources only.
  * *ApplicationMaster* handles application execution only.
* **Multi-Tenancy:** Spark, Flink, Storm, and MapReduce can run concurrently on the same physical cluster without conflict.

---

### Module 3: MapReduce Programming Paradigm

#### 1. Mathematical Formalism
$$\text{Map}: (K_1, V_1) \longrightarrow \text{List}(K_2, V_2)$$
$$\text{Reduce}: (K_2, \text{List}(V_2)) \longrightarrow \text{List}(K_3, V_3)$$

#### 2. Shuffle & Sort Internals
1. **Partitioner:** Computes the destination reducer index using hash partitioning:  
   $$\text{Reducer Index} = \text{hash}(\text{Key}) \pmod{\text{Total Reducers}}$$
2. **Sort:** Keys are sorted locally on the Mapper node before being spilled to disk.
3. **Shuffle:** The framework transfers sorted key-value output partitions over the network from Mapper nodes to the assigned Reducers.
4. **Merge-Sort:** Reducers merge sorted incoming streams so values belonging to identical keys are grouped together as $(K_2, [V_{21}, V_{22}, \dots])$.

---

### Module 4: Apache HBase

#### 1. Architecture Components
* **HMaster:** Coordinates administrative DDL tasks (table create, delete, schema modify), manages region splits, rebalances regions across RegionServers, and handles failovers.
* **RegionServer:** Worker daemon running on DataNodes. Serves read and write operations for specific table **Regions** (horizontal range-based slices of rows). Contains:
  * **WAL (Write Ahead Log):** Persists writes to disk before memory for crash recovery.
  * **MemStore:** In-memory write buffer.
  * **HFiles:** Immutable underlying columnar data files persisted in HDFS.
* **ZooKeeper:** Manages distributed consensus, tracks RegionServer health, and stores the location of the `-ROOT-` / `hbase:meta` system catalog table.

#### 2. Essential HBase Shell Command Reference

```bash
# General / Status
status
version
whoami

# DDL Commands
create 'employee', 'personal_data', 'professional_data'
list
describe 'employee'
alter 'employee', {NAME => 'salary_data', VERSIONS => 3}
disable 'employee'
is_disabled 'employee'
enable 'employee'
is_enabled 'employee'
drop 'employee'              # Note: Table MUST be disabled first!
truncate 'employee'          # Disables, drops, and recreates the table

# DML Commands
# put 'table', 'row_key', 'family:column', 'value'
put 'employee', 'emp_01', 'personal_data:name', 'Alice'
put 'employee', 'emp_01', 'personal_data:city', 'New York'
put 'employee', 'emp_01', 'professional_data:salary', '95000'

# Retrieval
get 'employee', 'emp_01'
get 'employee', 'emp_01', {COLUMN => 'personal_data:name'}
get 'employee', 'emp_01', {COLUMN => 'personal_data:name', VERSIONS => 3}

# Scanning
scan 'employee'
scan 'employee', {COLUMNS => ['personal_data:name'], LIMIT => 10}
scan 'employee', {STARTROW => 'emp_01', STOPROW => 'emp_05'}

# Deletions
delete 'employee', 'emp_01', 'personal_data:city'   # Deletes a specific cell
deleteall 'employee', 'emp_01'                      # Deletes entire row
count 'employee'                                   # Counts rows
```

---

### Module 5: Apache Hive & HiveQL

#### 1. Hive Architecture Flow

```
   User Query (CLI / Web UI / JDBC / ODBC)
                     |
                     v
               [ Hive Driver ]
                     |
         +-----------+-----------+
         |                       |
         v                       v
   [ Compiler ] <---------> [ Metastore ] (Schemas, Partitions)
         |                       |
         v                       |
   [ Optimizer ]                 |
         |                       |
         v                       |
   [ Execution Engine ] <--------+
         |
         v
   Executes MapReduce / Tez / Spark jobs on HDFS
```

#### 2. Metastore Connection Modes
1. **Embedded Mode:** Both Metastore service and Hive service share the same JVM. Uses an embedded Apache Derby database backed by local disk. **Limitation:** Supports only **one active user session** at a time; not suitable for production.
2. **Local Mode:** Metastore service still runs inside the same JVM as the Hive driver, but connects to an external database (e.g., MySQL, PostgreSQL) running in a separate process/machine via JDBC. Supports multiple concurrent client sessions.
3. **Remote Mode:** The Metastore service runs as an independent Thrift server process inside its own JVM. Multiple Hive clients and other engines (Spark, Presto) connect via network Thrift protocols. Database credentials are secured on the remote Metastore server.

#### 3. Managed Tables vs. External Tables

| Property | Managed (Internal) Table | External Table |
| :--- | :--- | :--- |
| **Creation Syntax** | `CREATE TABLE table_name ...` | `CREATE EXTERNAL TABLE ... LOCATION 'hdfs_path'` |
| **Default Location** | `/user/hive/warehouse/dbname.db/tablename` | Anywhere specified across HDFS |
| **Data Ownership** | Hive has full lifecycle control | External owner / Other engines share the data |
| **Effect of `DROP TABLE`** | **Deletes BOTH metadata AND physical data files in HDFS** | **Deletes ONLY metadata; physical files remain safe in HDFS** |
| **Ideal Use Case** | Temporary, intermediate, or Hive-exclusive data | Production raw data feeds, shared multi-engine datasets |

#### 4. Partitions vs. Buckets

```
Table: Sales
   |
   +-- Partition: Country=US  (Subdirectory)
   |      |
   |      +-- Bucket 1 (Hash modulo file)
   |      +-- Bucket 2 (Hash modulo file)
   |
   +-- Partition: Country=IN  (Subdirectory)
          |
          +-- Bucket 1
          +-- Bucket 2
```

* **Partitioning (`PARTITIONED BY`):**
  * Divides a table into subdirectories based on distinct column values (e.g., `Year`, `Country`, `Department`).
  * Prevents full-table scans via partition pruning.
  * **Static Partitioning:** Partition keys are hardcoded manually during load (`PARTITION (year='2024')`).
  * **Dynamic Partitioning:** Partition subdirectories are dynamically resolved at execution time based on the last selected columns.  
    *Settings Required:*
    ```sql
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode=nonstrict;
    ```
* **Bucketing (`CLUSTERED BY`):**
  * Subdivides partitions into fixed-count physical files based on a hash function:  
    $$\text{Bucket Number} = \text{hash}(\text{column}) \pmod{\text{num\_buckets}}$$
  * Solves data skew and prevents the "too many small files/directories" issue seen with high-cardinality partitions.
  * Optimizes Map-side joins and supports fast random table sampling (`TABLESAMPLE`).  
    *Setting Required:*
    ```sql
    SET hive.enforce.bucketing=true;
    ```

#### 5. Advanced HiveQL Syntax Patterns

##### Creating a Bucket Table
```sql
CREATE TABLE employee_bucketed (
    id INT,
    name STRING,
    salary FLOAT
)
CLUSTERED BY (id) INTO 4 BUCKETS
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ',';
```

##### Creating Views
* A Hive view is a purely logical alias for a query (it does not materialize data to disk):
```sql
CREATE VIEW high_earners AS
SELECT name, salary, department
FROM employee
WHERE salary > 80000;
```

##### Subquery Restrictions in Hive
* **Subqueries in `SELECT`:** **NOT SUPPORTED.**  
  *Wrong:* `SELECT name, (SELECT max(salary) FROM emp) FROM dept;` (Throws `ParseException`).  
  *Fix:* Rewrite using a `LEFT OUTER JOIN` or `CROSS JOIN`.
* **Subqueries in `WHERE`:** Supported starting in Hive 0.13 with constraints:
  * `IN` / `NOT IN` subqueries must select **only one column**.
  * `EXISTS` / `NOT EXISTS` requires at least one correlated predicate.

---

## Part 4: Exam Memory Sheet & Syntax Reference

### 1. HDFS Command Quick Sheet
```bash
# Uploading data
hdfs dfs -put localfile.txt /hdfs/destination/
hdfs dfs -copyFromLocal file.txt /hdfs/destination/
hdfs dfs -moveFromLocal file.txt /hdfs/destination/   # Deletes local source

# Downloading data
hdfs dfs -get /hdfs/file.txt local_path/
hdfs dfs -copyToLocal /hdfs/file.txt local_path/
hdfs dfs -getmerge /hdfs/dir/* merged_local.txt       # Concatenates HDFS blocks into 1 local file

# File Operations
hdfs dfs -ls /hdfs/path/
hdfs dfs -cat /hdfs/path/file.txt
hdfs dfs -rm -r /hdfs/path/
```

### 2. HiveQL Core Statements
```sql
-- Database creation with properties
CREATE DATABASE IF NOT EXISTS sales_db
COMMENT 'Company Sales Data'
LOCATION '/user/hive/custom_warehouse/'
WITH DBPROPERTIES ('creator'='DataTeam', 'dept'='Analytics');

-- Managed table creation with explicit delimiters
CREATE TABLE IF NOT EXISTS sales_data (
    trans_id BIGINT,
    customer_id STRING,
    amount DOUBLE
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t'
STORED AS TEXTFILE;

-- CTAS (Create Table As Select)
CREATE TABLE high_value_orders AS
SELECT customer_id, amount
FROM sales_data
WHERE amount > 5000.0;
```

---

## Part 5: Targeted Practice Drill for Your 25-Mark Exam

Test your readiness by writing out the solutions to these high-probability questions under exam conditions:

### Practice Set A (Expected Short Questions — 2 Marks Each)
1. **Differentiate between a Standby NameNode and a Secondary NameNode.**
   * *Answer cue:* Standby NameNode is a live hot-backup in a Hadoop 2.x High Availability (HA) cluster that provides automatic, instant failover via ZooKeeper. Secondary NameNode is merely a periodic checkpoint helper that merges `FsImage` and `EditLog`; it **cannot** act as a failover master if the Primary fails.
2. **What occurs during HDFS Safemode, and how does the cluster exit it?**
   * *Answer cue:* Read-only state; no blocks are replicated or written. Exits after DataNodes report $\ge 99.9\%$ of healthy blocks followed by a 30-second wait timer.
3. **What is the significance of the `CLUSTERED BY ... INTO n BUCKETS` clause in Hive?**
   * *Answer cue:* Divides data into $n$ files based on $\text{hash}(\text{column}) \pmod n$, accelerating joins and sampling.
4. **Why are subqueries in the Hive `SELECT` clause invalid, and what is the alternative?**
   * *Answer cue:* HiveQL parser restriction. Rewrite the query using a `LEFT JOIN` in the `FROM` clause with an aggregation group.

### Practice Set B (Expected Query Problem — 7 Marks)
**Problem:**  
Create a partitioned external table `CustomerLogs` with schema:  
`log_id INT, ip_address STRING, action STRING`  
partitioned by `log_date STRING`  
stored as comma-delimited text at `'/data/logs/'`.  
Then write the command to insert a single record into partition `'2025-09-20'`.

* **Solution:**
```sql
-- Part A: Table Creation (4 Marks)
CREATE EXTERNAL TABLE IF NOT EXISTS CustomerLogs (
    log_id INT,
    ip_address STRING,
    action STRING
)
PARTITIONED BY (log_date STRING)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION '/data/logs/';

-- Part B: Data Insertion (3 Marks)
INSERT INTO TABLE CustomerLogs 
PARTITION (log_date = '2025-09-20')
VALUES (1001, '192.168.1.1', 'LOGIN');
```

---

## Key Takeaways for Success
* **For 2-mark questions:** Provide a clear definition followed by two distinct, bulleted points or architectural roles.
* **For 7-mark query questions:** Include `IF NOT EXISTS`, declare correct datatypes, write explicit `ROW FORMAT DELIMITED FIELDS TERMINATED BY`, and distinguish whether `EXTERNAL` and `LOCATION` are required.
* **For 10-mark architectural questions:** Draw the component block diagram first, then follow up with a clear, step-by-step numbered breakdown of the interaction flow.
