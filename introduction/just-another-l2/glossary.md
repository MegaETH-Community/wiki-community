---
icon: book
---

# Glossary

#### **Consensus (Sequencing)**

* **Definition:** The process of collecting users’ transactions and determining their order for execution.
  * **Ordering**: Determines the exact sequence in which transactions are processed.
  * **Batching**: Groups multiple transactions into a single batch.

***

#### **Execution**

* **Definition:** The process of executing transactions in the defined order to calculate the blockchain state, such as account balances and storage.
  * **Re-execute**: Recalculates the same transaction without modifications to verify its correctness.

***

#### **Key Metrics**

* **TPS (Transactions Per Second):** A measure of the blockchain’s throughput, indicating how many transactions can be processed in one second.
* **Latency:** The time taken for a transaction to be processed and confirmed by the network.

***

#### Key Terms

* **Liveness:** The property that ensures the system continues to make progress (e.g., transactions are eventually processed). A blockchain with liveness guarantees will not halt indefinitely. In essence, it ensures that the system eventually completes operations and does not remain stuck or idle indefinitely.
* **Consistency:** The property that ensures all participants in the network share the same vision of the blockchain at any given moment. In other words, all nodes agree on the same state and history of transactions, preventing divergent or conflicting views.
* **Trustless**: A characteristic of blockchain systems where participants can interact and transact without needing to trust one another or a central authority. Security is maintained by the protocol.
* **Finality**: The assurance that a transaction, once confirmed, cannot be reversed or altered. Different blockchains may have probabilistic or deterministic finality.
* **Scalability**: The ability of a blockchain to handle increased transaction throughput as demand grows, without compromising performance.
* **Latency**: The time it takes for a transaction to be processed and confirmed by the network. Lower latency is crucial for real-time applications.
* **Throughput**: The number of transactions a blockchain can process in a given time period, typically measured in transactions per second (TPS).
* **Fork**: A divergence in the blockchain where two or more competing chains exist temporarily or permanently, often due to differing consensus or upgrades.
* **Gas**: The computational cost required to execute transactions or smart contracts on a blockchain. Fees are usually paid in the network’s native token.
* **State**: The current snapshot of the blockchain, including all account balances, storage, and contract states.

***

**Additional Concepts**

* **Witnesses:** Additional data required to verify transactions or validate a state without reloading the entire blockchain. Witnesses enable lightweight and efficient validation processes.
* **State Diff:** The calculated difference in blockchain state after executing transactions. In Ethereum, the **state diff** is managed by the EVM (Ethereum Virtual Machine) and involves calculating changes to account balances, storage, and other states. The **gas mechanism** in the EVM ensures efficient usage of computational resources by requiring transaction fees based on complexity.
* **State Sync:** A process that synchronizes full nodes with the sequencer to bring them up to date with the latest blockchain state.
* **Real-Time Blockchain:** Processes transactions as soon as they arrive and immediately publishes the results, minimizing delays.
