# Technical Overview

This is a technical overview of the things that power the Iris blockchain.

## Tech Stack

### Substrate

Iris is built using the substrate framework. Substrate is a blockchain framework built by parity. It provides the building blocks for creating a blockchain, including the database, consensus, rpc, and much more. Additionally, it also provides the opportunity to connect to a rely chain, allowing for Iris to be leveraged in the context of other blockchains. See [here](https://docs.substrate.io/) for more information on the substrate framework.

### IPFS

Iris uses kubo (previously go-ipfs) for our 'hot' storage system. IPFS is a distributed peer-to-peer file sharing tool. As opposed to a location based addresssing system (e.g. fetching data from a server by passing the server's address and file location on the server), IPFS uses a content identifier (CID) based approach. Each unique sequence of bytes is assigned a unique CID, which Iris uses to associate data with asset identifiers. See [here](https://ipfs.tech/) for more information on IPFS.

### React

We use react to build the user interface to interact with our node. We specifically rely on the `polkadotjs` and `ipfs-http-core` libraries.

## The Iris Runtime

Iris functions by embedding an IPFS node within the substrate runtime and allowing validator nodes to form a private IPFS network. By building a blockchain layer on top of the embedded storage, we are able to track calls and responses to IPFS on chain, allowing nodes to be rewarded for storing and retrieving data. Additionally, this allows us to represent offchain storage using on chain assets and to build a cryptographic relationship between data storage, ownership, and access.

The Iris runtime builds on exsiting modules within the Substrate runtime, specifically the session and assets modules. It is currently a proof of authority network. In general, the Iris-Assets module, which depends on the assets modules, provides data ingestion, and asset class management. The Iris-Session module enables session based storage for content owner, where storage is provided by network validators. Read more on the Iris-assets and Iris-Session modules [here](./pallets.md).

![runtime modules](../resources/runtime_modules.png)

### Node Types

There are several node types within Iris, each with their own distinct capabilities:

1. Data owner
2. Data consumer
3. [Validator](./validators.md)
4. [proxy Node](./proxy.md)

In the future another role will be created for moderation and governance capabilities.
