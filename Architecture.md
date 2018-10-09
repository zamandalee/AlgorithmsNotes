# Architecture

## Standard Web App Architecture
- Browser --> load balancer --> app servers --> caching layer --> CDN(s) --> DB

### Databases (slow)
- Relational DB: easy to use and query, denormalization often used to scale and avoid joins
  - Scaling
    - High read load + master-slave: leader handles writes, followers read
      - Ex.: Twitter, FB
    - High write load + shards: not for relational DB, sharding (designated handlers for each obj)
      - Ex.: WhatsApp


- NoSQL: schema not enforced
  - Document-based: ex. MongoDB (giant hash map w keys and vals as JSON obj)
  - K-V stores: ex. Redis (like document-based, but less powerful bc no indexes or joins)
  - Distributed dbs: used by all big websites, ex. Cassandra (cluster of dbs --> allows failures)

- Failover: prevent single point of failure
  - Leader and followers (master-slave relationship)

### To Make a Site Faster: CDN and Caching

#### Content Delivery Network (CDN)
  - CDN: system of distributed servers that deliver content to users, based on user, webpage, and server location
  - HTTP flow w a CDN
    - Browser makes DNS request for domain name that's handled by a CDN --> server handling DNS requests looks at incoming request to determine best set of servers to handle

#### Caching Layer
- Caches: generally stored in memory (like RAM), are K-V stores
  - Store common queries (ex.: someone's tweets), expensive queries (ex.: trending hashtag), static data
  - Cache invalidation: if cached data becomes invalid or unnecessary
    - Ex.: LRU cache

### Application Server


## Sources:
https://github.com/rlee0525/TechnicalConceptsForInterviews/blob/master/Architecture.md
