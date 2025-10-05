# livedrop-fouadgeagea
“Live Drops” — Flash-Sale and Follow Platform

We will Choose Consistency over Availability since we have transactions. We will go with SQL Database

.Client hit the server with API Gateaway (Rest API), that intercommunicate between the services (RPC) since its the fastest way. 

.SSE for Notifications, unidirectional where the client is consuming and our system is producing events.

.Rate Limiting for security measures and to not let the one client buy all the drops to let other clients do so.

.Auto-Scaling with Load-Balancer is needed since some creators are extermely popluar and can drive sudden traffic spikes.

.We need to have a Search Optimized Database for searching and browsing the products (paginated also), Elastic Search for example.

.We need to have Infrastructure Monitoring, where we monitor an error that happened with the correlation ID.

.We need to add also DataDog to monitor the services, to know which service has a lot of load.

.We need to have a payment Gateaway.

.Distributed Lock: lock in order to not let two clients buy the same product where one will get it and the other not, and a check on the database is needed. Also we can use Red-Lock where we lock the service until unlocking it in case of a horizontal scaling of two services available.

**Order Service**: client hit the post order API, I have the status update in the order service that is a database, updates whatever hapenning and getting back to the user telling him that he purchased his product successfully. SQL Database for secured transactions with a rollback function.

**Products Service**: client will communicate with the server to get the product details, database is storing the product details (S3ImageUrl, productId, name, description, price, stock,...) we will use Cloudflare (CDN) for caching and reducing cost purposes with a TTL and revalidates the caching data when the creator updates the product details or when its stock is 0 to remove the product from being listed as purchasable. Also scaling for the caching in order to prevent a full memory. Introduce Indexing is a good case also.

**Authentication & Authorization Service**: for the user to enter his credentials, authorize him to purchase, follow/unfollow creators, etc... 

**Followings Followers Service**: We introduce a seperate table for the followings and followers, we add indexing and we do hashing on the id and split into buckets. In this case we avoid data manipulation of huge arrays to know to following and followers and to check if user A follows creator B for example.

**Notification Service**: to notify users about live drops, stock, etc...
<img width="979" height="531" alt="Screenshot 2025-10-05 at 11 54 26 AM" src="https://github.com/user-attachments/assets/1be94a7b-8a23-4d6e-a118-ee0dd242ac3d" />
