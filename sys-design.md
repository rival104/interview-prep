- Be mindful of the common terminologies. Summarize types of consistency on a chart, load balancing strategies, rate limiting approaches, caching strategies etc. I have been caught off guard myself by this
Here is a quick list of examples:
    - Types of consistency: strong consistency, eventual consistency, causal consistency, and read-your-write consistency
    - Load balancing strategies: round-robin, least connections, IP hash, and consistent hashing
    - Rate limiting approaches: token bucket, leaky bucket, and fixed window counter
    - Caching strategies: write-through, write-around, write-back, and read-through

 # Caching:
 ### Type:
  - Write-through cache: both. avoid stale data and data inconsistency. but might put more load on the memory bus, filling the cache up with data that might not be accessed again.
  - Write-back cache: cache first.
### Eviction policies:
 - FIFO
 - LRU (Least Recently Used): LRU caching would be useful in popular tweet will be at top. But can become stale after some 
 - LFU (Least Frequently Used): it has limitations when applied to Twitter. For example, tweets from 2013 that have a large number of views might never be evicted due to their frequency, which would prevent new tweets from being stored. Consequently, LRU is a better model for Twitter.

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
