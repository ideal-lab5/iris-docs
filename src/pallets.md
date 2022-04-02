# Pallets

Iris provides several new pallets on top of those available by default in Substrate.

1. [Iris-Assets](./pallet_iris_assets.md)
2. [Iris-Session](./pallet_iris_session.md)
3. [Iris-Ledger](./pallet_iris_ledger.md)
4. Iris Democracy: Planned
5. Iris Treasury: Planned

![runtime modules](./resources/runtime_modules.png)
*Completed and active modules are marked in purple, planned modules in yellow. Dependencies are represented as arrows*

## Iris Assets

The [Iris-Assets](./pallet_iris_assets.md) pallet provides functionality for nodes to inject data into Iris, create and manage storage asset classes and to mint and burn assets.

## Iris Session

The [Iris-Session](./pallet_iris_session.md) pallet provides session-based storage capabilities for network validators as well as enables ejecting data from the network. The iris-session palelt contains all functionality to interact with the embedded IPFS node. While a strict content-owner only node does not require the iris-session pallet, for both consumers and storage providers it is a necessity.

## Iris Ledger

The [Iris-Ledger](./pallets_iris_ledger.md) pallet allows nodes to lock, unlock, and transfer native tokens.
