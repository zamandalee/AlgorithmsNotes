# Architecture

## Standard Web App Architecture
- Browser --> load balancer --> app servers --> caching layer --> CDN(s) --> DB

### Databases
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
