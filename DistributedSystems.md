# Distributed Systems
How do you deploy your application to cloud such that it doesn't crash while serving a large user base?

## Application Process
- Amazon EC2: rent computers in Amazon data center
  - Heroku does this for you
  - Can run make apps, run servers (ex.: instead of localhost3000, [username]3000), etc. remotely on this computer
  - Public DNS, IP, etc.
- Difference between domain name and IP
  - House address -> Internet Protocol address
  - Resident name -> domain name
  - Domain Name Service -> phonebook in the cloud


1. Phonebook (DNS) -> lookup address (IP) using name (domain name)
2. HTTP request to address
3. Server, server hands request to application
4. Application communicates with backend database (Postgres and mySQL have own server that accepts database requests, typically only from same machine as app)

## Scaling
- ^ doesn't scale well: not enough CPU power to compute all the requests
- Fixes:
  - Vertical scaling: pay to improve computing power of current machine
  - Horizontal scaling: add more servers to handle more requests
