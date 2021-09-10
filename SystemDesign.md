## List of Concepts

1. Amount of data (disk)
2. Amount of RAM (memory)
3. Does everything need to be in RAM? (often times – yes)
4. RAID configurations
5. Requests/sec
6. Request time\Latency
Data transfer rates
Network limits within a single data center
Geographically separated locations (multiple data centers)
Sharding/Partitioning (by user/date/content-type/alphabetically)
How do you re-balance?
Consistent hashing for sharding/partitioning
CAP theorem
MapReduce
Distributed hash tables
Difference between frontend/backend
SOA (service oriented architectures, also “micro-services”)
Backups
Backup a single user on how many servers?
Caching
Many requests for the same data/lots of updates – should be in cache
Distribute so that the network is negligible
Parallelizing network requests
Fan-out (scatter and gather)
Load-balancing
High availability
CDNs (content delivery networks)
POPs (points of presence)
Queues
Failures
Timeouts
Fault tolerance
Failing fast
Circuit breakers
Throttling
Consensus (e.g. Paxos, Raft) and membership protocols (heartbeats, SWIM)
Compression
Possible to work harder on writes in order to make reads easier
Operations should almost never be more than n*log(n), preferably n