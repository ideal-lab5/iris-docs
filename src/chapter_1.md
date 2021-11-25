# Introduction
This is the official documentation for the Iris fork of Substrate, available at: https://github.com/iridium-labs/substrate/tree/iris.

`This documentation and any information in it is subject to frequent and radical change as Iris is developed.`

## What is Iris?
Iris is a decentralized storage network built with Substrate and IPFS. Iris is extensible and can be used by parachains and smart contracts (via XCM) to take advantage of fully decentralized storage across multiple chains and dapps. The Iris runtime provides indexability, security, availability, and governance on top of a fully decentralized network.

Iris treats everything as an asset.  Content owners create new asset classes when adding data to the network. Assets derived (minted) from this asset class act as proof of access to the underlying content associated with the asset class. Owners of assets are authorized to download data from Iris. See [assets overview](../src/chapter_4.md) for more on this.

## How does it work?
Iris functions by taking advantage of an IPFS instance embedded in the runtime, which allows us to track input to and output from the DHT within the blockchain. Iris exposes extrinsics that allow nodes to add requests to the DHT to a queue. Offchain workers that can interact with IPFS process queued requests and publish the results on-chain.

Additionally, Iris acts as an asset creation and management pallet. To accomplish this we couple with the [assets pallet](https://github.com/iridium-labs/substrate/blob/iris/frame/assets/src/lib.rs). Each CID added to the network is treated as a new asset class, with ownership of assets derived from the asset class representing access to the underlying content. Accounts that hold a positive balance of an asset are authorized to access the underlying content that the asset class is associated with. 

## Key Features
- Governance
  We will provide a robust governance framework that allows us to accomplish the same level of governance as major platform and service providers while maintaining decentralization and full transparency. 
  - We plan to build a moderation mechanism into this framework
  
- Security
  The owner of an asset class is under total control over which nodes can and can't own assets derived from this class. That is, they maintain control over who can access their content. 

- Availability
  - earn rewards by providing storage to the network
  - Users provide incentive for storage providers to pin their content.

## Vision
The big picture is for Iris to act as a storage parachain used in polkadot and kusama. We envision that a vast number of dapps using our decentralized storage scheme could easily be made possible. 

https://github.com/w3f/Grants-Program/blob/master/applications/iris.md

## Contact
- twitter: https://twitter.com/Iridium_labs
- website: http://iridium.industries/
- email: driemworks@iridium.industries

