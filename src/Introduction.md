# Introduction

This is the official documentation for [Iris](https://github.com/ideal-lab5/substrate/tree/iris), developed and maintained by [ideal labs](https://idealabs.network).

`This documentation and any information in it is subject to frequent and radical change as Iris is developed.`

![sponsored by web3 foundation](./resources/web3_foundation_grants_badge_black.png)

Read our w3f grant proposal [here](https://github.com/w3f/Grants-Program/blob/master/applications/iris.md)

## What is Iris?

Iris is a decentralized network that provides a secure data storage, delivery, and ownership layer for Web 3.0 applications. It is infrastructure for the decentralized web, providing a storage and data exchange which enables the transfer and monetization of access to and ownership of data across chains, smart contracts and participants in the network or connected through a relay chain. Iris provides security, availability, reputation, and governance on top of IPFS, enabling data ownership, access management, and the commodification of latent storage capacity and content delivery. It applies defi concepts to data, reputation, storage capacity and availability to synthesize computation and storage and to represent off-chain assets in an on-chain context. We build a cryptographically verifiable relationship between data storage, access and ownership.

## How does it work?

Iris functions by embedding an IPFS node in the Substrate runtime, allowing us to encode the DHT status on-chain. This lets us enable a **cryptographically verifiable relationship** between data ownership, access, and availability.

Owned data is treated as a unique asset class within the blockchain, while access to the data is controlled by an asset minted from the asset class. Accounts that hold a positive balance of an asset are authorized to access the underlying content that the asset class is associated with. Iris will also have the capability to transfer assets between parachains and smart contracts, enabling a novel way to access data across the web.

## Key Features

- **Ownership and Access via Assets**
  - Owned content in Iris is treated as a unique asset class
  - Access to content is synonymous with owning assets minted from the asset class. This allows us to easily transfer *access* to data across parachains and smart contracts.
- **Data Spaces**
  - Data spaces act as unique, owned enclaves of data within the network. Any node can create their own data space, define who can associate their data with it, and further what kinds of data are allowed to exist within their space.
- **Availability Encouraging Storage System**
  - Iris uses an availability-encouraging storage system to maximize data aviailability without compromising the decentralized nature of the network
- **smart contract support**
  - interact with the iris runtime through the [chain extension](./contracts_chain_extension.md)
- **Secure**
  - Iris uses a **threshold encryption** mechanism to secure your data.
- **Social**
  - Through an anonymous feedback and reputation system, data consumers can rate data owners, individual data, and data spaces.
- **Transparent Governance**
  - In the future Iris will provide a robust governance framework that allows us to accomplish the same level of governance as major platform and service providers while maintaining decentralization and full transparency.

For a full breakdown of where we are in the implementation of these features, take a look at our [roadmap](./quickstart/development_status.md).

## Vision

Iris aims to be a general decentralized storage layer for web3 applications, specifically (but not limited to) in the dotsama ecosystem. Iris enables parachains, smart contracts, and parathreads to benefit from secure decentralized storage by taking advantage of XCM to transfer assets between chains.

We envision that Iris can facilitate a new variety of dapps (that are currently too expensive or not readily feasible) that leverage decentralized storage, represented as asset classes, in a cross-chain, cross contract environment, where Iris acts as a common storage layer.

The initial motivation of Iris is to solve the “streaming problem”: As the number of streaming services with exclusive rights to content increases, the actual content to which consumers have access diminishes due to the arbitrary cloistering of content. In a decentralized approach, individual content owners can retain ownership of their content while doing away with a subscription based model. However, Iris may facilitate a plethora of applications whose scope is far beyond streaming.

## Contact

- twitter: https://twitter.com/ideal_labs
- website: https://idealabs.network/
- email: driemworks@idealabs.network
- discord: https://discord.gg/w8PF9MM6
- github: github.com/ideal-lab5
