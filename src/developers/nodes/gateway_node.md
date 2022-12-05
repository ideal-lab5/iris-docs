# Gateway Node

We sometimes refer to these as proxy nodes as well.

Gateway nodes enable ingestion of data into the IPFS network. With the authorization mechanism determined by an election process, gateway nodes are responsible for allowing authorized nodes to invoke their RPC endpoint and to ingest data into IPFS.

## Responsibilities

Any validator node can declare their intentions to act as a gateway. When this is done, they're made capable of submitting a redistribution of their stake to pending ingestion requests. This redistribution acts as a weighted vote. After an election phase, ingestion requests in a pending queue are assigned to one or more gateway nodes which are then responsible for processing the request. This request is automatically processed by the offchain worker and requires no manual input or interaction.

## Stake Redistribution

During each election cycle, gateway nodes periodically redistribute their stake to items in the ingestion request queue. This is done by first filtering the list of ingestion requests by those which the gateway is capable of processing. Next, the node sorts the list by descending balance and chooses the first k items whose sum of total storage required doesn't exceed the total storage capacity of the node.

This process requires some major optimization, and should potentially be externalized. To externalize this, however, we would require some sort of bot/automation.

## Rewards

## Slashing