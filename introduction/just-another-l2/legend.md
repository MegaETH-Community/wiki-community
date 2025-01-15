---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Legend

#### **Consensus (Sequencing)**

The process of collecting users’ transactions and determining their order for execution.

* **Ordering**: Determines the exact sequence in which transactions are processed.
* **Batching**: Groups multiple transactions into a single batch.

***

#### **Execution**

The process of executing transactions in the defined order to calculate the blockchain state, such as account balances and storage.

* **Re-execute**: The process of recalculating the same transaction without modifications to verify its correctness.

***

#### Key Terms

* **Liveness**: The property that ensures the system continues to make progress (e.g., transactions are eventually processed). A blockchain with liveness guarantees will not halt indefinitely.
* **Trustless**: A characteristic of blockchain systems where participants can interact and transact without needing to trust one another or a central authority. Security is maintained by the protocol.
* **Finality**: The assurance that a transaction, once confirmed, cannot be reversed or altered. Different blockchains may have probabilistic or deterministic finality.
* **Scalability**: The ability of a blockchain to handle increased transaction throughput as demand grows, without compromising performance.
* **Latency**: The time it takes for a transaction to be processed and confirmed by the network. Lower latency is crucial for real-time applications.
* **Throughput**: The number of transactions a blockchain can process in a given time period, typically measured in transactions per second (TPS).
* **Fork**: A divergence in the blockchain where two or more competing chains exist temporarily or permanently, often due to differing consensus or upgrades.
* **Gas**: The computational cost required to execute transactions or smart contracts on a blockchain. Fees are usually paid in the network’s native token.
* **State**: The current snapshot of the blockchain, including all account balances, storage, and contract states.
