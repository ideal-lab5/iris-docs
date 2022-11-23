# Authorities Pallet

The authorities pallet incorporates both IPFS and the [session module](https://github.com/paritytech/substrate/blob/master/frame/session/README.md) to allow network validators to provide storage for some existing asset class for the duration of a session. In general, it provides the capabilities to:

- provide storage to the network
- capitalize on latent storage capacity
- eject data from the network

## Runtime Details

### Session-based approach to adding validators

Iris is a proof of authority network. Through the usage of the session pallet, we introduce a mechanism for an existing authority to add new validators to the network. Iris uses Aura for consensus and Grandpa for block finalization and there is no alteration to the default process through which nodes are rewarded.

### Session-based approach to adding and rewarding storage providers

*Note*: We currently follow a fairly naive scheme for incentivizing validators to store content. We intend to replace the below scheme with something much more mature in the future.

Validator nodes are a superset of the storage provider nodes. Validators, using the iris-session pallet, can request to store some owned content added to Iris. For example, if a node has added data and created a content asset class, then a validator node can request to store the content during the subsequent session.

There are three phases to each session:

  1. a pre-session planning phase
  2. a session start phase
  3. a session end phase

When we say **current session** we mean a session that has been *planned*, and for which the possible storage providers are locked but not yet necessarily providing active storage. An **active session** is a session that has been *started* and for which the nodes are active storage providers. This is elaborated below:

1. Pre-session planning: candidate storage providers that have pinned the CID they requested to store are added to a collection of active storage providers for that asset class for that session. The current session is incremented by one.

2. Session Start: The active session is incremented by one.

3. Session End: Validiators that have been storing data but have not accumulated any reward points for some preconfigured number of sessions (MaxDeadSessions) is removed from the validator pool.
