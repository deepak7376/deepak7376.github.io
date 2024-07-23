---
layout: post
title:  "System Design [HLD]"
date:   2019-01-20 00:04:58 +0530
categories: system-design
summary: Basics of System Design.
---
# Basics of System Design

## 1. What happens when you hit a URL in a browser
### DNS Resolution
- Converts the human-readable domain name (e.g., www.example.com) into an IP address.
- Uses a hierarchical structure: Root DNS, TLD DNS (Top-Level Domain), and Authoritative DNS servers.
- The browser caches DNS responses to reduce latency on subsequent requests.

### TCP/IP Connection
- Establishes a connection between the client and server using the Transmission Control Protocol (TCP).
- The three-way handshake process: SYN, SYN-ACK, ACK.
- Ensures reliable communication and data integrity.

### HTTP Request/Response Cycle
- The browser sends an HTTP request to the server, specifying the URL and method (GET, POST, etc.).
- The server processes the request and returns an HTTP response with a status code, headers, and optionally a body (e.g., HTML, JSON).
- The browser interprets the response and renders the content.

### Rendering the Page
- The browser parses the HTML, CSS, and JavaScript.
- Constructs the DOM (Document Object Model) and CSSOM (CSS Object Model).
- Executes JavaScript, which may modify the DOM and CSSOM.
- Paints the final visual representation on the screen.

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

## 3. Microservices
### Advantages and Disadvantages
- Advantages: Scalability, flexibility, independent deployment, technology diversity.
- Disadvantages: Increased complexity, network latency, data consistency challenges.

### Service Discovery
- Mechanism for services to find and communicate with each other.
- Uses service registries (e.g., Consul, Eureka) and service discovery protocols (e.g., DNS-based, HTTP-based).

### Inter-service Communication (REST, gRPC, Message Queues)
- REST: Simple, stateless communication using HTTP.
- gRPC: High-performance RPC framework using Protocol Buffers.
- Message Queues: Asynchronous communication using brokers (e.g., RabbitMQ, Kafka).

### Service Orchestration and Choreography
- Orchestration: Centralized control over service interactions, often using an orchestrator (e.g., Kubernetes).
- Choreography: Decentralized interaction where services react to events.

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

## 7. Consistent Hashing
### How Consistent Hashing Works
- Distributes data across nodes in a way that minimizes reorganization when nodes are added or removed.
- Uses a hash function to map data to a circular space and assigns nodes to points on the circle.

### Use Cases in Distributed Systems
- Load balancing, distributed caching, sharding.

### Virtual Nodes
- Nodes are assigned multiple positions on the hash ring to improve load distribution and fault tolerance.

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

## 10. Design URL Shortening Service
- Requirements and constraints
- Database schema
- API design
- Handling collisions

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