---
icon: fire-flame-simple
---

# State Sync & Gas Limits

Even if a blockchain **orders transactions** and **executes** them efficiently, keeping **all nodes synchronized** and maintaining stability through **gas limits** are critical for high-performance networks like MegaETH. Let’s explore how these mechanisms work together to ensure a decentralized yet scalable system.

***

### State Synchronization: Keeping Full Nodes Up to Speed

As transaction throughput rises, synchronizing the **full state** across the network becomes a **major challenge**. Here’s why:

1. **Frequent Updates**
   * High-performance blockchains, including MegaETH, can process a large number of transactions within a very short timeframe.
   * Each transaction modifies the global state (balances, contract storage, etc.), so nodes need continuous, near-real-time updates.
2. **Authenticated Structures**
   * Blockchains use **authenticated structures** like Merkle Patricia Tries to organize and secure state data.
   * After each block, a **new state root** (hash) must be computed and shared, so light clients (**replica nodes**) and external verifiers can trust the updated state without downloading it fully.
   * **Full nodes**, on the other hand, re-execute transactions to independently compute and validate the state root, ensuring the network’s security and integrity.
3. **Full Node Responsibility**
   * **Full nodes** maintain the complete blockchain history and the current state.
   * They also serve **new or lagging nodes**, helping them quickly **“catch up”** if they go offline or join the network later. This is known as **state sync**.
4. **Bandwidth & I/O Constraints**
   * Higher transaction throughput means larger and more frequent state updates.
   * Synchronizing this data across the network requires significant bandwidth and storage.
   * Without optimizations like parallel execution or write-optimized storage, nodes with limited hardware might struggle to keep up.

***

### Gas Limits: The Network’s Speed Governor

No matter how well a blockchain **orders** and **executes** transactions, it’s ultimately constrained by the **block gas limit**—the maximum amount of “work” (gas) allowed in a single block. Along with block time, this acts as a **throttling mechanism**.

1. **Why Have a Gas Limit?**
   * **Security**: Ensures that any block can be fully processed within the block interval. If blocks are too large or come too fast, nodes with standard hardware might be overwhelmed, leading to centralization.
   * **Reliability**: Prevents malicious actors from creating blocks so massive that the network can’t validate them in time.
2. **Block Time & Gas Limit**
   * **Block Time**: The interval at which new blocks are proposed (e.g., 2 seconds, 10 seconds, etc.).
   * **Gas Limit**: The amount of computational work or data allowed per block.
   * Together, these two parameters **define the upper bound** of a blockchain’s throughput.
3. **Bottleneck for High Throughput**
   * Even if you optimize execution (e.g., specialized node roles, parallel processing), you **can’t exceed** what the block gas limit permits in a single block interval.
   * To safely raise this limit, the network must ensure that **every node** can handle the worst-case scenario, preserving **decentralization**.
4. **MegaETH’s Approach**
   * Through **hardware-level optimizations**, **efficient state sync**, and **concentrated execution**, MegaETH can safely push block times and gas limits much higher than most L2s.
   * **Sub-10ms block times** and **>10G gas/second** capacity are possible precisely because the protocol and infrastructure are **designed** to handle heavier blocks without sacrificing node diversity.

***

### Why It Matters

* **State Sync** is essential for maintaining a healthy, permissionless network where anyone can join and catch up, ensuring **transparency** and **trustlessness**.
* **Gas Limits** serve as a critical safety feature, preventing runaway block sizes that could break the network or centralize it among powerful nodes only.
