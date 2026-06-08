## Core CS Knowledge (Concepts, Not Implementations)

At 7 years in, the goal is depth and sharpness — not re-implementing linked lists.

- ### Algorithmic Complexity
    - Know Big-O cold: time and space for all major data structures and algorithms
    - Amortized analysis (dynamic arrays, union-find), average vs worst case
    - [Cheat sheet](http://bigocheatsheet.com/)

- ### Data Structures — Know, Don't Re-implement
    - Arrays, Linked Lists, Stack, Queue, Deque — know complexity guarantees
    - Hash tables: collision resolution (chaining vs open addressing), load factor, rehashing
    - Heaps / Priority Queues: heapify, heap sort, use-cases
    - Trees: BST, AVL, Red-Black, B-Trees (critical for DB internals)
    - Tries, Segment Trees, Fenwick Trees — when to reach for them
    - Graphs: adjacency list vs matrix, BFS/DFS, Dijkstra, Bellman-Ford, topological sort

- ### Sorting & Searching
    - Mergesort, Quicksort, Heapsort — know stability, space complexity, pivot strategies
    - Binary search and variants (rotated arrays, first/last occurrence, answer-space binary search)
    - Radix sort / counting sort when applicable

- ### Dynamic Programming
    - Identify overlapping subproblems and optimal substructure
    - Top-down (memoization) vs bottom-up (tabulation)
    - Classic patterns: knapsack, LCS, LIS, edit distance, interval DP, tree DP
    - [Dynamic Programming – From Novice to Advanced (TopCoder)](https://www.topcoder.com/community/data-science/data-science-tutorials/dynamic-programming-from-novice-to-advanced/)

- ### Design Patterns
    - [ ] Strategy, Observer, Factory/Abstract Factory, Builder, Decorator, Proxy, Adapter, Facade, Command, Iterator, Composite, Flyweight, Memento, State, Visitor, Singleton (and why to avoid it)
    - [Design patterns for humans](https://github.com/kamranahmedse/design-patterns-for-humans)
    - [Handy reference: 101 Design Patterns & Tips](https://sourcemaking.com/design-patterns-and-tips)

- ### SOLID Principles
    - [ ] [Bob Martin SOLID Principles (video)](https://www.youtube.com/watch?v=TMuno5RZNeE)
    - S — Single Responsibility, O — Open/Closed, L — Liskov Substitution, I — Interface Segregation, D — Dependency Inversion

- ### Concurrency and Distributed Primitives
    - Threads vs processes, locks, mutexes, semaphores, monitors
    - Deadlock, livelock, starvation — detection and prevention
    - Memory models, happens-before, volatile, compare-and-swap
    - Java: `synchronized`, `ReentrantLock`, `CompletableFuture`, `ForkJoinPool`, virtual threads (JDK 21+)
    - [Computer Science 162 - Operating Systems (videos)](https://archive.org/details/ucberkeley-webcast-PL-XXv-cvA_iBDyz-ba4yDskqMDY6A1w_c)

- ### Networking
    - TCP vs UDP, TLS handshake, HTTP/1.1 vs HTTP/2 vs HTTP/3
    - Load balancers (L4 vs L7), CDNs, DNS resolution
    - REST vs gRPC vs GraphQL — trade-offs, not just definitions
    - WebSockets, SSE, long-polling — when to use which

- ### Caches
    - LRU, LFU, TTL-based eviction — implementation and trade-offs
    - Cache-aside vs write-through vs write-behind vs refresh-ahead
    - CPU cache hierarchy, cache lines, false sharing
    - Distributed caches: Redis, Memcached — consistency models


## System Design Learning Path

> Goal: design systems that are scalable, reliable, and maintainable — and be able to reason about trade-offs clearly under interview pressure and in real production contexts.

### Foundations to Nail First
- [ ] **Scalability primitives**: vertical vs horizontal scaling, stateless vs stateful services, shared-nothing architecture
- [ ] **CAP theorem**: consistency vs availability under partition — know which side your system sits on and why
- [ ] **Latency vs throughput**: P50/P99/P999, Little's Law, queueing theory basics
- [ ] **Back-of-envelope math**: RPS estimates, storage sizing, bandwidth, cache hit rate impact
    - Practice: 1M DAU, 10 reads/user/day, avg 1KB → ~116 MB/s read throughput
- [ ] **Fallacies of distributed computing**: network is reliable, latency is zero, bandwidth is infinite — burn these in

### Networking and APIs
- [ ] DNS, load balancers (L4 vs L7), reverse proxies, CDNs — how a request travels end-to-end
- [ ] REST vs gRPC vs GraphQL: when to use each, schema evolution, versioning strategies
- [ ] API design: idempotency keys, pagination (cursor vs offset), rate limiting (token bucket, sliding window)
- [ ] Long-polling, WebSockets, SSE, webhooks — trade-offs for real-time delivery
- [ ] Circuit breakers (Hystrix/Resilience4j), retries with exponential backoff + jitter, timeouts, bulkheads

### Databases (Deep)
- [ ] **SQL internals**: B-Tree indexes, LSM trees (RocksDB), MVCC, WAL, vacuum/compaction
- [ ] **Indexing**: composite indexes, covering indexes, partial indexes, index-only scans, write amplification cost
- [ ] **Replication**: single-leader, multi-leader, leaderless (Dynamo-style), replication lag, read-your-writes
- [ ] **Sharding**: range vs hash vs directory-based, cross-shard queries, resharding (consistent hashing)
- [ ] **NoSQL trade-offs**:
    - Wide-column (Cassandra, HBase): write-heavy, time-series, partitioning model
    - Document (MongoDB): flexible schema, $lookup cost, aggregation pipeline
    - Key-value (Redis, DynamoDB): hot key problem, TTL, item size limits
    - Graph (Neo4j, Neptune): when relationships are first-class
- [ ] **NewSQL** (CockroachDB, Spanner): distributed transactions, external consistency, TrueTime
- [ ] **Connection pooling**: PgBouncer, HikariCP, N+1 queries, connection limits at scale

### Caching Strategies
- [ ] Cache-aside (lazy loading) vs write-through vs write-behind vs refresh-ahead
- [ ] Eviction policies: LRU, LFU, FIFO, TTL — choosing based on access patterns
- [ ] Cache stampede / thundering herd: probabilistic early expiration, distributed locks, request coalescing
- [ ] Multi-level caching: L1 (in-process) → L2 (Redis) → L3 (CDN edge) → origin
- [ ] Cache consistency: invalidation vs TTL-based, write-through with versioned keys, pub/sub invalidation
- [ ] Redis deep dive: data structures (sorted sets, streams, hyperloglogs), Lua scripting, Redis Cluster vs Sentinel

### Message Queues and Event-Driven Systems
- [ ] **Kafka architecture**: brokers, topics, partitions, consumer groups, offsets, ISR, leader election
    - [ ] Producer: acks, batching, compression, idempotent producer
    - [ ] Consumer: at-most-once vs at-least-once vs exactly-once, rebalancing, lag monitoring
    - [ ] Log compaction, retention policies, partition key design
- [ ] **When to use queues**: decoupling, load leveling, fan-out, ordering guarantees
- [ ] **Competing consumers vs pub/sub**: SQS vs SNS vs Kafka — trade-offs
- [ ] **Outbox pattern**: transactional writes + event publishing without 2PC
- [ ] **Saga pattern**: choreography vs orchestration, compensating transactions
- [ ] **Event sourcing vs CQRS**: when it helps and the operational cost it adds

### Distributed Systems Concepts
- [ ] **Consistency models**: linearizability, sequential consistency, causal consistency, eventual consistency
- [ ] **Consensus**: Raft (leader election, log replication), Paxos (conceptual), ZooKeeper (ZAB)
- [ ] **Distributed transactions**: 2PC (blocking), 3PC, Saga, TCC — why 2PC is rare in practice
- [ ] **Clock synchronization**: physical vs logical clocks (Lamport), vector clocks, hybrid logical clocks
- [ ] **Failure detection**: heartbeats, gossip protocol, phi-accrual failure detector (Cassandra)
- [ ] **Service discovery**: client-side (Eureka) vs server-side (ELB), DNS-based, Consul/etcd

### High Availability and Reliability
- [ ] **Availability math**: 99.9% = 8.7h/year downtime, 99.99% = 52m/year — know the table cold
- [ ] **SLOs, SLAs, error budgets**: defining SLIs, alerting on burn rate, error budget policy
- [ ] **Graceful degradation**: feature flags, circuit breakers, shadow traffic, fallback responses
- [ ] **Disaster recovery**: RPO vs RTO, active-active vs active-passive, multi-region strategies
- [ ] **Chaos engineering**: fault injection, game days, Chaos Monkey principles

### Observability and Operations
- [ ] **Three pillars**: logs (structured JSON), metrics (counters/histograms/gauges), traces (distributed)
- [ ] **OpenTelemetry**: instrumentation, trace context propagation, OTLP exporters
- [ ] **Metrics systems**: Prometheus + Grafana, Datadog, CloudWatch — USE method (utilization, saturation, errors)
- [ ] **Log aggregation**: Elasticsearch + Kibana, Loki, Splunk — structured querying at scale
- [ ] **Distributed tracing**: Jaeger, Zipkin, trace sampling strategies, tail-based sampling
- [ ] **On-call practices**: runbooks, blameless post-mortems, toil reduction, SLO-based alerting

### Microservices and Service Mesh
- [ ] **Service decomposition**: domain-driven design, bounded contexts, strangler fig pattern
- [ ] **Communication patterns**: sync (REST/gRPC) vs async (Kafka/SQS), choreography vs orchestration
- [ ] **API gateway**: auth, rate limiting, request routing, response aggregation
- [ ] **Service mesh**: Istio/Linkerd — mTLS, traffic management, observability without code changes
- [ ] **Container orchestration**: Kubernetes — deployments, services, ingress, HPA, resource limits, probes

### Common System Design Problems to Practice

| System | Key Challenges |
|---|---|
| URL Shortener | Hash collision, redirect performance, analytics |
| Rate Limiter | Token bucket vs sliding window, distributed state |
| Distributed Cache | Consistent hashing, eviction, replication |
| News Feed / Timeline | Fan-out on write vs read, storage at scale |
| Search Autocomplete | Trie vs inverted index, ranking, latency |
| Notification System | Fan-out, delivery guarantees, mobile push |
| Distributed Message Queue | Ordering, at-least-once, offset management |
| Ride-Sharing (Uber/Lyft) | Geo-indexing (geohash/quadtree), matching, surge |
| Video Streaming (YouTube) | CDN, encoding pipeline, adaptive bitrate |
| Payments / Ledger | Idempotency, double-spend prevention, auditability |
| Web Crawler | Politeness, de-duplication, distributed coordination |
| LLM Inference Service | GPU batching, KV cache, autoscaling, cost |

### Books and Resources
- [ ] **Designing Data-Intensive Applications** — Martin Kleppmann (essential — read cover to cover)
- [ ] **System Design Interview Vol 1 & 2** — Alex Xu (breadth and practice)
- [ ] **Building Microservices** — Sam Newman
- [ ] **The Site Reliability Engineering Book** — Google SRE (free online)
- [ ] [High Scalability Blog](http://highscalability.com/) — real architecture teardowns
- [ ] [Grokking the System Design Interview](https://www.educative.io/courses/grokking-the-system-design-interview)
- [ ] [ByteByteGo Newsletter / YouTube](https://blog.bytebytego.com/) — visual system design explainers


## Topics for 7 Years of Experience

- **Technical Leadership**
    - [ ] Leading projects end-to-end: requirements, design docs, breaking work into milestones, de-risking
    - [ ] Writing RFCs / design docs that drive alignment, not just document decisions
    - [ ] Communicating trade-offs clearly to PMs, stakeholders, and non-technical leadership
    - [ ] Setting technical direction: when to pay down debt, when to greenfield, when to buy vs build

- **Code Quality and Reliability at Scale**
    - [ ] Designing clean interfaces, enforcing invariants, making wrong states unrepresentable
    - [ ] Testing strategy at scale: unit, integration, contract (Pact), load, chaos
    - [ ] Observability: structured logging, distributed tracing (OpenTelemetry), metrics, SLOs/error budgets
    - [ ] On-call practices: runbooks, post-mortems, reducing toil

- **Engineering Effectiveness**
    - [ ] Mentoring engineers at all levels; raising the bar through code reviews
    - [ ] Driving cross-team initiatives, aligning on standards, deprecating old systems safely
    - [ ] Knowing when NOT to build — saying no and what you gain from it


## AI / Machine Learning Learning Path

> Goal: enough depth to build AI-powered systems, lead ML platform decisions, and contribute to AI product strategy.

### Mathematics Foundations
- [ ] **Linear Algebra**: vectors, matrices, eigendecomposition, SVD — [3Blue1Brown Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)
- [ ] **Probability & Statistics**: Bayes' theorem, distributions, MLE, information theory (entropy, KL divergence)
- [ ] **Optimization**: gradient descent variants (SGD, Adam, AdamW), learning rate schedules, convexity

### Classical ML — Depth Over Breadth
- [ ] Linear/logistic regression (derive the gradient, understand regularization L1/L2)
- [ ] Decision trees, random forests, gradient boosting — XGBoost, LightGBM internals
- [ ] SVMs, k-means, PCA, UMAP — when and why
- [ ] Feature engineering, encoding, leakage, data splitting strategy, class imbalance handling
- [ ] Bias/variance tradeoff, cross-validation, hyperparameter tuning (Bayesian optimization)
- [ ] [fast.ai ML course](https://course.fast.ai/)

### Deep Learning
- [ ] Neural network fundamentals: forward/backprop, vanishing gradients, batch norm, dropout
- [ ] CNNs: convolutions, pooling, ResNet, EfficientNet — use-cases in vision
- [ ] RNNs, LSTMs, GRUs — limitations that led to Transformers
- [ ] **Transformers**: self-attention, multi-head attention, positional encoding, encoder/decoder variants
    - [ ] [Attention Is All You Need (paper)](https://arxiv.org/abs/1706.03762)
    - [ ] [Illustrated Transformer — Jay Alammar](https://jalammar.github.io/illustrated-transformer/)
- [ ] PyTorch hands-on: training loop, `DataLoader`, custom datasets, mixed precision, `torch.compile`

### LLMs and Generative AI
- [ ] **Pre-training**: next-token prediction, masked LM, data curation and tokenization (BPE, SentencePiece)
- [ ] **Fine-tuning strategies**: full fine-tuning, LoRA, QLoRA, PEFT — trade-offs in cost vs quality
- [ ] **RLHF / RLAIF**: reward modeling, PPO, DPO — how alignment is trained
- [ ] **Inference optimization**: quantization (GPTQ, AWQ), KV cache, speculative decoding, vLLM, tensor parallelism
- [ ] **Prompt engineering**: zero-shot, few-shot, chain-of-thought, structured outputs (JSON mode, tool use)
- [ ] **RAG (Retrieval-Augmented Generation)**:
    - [ ] Chunking strategies, embedding models, vector databases (Pinecone, Weaviate, pgvector)
    - [ ] Hybrid search (dense + sparse), reranking (cross-encoders), context window management
    - [ ] Agentic RAG: query rewriting, multi-hop retrieval
- [ ] **Agents and Tool Use**: ReAct pattern, function calling, MCP (Model Context Protocol), multi-agent orchestration
- [ ] **Evaluation**: BLEU/ROUGE (limitations), LLM-as-judge, RAGAS, human eval, red-teaming
- [ ] **Safety and alignment**: hallucinations, jailbreaks, prompt injection, guardrails
- [ ] [Andrej Karpathy — Let's build GPT from scratch](https://www.youtube.com/watch?v=kCc8FmEb1nY)
- [ ] [CS224N: NLP with Deep Learning — Stanford](https://web.stanford.edu/class/cs224n/)

### ML System Design
- [ ] End-to-end recommendation / search / ranking / LLM-based system design
- [ ] Online vs offline inference, latency/throughput/cost trade-offs, SLOs
- [ ] Feature stores (Feast, Tecton), model registry, A/B testing and experiment design
- [ ] Embedding serving at scale, approximate nearest neighbor (FAISS, ScaNN, HNSW)
- [ ] Monitoring: data drift, concept drift, model degradation, shadow deployment, canary rollouts

### MLOps and Platforms
- [ ] CI/CD for models: retraining triggers, model validation gates, rollback strategy
- [ ] Experiment tracking: MLflow, Weights & Biases
- [ ] Data versioning and lineage (DVC, Delta Lake)
- [ ] GPU infrastructure: CUDA basics, multi-GPU training (DDP, FSDP), spot instance strategies
- [ ] [Full Stack LLM Bootcamp](https://fullstackdeeplearning.com/llm-bootcamp/)
- [ ] [Chip Huyen — Designing Machine Learning Systems](https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/)

### Practical Tools to Know
- [ ] Hugging Face: `transformers`, `datasets`, `peft`, `trl`
- [ ] LangChain / LlamaIndex — when useful, when to bypass them
- [ ] OpenAI / Anthropic APIs: streaming, function calling, batching, cost management
- [ ] Weights & Biases or MLflow for experiment tracking
- [ ] FAISS / pgvector for local vector search


## Apache Spark Learning Path

> Goal: production-grade Spark expertise — write efficient jobs, tune performance, own pipelines end-to-end.

### Spark Architecture Internals
- [ ] Driver vs executors, DAG scheduler, task scheduler
- [ ] Jobs, stages, tasks — how an action triggers a DAG
- [ ] Wide vs narrow dependencies — what causes a shuffle and why it matters
- [ ] Catalyst optimizer: logical plan → optimized logical plan → physical plan → code generation (Tungsten)
- [ ] [Spark: The Definitive Guide — Chambers & Zaharia](https://www.oreilly.com/library/view/spark-the-definitive/9781491912201/)
- [ ] [Databricks Academy — Apache Spark Developer](https://www.databricks.com/learn/training)

### Core APIs
- [ ] **RDD vs DataFrame vs Dataset**: know when RDD is still the right tool (custom partitioners, low-level control)
- [ ] DataFrame API: transformations (lazy) vs actions (eager), column expressions, schema evolution
- [ ] Dataset API (typed): encoder overhead, when to prefer DataFrame
- [ ] Spark SQL: pushdown predicates, partition pruning, view resolution
- [ ] UDFs: scalar vs vectorized (Pandas UDFs / Arrow), serialization cost, avoiding them when possible

### Scala for Spark
- [ ] Immutability, case classes, pattern matching, `Option`/`Either`/`Try`
- [ ] Higher-order functions: `map`, `flatMap`, `filter`, `fold`, `reduce`
- [ ] Implicits, type classes — understanding Spark's Encoder derivation
- [ ] SBT basics, dependency management, fat JAR assembly
- [ ] [Scala with Cats — Underscore.io (free)](https://underscore.io/books/scala-with-cats/)

### Performance Tuning
- [ ] **Partitioning**: default parallelism, `repartition` vs `coalesce`, custom partitioners, target partition size (~128–256 MB)
- [ ] **Shuffle tuning**: `spark.sql.shuffle.partitions` (adaptive with AQE), sort-merge vs broadcast join thresholds
- [ ] **Data skew**: salting, skew join hints, AQE skew handling, pre-aggregation
- [ ] **Broadcast joins**: when to force, broadcast variable lifecycle, size limits
- [ ] **Caching**: `cache()` vs `persist(MEMORY_AND_DISK)`, unpersist discipline, Kryo serialization
- [ ] **Small files problem**: compaction strategies, `coalesce` at write time, merge operations
- [ ] **Memory management**: on-heap vs off-heap (Project Tungsten), executor memory breakdown (`spark.memory.fraction`)
- [ ] **Reading the Spark UI**: timeline view, stage DAG, shuffle read/write bytes, GC time, executor logs
- [ ] [Spark Performance Tuning — Official Docs](https://spark.apache.org/docs/latest/tuning.html)

### File Formats and Storage
- [ ] Parquet: columnar storage, row groups, predicate pushdown, dictionary encoding, bloom filters
- [ ] ORC vs Parquet — when to use which
- [ ] Avro: schema evolution, Confluent Schema Registry integration
- [ ] **Delta Lake**: ACID transactions, time travel, `MERGE` (upsert), `OPTIMIZE` + `ZORDER`, `VACUUM`
- [ ] **Apache Iceberg**: hidden partitioning, partition evolution, snapshot isolation, catalog integration
- [ ] Lakehouse architecture: medallion (bronze/silver/gold), separating compute from storage (S3/GCS/ADLS)

### Batch Pipeline Design
- [ ] ETL/ELT patterns: ingestion, deduplication, SCD Type 1/2, enrichment, late data handling
- [ ] Idempotency: checkpoint-based restarts, overwrite vs append strategies, output deduplication
- [ ] Data quality: Great Expectations, Deequ, Spark constraints — gate deployments on DQ checks
- [ ] Metadata management: Hive Metastore, AWS Glue Catalog, Unity Catalog (Databricks)
- [ ] Pipeline observability: lineage tracking, row count checks, data freshness SLOs

### Structured Streaming
- [ ] Micro-batch vs continuous processing, trigger types (`Trigger.ProcessingTime`, `Trigger.Once`, `Trigger.AvailableNow`)
- [ ] Watermarks: late data tolerance, stateful aggregations, stream-stream joins
- [ ] Checkpointing and recovery: exactly-once semantics (with idempotent sinks)
- [ ] Kafka source/sink: offsets management, Kafka-Spark offset commit coordination
- [ ] Delta Lake as a streaming sink: `outputMode("append")` vs `"complete"`, change data feed
- [ ] [Structured Streaming Programming Guide](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html)

### Orchestration and Operations
- [ ] Airflow: DAG design, XComs, sensors, dynamic task mapping, backfill strategies
- [ ] Dagster: asset-based orchestration, partitions, software-defined assets
- [ ] Kubernetes-native Spark: `spark-on-k8s-operator`, dynamic resource allocation, pod templates
- [ ] Databricks: clusters (all-purpose vs job), Workflows, Delta Live Tables, Unity Catalog RBAC
- [ ] Job SLAs: alerting on duration regression, cost tracking per pipeline run


## Data Modeling and Warehousing

- [ ] OLTP vs OLAP access patterns — why row vs columnar matters
- [ ] Star schema vs snowflake vs one-big-table — trade-offs for query performance vs storage
- [ ] Slowly Changing Dimensions (SCD) Type 1/2/3 — implementation in Spark and Delta
- [ ] Partitioning strategy: date vs ID vs enum — cardinality, query patterns, compaction cost
- [ ] Materialized views, pre-aggregation, cube/rollup — reducing query latency at the cost of freshness
- [ ] dbt: models, tests, snapshots, macros, lineage graph, docs


## Interview Coding Practice (Senior Level)

At 7 years, interviews test problem decomposition, complexity reasoning, and communication — not memorization.

**Focus areas:**
- Graph problems: BFS/DFS, topological sort, shortest path, union-find (connected components)
- Tree problems: LCA, diameter, path sum, serialization/deserialization
- Sliding window, two pointers, monotonic stack
- Heap-based problems: k-largest, merge k sorted lists, median of data stream
- Interval problems: merge, insert, meeting rooms
- DP: state machine patterns, interval DP, digit DP
- Backtracking with pruning

**Practice platforms:**
- [ ] [LeetCode](https://leetcode.com/) — focus on Medium/Hard, company-tagged sets
- [ ] [NeetCode 150](https://neetcode.io/practice) — curated list with video explanations
- [ ] [AlgoExpert](https://www.algoexpert.io/) — good for structured walkthroughs

**Books:**
- [ ] [Cracking the Coding Interview, 6th Edition](http://www.amazon.com/Cracking-Coding-Interview-6th-Programming/dp/0984782850/) — Java answers, good for concept review


## Behavioral and Leadership Questions

Prepare 2–3 stories for each. Use STAR format. Have specifics: scope, impact, numbers.

- Describe a technically complex project you led end-to-end. What was your biggest design decision?
- Tell me about a time you disagreed with your team/manager on a technical direction. What happened?
- How have you handled a production incident? What was your role and what did you change afterwards?
- Describe a time you improved an existing system's reliability, performance, or maintainability.
- How do you approach mentoring engineers? Give an example where you raised someone's trajectory.
- Tell me about a time you drove alignment across teams with conflicting priorities.
- How do you decide when to incur technical debt vs. pay it down?
- Describe a project where you had to balance speed with correctness/scalability.

## Questions for the Interviewer

- What does the engineering org's on-call culture look like? How are incidents handled?
- How are technical decisions made — RFC process, ADRs, consensus-driven?
- What's the ratio of greenfield work vs. maintaining existing systems?
- How does the team measure engineering effectiveness? SLOs, deployment frequency?
- What's the biggest technical challenge the team is solving right now?
- What does the growth path look like from senior to staff/principal?
- How autonomous are engineers in choosing tools and tech stack?
- What does a great first 90 days look like in this role?

---

## Once You've Got The Job

Keep learning — but deliberately. Pick one area per quarter to go deep on, not broad on everything.

You're never really done.
