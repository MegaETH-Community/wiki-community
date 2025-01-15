---
icon: layer-plus
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

# EigenLayer

EigenLayer is a protocol designed to enhance Ethereum's modularity and scalability. It allows developers to build decentralized applications (dApps) and rollups that leverage Ethereum’s security while introducing customizable layers to address specific challenges.

In this page, we’ll focus on **EigenDA**, its role in managing **data availability (DA)**, and how it tackles the limitations of Ethereum for rollups.

_Thanks to_ [_**Paramonov**_](https://x.com/paramonoww) _for his detailed explanation of EigenDA. If you’re interested in a deeper dive, I highly recommend reading his_ [_Twitter thread_](https://x.com/paramonoww/status/1879500495641006082)

***

### **The Problem of Data Availability**

Data availability is a critical bottleneck for rollups and decentralized applications that rely on Ethereum as their DA layer. Here’s why:

* **Limited Block Size:** Ethereum blocks can handle 768kB of blob data plus other information, reaching a total size of about 2.5MB.
* **Slow Bandwidth:** With a block time of 12 seconds, Ethereum achieves a bandwidth of only **0.2MB/s**.
* **Global TPS Limits:** This equates to approximately **9,000 transactions per second (TPS)**—not just for one rollup, but for all rollups sharing Ethereum as their DA layer.
* **No Horizontal Scaling:** Adding more nodes does not proportionally increase throughput, limiting scalability.

These constraints make it challenging to support the growing demand for high-throughput decentralized applications.

***

### **EigenDA: A Data Availability Solution**

**EigenDA** addresses these limitations by acting as a specialized layer for managing blob data and publishing it to Ethereum. It provides:

* **Increased Throughput:** EigenDA offers a write throughput of **15MB/s**, which translates to up to **654,000 TPS** with data compression—far surpassing Ethereum’s native capabilities.
* **Efficient Blob Handling:** EigenDA manages blob storage and ensures seamless publication of these blobs to Ethereum for validation and finalization.
* **Enhanced Security:** EigenDA incorporates a **slashing mechanism**, where operators are financially penalized for misbehavior.

By offloading the heavy lifting of data availability, EigenDA enables rollups to scale horizontally while maintaining the security and trust guarantees of Ethereum.

***

<figure><img src="../.gitbook/assets/GhVMSH1bcAAQfSY.jpeg" alt=""><figcaption></figcaption></figure>
