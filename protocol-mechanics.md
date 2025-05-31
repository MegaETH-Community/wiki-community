---
icon: gears
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

# Protocol Mechanics

Core mechanisms ensuring MegaETH's security, reliability, and economic sustainability.

### Fee Model

MegaETH is designing an "original" approach to sequencer revenue distribution:

* **Current state**: Sequencer collects ETH from transaction fees
* **Options being considered**:
  * Token buyback (benefits MegaETH holders)
  * Ecosystem funding (supports builders)
  * Hybrid models balancing multiple goals
* **Challenge**: Balancing MegaETH token economics with Ethereum community alignment
* **Timeline**: Model still being finalized with focus on long-term sustainability

The team emphasizes creating innovative incentive models rather than copying existing approaches.

**Discussion**: [https://x.com/GreenGeorgeHL/status/1912223926702264428](https://x.com/GreenGeorgeHL/status/1912223926702264428)

***

### Reorg Handling

While extremely rare today, MegaETH's reorg risk will further decrease with future ZK implementation:

**Current (Optimistic) model**:

* 7-day challenge period creates reorg window
* L1 reorganization forces L2 to follow
* Sequencer misbehavior theoretically possible

**Future (ZK) model**:

* Near-instant finality once proof hits L1
* Reorgs only possible in narrow window (execution → proof submission)
* L1 reorgs still require L2 to follow (but much rarer)

**Protection strategy today**:

* Sequencer economically and socially motivated to behave correctly
* All infrastructure components built to handle potential reorgs
* Automatic detection and response to L1 reorgs
* "Have a plan" philosophy - robust but not routine

**With ZK transition**: Reorg risk drops from "extremely unlikely" to "virtually impossible" except for L1 reorgs themselves.

**Technical approach**: [https://x.com/yangl1996/status/1913282712254771597](https://x.com/yangl1996/status/1913282712254771597)

***

### Sequencer Dynamics

MegaETH implements hot backup system for zero-downtime operations:

**How it works**:

* Primary sequencer broadcasts progress continuously
* Hot backups track every block in real-time
* On failure, backup takes over within tens of milliseconds
* New sequencer resumes exactly where previous stopped

**Key innovation**: Instead of asking "where did you stop?" during crisis, backups already know through continuous tracking. This flips the traditional handoff model for instant recovery.

**Performance considerations**:

* Switching sequencers pauses chain briefly
* Ethereum rotates every block (12s) - good for decentralization
* MegaETH rotates only on failure - optimized for consistent 10ms blocks
* Trade-off: Less frequent rotation for better performance

**Benefits**:

* Hardware failures recovered automatically
* Upgrades without downtime
* Foundation for future multi-sequencer model
* Maintains real-time performance

**Implementation details**: [https://x.com/megaeth\_labs/status/1927748927744282948](https://x.com/megaeth_labs/status/1927748927744282948)

***

### Security Model

MegaETH's security relies on multiple layers:

* **Ethereum anchoring**: Ultimate security from L1
* **Fraud proofs**: 7-day challenge period (current)
* **ZK proofs**: Near-instant finality (future upgrade)
* **Economic incentives**: Sequencer staking and slashing
* **Operational resilience**: Hot backups and monitoring
* **Data availability**: EigenDA with operator incentives

These mechanisms create a robust protocol supporting real-time applications without compromising security.
