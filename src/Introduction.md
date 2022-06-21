# Introduction

This is the official documentation for [Iris](https://github.com/ideal-lab5/iris), developed and maintained by [ideal labs](https://idealabs.network).

`This documentation and any information in it is subject to frequent and radical change as Iris is developed.`

![sponsored by web3 foundation](./resources/web3_foundation_grants_badge_black.png)

Read our w3f grant proposal [here](https://github.com/w3f/Grants-Program/blob/master/applications/iris.md)

## What is Iris?

Iris is a decentralized data exchange protocol that enables a secure data storage, delivery, and ownership layer for Web 3.0 applications. It is infrastructure for the decentralized web, providing a data exchange which enables the transfer and monetization of access to and ownership of data across chains, smart contracts and participants in the network or connected through a relay chain, by building a cryptographically verifiable relationship between storage and ownership. Iris provides security, availability, reputation, and governance on top of storage, enabling data ownership, access management, smart contract support for data, and content delivery. It applies defi concepts to data, reputation, storage capacity and availability to synthesize computation and storage and to represent off-chain assets in an on-chain context.

## How does it work?

Iris functions by building a **cryptographically verifiable relationship** between data ownership, access, and availability. Data ownership is treated as an on-chain asset class, while access (equivalently, partial ownership) is granted by owning an asset minted from the asset class, subject to business logic as determined by the data owner (via [composable access rules](./contracts/composable_access_rules.md)).

## Key Features

- **Ownership and Access via Assets**
  - Owned content in Iris is treated as a unique asset class
  - Access to content is synonymous with owning assets minted from the asset class. This allows us to easily transfer *access* to data across parachains and smart contracts.
- **Data Spaces**
  - Data spaces act as unique, owned enclaves of data within the network. Any node can create their own data space, define who can associate their data with it, and further what kinds of data are allowed to exist within their space.
- **Configurable Storage System**
  - Iris is capable of leveraging many different storage systems to meet user needs.
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



## Contact

- twitter: https://twitter.com/ideal_labs
- website: https://idealabs.network/
- email: driemworks@idealabs.network
- discord: https://discord.gg/w8PF9MM6
- github: github.com/ideal-lab5
