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

### Pinning Data
Our current scheme for pinning data is incomplete due to development underway on rust-ipfs. Until that development is complete, we will proceed with a modified version of the final pinning scheme.

In the final version, we intend to award unique assets to each node which is equivalent to the storage capacity that they have commited to Iris. That is, if a node configures X kb of storage for their embedded IPFS node, then they would be award x tokens to represent this. We then allow content owners to "lease" tokens from the storage provider at some interest rate which is paid out on regular intervals (some number of blocks as defined by the storage provider). However, the "stats" and "config" features are not yet available in rust-ipfs. Due to this, we are taking a somewhat altered approach temporarily, which will lay the groundwork for the scheme described above.

The modified approach is as follows:
1. A storage provider calls an extrinsic which allows them to create an asset class, set their storage rate, and mint some number of assets. The assets for now will each represent the fulfillment of a unique pin request made by a content owner.
2. Content owners can lease a *single* asset from the storage provider
3. When a token is leased, the storage provder fetches the data from the IPFS network and pins it to their node.
4. The size of the bytes that were retrieved is reported and can be used to determine a new storage rate.

- request that a node pins your content
- transfer of assets when pin request is fulfilled
- view files you pinned
- view your files pinned by others
- remove pin

