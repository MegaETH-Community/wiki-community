---
icon: ethereum
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

# EVM Optimization

Modern hardware is highly capable of supporting blockchain workloads at an incredible scale. However, software inefficiency prevents execution clients from fully utilizing these resources.

***

### Hardware Capabilities vs. Current Blockchain Performance

To illustrate, let’s break down the performance potential of the three primary hardware resources: **computing power**, **disk I/O**, and **network bandwidth**.

*   **Computing Power:**

    Executing transactions is fundamentally a computational task. CPUs process instructions to execute smart contracts and update the blockchain state.

    * **Current Capability**:\
      Modern EVM interpreters like **evmone** can process over **100,000 ERC-20 transfers per second** on a single CPU core. Even more computationally intensive tasks, such as token swaps, achieve over **6,000 swaps per second per core**.
    * **Scaling Potential**:\
      Almost all CPUs today have multiple cores. This means that, with proper software parallelization, the throughput of a blockchain could scale **linearly with the number of cores available**. For example, on a 16-core CPU, the potential transaction throughput would exceed **1.6 million ERC-20 transfers per second**.
*   **Disk I/O**

    Blockchain transactions update the state, and these updates must be written to disk efficiently. Disk performance plays a pivotal role in determining the upper limit of throughput.

    * **Current Capability**:\
      Modern **NVMe SSDs** can handle more than **300,000 random writes per second**. With this level of performance, the storage system could easily handle **150,000 ETH transfers per second**.
    * **Scaling Potential**:\
      Storage capacity is not limited to a single SSD. Adding more SSDs to a system can proportionally increase its Input/Output Operations Per Second (IOPS), allowing even higher transaction throughput.
*   **Network Bandwidth**

    State updates must be propagated across the network for nodes to stay synchronized. Bandwidth determines how quickly and efficiently these updates can be shared.

    * **Current Capability**:\
      Each state update can be encoded in about **20 bytes**. A **100 Mbps network connection** can theoretically support **625,000 state updates per second**, which translates to approximately **312,500 ETH transfers per second**.
    * **Scaling Potential**:\
      High-speed network connections (e.g., 1 Gbps or higher) can scale this capacity even further, enabling millions of updates per second across distributed systems.
    * However, these theoretical limits come with **practical challenges.** For example, assuming a sustainable bandwidth of **75 Mbps**, and reserving two-thirds of it for other activities, only **25 Mbps** remains available for state sync. Under these conditions, syncing **100,000 Uniswap swaps per second**, which normally requires **476 Mbps**, would demand a **19x compression rate** for state diffs to ensure feasibility.

    When combined, the theoretical limits of modern hardware suggest that even a modestly equipped server could achieve over **100,000 transactions per second (TPS)**. This makes it clear that **hardware is not the bottleneck**—it is the **software inefficiency** that limits blockchain performance today. Unlocking this potential requires optimizing the execution environment to leverage the full power of existing computing infrastructure.

***

### Software Optimization

To address this, we focus on three critical areas: **High Transaction Throughput (HTT)**, **Abundant Compute Capacity (ACC)**, and **Millisecond-Level Response Times (MLRT)**.

***

#### **High Transaction Throughput (HTT)**

*   **Efficient State Root Updates**

    The **state root** is a cryptographic summary of blockchain data stored in a **Merkle Patricia Trie (MPT)**. It ensures data integrity and enables light clients to verify changes using storage proofs. However, updating the state root is a major bottleneck, consuming over **90% of block production time** in Reth experiments.

    * **Challenges**:
      * **Excessive Disk I/O**: Updating the state root involves traversing the MPT, reading and writing several internal nodes to recompute hashes.
        * Example: A binary MPT with **1 TB of state** requires \~20 disk reads and \~10 writes per updated key.
        * For **100,000 ERC-20 transfers/second**, this results in **6M database reads/second**, exceeding SSD capabilities.
      * **Scalability Limits**: Current trie structures struggle with terabyte-scale states, especially under high transaction throughput.
      * **Software Overheads**: Even optimized approaches (e.g., grouping nodes into disk pages) fall short of desired performance.
    *   **Solution: A New State Trie**:

        * **Minimal Disk I/O**: Groups multiple trie nodes, reducing random reads and writes to the absolute minimum.
        * **Scalability**: Handles terabyte-scale blockchain states efficiently, even with limited RAM.
        * **Light Client Support**: Maintains compatibility with storage proofs for decentralized validation.

        → For detailed implementation, see our [QMDB solution in Technical Solutions](technical-solutions.md#qmdb-solving-state-root-updates)


*   **In-Memory Computing**

    Eliminates reliance on disk operations by storing the entire blockchain state in RAM. This approach significantly improves performance and removes the latency associated with fetching data from disk.

    * **Challenges**:
      * Fetching account or contract states with opcodes like **SLOAD** introduces delays when the required data is not already in memory.
        * **Disk Latency**: SSD access takes \~100 microseconds, making it **10,000x slower** than most opcode operations.
        * Unlike systems like Solana, EVM cannot prefetch required states due to the unpredictable nature of transactions.
    * **Solution**:
      * MegaETH leverages **large RAM capacities** in high-performance servers to store the entire blockchain state in memory.
        * Example: Current server CPUs support up to **4 TB of RAM**, while Ethereum's state is only \~100 GB.
        * Upcoming technologies like **Compute Express Link (CXL)** will increase RAM capacity by over **10x**, allowing states 40x larger than Ethereum’s to fit in commodity servers.
    * **Benefits**:
      * Removes the need for disk I/O during transaction execution.
      * Significantly boosts transaction throughput by fully utilizing available RAM.
      * Brings **Web2-inspired technology** to Web3, enabling the first generation of **data-intensive decentralized applications (dApps)**.

***

#### **Abundant Compute Capacity (ACC)**

*   **Bytecode Compilation**

    Interpreting EVM bytecode introduces significant overhead, slowing execution by up to **1000x compared to native code**. To address this bottleneck, **Just-In-Time (JIT) compilation** is used to convert bytecode into machine-native instructions.

    * **Challenges**:
      * **High Runtime Overhead**: EVM execution involves decoding bytecode, managing the stack, performing operations (e.g., arithmetic), and handling gas deductions.
        * Example: A simple **ADD** operation involves multiple memory accesses, stack adjustments, and conditional jumps, making it inefficient.
      * **Current Limitations**: While tools like **evmone** achieve >6,000 token swaps/second on a single core, this is still far from the native performance needed for compute-intensive applications.
      * **Limited Impact on Certain Contracts**: Non-compute-intensive operations (e.g., `keccak256`, `sload`, `sstore`) already optimized in Rust see marginal benefits from JIT.
    *   **Solution**:

        * Implemented **JIT Compilation**: Converts EVM bytecode into native machine code at runtime.
          * Eliminates interpretation overhead, reducing CPU instructions to the bare minimum.
          * Delivers near **bare-metal performance** for compute-heavy contracts.

        → See [JIT Compilation details in Technical Solutions](technical-solutions.md#jit-compilation-unlocking-compute-performance)
    * **Benefits**:
      * **Up to 100x Speedup**: Contracts like Uniswap swaps experience significant improvements, enabling execution that was previously impractical.
      * **Unlocks Compute-Intensive dApps**: Facilitates a new generation of applications requiring heavy computation, such as advanced financial models or gaming logic.
    *   **Considerations**:

        * **Gas Model Adjustments**: Compilation introduces overheads (e.g., CPU cycles, memory usage) that are not reflected in the current gas pricing.
        * **Workload Dependency**: Compute-heavy contracts benefit most, while simpler contracts see only modest gains.


* **Write-Optimized Storage Backend**
  * **Problem:** High write amplification and single-writer locks in existing databases (e.g., MDBX) lead to poor write performance.
  *   **Solution:**

      * Revamped the storage backend to:
        * Optimize write performance.
        * Maintain predictable read latencies.
      * Enables handling of extremely high state update rates while supporting higher block gas limits.

      → See [Write-Optimized Storage details in Technical Solutions](technical-solutions.md#write-optimized-storage-backend)

***

#### **Millisecond-Level Response Times (MLRT)**

*   **Two-Pronged Parallel Execution**

    Parallel EVM ensures that blockchain workloads can efficiently utilize multi-core CPUs by dividing strategies for **block production** and **block validation**. This approach resolves the limitations of existing parallel execution methods while maximizing performance.

    * **Challenges**:
      * **Limited Parallelism**:
        * Recent Ethereum blocks show a **median parallelism of less than 2**, with long dependency chains limiting opportunities for concurrent execution.
        * Even with advanced techniques like Block-STM, **contentious workloads** can lead to cascading aborts, reducing efficiency and sometimes making sequential execution faster.
      * **Deterministic Concurrency Control (CC)**:
        * Protocols like Block-STM guarantee consistency but cannot prevent cascading aborts, making them unsuitable for highly contentious workloads.
    *   **Solution: Two-Pronged Approach**:

        1. **Block Production**:
           * MegaETH’s centralized sequencer can leverage **non-deterministic CC algorithms** that:
             * Are simpler to implement.
             * Scale to 100s of cores.
             * Avoid cascading aborts entirely.
        2. **Block Validation**:
           * Full nodes use **stateless validation**, executing blocks in parallel without risking state contention.
           * This ensures that validation workloads can fully benefit from available hardware resources.

        → For implementation details, see [Two-Pronged Parallel Execution in Technical Solutions](technical-solutions.md#two-pronged-parallel-execution)
    *   **Benefits**:

        * **Maximized Parallel Speedup**: By optimizing both production and validation workflows, the system avoids bottlenecks seen in deterministic approaches.
        * **Scalability**: The unique node specialization architecture of MegaETH allows sequencers to utilize **100+ cores**, unlocking the full potential of modern server hardware.
        * **Future-Ready**: Adopting the latest advancements in database concurrency ensures compatibility with future hardware innovations and workload demands.


*   **Efficient State Sync**

    State sync ensures full nodes remain synchronized with the blockchain's latest state. This is particularly challenging in high-performance blockchains, where the volume of updates can strain bandwidth and system resources.

    * **Challenges**:
      * **High Bandwidth Requirements**:
        * A simple ERC-20 transfer modifies three values, requiring **200 bytes per transaction**. At **100,000 transfers/second**, this translates to **152.6 Mbps** of bandwidth.
        * Complex transactions like Uniswap swaps, modifying multiple storage slots, can require **624 bytes each**, pushing bandwidth consumption to **476 Mbps**.
      * **Network Limitations**:
        * Sustainable bandwidth for many nodes is lower than advertised (e.g., \~75 Mbps in practice).
        * Connections must share bandwidth with other applications and reserve headroom for bootstrapping new nodes.
        * Peer-to-peer protocols introduce additional overheads, reducing effective utilization.
    *   **Solution**:

        * **Custom Networking Protocol**: Optimized for **low-latency** and **high-throughput synchronization**.
        * **Novel Compression Techniques**: Reduce the size of state diffs to fit within limited bandwidth (e.g., **19x compression** for syncing 100,000 Uniswap swaps/second within **25 Mbps**).
        * **Scalable Design**: Allows even low-cost, low-bandwidth nodes to stay synchronized with the network.

        → Learn more about our [State Sync Compression in Technical Solutions](technical-solutions.md#state-sync-compression-solving-bandwidth-limits)
    * **Benefits**:
      * Maintains **100,000 TPS synchronization** even under constrained network conditions.
      * Ensures new nodes can join and catch up quickly to the latest blockchain state.


*   **Streaming EVM**

    Introduces a **co-designed pipeline** for real-time transaction processing, operating asynchronously with key components like the **storage backend** and **state trie**.

    *   **Core Features**:

        * Processes transactions continuously, emitting results in real time.
        * Achieves **1-ms block times** for fast transaction propagation and low-latency communication.

        → See the [mini-blocks implementation](technical-solutions.md#mini-blocks-enabling-real-time-blockchain) enabling 10ms block times (targeting 1ms).
    * **User Experience and Infrastructure**:
      * Users rely on **RPC nodes** and web frontends (e.g., **etherscan.io**) to interact with the blockchain.
      * Supporting infrastructure must:
        * Efficiently handle high read volumes during peak times.
        * Propagate transactions quickly to sequencer nodes.
        * Update application views in real time to match chain speed.
    * **Impact**:
      * Combines real-time processing with robust infrastructure to ensure a seamless experience, even under high transaction loads.

***

**MegaETH** unites these optimizations in a **single integrated framework**, harnessing every ounce of hardware capability to deliver **real-time blockchain performance**. Coupled with node specialization and robust consensus anchoring on Ethereum, MegaETH offers a next-gen environment where **100,000+ TPS** and **sub-10ms response times** become the new normal.
