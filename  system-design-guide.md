# SYSTEM DESIGN – COMPLETE GUIDE

## 1. Introduction to System Design

System Design is the process of defining how a system works, scales, and meets requirements. It involves planning the **architecture**, **components**, data flow, and trade-offs to build reliable, scalable, and maintainable systems.

**Types:**

* **High-Level Design (HLD):** Focuses on architecture, components, modules, and data flow.
* **Low-Level Design (LLD):** Focuses on classes, APIs, database schemas, and detailed algorithms.

**Key Questions in System Design:**

* What problem does the system solve?
* What scale do we expect (users, requests, data)?
* What are the bottlenecks and failure points?

---

## 2. Key Concepts

### A. Scalability

The ability to handle growth in traffic and data.

* **Vertical Scaling:** Adding CPU or RAM to a single server. It's easy but has limited capacity.
* **Horizontal Scaling:** Adding more servers or nodes. This is the **preferred method for large systems**.

### B. Load Balancing

Distributes traffic across multiple servers to prevent any one server from being overloaded.

* **Types:** Round Robin, Least Connections, and IP Hash.
* **Tools:** Nginx, HAProxy, and AWS ELB.

### C. Caching

Temporarily stores frequently accessed data for fast retrieval, reducing latency and database load.

* **Tools:** Redis, Memcached.
* **Types:** Client-side, server-side, and CDN cache.
* **Eviction Policies:** Least Recently Used (LRU), Least Frequently Used (LFU).

### D. Database Design

Choosing the right database type is crucial for system performance.

* **Relational (SQL):** Provides **ACID** properties (Atomicity, Consistency, Isolation, Durability) and structured queries (e.g., PostgreSQL, MySQL).
* **NoSQL:** Offers a flexible schema and **high scalability** (e.g., MongoDB, Cassandra).
* **Sharding:** Splits data across multiple databases.
* **Replication:** Copies data for **high availability** and read scalability.

### E. Indexing

Creates a data structure that speeds up database queries. The trade-off is **faster reads versus slower writes**.

### F. Message Queues / Async Processing

Used for tasks that don't require an instant response (e.g., notifications, video processing). This decouples services and improves responsiveness.

* **Tools:** Kafka, RabbitMQ, and AWS SQS.

### G. Consistency vs. Availability (CAP Theorem)

In a distributed system, you can only pick two of the three properties:

* **Consistency:** Every read returns the latest write.
* **Availability:** Every request receives a response.
* **Partition Tolerance:** The system continues to work even if network partitions occur.

---

## 3. Core Components of a System

| Component | Role | Examples |
| :--- | :--- | :--- |
| **API Layer** | Handles client requests. | REST, GraphQL, gRPC |
| **Load Balancer** | Distributes traffic. | Nginx, HAProxy, AWS ELB |
| **Web/App Server** | Manages business logic. | Node.js, Spring Boot |
| **Database** | Stores persistent data. | SQL, NoSQL |
| **Cache** | Enables fast data access. | Redis, Memcached |
| **Message Queue** | Processes asynchronous tasks. | Kafka, RabbitMQ |
| **CDN** | Serves static content. | CloudFront, Akamai |
| **Monitoring & Logging** | Observes and debugs system behavior. | Prometheus, Grafana |
| **Security** | Protects the system. | OAuth, JWT, HTTPS |

---

## 4. Architecture Patterns

* **Monolithic:** A single codebase; simple to start with but **hard to scale**.
* **Microservices:** Independent, small services; **scalable** but complex to manage.
* **Event-Driven:** Asynchronous communication via events, leading to **decoupled** services.
* **CQRS:** Separates read and write models, optimizing for high read/write workloads.
* **Leader-Follower / Master-Slave:** A replication pattern for database failover.
* **API Gateway / Proxy:** Routes traffic, handles authentication, and performs rate limiting.

---

## 5. Database Concepts

| Type | Pros | Cons | Use Cases |
| :--- | :--- | :--- | :--- |
| **SQL** | ACID, strong consistency. | Hard to scale horizontally. | Transactions, e-commerce. |
| **NoSQL** | Scalable, flexible schema. | Eventual consistency. | Social media, analytics. |
| **Key-Value** | Very fast. | Limited query functionality. | Sessions, caching. |
| **Time-Series** | Optimized for timestamps. | Specialized use cases. | Metrics, logs. |
| **Blob Storage** | Stores large, unstructured files. | Not queryable. | Videos, images. |

**Other Important DB Concepts:**

* **Sharding:** Horizontal partitioning.
* **Replication:** High availability and fault tolerance.
* **Indexing:** Speeds up queries.
* **Partitioning:** Dividing data by key or range.

---

## 6. Caching & CDN

* **Cache:** Reduces **latency** and database load by storing data in memory.
* **CDN (Content Delivery Network):** Caches **static assets** (e.g., images, JavaScript files) closer to users globally to reduce latency.
* **Eviction Policies:** Algorithms like LRU and LFU manage what data to remove when the cache is full.
* **Trade-offs:** You must balance **data freshness** with the cost of storage.

---

## 7. Message Queues

Message queues facilitate **asynchronous task processing** and decouple services.

* **Guarantees:** Can provide guarantees like **at-least-once** or **exactly-once** delivery.
* **Tools:** Kafka, RabbitMQ, and AWS SQS.
* **Use Cases:** Sending notifications, generating social media feeds, and video transcoding.

---

## 8. Scaling & Load Management

* **Vertical Scaling:** Increasing resources on a single server.
* **Horizontal Scaling:** Adding more servers, which is ideal for **stateless services**.
* **Load Balancing:** Distributes incoming traffic across servers.
* **Bottlenecks:** Common choke points include the database, network, CPU, or a single server.

---

## 9. CAP Theorem & Trade-offs

| Acronym | Definition |
| :--- | :--- |
| **Consistency** | All reads return the most recent write. |
| **Availability** | All requests receive a non-error response. |
| **Partition Tolerance** | The system remains operational despite network failures. |

Systems can only achieve **two of the three** at once. For example, a traditional SQL database is often **CP**, while a system like DynamoDB is typically **AP**.

---

## 10. Common Interview Problems

| System | Key Points | Patterns / Tools |
| :--- | :--- | :--- |
| **URL Shortener** | High read traffic, short code generation. | SQL/NoSQL, Redis, Load Balancer. |
| **Social Media Feed** | Pull vs. Push models, high read loads. | Microservices, Message Queues, Cache. |
| **Messaging App** | Real-time delivery, offline support. | WebSocket, Message Queues, NoSQL. |
| **E-commerce** | Transactions, catalog, search. | SQL/NoSQL, Cache, Message Queues. |
| **Video Streaming** | Uploads, CDN, transcoding. | Blob Storage, CDN, Async Processing. |

---

## 11. Step-by-Step System Design Approach

1.  **Clarify requirements** and constraints.
2.  **Estimate scale** (e.g., users, requests, data).
3.  Design the **high-level architecture**.
4.  Define **APIs** and data flow.
5.  Identify **bottlenecks** and scaling strategies.
6.  Dive into database and caching strategies.
7.  Discuss **trade-offs** and alternatives.
8.  Consider security, monitoring, and logging.

---

## 12. System Design Trade-offs to Remember

* **SQL vs. NoSQL**
* **Monolith vs. Microservices**
* **Push vs. Pull** feed generation
* **Cache freshness vs. storage cost**
* **Vertical vs. Horizontal** scaling
* **Eventual consistency vs. strong consistency**

---

## COMMON SYSTEM DESIGN INTERVIEW PROBLEMS

### 1. URL Shortener (like bit.ly)

**Requirements:**
* Convert long URLs to short codes.
* Redirect users to the original URL.
* Track click analytics (optional).

**Key Design Points:**
* **Short Code Generation:** Use a hashing algorithm or Base62 encoding.
* **Database:** A simple SQL or NoSQL table to map `short_code` to `long_url`.
* **Caching:** Store popular redirects in a cache like Redis.
* **Scaling:** The system is **read-heavy**, so use replication and caching extensively.

### 2. Social Media Feed (like Twitter)

**Requirements:**
* Show recent posts from users you follow.
* Support likes, comments, and posts.
* Load the feed quickly.

**Key Design Points:**
* **Pull vs. Push Model:** For large-scale systems, a **push model** (pre-computing feeds for followers) is often used for a fast user experience, while a **pull model** is simpler.
* **Microservices:** Separate services for users, posts, and feeds.
* **Caching:** Cache pre-computed feeds in Redis for fast retrieval.
* **Database:** Use database **sharding by `user_id`** to distribute data.

### 3. Messaging System (like WhatsApp / Messenger)

**Requirements:**
* Real-time message delivery.
* Offline support.
* Maintain message order.

**Key Design Points:**
* **Real-time Communication:** Use **WebSocket** or MQTT for low-latency, persistent connections.
* **Asynchronous Delivery:** A **message queue** (e.g., Kafka) handles message delivery and ordering.
* **Database:** A NoSQL database is ideal for storing messages due to its scalability and flexible schema.
* **Retry Logic:** A mechanism to deliver messages to users when they come back online.

### 4. E-commerce Platform (like Amazon)

**Requirements:**
* Product catalog and search.
* Shopping cart and checkout.
* Payment processing.
* High availability.

**Key Design Points:**
* **Database:** Use a **SQL database** for transactional integrity (**ACID**) for payments and orders. Use a **NoSQL database** for a scalable product catalog.
* **Microservices:** Separate services for Catalog, Cart, Checkout, and Payment.
* **Caching:** Cache popular products and search results in Redis.
* **Async Processing:** Use a **message queue** for order processing to decouple services.

### 5. Video Streaming Platform (like YouTube / Netflix)

**Requirements:**
* Upload and stream videos.
* Adaptive bitrate streaming.
* High availability and low latency.

**Key Design Points:**
* **Storage:** Use distributed **blob storage** (e.g., AWS S3) to store video files.
* **CDN:** A **Content Delivery Network** is essential to deliver video segments closer to users.
* **Async Transcoding:** Use a message queue to trigger asynchronous services that transcode uploaded videos into multiple formats and bitrates.
* **Database:** A metadata database (SQL/NoSQL) stores information about videos (e.g., title, views, likes).

---

## **Key Visual Elements Across All Systems**

| Element | Purpose |
| :--- | :--- |
| **API Layer** | Handles client requests and validation. |
| **DB Layer** | Provides persistent storage (SQL/NoSQL). |
| **Cache** | Enables fast data retrieval and reduces database load. |
| **Message Queue** | Handles asynchronous tasks and decouples services. |
| **Load Balancer** | Distributes traffic across multiple servers. |
| **CDN** | Delivers static content closer to users globally. |
| **Microservices** | Provides a modular, independently scalable architecture. |