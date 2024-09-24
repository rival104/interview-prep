- Be mindful of the common terminologies. Summarize types of consistency on a chart, load balancing strategies, rate limiting approaches, caching strategies etc. I have been caught off guard myself by this
Here is a quick list of examples:
    - Types of consistency: strong consistency, eventual consistency, causal consistency, and read-your-write consistency
    - Load balancing strategies: round-robin, least connections, IP hash, and consistent hashing
    - Rate limiting approaches: token bucket, leaky bucket, and fixed window counter
    - Caching strategies: write-through, write-around, write-back, and read-through

# Things to Remember:
FARMS
 - Fault Tolerance
 - Availability
 - Realibilitiy
 - Maintainability
 - Scalability
# DB
## No-SQL
- BaSE (Eventual Consistency)
- PACELC Theorem (an extension of the CAP theorem)
  - "Given P (a network partition), choose A (availability) or C (consistency). Else, favor Latency or Consistency. (In replication, rudundancy)"
## SQL
- ACID
  - Atomicity
  - Consistency
  - Isolation
  - Durability
