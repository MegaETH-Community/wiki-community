---
icon: money-from-bracket
---

# Transaction Lifecycle

When you click “Send” or “Confirm” in your wallet, you’re kicking off a **multi-step process** that involves various nodes in the network—each with a specific role. Below is an overview of how a typical transaction flows, from the user’s device all the way to final settlement on the blockchain.

***

### Putting It All Together: A Detailed Transaction Workflow

<figure><img src="../../.gitbook/assets/MEGAETH - USER TRANSACTION (1).PNG" alt=""><figcaption></figcaption></figure>

* **User (Wallet or dApp)**
  * You create a transaction (e.g., sending tokens, calling a contract function) and sign it with your **private key**.
  * This signature ensures authenticity and prevents tampering.
* **RPC Node**
  * **Receives** the signed transaction from the user. The RPC node serves as the entry point to the network.
  * **Relays** the transaction to other nodes in the network, such as the sequencer or validator nodes.
  * Provides **API endpoints** for wallets and dApps, allowing users to interact with the blockchain without running a node themselves.
  * Could be a full node or a lighter replica node.
* **Leader**
  * The leader **orders** the incoming transactions, determining their sequence.
  * It executes them in an **EVM** (or equivalent execution environment), updating the state as it goes.
  * A **proposed block** is then assembled, containing the ordered transactions and a **state commitment** (e.g., the state root—a cryptographic fingerprint that represents the entire updated state).
  * The leader **broadcasts** the proposed block to other validator nodes.
* **Network Nodes (full or replica node)**
  * These nodes **verify** the transactions in the block (e.g., check signatures, ensure no double-spends).
  * They then **vote** on whether to accept the block. If the network agrees the block is valid, it becomes part of the chain.
  * Upon receiving an approved block, each node replays (or verifies) the transactions to confirm the state changes.
  * They update their **local copy** of the blockchain’s state (e.g., balances, contract data).
* **RPC Nodes Synchronize (**[State Sync](state-sync-and-gas-limits.md)**)**
  * As **full nodes** and **replica nodes** update their state. This allows them to serve up-to-date information to users and dApps, including updated balances, contract outputs, and the latest blockchain state.
* **Final Settlement (L2 only)**
  * In a Layer-2 context, periodic **state commitments** or **proofs** are submitted to an L1 (like Ethereum) to ensure trust-minimized security.
  * This step provides an extra layer of safety: if the L2 fails or acts maliciously, the L1’s data can be used to resolve disputes or recover funds.

***

**Result:**\
By the end of this process, all nodes in the network have an identical, updated view of the blockchain’s state, and your transaction is finalized.
