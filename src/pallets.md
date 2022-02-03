# Pallets

Iris provides two new pallets on top of those available by default in Substrate.

![runtime modules](./resources/runtime_modules.png)
*Modules unique to iris are marked in purple. Dependencies are represented as arrows*

The [Iris-Assets](./pallet_iris_assets.md) pallet provides functionality for nodes to inject data into Iris, create and manage storage asset classes and to mint and burn assets.

The [Iris-Session](./pallet_iris_session.md) pallet provides session-based storage capabilities for network validators as well as enables ejecting data from the network. The iris-session palelt contains all functionality to interact with the embedded IPFS node. While a strict content-owner only node does not require the iris-session pallet, for both consumers and storage providers it is a necessity.

These two pallets work in tandem to provide full functionality to inject and eject data from Iris. Though we discuss both pallets in depth in their respective chapters, here we will lay out the way that the two pallets work together to inject data, create asset classes, and to eject data. In general, the iris-assets pallet is responsible for adding commands to the data queue and the iris-session pallet is responsible for executing commands in the data queue.

## Data Ownership as Asset Class Ownership

When a node adds data to Iris, the OCW that processes the request constructs a new asset class backed by some initial (user defined) amount of native currency (see the `create_storage_asset` [extrinsic](./chapter_3.md)). This results in a new `DataCommand` being added to the processing queue. When an OCW proceses the command and publishes results on chain, a new asset class is created. Asset creation and access is initiated in the iris-assets pallet but processed in the iris-session pallet.

![data-ingestion](./resources/data_ingestion.drawio.png)

Our initial use case makes assumptions that we will break in the future:

1. There is an injective and surjective map between owner/cid and asset class.
2. Owning any non-zero quantity of assets in an asset class grants the owner access to the underlying data

### Accessing Data Via Minted Assets

To retrieve data, a node makes a request to Iris, adding a request to retrieve bytes to the queue. An OCW processes the command and adds the fetched content to local offchain storage. The node which requested the data can then invoke the `iris_retrieveBytes` RPC endpoint exposed on the node who fetched the content in order to retrieve it.

First, a node that owns some positive balance of an asset requests access to it. When this request is processed by the calling node's OCW, the OCW stores the data in offchain storage. When the RPC endpoint is invoked, the data is returned to the authorized caller in the response.

![data-ejection part 1](./resources/data_ejection_p1.drawio.png)
