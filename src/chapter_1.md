# Introduction
This is the official documentation for Iris, available at: https://github.com/iridium-labs/substrate/tree/iris.
`This documentation and any information in it is subject to frequent and radical change as Iris is developed.`

## What is Iris?
Iris is a decentralized storage network that acts as a secure storage layer for Web 3.0. It provides indexability, security, availability, and governance on top of a decentralized storage layer, enabling data ownership and access management. Built with IPFS and Substrate, Iris can be used by parachains and smart contracts to create dapps that leverage private decentralized storage (for example, a smart contract deployed to the shiden/astar network).

## How does it work?
Iris functions by embedding an IPFS node in the Substrate runtime, allowing us to encode the DHT status within transactions. 

Each CID added to the network is treated as a new asset class, with ownership of assets derived from the asset class representing access to the underlying content. Accounts that hold a positive balance of an asset are authorized to access the underlying content that the asset class is associated with. 

## Key Features
  We will provide a robust governance framework that allows us to accomplish the same level of governance as major platform and service providers while maintaining decentralization and full transparency. 
  - We plan to build a moderation mechanism into this framework
  
- Security
  - The owner of an asset class is under total control over which nodes can and can't own assets derived from this class.

- Availability
  - earn rewards by providing storage to the network
  - Users provide incentive for storage providers to pin their content.

## Vision
The big picture is for Iris to act as a storage parachain used by other chains in polkadot and kusama. We envision that a vast number of dapps using our decentralized storage scheme could be made possible. 

https://github.com/w3f/Grants-Program/blob/master/applications/iris.md

## Contact
- twitter: https://twitter.com/Iridium_labs
- website: http://iridium.industries/
- email: driemworks@iridium.industries
