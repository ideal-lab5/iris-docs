# Introduction
This is the official documentation for Iris, available at: https://github.com/iridium-labs/substrate/tree/iris.
`This documentation and any information in it is subject to frequent and radical change as Iris is developed.`

## What is Iris?
Iris is a decentralized storage network that acts as a secure storage layer for Web 3.0. That is, Iris is intended to be **infrastructure for the decentralized web** by providing a decentralized storage layer that can be leveraged by parachains and smart contracts in the Polkadot/Kusama ecosystem. It provides indexability, security, availability, and governance on top of IPFS, enabling data ownership, access management, and the commodification of latent storage capacity and delivery. Built with IPFS and Substrate, Iris can be used by parachains and smart contracts to create dapps that leverage private decentralized storage (for example, a smart contract deployed to the shiden/astar network).

## How does it work?
Iris functions by embedding an IPFS node in the Substrate runtime, allowing us to encode the DHT status within transactions. 

Owned data is treated as a unique asset class within the blockchain, while access to the data is controlled by an asset minted from the asset class. Accounts that hold a positive balance of an asset are authorized to access the underlying content that the asset class is associated with. 

## Key Features
- **Governance**
  - In the future Iris will provide a robust governance framework that allows us to accomplish the same level of governance as major platform and service providers while maintaining decentralization and full transparency.

- **Transparency**
  - Data ownership and access to the data is completely transparent. Unlike centralized storage providers, data in Iris can never be removed by an external party (e.g. Iridium Industries) and instead can only be forcefully removed as a result of onchain governance. 
 
- **Security**
  - The owner of an asset class is under total control over which nodes can and can't own assets derived from this class.
  -  The iris network operates as a private IPFS swarm. 
  -  Note: In its current state there is no easy way to add new validator nodes to the PoA network, however we intend to modify this in the next iteration.

- **Availability**
  - Iris incentivizes storage of data that is more widely accessed, but also allows individuals to reserve storage space within the network. 

## Vision
The big picture is for Iris to act as a storage parachain in polkadot and kusama. We envision that a vast number of dapps using our decentralized storage scheme could be made possible.

The initial motivation of Iris is to solve the "streaming problem": As the number of streaming services with exclusive rights to content increases, the actual content to which consumers have access diminishes along with the siloing of data. In a decentralized approach, individual content owners can retain ownership of their content while doing away with a subscription based model.

https://github.com/w3f/Grants-Program/blob/master/applications/iris.md

## Contact
- twitter: https://twitter.com/Iridium_labs
- website: http://iridium.industries/
- email: driemworks@iridium.industries
