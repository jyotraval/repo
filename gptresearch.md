# 6G Network Slicing: Load Balancer & Request Routing

6G network slicing enables multiple virtual networks (slices) on shared infrastructure, tailored to different use cases (eMBB, URLLC, mMTC).  An intelligent load balancer/router at the edge must select the best server for each incoming request (already tagged as eMBB, URLLC, or mMTC) by considering many metrics.  Rather than naively choosing the least-loaded server, the balancer scores each candidate using slice-aware criteria.  For example, **eMBB** traffic demands high bandwidth/throughput, **URLLC** demands ultra-low latency and high reliability, and **mMTC** demands massive connection capacity with efficient resource use.  A good scoring function will weigh parameters like load, resource availability, latency, and reliability **differently for each slice type**.  For instance, URLLC routes should heavily penalize latency and packet loss, whereas eMBB routes prioritize available bandwidth.  

```mermaid
flowchart LR
    subgraph User Equipment
      UE[Client / UE]
    end
    subgraph Access Network
      RAN[Radio Access (gNB/microcell)]
    end
    subgraph Core Network
      CN[5G/6G Core]
      SM[Slice Manager & Orchestrator]
    end
    subgraph Edge Cloud
      LB[Slice-Aware Load Balancer]
      S1[Edge Server 1]
      S2[Edge Server 2]
      S3[Edge Server 3]
    end
    UE --> RAN --> CN
    CN --> SM --> LB
    LB --> S1
    LB --> S2
    LB --> S3
```  

**Figure:** Example 6G slicing architecture.  Edge servers (S1–S3) serve slice-specific workloads.  The Load Balancer (LB) queries server metrics (CPU, RAM, latency, etc.) and slice QoS requirements from the Slice Manager (SM) to score and route each request.  

## Key Parameters for Routing

The load balancer considers numerous parameters.  Each affects eMBB/URLLC/mMTC differently.  Below we list important metrics, their meaning, relevance, slice impact, and how to score/normalize them:

- **Current Server Load:**  
  - *Definition:* The aggregate processing load on the server (e.g. number of active tasks or CPU queue length).  
  - *Relevance:* Indicates how busy a server is.  A highly loaded server takes longer to handle new requests.  Balancing aims to avoid overloaded nodes to prevent latency spikes.  
  - *Slice Impact:* URLLC requires servers with very low current load to minimize processing delay.  eMBB can tolerate higher load (if throughput is high), and mMTC may involve many light-weight tasks so total load can be high but still manageable.  
  - *Goal:* Minimize (i.e., favor lightly-loaded servers).  
  - *Normalization:* If `L` is current load (0 = idle, 1 = full), use score = 1 – (L), or map to [0,1] relative to known capacity.  (E.g. score = (maxLoad–L)/maxLoad.)  
  - *Note:* Some works rank servers by *available* resources (the inverse of load).  

- **CPU Utilization:**  
  - *Definition:* Fraction of CPU (or cores) in use.  
  - *Relevance:* High CPU usage implies less headroom for processing new requests.  Overloaded CPU can delay task handling.  Load balancers often poll CPU to detect hotspots.  
  - *Slice Impact:* URLLC demands servers with very low CPU usage to ensure instant processing.  eMBB can use more CPU (for heavy encoding/throughput), and mMTC (many small IoT messages) can tolerate moderate CPU use per device.  
  - *Goal:* Minimize (favor servers with low CPU%) to reduce queuing.  
  - *Normalization:* `CPU_score = 1 – (CPU_usage / 100)`.  (If usage is given as %.)  

- **Memory Utilization:**  
  - *Definition:* Fraction of RAM used by processes.  
  - *Relevance:* High memory usage can cause paging or prevent caching, degrading performance.  It often correlates with server load.  
  - *Slice Impact:* URLLC prefers low memory usage (to avoid GC pauses, for example), eMBB can allow higher usage for buffering large video streams, mMTC depends on how many devices’ data are held.  
  - *Goal:* Minimize (favor servers with more free memory).  
  - *Normalization:* `Mem_score = 1 – (Mem_used / Mem_total)`.  

- **Network Bandwidth / Utilization:**  
  - *Definition:* Current network throughput or % of link capacity used by the server.  
  - *Relevance:* A saturated network interface can delay packet forwarding and limit throughput.  It reflects congestion on the server’s link.  
  - *Slice Impact:* eMBB requires high available bandwidth (large downloads). URLLC uses smaller packets but still needs available link to meet latency; mMTC involves many devices but each with small payloads, so aggregate bandwidth matters.  
  - *Goal:* Minimize utilization (maximize free bandwidth).  
  - *Normalization:* If `B_used` is current bandwidth use and `B_cap` is capacity, score = 1 – (B_used/B_cap).  
  - *Citation:* Multi-criteria balancing schemes explicitly consider “available bandwidth” as a criterion.  

- **Network Latency:**  
  - *Definition:* Round-trip (or one-way) delay between client and server.  
  - *Relevance:* Directly adds to end-to-end delay.  It includes propagation, queuing, and processing delays on the network.  It is a key QoS measure.  
  - *Slice Impact:* URLLC prioritizes *extremely* low latency (sub-10ms is common).  eMBB cares less (tens of ms is acceptable); mMTC devices often tolerate higher latency (they send small periodic data).  
  - *Goal:* Minimize.  
  - *Normalization:* E.g. if `D` is measured latency and `D_max` is a threshold (e.g. QoS target), use `Latency_score = 1 – (D/D_max)`, clamped to [0,1].  

- **Database Latency:**  
  - *Definition:* Time to perform necessary database (or storage) operations for the request.  
  - *Relevance:* Adds to service time.  For applications requiring DB access, slow database queries can bottleneck the service.  
  - *Slice Impact:* URLLC ideally uses in-memory or edge DB to minimize this.  eMBB (e.g. video on demand) may have cached content; mMTC (e.g. IoT metrics) may do batched updates.  In all cases, lower DB latency is better.  
  - *Goal:* Minimize.  
  - *Normalization:* Similar to network latency: `DB_score = 1 – (DB_latency / DB_thresh)`.  

- **Queue Length:**  
  - *Definition:* Number of pending requests/tasks queued on the server (beyond those being processed).  
  - *Relevance:* Long queues indicate backlog and higher waiting times.  Useful for predicting queuing delay.  
  - *Slice Impact:* URLLC must have very short queues (often one goal is zero queue backlog).  eMBB can tolerate longer queues (trading latency for throughput).  mMTC can have many queued small requests, but ideal routing will balance them.  
  - *Goal:* Minimize.  
  - *Normalization:* If `Q` is queue length and `Q_max` is capacity (or a chosen threshold), score = 1 – (Q/Q_max).  
  - *Citation:* In experiments, URLLC queues remained very small while eMBB queues grew larger under load.  

- **Active Requests (Current Connections):**  
  - *Definition:* Number of active client connections or sessions handled by the server.  
  - *Relevance:* Similar to load; a high number of concurrent requests can increase context-switching and overhead.  Monitoring active connections helps prevent overload.  
  - *Slice Impact:* URLLC aims to limit concurrent tasks to prioritize each one, eMBB (especially for streaming) may have many simultaneous flows, mMTC inherently has huge device counts (so this metric can be very large).  
  - *Goal:* Minimize (or at least not exceed safe concurrency limits).  
  - *Normalization:* e.g. `Conn_score = 1 – (Conns / Conns_max)`.  

- **Response Time:**  
  - *Definition:* Time taken by a server to respond to a request (from arrival to completion).  
  - *Relevance:* Direct KPI of performance.  The balancer should aim to route to servers with lower recent response times, indicating better load conditions.  High response time signals bottlenecks.  
  - *Slice Impact:* URLLC requires extremely low response times.  eMBB cares less about immediate response (preferring sustained throughput), mMTC can tolerate moderate response times if connections are long-lived.  
  - *Goal:* Minimize.  
  - *Normalization:* If `R` is current response time and `R_max` is acceptable max, score = 1 – (R/R_max).  
  - *Citation:* Monitoring response time (latency) is a standard LB metric.  

- **Packet Loss Rate:**  
  - *Definition:* Fraction of packets dropped or lost on the server’s network interface or processing.  
  - *Relevance:* High packet loss forces retransmissions and degrades reliability.  Indicates network or server issues.  
  - *Slice Impact:* URLLC demands *ultra-high reliability* (e.g. loss rates < 10^−6).  eMBB (e.g. video) can tolerate some loss (few percent errors).  mMTC devices (e.g. sensor data) may tolerate occasional drops but prefer reliability too.  
  - *Goal:* Minimize.  
  - *Normalization:* If `p_loss` is error rate (0–1), score = 1 – p_loss.  
  - *Citation:* URLLC typically targets 99.9999% delivery (10^−6 loss), whereas multimedia services might accept ~2% loss.  

- **Reliability / Availability:**  
  - *Definition:* The probability that the server will successfully serve the request (uptime or success rate).  Often measured as 1 – (failure probability).  
  - *Relevance:* A highly reliable (available) server is less likely to fail or drop connections.  Balancers often avoid nodes with past instability.  
  - *Slice Impact:* URLLC prioritizes servers with extremely high reliability (close to 100%).  eMBB and mMTC have looser needs (intermittent failures are tolerable up to a degree).  
  - *Goal:* Maximize.  
  - *Normalization:* If `A` is availability (0–1), use it directly as score.  (Or use long-term uptime percentages.)  
  - *Citation:* For example, industrial automation (URLLC use case) often requires ~99.9999% reliability.  

- **Distance / Network Delay:**  
  - *Definition:* Physical or network distance (e.g. hop count or geographic distance) between client and server.  
  - *Relevance:* Greater distance means higher propagation delay.  Latency grows roughly linearly with distance (≈0.019 ms/km).  Thus, nearby edge servers usually yield lower delay.  
  - *Slice Impact:* URLLC should be routed to the nearest available node (to meet strict latency).  eMBB can span moderate distances if bandwidth is high.  mMTC devices often tolerate some delay, but proximity still helps (and reduces backhaul load).  
  - *Goal:* Minimize.  
  - *Normalization:* If `d` is distance (or measured delay) and `d_max` is a cutoff, score = 1 – (d/d_max).  

- **(Other Metrics):** Depending on application, one might also consider parameters like **server temperature/thermal status**, **energy remaining**, or **specialized hardware availability**.  For example, some fog LB schemes include “available energy” (to prefer energy-rich nodes).  In general, any metric that affects service time or QoS can be scored similarly.  

Each metric is normalized to [0,1] so they can be combined.  For “benefit” metrics (higher is better, e.g. available CPU or availability), use \(score = (value - min)/(max - min)\).  For “cost” metrics (lower is better, e.g. latency, load), invert it: \(score = 1 - (value - min)/(max - min)\).  All metrics can then be weighted and summed for a final route score.  

## Request Routing Flow (Mermaid)

The decision process can be visualized as a flowchart:  

```mermaid
flowchart LR
    I([Incoming Request<br/>(slice type)]) 
    I --> T{Determine Slice Type}
    T -->|eMBB| S[eMBB requirements]
    T -->|URLLC| S[URLLC requirements]
    T -->|mMTC| S[mMTC requirements]
    S --> M[Query server metrics (CPU, RAM, latency, etc.)]
    M --> C[Compute weighted score for each server]
    C --> D{Highest score?}
    D -->|Select| X[Choose best server]
    X --> F[Forward request to server]
```  

**Figure:** Request-routing logic.  The balancer reads the slice type of the request, gathers relevant metrics from candidate servers, computes a multi-parameter score per server (giving slice-prioritized weights), and selects the server with the highest score.  

## Summary

An effective 6G slicing load balancer uses a **multi-metric scoring function**.  It considers real-time server measurements (load, CPU/memory use, bandwidth) and network QoS metrics (latency, loss, distance) to align with slice needs.  For example, URLLC slices will weight latency and reliability **highest**, eMBB slices will weight bandwidth/throughput **highest**, and mMTC will weight capacity (supporting many devices) and efficient resource use.  Studies show such multi-criteria approaches significantly improve overall performance (reducing response time and balancing load) compared to single-metric methods.  By normalizing each metric to [0,1] and applying slice-specific weights, the load balancer can make nuanced routing decisions that meet the diverse demands of eMBB, URLLC, and mMTC slices.

**Sources:** Contemporary research on 5G/6G network slicing and fog/edge load balancing.
