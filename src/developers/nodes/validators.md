# Validators

## Consensus

Currently Iris is a proof of authority network. Validator nodes are pre-defined or newly approved (by existing validators) nodes that are responsible for finalizing blocks in the network.

We intend to transition to a proof of stake system in the future.

## Becoming a Validator

Request to become a validator via the `add_validator` extrinsic in the [iris-session](../pallets/palles_authorities.md). When the network root node (Alice by default) approves the request, the node is added as a validator in the next session.
