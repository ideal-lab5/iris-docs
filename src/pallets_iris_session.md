# Iris-Session

The Iris-session pallet incorporates both IPFS and the [session module](https://github.com/paritytech/substrate/blob/master/frame/session/README.md) to allow network validators to provide storage for some existing asset class for the duration of a session. In general, it provides the capabilities to:

- provide storage to the network
- capitalize on latent storage capacity
- eject data from the network

## Runtime Details

### Interaction with Embedded IPFS

The iris-session pallet contains the core logic for interacting with the embedded IPFS instance. In this module we expose the capability for offchain workers to process commands added to the DataQueue. Specifically, to:

- read IPFS public key and muiltiaddresses
- add data to the IPFS by processing an AddBytes command
- fetch data from IPFS by processing a CatBytes command
- pin data to IPFS by processing a PinBytes command

When a node adds an AddBytes command to the queue (via the iris-assets pallet), any other node is capable of processing the command and injecting the data into the network.

When a node adds a CatBytes command to the queue, it is uniquely processed by the calling node, adding the data to offchain storage so that it can be fetched via the RPC endpoint.

When a node adds a PinBytes command to the queue, it is uniquely processed by the calling node. The also results in the addition of the node to the *Pinners* storage map.

### Session-based approach to adding validators

Iris is a proof of authority network. Through the usage of the session pallet, we introduce a mechanism for an existing authority to add new validators to the network. Iris uses Aura for consensus and Grandpa for block finalization and there is no alteration to the default process through which nodes are rewarded.

In the long term, we intend to create a new consensus, which we are calling `Nominated Proof of Storage Capacity`. Details of this to come.

### Session-based approach to adding and rewarding storage providers

Validator nodes are a superset of the storage provider nodes. Validators, using the iris-session pallet, can request to store some owned content added to Iris. For example, if a node has added data and created a content asset class, then a validator node can request to store the content during the subsequent session.

There are three phases to each session:

  1. a pre-session planning phase
  2. a session start phase
  3. a session end phase

When we say **current session** we mean a session that has been *planned*, and for which the possible storage providers are locked but not yet necessarily providing active storage. An **active session** is a session that has been *started* and for which the nodes are active storage providers. This is elaborated below:

1. Pre-session planning: candidate storage providers that have pinned the CID they requested to store are added to a collection of active storage providers for that asset class for that session. The current session is incremented by one.

2. Session Start: The active session is incremented by one.

3. Session End: Rewards are distributed to the participants during the session. Currently, this is manifested as "reward points" but will be OBOL (as calculated by reward points) in the future.

### Reward Point Calculation

Reward points are the interim rewards that storage providers receive processing requests in the DataQueue. These scenarios are when a content owner has requested to add data to Iris via the `create` extrinsic, when successfully pinning data, when a consumer has requested to fetch bytes from ipfs through the `retrieve_data` extrinsic.

All nodes with sufficient storage process AddBytes requests.

When data is requested from Iris, the underlying IPFS network will fetch the bytes from one of the storage providers (though it's possible it could exist in another node since we don't have much in terms of garbage collection in rust-ipfs). Though it may be possible to determine exactly which IPFS node the data was fetched from, this is most likely computationally expensive. We track the number of times some data was successfully requested (i.e. the number of times a consumer requested to fetch the content of an asset class of which they own an asset). At the end of the session, the total sum is distributed evenly to storage providers for that asset during the session.
