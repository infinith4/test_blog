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
