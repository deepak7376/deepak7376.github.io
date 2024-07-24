---
layout: post
title:  "System Design [HLD]"
date:   2019-01-20 00:04:58 +0530
categories: system-design
summary: Basics of System Design.
---
# Basics of System Design

## 1. What happens when you hit a URL in a browser
When you hit a URL in a browser, several processes occur to retrieve and display the webpage. Here's a simplified block diagram representing these steps:

1. **URL Entry**: The user enters a URL in the browser's address bar.
2. **DNS Lookup**: The browser contacts a DNS server to resolve the domain name to an IP address.
3. **TCP Connection**: The browser establishes a TCP connection with the web server using the IP address.
4. **HTTP Request**: The browser sends an HTTP request to the web server for the desired resource.
5. **Server Processing**: The web server processes the request and prepares an HTTP response.
6. **HTTP Response**: The server sends the HTTP response back to the browser.
7. **Rendering**: The browser renders the received content and displays it to the user.

Here’s a simple block diagram:

```
+---------+       +-----------+       +---------+       +--------+       +---------+       +---------+       +---------+       +---------+
|  User   |--->---|  Browser  |--->---|  DNS    |--->---|  IP    |--->---|  TCP    |--->---|  HTTP   |--->---|  Server  |--->---| Browser |
| Action  |       |           |       | Lookup  |       | Address|       | Conn.   |       | Request |       | Process  |       | Rendering |
+---------+       +-----------+       +---------+       +--------+       +---------+       +---------+       +---------+       +---------+
```

This diagram highlights the main components and interactions involved when a URL is hit in a browser.

---
## 2. Distributed Systems
### Characteristics of Distributed Systems
- Multiple independent components interact to achieve a common goal.
- Scalability, fault tolerance, and transparency.
- Examples include distributed databases, cloud computing, and microservices.

### CAP Theorem
- Consistency: Every read receives the most recent write.
- Availability: Every request receives a response, without guarantee of the most recent write.
- Partition Tolerance: The system continues to operate despite network partitions.
- A distributed system can only provide two out of the three guarantees simultaneously.

### Consensus Algorithms (Paxos, Raft)
- Ensure all nodes in a distributed system agree on a single value or state.
- Paxos: A protocol for achieving consensus despite failures.
- Raft: Easier to understand and implement compared to Paxos, used for leader election and log replication.

### Fault Tolerance and Replication
- Fault tolerance: The ability to continue operating despite failures.
- Replication: Storing copies of data on multiple nodes to ensure availability and reliability.
- Techniques include active-passive and active-active replication.

---

## 3. Microservices
### Microservice Architecture for E-commerce Application

```
+--------+        +--------------+        +------------------+
| Client |<----->|  API Gateway  |<----->| Aggregation Svc   |
+--------+        +--------------+        +------------------+
                                         /        |         \
                                +---------------+ | +---------------+
                                | User Service   | | | Product Service |
                                | User Database  | | | Product Database|
                                +---------------+ | +---------------+
                                | Order Service  | | | Payment Service |
                                | Order Database | | | Payment Database|
                                +---------------+ | +---------------+
                                | Inventory Svc  | | 
                                | Inventory DB   | | 
                                +---------------+ | 
                                | Message Broker  |
                                +-----------------+
```

### Explanation

1. **Client**: Sends requests to the API Gateway.
2. **API Gateway**: Routes requests to the Aggregation Service for requests that require data from multiple microservices.
3. **Aggregation Service**: 
   - **User Service**: Fetches user-related data and interacts with the User Database.
   - **Product Service**: Retrieves product information from the Product Database.
   - **Order Service**: Gathers order details from the Order Database.
   - **Payment Service**: Obtains payment status from the Payment Database.
   - **Inventory Service**: Checks inventory levels in the Inventory Database.
4. **Aggregation Service**: Combines data from the above services to provide a unified response.
5. **Message Broker**: Ensures asynchronous communication between services as needed.

### Use Cases for Aggregation Service

1. **User Dashboard**: Combines user profile, recent orders, and payment status.
2. **Product Details Page**: Aggregates product information, inventory status, and user reviews.
3. **Order Summary**: Gathers order details, payment status, and shipment tracking.

By using an Aggregation Service, the system simplifies complex data retrieval processes for the client, reduces the number of client-server interactions, and improves overall system performance.

---
## 4. Data Partitioning
### Horizontal vs Vertical Partitioning
- Horizontal Partitioning: Dividing data across different nodes (sharding).
- Vertical Partitioning: Splitting a table into columns and storing them in separate databases.

### Sharding
- Distributing data across multiple databases to improve performance and scalability.
- Each shard contains a subset of the data.

### Partitioning Strategies (Range, Hash, List, Composite)
- Range Partitioning: Dividing data based on value ranges.
- Hash Partitioning: Using a hash function to determine the partition.
- List Partitioning: Dividing data based on predefined lists.
- Composite Partitioning: Combining multiple partitioning methods.

---
## 5. Caching
### Caching Strategies (Write-through, Write-back, Write-around)
- Write-through: Data is written to both the cache and the underlying storage.
- Write-back: Data is written to the cache and later synchronized with the storage.
- Write-around: Data is written directly to the storage, bypassing the cache.

### Cache Eviction Policies (LRU, LFU, FIFO)
- LRU (Least Recently Used): Evicts the least recently accessed items.
- LFU (Least Frequently Used): Evicts the least frequently accessed items.
- FIFO (First In, First Out): Evicts the oldest items first.

### Distributed Caches (Redis, Memcached)
- Redis: In-memory data structure store, supports complex data types, persistence, and replication.
- Memcached: High-performance distributed memory caching system, simple key-value store.

---
## 6. SQL vs NoSQL
### Relational vs Non-relational Databases
- SQL (Relational): Structured data, predefined schema, ACID properties.
- NoSQL (Non-relational): Flexible schema, horizontal scalability, BASE properties.

### ACID vs BASE Properties
- ACID: Atomicity, Consistency, Isolation, Durability.
- BASE: Basically Available, Soft state, Eventual consistency.

### Use Cases and Examples
- SQL: Financial systems, ERP, CRM.
- NoSQL: Social media, real-time analytics, IoT applications.

---
## 7. Consistent Hashing
### How Consistent Hashing Works
- Distributes data across nodes in a way that minimizes reorganization when nodes are added or removed.
- Uses a hash function to map data to a circular space and assigns nodes to points on the circle.

### Use Cases in Distributed Systems
- Load balancing, distributed caching, sharding.

### Virtual Nodes
- Nodes are assigned multiple positions on the hash ring to improve load distribution and fault tolerance.

---
## 8. Sync vs Async
### Synchronous and Asynchronous Processing
- Synchronous: Operations are performed sequentially, blocking until completion.
- Asynchronous: Operations can be performed concurrently, allowing for non-blocking execution.

### Blocking vs Non-blocking I/O
- Blocking I/O: Waits for the operation to complete before continuing.
- Non-blocking I/O: Allows other operations to proceed while waiting.

### Use Cases and Trade-offs
- Synchronous: Simplicity, predictable behavior.
- Asynchronous: Higher performance, better resource utilization.

---
## 9. Resilience and Fallback
### Circuit Breaker Pattern
- Prevents repeated failures by stopping requests to a failing service.
- Opens the circuit after a threshold of failures, and retries after a timeout.

### Retries and Exponential Backoff
- Retries: Automatically retry failed operations.
- Exponential Backoff: Gradually increase the wait time between retries.

### Bulkhead Pattern
- Isolates different parts of a system to prevent failures from spreading.
- Ensures that failures in one component do not affect others.

---------
# System Design Questions

## 10. Design URL Shortening Service (Tiny URL)

#### Requirements

**Functional Requirements**:
1. Users can generate short links from the given URL.
2. Redirect to the original URL when clicking on the short link.
3. Users can generate custom short links.
4. Expiration of links after some duration.

**Non-Functional Requirements**:
1. The system should be highly available because if the service is down, all links become dead.
2. Generated links should not be easily guessable.
3. Redirection should take less time (low latency).

#### Capacity Estimation and Constraints

**Traffic Estimate**:
- Assume a 100:1 read-write ratio for a read-heavy system.
- 500 million new URLs added per month.
- 500 million * 100 = 50 billion redirections per month.

**Queries Per Second (QPS)**:
- Write: 500 million / (30 days * 24 hours * 3600 seconds) ≈ 200 writes per second.
- Read: 200 * 100 = 20,000 reads per second.

**Storage (Assume for 5 years)**:
- 200 writes per second * 1KB per URL * 5 years * 365 days * 24 hours * 3600 seconds ≈ 30 TB.

**Bandwidth**:
- Downlink: 200 writes per second * 1KB = 200KB per second.
- Uplink: 200KB * 100 = 20MB per second.

**Memory Estimate**:
- Follow the 80-20 rule: 20% of URLs generate 80% of traffic.
- 500 million writes per month.
- 20,000 requests per second * 24 hours * 3600 seconds = 1.7 billion requests per day.
- 20% of 1.7 billion requests need ≈ 170GB of memory.

#### Algorithm

**Short URL Generation**:
1. Generate a unique short URL using a hashing algorithm.
2. Check for collisions:
   - If a collision occurs, append additional characters or rehash.
3. Store the original URL and short URL in the database.

**Redirection**:
1. When a short URL is accessed, query the database for the original URL.
2. Increment the access count.
3. Redirect to the original URL.

**Expiration Handling**:
1. Store the creation timestamp of each short URL.
2. Periodically check for expired URLs and remove them from the database.

**Handling Custom URLs**:
1. Allow users to specify a custom short URL.
2. Check for availability of the custom URL before storing.

---

## 11. Design Instagram Timeline
- Requirements and constraints
- Data modeling
- Feed generation strategies
- Handling real-time updates

## 12. Design Dropbox
- Requirements and constraints
- File storage and synchronization
- Data deduplication
- Minimizing data transfer

## 13. Design Flash Sale System
- Requirements and constraints
- Load balancing
- Inventory management
- Handling sudden load increases

## 14. Design YouTube/Netflix
- Requirements and constraints
- Video storage and encoding
- Chunking and streaming
- Content Delivery Network (CDN) usage

## 15. Design API Rate Limiter
- Requirements and constraints
- Rate limiting algorithms (token bucket, leaky bucket)
- Distributed rate limiting

## 16. Design Typeahead Suggestion
- Requirements and constraints
- Data structures (Trie, Ternary Search Tree)
- Handling large datasets
- Ranking and relevance

## 17. Design Web Crawler
- Requirements and constraints
- URL frontier management
- Politeness policies
- Distributed crawling

## 18. Design Nearby Search
- Requirements and constraints
- Geospatial indexing (R-tree, Quad-tree)
- Efficient querying
- Handling large datasets

## 19. Design Uber-like System
- Requirements and constraints
- Real-time location tracking
- Matching algorithms
- Surge pricing

## 20. Design Payment Service
- Requirements and constraints
- Payment gateways
- Security and fraud detection
- Handling concurrency and idempotency

## 21. Design WhatsApp
- Requirements and constraints
- Real-time messaging
- Data storage and synchronization
- End-to-end encryption

## 22. Design Scalable Notification System
- Requirements and constraints
- Notification delivery mechanisms (push, SMS, email)
- Handling millions of notifications within a short time
- Ensuring reliability and scalability

## 23. Design Event Pipeline
- Requirements and constraints
- Event sourcing
- Stream processing frameworks (Kafka, Flink)
- Ensuring data integrity and consistency

## 24. Design Scalable Logging Framework
- Requirements and constraints
- Log collection and aggregation
- Storage and retrieval
- Real-time log analysis

## 25. Design Swiggy-like Hyperlocal Search
- Requirements and constraints
- Efficient search algorithms
- Handling dynamic data
- Real-time updates