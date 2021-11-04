# Introduction

Iris is a decentralized storage network for substrate-based chains. It aims to provide infrastructure for parachains, allowing nodes to securely store data assets offchain through Iris while access to that data is managed in the parachain. We envision that this chain can facilitate a myriad of decentralized applications that are not currently feasible, like dropbox-like applications, pay-as-you-go streaming services, and much more. 

This goal is conceptually achieved by disseminating and resolving the barriers to adoption of decentralized storage and by contrasting with features provided by centralized services. Decentralized storage networks and blockchains generally do not provide more than storage, forgoing the higher-level capabilities available in a traditional centralized system. The greater the decentralization of the network, the less secure or private your data is. In contrast to centralized services, decentralized services are generally not privacy preserving, since any data on chain is by default public, so enabling privacy usually takes the form of some centralized service. A key feature of Iris is that file data is *never* stored on chain. 

The major differences between DHT-based decentralized storage (using IPFS since it is commonly the DHT platform used as a basis) and centralized storage can be stated as:

1) **Indexability**: IPFS is not a search engine and is not intended to act as one. There is not an easy way to identify or track data in IPFS without a CID.

2) **Security**: When data is hosted in a decentralized network it is available to any node in the network. There are no permissions and no encryption.

3) **Availability**: Availability of any CID in the network is not guaranteed, and approaches to ensuring it is are not necessarily decentralized.

4) **Governance**: There are no native governance options and no simple way to purge content from all nodes in the network. IPFS provides a customizable blockList, but attempting to “revoke” data from other nodes is not fundamentally doable. If the IPFS network is public and truly decentralized, then this could allow for malicious content to exist in the network.

# Usage

## Installation
Future state -> doesn't exist yet
`docker install iridium/iris`

## Build
Clone this repo and then run:
`cargo +nightly build --release` 

to build the node. 

### Docker
`docker build -t driemworks/substrate -f ./.maintain/Dockerfile .`

```
docker run -p 9944:9944 \
  -p 9933:9933 \
  -p 30333:30333 \
  -p 9615:9615 \
  -it \
  --rm \
  --name node-template \
  driemworks/substrate \
  --dev --ws-external --rpc-external
```