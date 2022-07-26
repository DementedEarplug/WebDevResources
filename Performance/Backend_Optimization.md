# Backend Optimizations
When trying to optimize backend operations there are some areas that are key. Among these areas are implementing CDNs, file compression (gzip, deflate, bratli), DB optimizations, caching, and load balancers.

## CDNs
Content Delivery Networks (CDNs) are servers located around the world that can help speed up access to your resources by providing a cached version of them to the client. CDNs limit the necessary number of hops necessary the client needs to reach a resource after the first time they are fetched. This greatly imporves performance and availability of the resources.

Among the most popular CDN providers are Cloud Flare, Amazon Cloud Front, and Azure Content Delivery Network.

## File Compression
Tools like GZIP, Deflate, and Bratli greatly reduce the file size that gets sent through the wire, thus improving performance. These tools can be configured as middleware in a set and forget fashion. I.e npm has a compression package that can be used as a middleware in express; and NGINX has a config line that turns on gzip to compress the files.

## Database Optimizations
There are 6  principal aspects to keep in mind when you are trying to imporve database scaling. They are listed below.
### Identify ineficient Queries
When doing DB queries, be sure to request the info you absolutely need and use indexes, allowing for binary search (assuming you dont have any space contrains). Avoiding unnesesary joins or asking for too much data when you dont need it.
### Increase Memory
If the bottleneck is storage, you can improve the hardware the DB is operating on. By increasing the amount of information in memory you give a buffer from wich to access data without having to directly hit the DB. But there is so much memory you can add, and the whole DB cant be placed in memory.
### Vertical Scaling (Redis, Memcached)
Use another server with a service with Redis or Memecached to cache frequently performed queries. Since these services run in memory they will be more performant in returning the desired information.
### Sharding
This implementation entails partioning the DB into subsets of a particular query. That way when doing a query you can search in the shard that pertains to that subset, instead of searching the whole database. I.e. partitioning the DB into users by the state they live in.
### More Databases
By having multiple databases you can distribute the load of queries that a database handle. Note the databases in this case are identical. (It's kind of like a load balancer.)
### Database Type
There are various types of databases and each type is might be better to handle certain types of problems. So you have to decide what type of characteristics and behaviors you want out of the database.   

## Caching
Caching is the process of storing data in the cache. The cache is a temp storage where data can be stored, so in the future data can be served faster. 

There are a miriad of ways you can use caching to improve performance, among them:
- Use CDN to cache files and save a trip to the server.
- Use a cache to store the result of an API call to avoid calling the API constanlty to fetch the same info. (Gotta update the cache every time the info changes tho')
- Use a cache like mentioned in the `Vertical Scaling` section to store frequently performed queries on a database.
- Use a cache for session management.
- Use cache within the web browser.

### Caching in the web browser
Under the application tab within the browser you have a miriad of tools available that are cache base that can help improve performance: 
- Storage like cookies, local storage, session storage, and cache storage. 
- Service workers in PWAs.
- HTTP Cache control

### Caching Resources
A couple of resources for further reading into caching and HTTP Cache implementations:
1. [Caching Everywhere](!https://www.freecodecamp.org/news/the-hidden-components-of-web-caching-970854fe2c49)

2. [Cache Headers](!https://web.dev/http-cache/)

3. [Caching and Performance](!https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers)

## Load Balancing
Load balancing is a way to balance multiple requests made at the same time and distribute them to different services. You can create a custom load balancer using nginx, or you can use a platform like AWS, GCP, Azure, Digital Ocean, etc... to create load balancers for you.
 