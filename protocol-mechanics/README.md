---
icon: gears
---

# Protocol Mechanics

Core mechanisms ensuring MegaETH's security, reliability, and economic sustainability.

### USDm & Fee Model

MegaETH partnered with Ethena to launch **USDm**, a native stablecoin that fundamentally reimagines how L2s sustain themselves economically.

**The Problem with Traditional L2 Economics:**

Most L2s make money by adding a markup to transaction costs. They pay X to post data on Ethereum, but charge users 2X or 3X. The higher the fees, the more profit for the L2 - but the less people want to use it. This creates a conflict: the chain makes more money when users pay more, which directly discourages the usage needed for growth.

**USDm Solution:**

MegaETH redirects value from **financial yield rather than users** to fund network operations, enabling the chain to price gas at-cost.

**How It Works:**

* **Reserve-backed issuance** - USDm v1 built on Ethena's USDtb rails, backed primarily by BlackRock's tokenized U.S. Treasury fund (BUIDL) via Securitize
* **Yield funds operations** - Reserve yield programmatically covers sequencer operational costs
* **At-cost gas pricing** - No margin extraction from users, keeping fees low and predictable
* **Incentives realigned** - Network growth increases stablecoin circulation, not user fees
* **Reserve flexibility** - Architecture allows future adjustment to include other Ethena products like USDe

**Benefits:**

* Sub-cent, predictable transaction costs enable new categories of applications
* Network sustainability without raising fees as activity grows
* Complements [token utility](tokenomics.md#token-utility) (sequencer rotation, proximity markets) for diversified revenue

**Other Stablecoins:**

USDT0 (canonical USDT) and cUSD remain first-class citizens with deep liquidity, oracle coverage, and best-execution routing across the ecosystem.

[Announcement](https://x.com/megaeth_labs/status/1965082874627199414)

***

### Settlement & Fraud Proofs

MegaETH secures its optimistic rollup model with a revolutionary **non-interactive ZK fraud proof system**, built in partnership with RISC Zero and following the OP Kailua hybrid architecture.

**Traditional Interactive Fraud Proofs (Bisection Game):**

Classic optimistic systems require challengers and proposers to engage in back-and-forth disputes on Ethereum, bisecting transaction execution step-by-step until isolating a single faulty operation.

**Problems:**

* High latency - hours or days per dispute
* Heavy proposer involvement - even honest proposers must defend against baseless challenges
* Griefing risk - malicious challengers force honest parties to waste gas repeatedly

**MegaETH's ZK Fraud Proof Model:**

Instead of interactive games, challengers submit a **single succinct zero-knowledge proof** demonstrating that executing the payload from the initial state does not produce the claimed final state.

**How It Works:**

* Challenger runs disputed computation in RISC Zero zkVM
* Generates proof showing the state proposal is invalid
* Submits proof to Ethereum verifier contract in one transaction
* Proposer does no work and cannot interfere
* Proof generation costs \~$100 in worst case, borne by dishonest party

**Key Innovation: ZK for Fraud, Not Validity**

MegaETH uses ZK not to prove correctness upfront (like ZK rollups), but to prove fraud when detected. This retains the efficiency of optimistic rollups while adding trust-minimized, non-interactive dispute resolution.

**Finality Timeline:**

* **7-day challenge window** - retained for maximum security
* **\~1 hour dispute resolution** - once challenge raised, ZK proof resolves it quickly vs. days in interactive systems
* **Near-instant finality post-ZK transition** - reorg window reduced to narrow gap between execution and proof submission

**Understanding the Two ZK Models:**

**Today (Optimistic + ZK Fraud Proofs):**

* State updates posted optimistically to Ethereum
* If disputed, ZK proof demonstrates fraud and resolves in \~1 hour
* 7-day window means theoretical reorg risk exists throughout challenge period
* Protection: sequencer economically aligned, all infrastructure handles reorgs automatically

**Future (ZK Validity Proofs):**

* Every state update accompanied by ZK proof of correctness
* Finalized on Ethereum immediately upon proof verification
* Reorg risk reduced to narrow gap between execution and proof submission
* **L1 reorgs** - if Ethereum itself reorganizes, MegaETH must follow and rebuild its state accordingly (this is by design - MegaETH's security is anchored to Ethereum, so it inherits both Ethereum's stability and any rare reorganizations) - [Source](https://x.com/yangl1996/status/1913282712254771597)

This two-phase approach delivers optimistic efficiency today while building toward ZK-level finality guarantees.

**Data Availability via EigenDA:**

Challengers need reliable access to raw block data to reconstruct disputed computations. MegaETH uses [EigenDA](../deep-dive/architecture/eigenlayer.md) for decentralized, high-throughput data availability.

* Sequencer publishes block data to EigenDA
* Only small reference committed to Ethereum
* Cryptographic guarantees ensure data retrievability
* Any watcher can reconstruct blocks and generate fraud proofs
* Prevents sequencer from withholding data to evade detection

**Benefits:**

* Removes griefing attacks
* Protects chain liveness from malicious stall attempts
* Scales to high throughput without compromise
* Maintains security through cryptographic proofs

[Technical Details](https://x.com/megaeth/status/1948030099665666446)

***

### Sequencer Dynamics

MegaETH implements a **hot backup system** for zero-downtime operations, with future evolution toward multi-region sequencer rotation.

**Current Implementation:**

* **Primary sequencer** broadcasts execution progress continuously
* **Hot backups** track every block in real-time
* On failure, backup takes over within **tens of milliseconds**
* New sequencer resumes exactly where previous stopped

**Key Innovation:**

Instead of asking "where did you stop?" during a crisis, backups already know through continuous tracking. This flips traditional handoff models for instant recovery.

**Performance Trade-offs:**

* Ethereum rotates validators every 12 seconds - maximizes decentralization
* MegaETH rotates only on failure or scheduled maintenance - optimizes for consistent 10ms blocks
* Brief pause during sequencer switch vs. continuous real-time execution

**Benefits:**

* Automatic hardware failure recovery
* Upgrades without downtime
* Foundation for future **sequencer rotation model** (see [Tokenomics](tokenomics.md#token-utility))
* Maintains real-time performance guarantees

[Implementation Details](https://x.com/megaeth_labs/status/1927748927744282948)

***

### Decentralization Path

MegaETH's approach to decentralization is nuanced and progressive, addressing multiple dimensions beyond simple validator counts.

**Four Key Dimensions:**

1. **Liveness** - Multi-sequencer failover today, regional rotation coming
2. **Censorship Resistance** - Exit to Ethereum always available, future sequencer rotation provides diverse operators
3. **Credible Neutrality** - Progressing toward Stage 2-like bridge contract where team has minimal control
4. **Permissionless Participation** - Sequencer rotation enables anyone to operate based on stake and reputation

**Why MegaETH Can Credibly Decentralize:**

Traditional L2s struggle to give up sequencer control because it's their primary revenue source. MegaETH has diversified revenue through:

* **USDm yield** - Stablecoin reserves fund operations
* **Proximity markets** - Colocation bidding generates value (see [Tokenomics](tokenomics.md#token-utility))
* **Transaction fees** - Only when MegaETH is operating as a sequencer

This enables MegaETH to credibly decentralize sequencing without sacrificing sustainability.

**Current State:**

* Multi-sequencer failover live
* Settlement to Ethereum provides ultimate censorship resistance
* Team-operated but economically aligned with ecosystem

**Future State:**

* Rotational sequencer across geographic regions
* Proof-of-Authority style inclusion with staked reputation
* Stage 2-like security guarantees
* Diverse operator set

**Philosophy:**

Decentralization isn't binary. It's a spectrum of technical properties implemented differently across chains. MegaETH prioritizes sustainable growth while progressively reducing trust assumptions.

[Detailed Analysis](https://x.com/bread_/status/1984702576202563903)
