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

# GTE

GTE is building the world's fastest **decentralized trading platform** that covers the entire lifecycle of a token – from initial launch to sophisticated perpetuals trading – all on a single, high-performance platform powered by MegaETH's infrastructure.

[Website](https://www.gte.xyz/) | [Twitter](https://x.com/GTE_XYZ) | [Discord](https://discord.com/invite/gte-xyz) | [Documentation](https://docs.gte.xyz/)

### Vision & Platform Overview

GTE eliminates the fragmentation plaguing crypto trading by unifying critical market structures that traditionally exist in silos. Instead of forcing users to navigate between PumpFun for launches, Raydium for swaps, and Binance for advanced trading, GTE delivers **"Binance onchain"** – a complete trading ecosystem with CEX-level performance. [Visual](https://x.com/0xBreadguy/status/1910789448281055649)

**Unified Trading Infrastructure:**

* **Token Launchpad** – Fair launch mechanism for bootstrapping initial liquidity
* **Classic AMM** – Price discovery and trading for newer or long-tail assets
* **Spot & Perpetual CLOBs** – CEX-level liquidity with crankless onchain design
* **Best-Price Aggregator** – Optimal execution across all GTE venues and MegaETH ecosystem

This integration means users can follow a token's entire journey within one interface – from fair launch through AMM discovery to professional CLOB trading and perpetuals – without bridging assets or managing multiple accounts.

### Team & Background

**Liquid Labs**, the core contributor behind GTE, brings together talent from **Nasdaq, Mastercard, Morgan Stanley, Palantir, AWS, GSR**, and **Bitstamp**. The founding team combines:

* **HFT expertise** from firms like Jump Trading – crucial for building microsecond-optimized infrastructure
* **Blockchain infrastructure** experience including 3 years running nodes at Alchemy
* **High-performance engineering** focused on ultra-low latency data pipelines

Co-founders [Matteo](https://x.com/mlunghi2000) and [Enzo](https://x.com/enzo_gte) lead this synthesis of traditional finance performance with blockchain innovation, approaching infrastructure challenges with a unique perspective that goes beyond adapting existing tools.

**Funding & Community:**

* **$2.5M Echo raise** – Community round with 720+ investors, sold out in 1 hour
* **$8.4M institutional funding** – Pre-seed ($1.5M) and seed ($6.942M) from Maven 11, Wintermute, Flow Traders, Robot Ventures, IMC Trading, and notable angels including Guy Young (Ethena) and traders from Jump Trading
* **$15M Series A** – From Paradigm to scale the Global Token Exchange

The dual approach mirrors MegaETH's own raise, prioritizing both grassroots support and institutional backing to align all stakeholders. [Source](https://cryptorank.io/ico/gte)

### Why MegaETH Powers GTE

GTE's architecture is **only possible on MegaETH** – no other general-purpose blockchain has closed the performance gap with centralized exchanges:

**Performance Breakthrough:** [Source](https://x.com/megaeth_labs/status/1910370982868770889)

* **\~15ms end-to-end latency** with sequencer colocation (vs Hyperliquid's 200ms best-case)
* **100k TPS** and **1ms block times** enable fully onchain CLOB matching
* **1.7 Ggas/s** throughput maintains consistent performance under load
* Approaching **Binance's \~5ms** colocated latency as MegaETH optimizes further

**Technical Advantages:**

* **Crankless design** – Cheap gas lets market makers freely place/cancel orders, creating tighter spreads
* **True price-time priority** – Centralized sequencer enables fair matching like traditional markets
* **Full composability** – EVM compatibility maximizes integration with DeFi protocols
* **Transparent execution** – All matching logic runs onchain, unlike hybrid DEX approaches

**Capital Efficiency Benefits:**

* **Micro-transactions enabled** – Previously uneconomical strategies become viable
* **Complex interactions affordable** – Multi-step DeFi operations without prohibitive fees
* **Professional trading onchain** – HFT strategies finally practical in decentralized venues

As the team notes: "The bitter truth is that trading on DEXs is slower and more expensive than trading on a CEX" – GTE on MegaETH changes this reality by delivering the first serious attempt at a fully onchain CLOB with CEX-level execution.

***

### Technical Architecture

**Core Innovation:**

* **Fully onchain execution** – All matching logic runs on-chain, unlike hybrid DEXs that compromise transparency
* **1-5ms latency updates** – Market makers can quote with the same confidence as on Binance or Bybit
* **Crankless design** – Cheap gas enables continuous order updates without external keepers
* **FIFO sequencing** – Fair price-time priority without sacrificing composability

As [Enzo notes](https://x.com/enzo_gte/status/1923412379179925606): "Price feeds are censorship resistant and the CLOB is fully composable – we're one step closer to price discovery onchain."

### Trading Infrastructure

#### **Takeoff - Permissionless Token Launcher**

GTE's launchpad provides **fair, transparent token launches** with automatic liquidity bootstrapping:

* **80% supply** sold through bonding curve mechanism
* **20% supply** seeds AMM pool automatically upon completion
* **Instant migration** – No waiting periods, immediate AMM trading post-bond
* **0.005 ETH launch cost** – Minimal barrier for creators

The bonding curve ensures fair distribution while preventing team pre-purchases, establishing trust from day one. ([Details](https://docs.gte.xyz/home/trading/launchpad/token-launcher))

#### **AMM - Proven Liquidity Foundation**

GTE's AMM leverages **battle-tested Uniswap V2 architecture** for long-tail assets:

* **Constant product model** (x \* y = k) for reliable pricing
* **50/50 liquidity provision** – Simple, proven mechanism
* **Ideal for memecoins** and low-liquidity markets where CLOBs would have sparse orders
* **Immediate integration** with tokens graduating from Takeoff

This dual-venue approach recognizes that different assets require different market structures – passive AMM liquidity for emerging tokens, active CLOB liquidity for mature markets.

#### **Spot & Perpetual CLOBs**

The crown jewel of GTE's infrastructure – **the first truly competitive onchain orderbook**:

**Spot CLOB** ([Live on testnet](https://x.com/mlunghi2000/status/1923046712953712962)):

* **BTC trading live** with ETH, SOL, and more coming soon
* **Top-tier market makers** already providing liquidity
* **Professional features** – Limit, market, stop orders, TWAP execution
* **Full Python SDK** for programmatic access

**Perpetuals CLOB** (Coming soon):

* **50x leverage** using ETH as collateral
* **Cross-margin trading** across multiple positions

[Enzo explains](https://x.com/enzo_gte/status/1925970414007615730): "Perps will lead the charge to get tradfi assets onchain. Derivatives allow exposure without requiring asset issuance."

#### **DEX Aggregator**

GTE's aggregator ensures **optimal execution across all MegaETH venues**:

* **Smart routing** between GTE AMM, CLOB, and ecosystem DEXs
* **Programmatic access** via [API for developers](https://docs.gte.xyz/api-reference/introduction)
* **Frontend integration** for seamless user experience
* **Best-price guarantee** through continuous market scanning

### Performance Advantages

#### **vs. Hyperliquid**

GTE's architecture fundamentally outperforms even specialized trading chains:

* **15ms latency** with colocation vs Hyperliquid's 200ms best-case
* **True composability** – Single execution environment vs HyperCore/HyperEVM split
* **No consensus bottleneck** – MegaETH separates execution from consensus

[As Enzo details](https://x.com/enzo_gte/status/1927905984955175297): "HL's validators are all in one Tokyo datacenter to compete with Binance. Only way to beat HL is to take another step function in scaling."

#### **vs. Other L1s/L2s**

Legacy chains face fundamental limitations:

* **Consensus-bound latency** – Can't achieve sub-10ms with global validators
* **Mempool racing** – Market makers struggle with stale quotes after 200ms
* **Priority fee wars** – Makes continuous order updates economically unfeasible

[As Enzo details](https://x.com/enzo_gte/status/1915511068996391133): "If your chain is focused on increasing bandwidth and reducing latency for the sole purpose of trading onchain, it will lose to our architecture in the long run."

### Advanced Features & Roadmap

#### **Cross-Chain Abstraction**

* GTE eliminates bridging friction through innovative integration:
  * **1-click trading** using stables from any chain ([Announcement](https://x.com/enzo_gte/status/1912558956754682181))
  * **Aggregate balance display** – See all your stables across chains
  * **Native re-issuance** on MegaETH when trading
  * **"50x long BTC using L1 stables in 5ms"** – The future of DeFi UX

#### **Phased Rollout Approach**

* **Phase 1** ✅ (Complete):
  * Takeoff launcher
  * Swap AMM
  * Dash analytics dashboard
* **Phase 2** 🚀 (Current):
  * [Spot CLOB live on testnet](https://x.com/enzo_gte/status/1923046182219284917)
  * Market maker integrations
  * Token graduation pipeline
* **Phase 3** (Coming):
  * Perpetuals CLOB
  * Cross-margin system
  * Advanced order types
  * Institutional features

### Technical Resources

* [Official Documentation](https://docs.gte.xyz/) – Complete API reference and integration guides
* [Python SDK](https://github.com/Liquid-Labs-Inc) – Full programmatic suite for CLOB interaction
* [Architecture Deep Dive](https://x.com/defi_monk/status/1908200176805961953) – Messari's technical analysis
* [GTE: The Vertical Exchange on MegaETH](https://x.com/castle_labs/status/1907829178512122329) by @CryptoNdee

***

**The Bottom Line:** GTE isn't just building another DEX – they're creating the infrastructure for **all of centralized finance to move onchain**. By solving the fundamental technical barriers that have kept sophisticated trading centralized, GTE on MegaETH finally delivers the promise of DeFi: **CEX performance with DEX principles**.
