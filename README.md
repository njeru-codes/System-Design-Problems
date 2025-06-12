# System-Design-Problems
A structured approach to solving system design problems during interviews or while architecting real-world systems.

## approach 
- STEP 1: Requirements clarifications
```
  **Functional requirements**: What should the system do? (e.g., “users can upload and view videos”)
  
  **Non-functional requirements**: Performance, availability, scalability, latency
  
  **Constraints**: Tech stack, team size, legacy systems
  
  **Out of scope**: Define what you’re not designing
```
- STEP 2: system interface definition
```
  APIs: What are the key API endpoints and their inputs/outputs?
  User flows: What are the major interactions?
  Protocols: REST, gRPC, WebSockets?
```
- STEP 3: back-of-the-envlope estimation
```
Estimate scale to understand the load on your system.
    Users: DAUs/MAUs
    Data Size: per user / per item
    Traffic: RPS (requests per second), bandwidth
    Storage: DB size, media files
    QPS: Read vs. Write ratio
📊 Helps guide storage, caching, sharding, and architecture decisions.
```
- STEP 4: defining data model
```
Design a minimal, scalable data schema.
Use normalized tables or NoSQL documents
Include indexes
Support for horizontal scaling if needed
```
- STEP 5: High level design
```
Describe the overall system architecture.
  - Clients ↔ API servers ↔ Databases
  - Include major components: load balancer, CDN, cache, pub/sub
  - Draw diagrams (optional in interviews, helpful in docs)
  - Think in terms of components, responsibilities, and data flow.
```
- STEP 6: Detailed design
```
Deep-dive into key components (1–3 max).
  - Caching layer (e.g., Redis, Memcached)
  - Database architecture (replication, sharding)
  - Queues for async jobs (e.g., RabbitMQ, Kafka)
  - Rate limiting, authentication
```
- STEP 7: Identifying and resolving bottlenecks
```
Identify weak points and suggest optimizations:
  - Traffic: Add load balancing
  - Latency: Use CDN or caching
  - Storage: Archive old data, use S3
  - Writes: Async processing with queues
  - DB: Partitioning or read replicas
Discuss trade-offs and alternatives (e.g., SQL vs. NoSQL, strong vs. eventual consistency).
```
- STEP 8: summary
```
Wrap it up clearly:
  - Recap the architecture
  - Highlight strengths: scalability, reliability, fault tolerance
  - Note trade-offs or areas for future improvement

Optionally suggest enhancements (analytics, monitoring)
```
