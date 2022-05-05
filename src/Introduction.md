# Introduction

This is the official documentation for [Iris](https://github.com/ideal-labs/substrate/tree/iris).

`This documentation and any information in it is subject to frequent and radical change as Iris is developed.`

![sponsored by web3 foundation](./resources/web3_foundation_grants_badge_black.png)

Read our w3f grant proposal [here](https://github.com/w3f/Grants-Program/blob/master/applications/iris.md)

## What is Iris?

Iris is a decentralized storage layer for Web 3.0. It is **infrastructure for the decentralized web**, providing a decentralized storage layer that can be leveraged by smart contracts and parachains, allowing access to content to be transferred across chains and monetized. It provides indexability, security, availability, and governance on top of IPFS, enabling data ownership, access management, and the commodification of latent storage capacity and content delivery. Built with IPFS and Substrate, Iris' dual network topology allows it to treat unique data as owned asset classes on the blockchain, while actual data is stored offchain in an IPFS network.

## How does it work?

Iris functions by embedding an IPFS node in the Substrate runtime, allowing us to encode the DHT status on-chain.

Owned data is treated as a unique asset class within the blockchain, while access to the data is controlled by an asset minted from the asset class. Accounts that hold a positive balance of an asset are authorized to access the underlying content that the asset class is associated with. Iris will also have the capability to transfer assets between parachains and smart contracts, enabling a novel way to access data across the web.

## Key Features

- **Ownership and Access via Assets**
  - Owned content in Iris is treated as a unique asset class
  - Access to content is synonymous with owning assets minted from the asset class. This allows us to easily transfer *access* to data across parachains and smart contracts.
- **Decentralized Storage**
  - validator nodes can opt-in to provide storage to the network. Currently, this is only semi-decentralized while we are a proof of authority network, however we intend to transition to proof of storage capacity in the future.
- **smart contract support**
  - interact with the iris runtime through the [chain extension](./contracts_chain_extension.md)
- **Transparent Governance**
  - In the future Iris will provide a robust governance framework that allows us to accomplish the same level of governance as major platform and service providers while maintaining decentralization and full transparency.

## Vision

Iris aims to be a general decentralized storage layer for web3 applications, specifically in the kusama/polkadot ecosystems. Iris enables parachains, smart contracts, and parathreads to benefit from secure decentralized storage by taking advantage of XCM to transfer assets between chains.

We envision that Iris can facilitate a new variety of dapps that leverage decentralized storage, represented as asset classes, in a cross-chain, cross contract environment, where Iris can act as a common storage layer.

The initial motivation of Iris is to solve the “streaming problem”: As the number of streaming services with exclusive rights to content increases, the actual content to which consumers have access diminishes due to the arbitrary cloistering of content. In a decentralized approach, individual content owners can retain ownership of their content while doing away with a subscription based model. However, Iris may facilitate a plethora of applications whose scope is far beyond streaming.

## Contact

- twitter: https://twitter.com/ideal_labs
- website: http://idealabs.network/
- email: driemworks@idealabs.network
- discord: https://discord.gg/w8PF9MM6
