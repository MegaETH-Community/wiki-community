---
icon: road-bridge
---

# Infrastructure

MegaETH solved the slow-chain problem. Next is the slow-infra problem. Oracles, indexers, apps—real-time chains demand innovation on traditional tools before users can _feel_ real-time.

### The Infrastructure Challenge

Traditional blockchain infrastructure assumes multi-second block times:

* **RPCs** poll for receipts every few seconds
* **Indexers** batch process blocks periodically
* **Oracles** update prices on minute intervals
* **Apps** show "pending" states for seconds

With 10ms blocks and instant execution, this infrastructure becomes the bottleneck. Users won't feel real-time performance if the tools can't keep up.

***

### Realtime API

MegaETH's extension to Ethereum JSON-RPC optimized for sub-10ms latency.

**Core Innovation**: Query against mini-blocks, not EVM blocks

* Transactions reflected within 10ms of arrival
* State changes visible immediately
* Full preconfirmation guarantees maintained

**Enhanced Methods**:

* **State queries** (`eth_getBalance`, `eth_call`, etc.):
  * Return results up to most recent mini-block
  * Use `pending` or `latest` tag for real-time data
  * 100x faster state visibility vs waiting for EVM blocks
* **Transaction queries** (`eth_getTransactionReceipt`):
  * See transactions as soon as mini-block includes them
  * No more waiting for next EVM block
  * Receipt available in \~10ms
* **WebSocket subscriptions** (`eth_subscribe`):
  * **Logs**: Stream as transactions execute
  * **State changes**: Monitor account updates in real-time
  * **Fragments**: Subscribe to mini-block stream

**Example timeline**:

* 0ms: Transaction sent
* 10ms: Included in mini-block, visible in Realtime API
* 1000ms: Included in EVM block (traditional visibility)

**Full specification**: [https://docs.megaeth.com/realtime-api](https://docs.megaeth.com/realtime-api)

***

### realtime\_sendRawTransaction

Revolutionary RPC method that bundles send + receipt in one call.

**Problem it solves**:

* Traditional flow: Send tx → Poll for receipt → Multiple round trips
* Polling wastes time between checks
* Too frequent polling overloads infrastructure
* Like checking mailbox every 10 minutes vs getting notification

**How it works**:

* Send transaction to sequencer
* Sequencer executes immediately (<10ms)
* Returns receipt in same response
* One RPC call for entire flow

**Benefits**:

* **Zero polling overhead**
* **Minimal latency** (network + 10ms execution)
* **Simple integration** (drop-in replacement)
* **Better DevEx** (no subscription management)

**Implementation**:

```json
// Traditional (multiple calls)
1. eth_sendRawTransaction → returns hash
2. eth_getTransactionReceipt (poll) → null
3. eth_getTransactionReceipt (poll) → null
4. eth_getTransactionReceipt (poll) → receipt
// MegaETH (single call)
1. realtime_sendRawTransaction → returns receipt
```

**Technical breakdown**: [https://x.com/yangl1996/status/1913241582700015914](https://x.com/yangl1996/status/1913241582700015914)

***

### Paginated Reads

Robust API for processing massive chain data efficiently.

**The data scale problem**:

* MegaETH testnet: 1000 TPS sustained
* Generates 1 year of Ethereum data every 5 days
* Traditional RPCs timeout on large queries
* Apps forced to break queries into tiny chunks

**Pagination solution**:

* **Partial results**: Return what's processed before limits hit
* **Resume pointers**: Continue exactly where query stopped
* **No wasted work**: Every computation counts
* **Optimal round trips**: Minimize network overhead

**Example use case**: Query 1M blocks of logs:

* **Without pagination**:
  * Query fails at 300k blocks
  * Retry with smaller range
  * Start from scratch each time
  * Unreliable, slow, complex
* **With pagination**:
  * First call returns 300k blocks + pointer
  * Second call continues from block 300,001
  * Zero wasted computation
  * Predictable, fast, simple

**Benefits for builders**:

* **Indexers**: Efficient backfilling after downtime
* **Analytics**: Process entire chain history
* **Dashboards**: Load large datasets reliably
* **Infrastructure**: Handle data at scale

**Details**: [https://x.com/yangl1996/status/1924812272679129421](https://x.com/yangl1996/status/1924812272679129421)

***

#### Real-Time Oracles

Traditional oracles update prices on minute intervals. MegaETH needs something radically faster.

**RedStone Integration:**

MegaETH partnered with RedStone to build the **fastest push oracle to date**, updating onchain every **2.4ms**.

* **416 oracle updates per second** - in an industry where most chains run at double-digit TPS
* Price data refreshed 250x faster than traditional oracle models
* Enables new categories of DeFi applications requiring instant price feeds
* Real-time capital markets, high-frequency trading strategies, and instant liquidations become viable

This is infrastructure innovation matching chain performance - where oracles keep pace with 10ms blocks instead of becoming the bottleneck.

[Announcement](https://x.com/megaeth/status/1909614320755130514)

***

### Infrastructure Roadmap

**Current (Testnet)**:

* ✅ Realtime API with mini-block queries
* ✅ realtime\_sendRawTransaction
* ✅ Paginated reads for logs
* ✅ WebSocket subscriptions
* ✅ Sub-millisecond oracles

**Coming Soon**:

* Extended pagination (traces, state)
* Batch transaction submission
* Priority transaction lanes
* Historical state queries at mini-block level

**Future Vision**:

* Streaming indexers
* Real-time analytics
* Instant cross-chain messaging

The infrastructure revolution is just beginning. As MegaETH pushes blockchain performance to new limits, expect innovative tools and services that reimagine what's possible in Web3.
