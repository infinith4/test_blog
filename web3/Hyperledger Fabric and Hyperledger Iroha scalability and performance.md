Hyperledger Fabric and Hyperledger Iroha are both blockchain frameworks under the Hyperledger umbrella, each designed with different features and use cases in mind. Here’s a comparison of their scalability and performance based on recent studies and experiments:

### Hyperledger Fabric

1. **Architecture**: Hyperledger Fabric is designed with a modular architecture that allows for plug-and-play components. It separates the transaction processing workflow into three phases: execute, order, and validate, which helps in optimizing performance and scalability.
2. **Performance Metrics**:
   - **Throughput**: A study found that Hyperledger Fabric can achieve a maximum throughput of around 3,000 transactions per second (TPS) under optimal conditions with a simple transaction model and sufficient resources【22†source】【24†source】.
   - **Latency**: The average transaction latency in Hyperledger Fabric tends to increase as the system reaches peak throughput. For example, the latency can rapidly increase beyond 3 seconds under high load conditions【22†source】.
   - **Scalability**: Fabric scales well with the number of nodes and channels. Experiments have demonstrated that a network with 128 peer nodes and 325 channels can achieve an aggregate throughput of approximately 13,000 TPS, showing minimal performance degradation per channel as the number of channels increases【24†source】.

### Hyperledger Iroha

1. **Architecture**: Hyperledger Iroha is designed to be simple and easy to incorporate into various projects. It uses a unique consensus algorithm called YAC (Yet Another Consensus), which aims to provide high fault tolerance and fast finality.
2. **Performance Metrics**:
   - **Throughput**: Hyperledger Iroha generally achieves lower throughput compared to Fabric, typically around several hundred TPS. This is due to its simpler consensus mechanism and focus on ease of use and integration【23†source】.
   - **Latency**: Iroha’s latency is competitive for smaller-scale deployments, providing rapid transaction finality suitable for applications that do not require extremely high throughput【23†source】.
   - **Scalability**: While Iroha is scalable to an extent, its design prioritizes ease of deployment and integration over high scalability. It is ideal for smaller networks or specific use cases where simplicity and quick finality are more critical than handling thousands of transactions per second【23†source】.

### Conclusion

- **Scalability**: Hyperledger Fabric generally offers better scalability than Hyperledger Iroha, making it suitable for large and complex networks with high transaction volumes.
- **Performance**: Hyperledger Fabric can handle a higher throughput and more complex transaction workflows, whereas Hyperledger Iroha excels in simplicity and ease of integration with moderate performance capabilities.

For specific details and performance benchmarks, you can refer to the respective technical documentation and performance evaluation studies of both Hyperledger Fabric and Hyperledger Iroha.



------



### Hyperledger Fabric vs. Hyperledger Iroha: Scalability and Performance

#### Hyperledger Fabric v2.5

**Performance Benchmarks:**
- **Transactions Per Second (TPS):** Hyperledger Fabric 2.5 achieved approximately 3,000 TPS in a controlled benchmark environment.
- **Latency:** Average latency for transaction confirmation was around 0.35 seconds.
- **Hardware and Topology:** Tests were conducted with two peer organizations, each with one peer node, and a single orderer service node. All nodes were running on Intel Xeon Silver 4210 CPUs with 40 cores and 64GB of RAM.
- **Configuration:** The system utilized LevelDB for state storage, TLS for security, and the peer Gateway service for transaction processing. The block cutting parameters were set to a block time of 2 seconds and a block size of 500 transactions【32†source】【34†source】.

#### Hyperledger Iroha v2

**Performance Benchmarks:**
- **Transactions Per Second (TPS):** Hyperledger Iroha v2 showed a TPS of around 1,500 in similar controlled environments.
- **Latency:** The average transaction confirmation latency was approximately 0.5 seconds.
- **Hardware and Topology:** Similar to Fabric, Iroha was tested on a network with multiple nodes, each running on comparable hardware configurations (e.g., Intel Xeon CPUs, 32-64GB of RAM).
- **Configuration:** Iroha’s consensus mechanism is YAC (Yet Another Consensus), optimized for high throughput and quick finality, suitable for use cases requiring fast and frequent updates【35†source】.

### Key Differences

1. **Consensus Mechanism:**
   - **Fabric:** Uses a pluggable consensus mechanism with Raft being commonly used, which can support high throughput and is configurable for various use cases.
   - **Iroha:** Utilizes YAC, designed for high-speed consensus and quick transaction finality, ideal for applications needing frequent updates.

2. **Network Complexity:**
   - **Fabric:** Supports complex network topologies with multiple roles such as endorsing peers, orderers, and validating peers, allowing for detailed control over transaction processing and validation.
   - **Iroha:** Simplified architecture with a focus on ease of use and straightforward node roles, making it easier to set up and maintain but potentially less flexible for complex scenarios.

3. **Performance Scalability:**
   - **Fabric:** Generally shows higher scalability with its ability to handle a larger number of transactions per second and lower latency, attributed to its robust and configurable infrastructure.
   - **Iroha:** Offers competitive performance but is slightly less scalable compared to Fabric, making it suitable for medium-scale applications where simplicity and ease of integration are more critical.

For more detailed information on specific performance metrics and benchmarking methodologies, you can refer to the [Hyperledger Fabric documentation](https://www.hyperledger.org/resources/publications/white-paper-fabric-performance) and the [Hyperledger Iroha performance testing results](https://wiki.hyperledger.org/display/iroha/Performance+testing)【32†source】【33†source】【34†source】【35†source】.


https://www.hyperledger.org/blog/2023/02/16/benchmarking-hyperledger-fabric-2-5-performance
https://hyperledger.github.io/caliper/
https://wiki.hyperledger.org/display/iroha/Performance+testing
https://www.hyperledger.org/learn/publications/blockchain-performance-metrics
