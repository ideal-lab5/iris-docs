# Gateway Node

Gateway nodes are a subset of the Iris validator nodes. These nodes act as the gateway between the on-chain representation of data and the off-chain storage of data. This type of node is able to use permissioned off-chain calls that allow it to ingest data from other IPFS nodes, and in doing so, verify that the data exists and is decryptable, properly establish ownership models, and create asset classes on behalf of data owners.

## Staking and Slot Reservation

Since gateway nodes are responsible for creating asset classes, they are also ultimately responsible for generating the asset id of the new data asset class. To ensure that all asset ids are unique, at network gensis a static set of prime numbers, $p_1, ..., p_n$, is generated. When a node declares itself as a gateway, it claims an unclaimed prime from the list. As many gateways can be added as prime numbers are generated. The only limitation here is that we provide no mechanism to modify the asset id assignments after the runtime has been started. 

We refer to each of hese prime numbers as 'slots'. In order to act as a gateway, a node must:

- be a validator
- prove that they have a reachable IPFS node with storage capacity of at least 50GB.
- reserve a slot

In the current design, slot reservation only requires that a validator stakes 50 IRIS. Once done, if a slot is available then it can be claimed by the validator. In the future, we intend to explore an 'auction' based design wherein validator nodes can participate in 'slot auctions', reminiscent to 'parachain auctions' on Polkadot. Using this approach, we can add strict permissions around data asset class creation, ensuring that only authorized gateways have the capability. 

## Responsibilities

Gateway nodes are ultimately responsible for generating new asset ids and creating data asset classes. They do this by using the slot that they claimed when they became a gateway and then multiplying it by the number of time they've ingested data into the network. When requested by a potential data owner, the gateway node fetches data based on the CID that is provided to them. Though theoretically the data should already exist in the network, this allows the gateway node to verify that the CID provided to it indeed exits. Subsequently, the gateway uses the public key that should have been 'staged' by the caller in order to identify the associated encryption artifacts and ensure that they exists and a proxy has been assigned. Finally, the gateway node generates a new asset id and creates a new asset class.

## Stake Redistribution

TODO

## Rewards

TODO

## Slashing

TODO

