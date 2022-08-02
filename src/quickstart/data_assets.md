# Data Assets

Data assets form the core cryptographic relationship between data storage, access, and ownership.

## Adding data and Creating Asset Classes

To add data to the network, a data owner must first run the [offchain client](./offchain_client.md) and there must be at least one available [proxy node](./proxy.md). First, the desired data to be ingested is added to the offchain client. The data owner then invokes the `create` extrinsic from the [iris-assets](../pallets/pallets_iris_assets.md) pallet.

### Adding Composable Access Rules and Rule Executors

TODO

## Provisioning data access

To provision access to data, an owner of a data asset class mints new assets from the asset class and distributes them to addresses who should be allowed access (this is the same approach used by granting access to [data spaces](./data_spaces.md)).

## Retrieving data

To retrieve data to the network, a data owner must first run the [offchain client](./offchain_client.md) and there must be at least one available [proxy node](./proxy.md).
