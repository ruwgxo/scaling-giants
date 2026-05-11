# 20250104 | Scaling Giants: Search & Discovery at Scale by Raghav Dinesh  
#wrap #paper   
  
**Scaling Giants**  
*Architecture Lessons from Tech’s Most Demanding Systems*  
  
**Contents**  
‣ Scaling Giants  
‣‣ Search & Discovery at Scale  
1. Introduction  
2. Google Ads - Supporting 4.77 Billion Users  
    1. SQL database sharding strategies  
    2. Real-time bidding architecture  
    3. Index distribution and replication  
3. Uber - 1 Million Driver Matching Requests per Second  
    1. Geospatial indexing and search  
    2. Real-time location processing  
    3. Demand prediction algorithms  
  
  
1. **Introduction**  
  
**Quick Take** Search and discovery systems like Google Ads and Uber handle massive query volumes and real-time data, requiring optimized indexing, low-latency processing, and predictive algorithms. This chapter explores their architectures, focusing on sharding, real-time bidding, and geospatial matching to deliver fast, relevant results at scale.  
  
**The Challenge** Supporting billions of users or millions of requests per second demands architectures that index vast datasets, process queries in milliseconds, and adapt to dynamic patterns (e.g., ad auctions, ride matching). Balancing speed, accuracy, and cost under extreme load is the core challenge.  
  
**The Numbers**  
- Queries: 1M to 10B/day  
- Latency: <50ms for 99.9% of requests  
- Uptime: 99.99% or higher  
- Data Size: 10TB to 1PB indexed data  
- Cost: $0.001–$0.05 per 1,000 queries  
  
**The Architecture** Search and discovery systems typically include:  
- Indexing Layer: Sharded or distributed indexes (e.g., Elasticsearch).  
- Query Processing: Real-time pipelines for matching (e.g., Flink).  
- Caching: Reduces index load (e.g., Redis).  
- Prediction Models: ML for relevance or demand (e.g., TensorFlow).  
  
```
ASCII Diagram (Generic Search System)

[Query] --> [Load Balancer] --> [Query Processor] --> [Cache] --> [Index]
                                       |               |          |
                                       +-->        [ML Model] --> [Logs]

```
  
**Key Innovations**  
- Sharding: Distributes data for scalability (Google Ads).  
- Real-Time Processing: Handles dynamic queries (Uber).  
- Predictive Algorithms: Optimize relevance or matching.  
  
**Lessons Learned**  
- Indexing efficiency is critical for low-latency queries.  
- Real-time systems trade accuracy for speed—calibrate carefully.  
- Caching reduces load but requires invalidation strategies.  
  
**Evolution Path** Early search systems used single-node databases (e.g., Google’s early SQL-based index). As scale grew, they adopted distributed sharding, caching, and real-time pipelines. Google Ads’ 2005–2015 shift to distributed indexes supported 4.77B users.  
  
**Related Patterns**  
- Sharding: PayPal’s database strategy.  
- Caching: Meta’s consistency model.  
- Event-Driven: Stripe’s pipelines.  
  
```
YAML Pattern Card

pattern:
  name: Sharding
  use_case: Distribute data for scalability
  pros: High throughput, fault isolation
  cons: Complex query routing, rebalancing
  examples: Google Ads, PayPal

```
  
**Reader Challenge** Design a search system for 1B queries/day with <50ms latency. How would you balance indexing speed and query accuracy?  
  
  
2. **Google Ads - Supporting 4.77 Billion Users**  
  
**Quick Take** Google Ads serves 4.77 billion users with sharded SQL databases, real-time bidding, and distributed indexing. This section breaks down its architecture, highlighting how it achieves low-latency ad delivery at global scale.  
  
**The Challenge** Delivering relevant ads to 4.77 billion users requires sharding massive datasets, processing bids in real time, and replicating indexes globally, all while maintaining <50ms latency and high availability.  
  
**The Numbers**  
- Users: 4.77B  
- Queries: ~8.5B/day (~100K/second)  
- Latency: <50ms for 99.9% of bids  
- Uptime: 99.99%  
- Index Size: ~100TB  
  
**The Architecture** Google Ads’ system includes:  
- Sharded SQL Databases: Store ad metadata and user data.  
- Bidding Engine: Real-time auction processing.  
- Index Layer: Distributed for fast query resolution.  
- Caching: Memcached for frequent queries.  
  
```
ASCII Diagram (Google Ads Architecture)
[Ad Request] --> [Load Balancer] --> [Bidding Engine] --> [Cache] --> [Sharded SQL]
                                         |                |           |
                                         +--> [Index] --> [Logs] --> [Analytics]

```
  
**Key Innovations**  
- Database Sharding: Splits ad data across thousands of nodes.  
- Real-Time Bidding: Processes auctions in milliseconds.  
- Index Replication: Ensures global availability.  
  
**Lessons Learned**  
- Sharding reduces latency but complicates query routing.  
- Real-time bidding requires tight integration with caching.  
- Replication must balance consistency and speed.  
  
**Evolution Path** Google Ads started with a monolithic SQL database in the early 2000s. By 2010, it adopted sharded MySQL and distributed indexing. By 2020, custom bidding engines and global replication supported 4.77B users.  
  
**Related Patterns**  
- Sharding: PayPal’s transaction system.  
- Caching: Meta’s cache consistency.  
- Event-Driven: Stripe’s architecture.  
  
```
YAML Pattern Card

pattern:
  name: Real-Time Bidding
  use_case: Process auctions at scale
  pros: Low latency, high throughput
  cons: Complex synchronization, high compute cost
  examples: Google Ads

```
  
**Reader Challenge** Design a bidding system for 100K auctions/second. How would you optimize for latency and cost?  
  
**2.1 SQL database sharding strategies**  
- Problem: Single-node SQL databases bottleneck at billion-user scale.  
- Solution: Shard data by user or ad ID across multiple nodes.  
- Example: Google Ads shards MySQL databases to handle 8.5B queries/day.  
- Trade-off: Scalability vs. query complexity.  
  
```
ASCII Diagram

[Query] --> [Shard Router] --> [Shard 1] --> [Result]
                            |            |
                            +--> [Shard 2] --> [Result]

```
  
**2.2 Real-time bidding architecture**  
- Problem: Auction processing must complete in <50ms under high load.  
- Solution: Use in-memory bidding engines with caching.  
- Example: Google Ads’ custom engine processes 100K bids/second.  
- Trade-off: Speed vs. compute cost.  
  
```
ASCII Diagram

[Bid Request] --> [In-Memory Engine] --> [Cache] --> [Bid Response]

```
  
**2.3 Index distribution and replication**  
- Problem: Global queries require fast, consistent index access.  
- Solution: Replicate indexes across regions with eventual consistency.  
- Example: Google Ads replicates 100TB indexes for global availability.  
- Trade-off: Availability vs. consistency.  
  
```
ASCII Diagram

[Query] --> [Region A Index] --> [Result]
          |
          +--> [Region B Index] --> [Result]

```
  
  
3. **Uber - 1 Million Driver Matching Requests per Second**  
  
**Quick Take** Uber matches 1 million driver requests per second using geospatial indexing, real-time location processing, and demand prediction. This section explores its architecture for fast, accurate ride matching at scale.  
  
**The Challenge** Matching drivers and riders in real time requires indexing billions of location points, processing dynamic data, and predicting demand, all with <50ms latency and high accuracy across global cities.  
  
**The Numbers**  
- Requests: 1M/second  
- Latency: <50ms for 99.9% of matches  
- Uptime: 99.99%  
- Data Points: ~10B location updates/day  
- Cost: ~$0.01 per match  
  
**The Architecture** Uber’s system includes:  
- Geospatial Index: Stores location data (e.g., quad-trees).  
- Real-Time Pipeline: Processes streaming location updates (e.g., Kafka).  
- Prediction Models: ML for demand forecasting (e.g., TensorFlow).  
- Caching: Redis for frequent queries.  
  
```
ASCII Diagram (Uber Matching Architecture)

[Rider Request] --> [Load Balancer] --> [Matching Engine] --> [Cache] --> [Geospatial Index]
                                            |                |            |
                                            +--> [ML Model] --> [Kafka] --> [Logs]

```
  
**Key Innovations**  
- Geospatial Indexing: Optimizes location-based queries.  
- Real-Time Streaming: Processes dynamic location data.  
- Demand Prediction: Balances supply and demand.  
  
**Lessons Learned**  
- Geospatial indexes must scale with location density.  
- Real-time pipelines require robust fault tolerance.  
- Predictive models improve efficiency but need frequent retraining.  
  
**Evolution Path** Uber’s early system (2010) used simple SQL databases for matching. By 2015, it adopted quad-tree indexing and Kafka for real-time processing. By 2020, ML-driven demand prediction supported 1M requests/second.  
  
**Related Patterns**  
- Sharding: Google Ads’ database strategy.  
- Event-Driven: Stripe’s pipelines.  
- Caching: Meta’s consistency model.  
  
```
YAML Pattern Card

pattern:
  name: Geospatial Indexing
  use_case: Optimize location-based queries
  pros: Fast spatial lookups, scalable
  cons: Complex updates, memory overhead
  examples: Uber, Google Maps

```
  
**Reader Challenge** Design a matching system for 1M ride requests/second. How would you handle dense urban areas?  
  
**3.1 Geospatial indexing and search**  
- Problem: Matching riders and drivers requires fast spatial queries.  
- Solution: Use quad-trees or geohashes to index location data.  
- Example: Uber’s quad-tree index processes 1M requests/second.  
- Trade-off: Query speed vs. index maintenance.  
  
```
ASCII Diagram

[Location] --> [QuadTree] --> [Nearest Drivers] --> [Match]

```
  
**3.2 Real-time location processing**  
- Problem: Dynamic location updates overwhelm batch processing.  
- Solution: Stream data via Kafka to update indexes in real time.  
- Example: Uber processes 10B location updates/day with <50ms latency.  
- Trade-off: Speed vs. processing cost.  
  
```
ASCII Diagram

[Driver Update] --> [Kafka] --> [Stream Processor] --> [Index]

```
  
**3.3 Demand prediction algorithms**  
- Problem: Imbalanced supply and demand cause delays or surges.  
- Solution: Use ML models to predict ride demand by region.  
- Example: Uber’s TensorFlow models optimize driver allocation.  
- Trade-off: Accuracy vs. compute cost.  
  
```
ASCII Diagram

[Data] --> [ML Model] --> [Demand Prediction] --> [Driver Allocation]

```
