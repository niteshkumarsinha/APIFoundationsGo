## Setting up Redis

We will also use Docker to run Redis, which is as simple as setting up Go. 

### Redis is an in-memory data structure store. 

It provides functionality to store and retrieve data in various structures, beyond
a simple key-value database like Memcache. 

We will use this service later in the book when implementing our example API endpoints.

To run an instance of Redis named `redis`:

```bash
docker run --restart=always -h redis --name redis --net=party -d redis
```

#### Other services

In addition to Go and Redis, other services are also available on the Docker Hub¹. Depending on
your use case, you might want to install additional services via docker.
Popular projects which I use from Docker on a daily basis:
* nginx (and nginx-extras flavours)
* Percona (MySQL, MariaDB) - also covered later in the book
* letsencrypt
* redis
* samba
* php

Docker is a very powerful tool which gives you all the software you might need. It’s very useful
also for testing, as you can use it to set up a database, populate it with test data, and then tear down
and clean up after it. It’s a very convenient way to run programs that are isolated from your actual
environment, and may only be active temporary.