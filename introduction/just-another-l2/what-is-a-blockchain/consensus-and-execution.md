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

# Consensus & Execution

Blockchains rely on two fundamental processes: **consensus** and **execution**. These mechanisms ensure the network operates securely, efficiently, and without relying on a central authority.

1. **Consensus:** How nodes agree on the next block to add to the chain.
2. **Execution:** How the transactions within those blocks update the blockchain's global state.

Understanding these components is essential to grasp both the strengths and limitations of Layer-1 (L1) networks and how Layer-2 (L2) solutions like MegaETH enhance scalability and performance.

***

### Consensus: Agreeing on the Next Block

Consensus protocols are responsible for validating transactions, determining their order, and adding new blocks to the blockchain. While the specifics vary across protocols, the process generally follows these steps:

1. **Transaction Ordering:**\
   A designated **leader node** (e.g., a miner or validator) organizes pending transactions into a block. This leader may be chosen based on computational effort (Proof of Work) or stake (Proof of Stake).
2. **Block Proposal:**\
   The leader proposes the block to the network, which includes the ordered transactions.
3. **Validation and Agreement:**\
   Other nodes verify the validity of the block (e.g., ensuring no double-spending) and agree on its inclusion through the consensus mechanism. If the block meets the network's rules, it is added to the chain.

Finding consensus and designating a leader in Proof of Stake is a complex challenge. The protocol must achieve **Byzantine Practical Fault Tolerance (BPFT)**, meaning it can tolerate up to one-third of nodes being malicious. However, no consensus algorithm is perfectly reliable. In practice, modern blockchain security heavily relies on staking, as validators are financially disincentivized to act maliciously.

***

### Execution: Updating the State

After a block is finalized through consensus, each node processes the block’s transactions in order, **updating** their local copy of the blockchain’s “**state**” (e.g., account balances, contract data). This ensures that all nodes maintain an identical view of the network. The process can be understood as follows:

1. **State:** The blockchain’s current data, including accounts, balances, and contract storage.
2. **Transactions:** Requests to modify that state, such as sending tokens or invoking smart contracts.
3. **Execution Environment:** The system enforcing transaction logic and applying changes to the state. For example, the **Ethereum Virtual Machine (EVM)** processes transactions and updates the state accordingly.

In most L1s (like Ethereum), **every node** participates in both consensus and full execution.

***

### Why Is This a Bottleneck?

* **Redundancy**: Every node repeats the same calculations, which ensures trustlessness but caps overall throughput.
* **Hardware Constraints**: If you raise block size or transaction throughput too high, you risk pricing out smaller nodes (they can’t keep up), reducing **decentralization**.

***

### **Innovations in Execution: Layer 2 and Beyond**

To address the bottlenecks inherent in Layer-1 networks, Layer-2 (L2) solutions rely on **task specialization**. This approach improves efficiency and throughput while leveraging the security guarantees of the underlying Layer-1 (L1) blockchain.

**How It Works in Layer 2**

1.  **Sequencer:**\
    The sequencer is a highly centralized and powerful node responsible for:

    * Ordering and executing transactions efficiently.
    * Publishing a block.

    While centralized, this approach is viable because the **security of the L2 is anchored to the L1**, which validates the correctness of the sequencer’s outputs.
2. **Verification by Nodes:**\
   All nodes on the L2 re-execute the transactions ordered by the sequencer to:
   * Update their local state.
   * Verify the sequencer’s work and ensure no errors or malicious behavior occurred.
3. **Batch Commitments:**\
   The sequencer periodically submits a batch of transactions and the resulting state changes to the L1. This ensures the L2 inherits the trust and immutability of the L1.

**MegaETH** introduces an innovation to this model by further optimizing execution: The sequencer directly publishes the **state diff**, allowing other nodes to skip redundant execution. Nodes simply update their local state based on the diff.
