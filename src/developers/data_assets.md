# Data Assets

Asset classes form the core cryptographic representation of owned data within an on-chain context.

## Data Assets

In the context of Iris, an **asset class** is an owned 'class' that is able to mint **assets** from that class and distribute them to peers. At the bare minimum, each asset class has an owner, an administrator, a set of metadata which defines an identifier, along with functionality to mint assets defined by that asset class. That is, the asset class has an additional property, `supply`, which is the total number of assets minted from the class. For those familiar with EVM based smart contracts, asset classes behave similarly to an ERC20 contract, with coins minted by the ERC20 being synonymous with those derived from the asset class.

Taking this one step further, we introduce the concept of a `data asset class`, which Iris uses to verify existence, ownership, and accessibility of data. A data asset class is an asset class mapped to a set of metadata which identifies some ciphertext, based on a [CID](../glossary.md#cid), which has been verified as having been both properly encrypted and able to be decrypted by parties when they are authorized. In our network, data asset classes are (almost) never directly created by a data owner, but on their behalf by a 'gateway' node. The data asset class ties together data ingestion, encryption, and authorization into a cohesive cryptographically verifiable onchain entity. Further, it enables the fractionalization of data ownership (and thus fractionalization of rewards), the programmability of data access models, and more.

## Adding data and Creating Asset Classes

As can be seen from the description above, data asset class creation is always preceded by data encryption, ciphertext ingestion, and finally gateway node ingestion and verification.

The first step is to invoke the iris_encrypt RPC endpoint that is exposed by all Iris nodes. 

To add data to the network, a data owner must first run the [offchain client](./offchain_client.md) and there must be at least one available [proxy node](./proxy.md). First, the desired data to be ingested is added to the offchain client. The data owner then invokes the `create` extrinsic from the [iris-assets](../pallets/pallet_dat_assets.md) pallet.

### Adding Composable Access Rules and Rule Executors

TODO

## Provisioning data access

To provision access to data, an owner of a data asset class mints new assets from the asset class and distributes them to addresses who should be allowed access (this is the same approach used by granting access to [data spaces](./data_spaces.md)).

## Retrieving data

To retrieve data to the network, a data owner must first run the [offchain client](./offchain_client.md) and there must be at least one available [proxy node](./proxy.md).
