# 2025 Big Data Analytics and Computing - 25 Marks

**Course Code:** 20IC404T  

---

### Questions

#### 1. Answer the following: **[2 × 4 = 8 Marks]**
a) Define the role of the Combiner in a MapReduce job? State the phase after which it will be used?  
b) Why is checkpointing used in HDFS?  
c) How does HBase's data model differ from a traditional relational database? Give two main differences.  
d) What is the core principle of "Schema-on-Read" as used by Hive? How is it different from "Schema-on-Write"?  

---

#### 2.
Given a Hive external table `Book` with schema:  
`(book_id INT, title STRING, author STRING, price FLOAT)`  
and located at `'/user/hive/input/'`  
a) Write the Hive Query to create this table, specifying comma delimited text format. **(3 Marks)**  
b) Write the command to load data into it from the local file `'/home/cloudera/book_data.txt'` by overwriting the previous content. **(2 Marks)**  
c) Write a query to create a new managed table, `'ExpensiveBooks'`, containing all columns for books with a price greater than 100. **(2 Marks)** **[Total: 7 Marks]**

---

#### 3.
Explain the purpose of each core component of Hadoop YARN and the workflow? **[5 + 5 = 10 Marks]**

**OR**

Apache Hadoop HDFS is a distributed file system designed for storing very large data sets reliably and for streaming access to them across clusters of commodity hardware: **[10 Marks]**  
a) Explain the two main architectural components of HDFS and their primary responsibilities. **(4 Marks)**  
b) Describe the step-by-step process that occurs when a client application writes a new file (e.g., `data.txt`) into HDFS. Your answer should clearly explain the role of each component used in this process. **(4 Marks)**  
c) State one key advantage and one key limitation of using HDFS over a traditional local file system. **(2 Marks)**  

---
---
---
---
---

# 2024 Big Data Analytics and Computing - 50 Marks

**Course Code:** 20IC404T  

---

### Questions

#### Q.1
**1.** Big Data is often associated with the 'three Vs' (volume, velocity, variety). However, additional 'Vs' are often considered, such as veracity and value. Explain the significance of all 5 V’s in the context of Big Data Analytics. **[5 Marks]**

**2.** Draw and explain Hadoop ecosystem in detail. **[10 Marks]**  

**OR**

**2.** Draw and explain read and write operations performed in HDFS in Hadoop. **[10 Marks]**

---

#### Q.2
**1.** You are tasked with processing a massive dataset that is growing every minute. Would you choose Spark or Hadoop MapReduce for this task, and why? Justify your answer by discussing the trade-offs in terms of performance, fault tolerance, and ease of use. **[5 Marks]**

**2.** Discuss the importance of RDDs in Apache Spark. How do they enable parallelism in distributed computing? **[5 Marks]**

**3.** List and explain with example, any five transformation functions and action functions, available in Spark. **[5 Marks]**

**4.** Compare in detail Pig, SQL and Hive. **[5 Marks]**

---

#### Q.3
**1.** If `df.columns` has the fields: `['salary', 'age', 'experience', 'department', 'city']`  
Perform the following operations using PySpark SQL on this DataFrame: **[10 Marks]**  
a) Display the shape of the data.  
b) View only the columns `age` and `city`, and show 5 records.  
c) Add a new column in the DataFrame that stores the projected salary after 5 years.  
d) Fetch the records for employees working in the Finance department.  
e) View the distinct values for the column `department`.  

**2.** What is the output of the following Scala code, explain each step? **[5 Marks]**
```scala
val input = Seq(("Big", 1), ("Data", 3), ("big", 4), ("Big", 4), ("data", 2), ("data", 6))
val input2 = sc.parallelize(input)
val input3 = input2.reduceByKey((x, y) => x + y).collect
```

**OR**

**2.** Write a simple example of a MapReduce program to count the occurrences of each letter in a text file. **[5 Marks]**


