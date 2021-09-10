## Template




## List of Concepts

1. Amount of data (disk)
2. Amount of RAM (memory)
3. Does everything need to be in RAM? (often times – yes)
4. RAID configurations
5. Requests/sec
6. Request time
7. Latency
8. Data transfer rates
9. Network limits within a single data center
10. Geographically separated locations (multiple data centers)
11. Sharding/Partitioning (by user/date/content-type/alphabetically)
12. How do you re-balance?
13. Consistent hashing for sharding/partitioning
14. CAP theorem
15. MapReduce
16. Distributed hash tables
17. Difference between frontend/backend
18. SOA (service oriented architectures, also “micro-services”)
19. Backups
20. Backup a single user on how many servers?
21. Caching
22. Many requests for the same data/lots of updates – should be in cache
23. Distribute so that the network is negligible
24. Parallelizing network requests
25. Fan-out (scatter and gather)
26. Load-balancing
27. High availability
28. CDNs (content delivery networks)
29. POPs (points of presence)
30. Queues
31. Failures
32. Timeouts
33. Fault tolerance
34. Failing fast
35. Circuit breakers
36. Throttling
37. Consensus (e.g. Paxos, Raft) and membership protocols (heartbeats, SWIM)
38. Compression
39. Possible to work harder on writes in order to make reads easier
40. Operations should almost never be more than n*log(n), preferably n