# Assets and Storage

In Iris, owned content is treated as a unique asset class and access to the content is controlled by ownership of assets minted from the asset class. Future plans include building a bridge to allow these assets to be transfered cross-chain, or to be used in smart contracts. 

1. Content Asset Class Creation
2. Provisioning Access
3. Retrieving Data
4. Pinning Data

## The Ticket Asset Class

When a node adds data to Iris, the OCW that processes the request constructs a new asset class backed by some initial (user defined) amount of native currency (see the `create_storage_asset` [extrinsic](./chapter_3.md)). This results in a new `DataCommand` being added to the processing queue. When an OCW proceses the command and publishes results on chain, a new asset class is created. 

![data-ingestion](./resources/data_ingestion.drawio.png)

Our initial use case makes assumptions that we will break in the future:

1. Each owner and CID combination has at most one associated asset class
2. Asset classes can correspond to at most one owner/CID combination
3. Owning a non-zero quantity of assets in an asset class grants the owner access to the underlying data

### Creating Tickets

This is equivalent to granting access to some of your owned data to another node.

Only the admin node (i.e. content owner) is capable of minting new assets for an asset class. The admin specifies a `beneficiary` and the `amount` of assets to mint. (see: `mint_tokens` extrinsic). When completed, the beneficiary will own the specified amount of assets. The beneficiary can then distribute or sell the assets to other nodes.

### Accessing Data

Based on assumption three, owning a single asset of an asset class grants the owner access to the underlying data stored in IPFS. To retrieve data, a node makes a request to Iris, adding a request to retrieve bytes to the queue. An OCW processes the command and adds the fetched content to local offchain storage. The node which requested the data can then invoke the `iris_retrieveBytes` RPC endpoint exposed on the node who fetched the content in order to retrieve it. 

First, a node that owns some positive balance of an asset requests access to it. When this request is processed by an OCW, the result is that the OCW stores the data in offchain storage. When the RPC endpoint is invoked by the right now, the data is returned to the authorized caller in the response.

![data-ejection part 1](./resources/data_ejection_p1.drawio.png)

## Storage

Storage is provided to the network by the network validators. Any network validator has the ability to provide at-will storage to the network.

Storage in Iris is session based.

Prior to a session, a validator can request to store some content, as identified by its asset id and owner. First, the call to the extrinsic results in the node being added to a collection of candidate storage providers for that asset class. Next, a command is issued to the DataQueue that will only be processed by the validator who made the original call. When processed, the validator attempts to pin the CID to their embedded IPFS node. If successful, the node submits an extrinsic to tell the network that the cid is pinned.

On the start of each new session, the candidate storage providers who have proved they pinned the content are moved to the active storage providers collection for the duration of the session.
