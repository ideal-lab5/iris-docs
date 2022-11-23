# Pallets

Iris provides several new pallets on top of those available by default in Substrate.

1. [Data Assets](./pallets/pallet_data_assets.md.md)
2. [Authorities](./pallets/pallet_iris_session.md)
3. [Ledger](./pallets/pallet_iris_ledger.md)
4. [Data Spaces](./pallets/pallet_data_spaces.md)
5. [Proxy](./pallets/pallet_proxy.md)

![runtime modules](./resources/runtime_modules.png)
*Completed and active modules are marked in purple, planned modules in yellow. Dependencies are represented as arrows*

## Data Spaces

The [Data Spaces](./pallets/pallet_data_spaces.md) pallet lets users define data spaces that data asset classes can be associated with.

## Iris Assets

The [Iris-Assets](./pallets/pallet_iris_assets.md) pallet provides functionality for nodes to inject data into Iris, create and manage storage asset classes and to mint and burn assets.

## Iris Session

The [Iris-Session](./pallets/pallet_iris_session.md) pallet provides session-based storage capabilities for network validators as well as enables ejecting data from the network. The iris-session palelt contains all functionality to interact with the embedded IPFS node. While a strict content-owner only node does not require the iris-session pallet, for both consumers and storage providers it is a necessity.

## Iris Ledger

The [Iris-Ledger](./pallets/pallet_iris_ledger.md) pallet allows nodes to lock, unlock, and transfer native tokens.

## Iris Storage

A to-be-developed pallet which will enable the storage system.

## Iris Proxy

A to-be-developed pallet which will enable proxy node functionality.
