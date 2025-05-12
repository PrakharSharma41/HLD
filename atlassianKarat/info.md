# Index  

- [Music Streaming / Consistent Hashing](#music-streaming--consistent-hashing)
  - [Issues & Solutions](#issues--solutions)
    - [Uneven Load Distribution](#1-uneven-load-distribution)
    - [Load on Central Load Balancer](#2-load-on-central-load-balancer)
    - [Server Failures](#3-server-failures)
- [Crosswords / Online-Offline App](#crosswords--online-offline-app)
  - [Access Hints from Server](#access-hints-from-server)
  - [Preloaded Hints in the App](#preloaded-hints-in-the-app)
- [XML File Processing](#xml-file-processing)
  - [Techniques for Handling Large XML Files](#techniques-for-handling-large-xml-files)
- [Sports App / Budget Planning for 6 Months](#sports-app--budget-planning-for-6-months)
- [Scaling a Social Network for International Traffic](#scaling-a-social-network-for-international-traffic)
- [Budget Estimation for System Planning](#budget-estimation-for-system-planning)
- [Porting Code to Embedded Systems](#porting-code-to-embedded-systems)
- [System Slowness Troubleshooting](#system-slowness-troubleshooting)
- [Design: Read-Heavy System](#design-read-heavy-system)
- [Design: Write-Heavy System](#design-write-heavy-system)
- [Design: idempotent apis](#Design-idempotent-apis)
- [Round robin approach in google docs](#Round-robin-approach-in-google-docs)
- [strong consistency for banking applications](#strong-consistency-for-banking-applications)
- [Budgeting for a smart engine service](#Budgeting-for-a-smart-engine-service)
- [Find missing notifications list](#Find-missing-notifications-list)
- [Throughput question](#Throughput-question)
- [use strong consistency or eventual consistency](#use-strong-consistency-or-eventual-consistency)
- [post with friends counter, define schema](#post-with-friends-counter,-define-schema)
# Music Streaming / Consistent Hashing

## Issues & Solutions
### 1. Uneven Load Distribution / Data Skew & Hot Keys 
- **Solution**: Use **virtual nodes** so that a single physical server is responsible for multiple partitions.

### 2. Load on Central Load Balancer / Latency and Proximity Issues  
- **Solution**: Use **distributed load balancing**, such as **DNS-based Load Balancing** to distribute traffic across multiple regional balancers.

### 3. Server Failures  
- **Solution**: Use **replication** to ensure fault tolerance.
### 4. Cache Invalidation During Rebalancing
- **Solution**: When nodes are added or removed from the cluster, consistent hashing minimizes rebalancing, but a small percentage of keys must still be reassigned. , use virtual nodes

---

# Crosswords / Online-Offline App

## Access Hints from Server  

### **Pros**:
1. Dynamic
2. Better security and control over hints. Premium hints stay on the server reducing the risk of reverse engineering
3. Requires less storage on the client side
4. Lower initial app load time

### **Cons**:
1. Slower due to network latency
2. Requires internet connectivity
3. Higher operational cost

## Preloaded Hints in the App  

### **Pros**:
1. Faster access
2. Works offline
3. Lower operational cost

### **Cons**:
1. May not be useful if the user needs additional hints
2. Requires more local storage

---

# XML File Processing  

### **Techniques for Handling Large XML Files**:
1. **Streaming (SAX Parser)**:  
   - Keeps only a small portion in memory.
   - Best for processing large XML sequentially with minimal memory usage.
   
2. **Chunk-Based Processing**:  
   - Split into chunks based on key tags and process in parallel.

3. **Incremental Parsing & DB Storage**:  
   - Parse XML in chunks and store in a database.
   - Suitable for scenarios requiring later aggregations.

4. **Using python `ElementTree.iterparse()`**:  
   - Processes XML incrementally and frees up memory after each element.

---

# Sports App / Budget Planning for 6 Months  

### **Factors to Consider**:
1. Number of users
2. Number of articles
3. Article size
4. Average server usage per article
5. Cost per article
6. Processing time per link
7. Server types (CPU, GPU, etc.)
8. Resource scaling for traffic spikes
9. Licensing and miscellaneous costs

---

# Scaling a Social Network for International Traffic  

### **Key Scaling Strategies**:
1. Deploy backend services across **global regions**.
2. Use **geo-spatial load balancers**.
3. Implement **CDN** for static content.
4. Manage **data compliance for different countries**.
5. Support **multi-language content storage**.
6. Plan for **traffic surges and scalability**. Prepare for spikes in user activity across time zones with cloud auto-scaling and regionally deployed servers.

---

# Budget Estimation for System Planning  

### **Cost Considerations**:
1. Storage costs for 6 months
2. Average server costs
3. Traffic surge handling requirements
4. Developer hiring costs
5. Marketing and licensing costs

---

# Porting Code to Embedded Systems  

### **Challenges & Considerations**:
1. **Hardware Limitations** – Raspberry Pi has limited memory compared to a full-fledged computer.
2. **Software Compatibility** – OS differences (Linux vs Raspberry Pi OS).
3. **Language Efficiency** – High-level languages (Python, Java) may perform differently.
4. **Power Supply** – Ensure stable power consumption.
5. **Communication with External Systems** – Protocol compatibility.
6. **Overall Cost Impact** – Maintenance & production costs.

---

# System Slowness Troubleshooting  

### **Performance Optimization Techniques**:
1. Use **APM tools** (New Relic, Datadog, Prometheus) to analyze API latencies.
2. Check **infrastructure metrics** (CPU, Memory, Disk I/O).
3. Scale by **increasing the number of servers**.
4. Distribute load using **consistent hashing**.
5. Use **geo-spatial load balancing** for regional requests.
6. Implement **caching for API calls**.
7. Use **CDN for static resources**.
8. Use **read replicas for database queries**.

---

# Design: Read-Heavy System  

### **Key Considerations**:
1. **Read QPS (Queries Per Second)**  
2. **Consistency vs. Availability Trade-offs**  
3. **Latency Tolerance**  
4. **Optimized Database Selection**:
   - Read replicas to distribute queries.
   - Elasticsearch for full-text search.
   - Cassandra/DynamoDB for fast, distributed reads.

5. **Scaling Reads**:
   - **Leader-Follower Replication** (for consistency)
   - **Multi-Leader Replication** (for global distribution)
   - **Quorum-Based Reads** (balance between consistency & availability)

6. **Caching Strategies**:
   - CDN, application-level caching, query caching

7. **Index Optimization**:
   - B+ Tree Indexes
   - Hash Indexes (Redis, DynamoDB)
   - Composite Indexing

8. **Load Balancing for Scalability**  
9. **Performance Monitoring & Optimization**  

---

# Design: Write-Heavy System  

### **Core Design Choices**:
1. Write QPS (Queries Per Second)
2. Consistency vs. Availability Trade-offs
3. Latency Tolerance
4. **Storage Strategy**:
   - Cassandra, RocksDB, LevelDB, ScyllaDB, DynamoDB
   - Use **batched writes** in memory before flushing to disk.

5. **Write Buffering**:
   - Kafka, Apache Pulsar, Redis Streams

6. **Horizontal Scaling**:
   - Use **consistent hashing (virtual nodes)** to balance writes.

7. **Write-Optimized Caching**:
   - **Write-back cache** (async flush to DB).

8. **Durability & Replication**:
   - Ensure **fault tolerance** with proper replication strategies.


---
# Design: idempotent apis 
1. Assign a Unique Idempotency Key
2. Use Safe HTTP Methods: GET, HEAD, OPTIONS, DELETE are naturally idempotent
3. Handle Retries Gracefully: If a request is processed once, return the same result on retries.
4. Use a Strong Database Consistency Model: Use unique constraints
5. Implement Distributed Locks: Prevent race conditions when multiple requests update the same resource


---
# Round robin approach in google docs
1. Real-Time Collaboration Latency: Round Robin assigns user requests to different servers without considering ongoing  editing sessions.
    If two users editing the same document are assigned to different backend instances, their edits must sync frequently across servers, increasing latency and conflicts.
2. If different users editing the same document are handled by different backend instances, synchronizing changes across servers becomes complex and costly.
3. Load Imbalance for Active Documents: Some documents are edited by hundreds or thousands of users simultaneously, while others have just one or two.
4. Inefficient Resource Utilization: Round Robin might route a lightweight read request and a heavy collaborative edit session to different instances indiscriminately.
5. With Round Robin, subsequent requests from the same user (or document) may go to different servers leading to inconsistencies in their editing experience.

---
# strong consistency for banking applications
1. Prevents Double Spending
2. Ensures Accurate Balances
3. Compliance & Regulatory Requirements: These regulations require accurate record-keeping, transaction integrity, and auditable histories.
4. Avoids Race Conditions in Multi-Node Environments: Strong consistency ensures all nodes see the latest transaction history, eliminating race conditions.


---
# Budgeting for a smart engine service
1. Data Requirements & Format — What type of data needs extraction
2. how many urls will we get
3. types of servers we may need to process
4. storage for the data 
5. average cost per url
6. resource scaling
7. Security & Compliance — Is encryption required? 

---
# Find missing notifications list
you have successful notifications stored 
We have two pieces of information:
1. A database that tracks fully signed documents.
2. Flat-file logs from 500 production servers. The logs track the document IDs for successfully sent notifications, but failed attempts are missing.

Solution:

1. Extract Document IDs from Database: Get all document IDs that are fully signed.

2. Parse Logs in Parallel: From the 500 servers, extract document IDs with successful notifications using a distributed processing system (e.g., Hadoop, Spark, or a cloud-native map-reduce framework).

3. Compute Set Difference:
3.1. Let A be the set of fully signed document IDs.
3.2. Let B be the set of document IDs with successful notifications from logs.
3.3. Missed = A - B (documents that never triggered notifications).

4. Store and Act:
4.1. Store Missed in a scalable key-value store or message queue.
4.2. Re-trigger notifications for each missed document ID.


---
# Throughput question
   A(50)      
      |         
     B(30)     
      |         
     C(30)     
     /   \     
  D(90)  E(10)  
          |    
         F(20) 
          |    
         G(25) 
find maximum throughput
how will you improve throughput if you are given information about each stage

---

# use strong consistency or eventual consistency
1. banking application SC
2. page click counter EC
3. api that need to return in 20ms EC

# post with friends counter, define schema
given users table and friends table
how will you find friends counter:
1. use separate friends counter table
2. do join between user and friend counter table


# We are working on a service that generates subtitles for users' videos. This process starts a new thread per video and is processor-intensive. Currently, this service runs as a single process on a machine.

We've run into a bug where if the service is processing more than 10 videos at the same time, the server crashes, losing all requests currently being processed and affecting other processes on the machine.

It may take a long time to find and fix this bug. What workarounds could we implement to continue running while we do so?
1. Introduce a Queue/Job Dispatcher
2. Rate Limiting and Backpressure
3. Horizontal Scaling with Load Balancer
4. Circuit Breaker Pattern
5. Persist Requests for Retry

---

# You're working on infrastructure for internet-connected vending machines. The plan is to install around 100,000 of these vending machines in the coming year, in major cities around the world. These machines will connect to the internet through cellular devices.

Each machine will connect to a central server at midnight to report remaining stock and any maintenance issues like jams or stuck items. These machine status updates will be stored in a database, and a batch job will run at 3am to schedule the restocking and maintenance of machines.

Are there any problems with the above design?
1. Thundering Herd Problem (Midnight Spike)
2. Global Time Zone Handling
3. Cellular Connectivity Failures
4. Batch Job as Single Point of Failure
5. Scalability of the Central Server & Database


---

# We are running a simple photo storage and sharing service. People upload their photos to our service and then optionally send links to other users who can then view them.

Instead of using a cloud service, we have our own datacenters. You've been tasked with creating an estimate of the storage required over the coming year and the cost of that storage. What information would you need and what factors would you consider as you generate this estimate?

1. User Growth Estimates
2. Upload Patterns, average photo per user per duration of time
3. Retention Policy: Are photos stored indefinitely?
4. Sharing Behavior
5. Redundancy/Replication
6. Storage Architecture: filesystem, object storage etc
7. Hardware Details: Cost per TB of storage


---

# We are running a simple photo storage and sharing service. People upload their photos to our servers and then give links to other users who can then view them.

I’m trying to figure out how to split the photos and associated data evenly onto multiple machines, especially as the number of users rises. I’ve decided to shard the photos evenly alphabetically by username. For example, if we had 26 users:

A–I usernames storing with 1,
J–R with server 2,
S–Z with server 3, etc.
I have created a scheme like this that will work for any number of servers.
Are there any problems with this design?

1. Uneven Load Distribution (Skew)
2. Lack of Scalability
3. Hotspots
4. No Fault Tolerance Mentioned
5. Poor Flexibility for Horizontal Scaling


---
