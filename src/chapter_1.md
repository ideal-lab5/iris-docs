# Introduction
Iris is a substrate-based decentralized storage network. Iris intends to be extensible and used by parachains and smart contracts to take advantage of truly decentralized storage. 

Iris treats everything as an asset. When data is added to the network a brand new asset class is created to identify that data. Assets derived (minted) from this asset class act as proof of access to the underlying content associated with the asset class.

On top of decentralized storage, Iris delivers four key features:
1) Indexability
2) Security
3) Availability
4) Governance

## IPFS
Our integration with rust-ipfs (embedded within the substrate runtime) is based on prior work done here: https://rs-ipfs.github.io/offchain-ipfs-manual/introduction.html, with the iridium-labs/substrate offchain_ipfs_v3 branch being maintaining in sync with the latest substrate master. 

# Usage

## Installation

### Sources
Clone the repo:
`git clone https://github.com/iridium-labs/substrate.git`

From the master branch:
Build the node:
`cargo +nightly build --release`

And then run:
`cargo +nightly run -- --dev --tmp`

### Docker
(The easiest way to install) DNE... future state.
`docker install iridium/substrate`

Build the docker image:
`docker build -t iridium/substrate -f ./.maintain/Dockerfile .`

```
docker run -p 9944:9944 \
  -p 9933:9933 \
  -p 30333:30333 \
  -p 9615:9615 \
  -it \
  --rm \
  --name node-template \
  iridium/substrate \
  --dev --ws-external --rpc-external
```
