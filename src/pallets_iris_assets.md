# Iris-Assets

The iris-assets module relies on the [assets module](https://github.com/paritytech/substrate/blob/master/frame/assets/README.md) available in Substrate. This pallet provides capabilities for content owners and content consumers. This module is entirely independent of IPFS. It provides capabilities to:

- inject data into the network
- create and manage storage asset classes
- mint assets

The iris-assets module delivers asset class and derived asset management. This module appends commands to a DataQueue which are processed by validator nodes (see the [iris-session](./pallets_iris_session.md) module for more info) in a module which implements logic for offchain workers to process commands in the DataQueue (in our case, the iris-session pallet).

## Runtime Details

### Content as an asset class

Asset class creation is accomplished through the `create` extrinsic. The extrinsic writes to the DataQueue, adding an Addbytes command. This command is processed by validator nodes in the iris-session pallet

### Access via Assets

After a node has successfully created an asset class, they can mint assets from the asset class. Each asset is synonymous with access to the underlying content.
