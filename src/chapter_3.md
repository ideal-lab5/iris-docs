# Technical Overview

1. [Tech Stack](#tech-stack)
2. [Node Roles](#node-roles)
3. [Runtime](#runtime)

## Tech Stack

### IPFS

Our integration with [rust-ipfs](https://github.com/rs-ipfs/rust-ipfs) is based on [prior work](https://rs-ipfs.github.io/offchain-ipfs-manual/introduction.html). The iridium-labs/substrate [offchain_ipfs_v3](https://github.com/iridium-labs/substrate/tree/offchain_ipfs_v3) branch maintained in sync with the latest substrate master.

The ui we provide relies on a local IPFS instance to add data (iris does not). To add data through the UI you must first run an instance of IPFS locally (you don't need to run an IPFS if you want read only access).

### Substrate

Substrate is a blockchain framework built by parity. It provides the building blocks for creating a blockchain, including the database, consensus, rpc, and much more.

### React

We use react to build the user interface to interact with our node. We specifically rely on the `polkadotjs` and `ipfs-http-core` libraries.

## Node Roles

- **Storage Provider**: The storage provider node's responsibility includes processing commands added to the queue by other nodes and submitting the results of the command on chain.
- **Content Owner**: A content owner is responsible for making data available in some external IPFS node and interacting with Iris to ingest and maintain access to it.
- **Content Consumer**: A content consumer is responsible for using owned tickets to access owned content.

## Runtime

Iris is a proof of authority network. In the future we intend to migrate to a PoS network, but due to the current limitations of rust-ipfs we will use PoA.

The Iris runtime builds from exsiting modules within the Substrate runtime, specifically the session and assets modules. In general, the Iris-Assets module, which depends on the assets modules, provides data ingestion, and asset class management. The Iris-Session module enables session based storage for content owner, where storage is provided by network validators. Read more on the Iris-assets and Iris-Session modules [here](./pallets.md).

![runtime modules](./resources/runtime_modules.png)

*The Iris runtime modules and dependencies*
