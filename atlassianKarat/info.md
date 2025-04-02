# Music Streaming / Consistent Hashing

## Issues & Solutions
### 1. Uneven Load Distribution  
- **Solution**: Use **virtual nodes** so that a single physical server is responsible for multiple partitions.

### 2. Load on Central Load Balancer  
- **Solution**: Use **distributed load balancing**, such as **DNS-based Load Balancing** to distribute traffic across multiple regional balancers.

### 3. Server Failures  
- **Solution**: Use **replication** to ensure fault tolerance.

---

# Crosswords / Online-Offline App

## Access Hints from Server  

### **Pros**:
1. Dynamic
2. Learn about user behavior based on accessed hints
3. Requires less storage on the client side

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

4. **Using `ElementTree.iterparse()`**:  
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
6. Plan for **traffic surges and scalability**.

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
   - Ensure **fault**
