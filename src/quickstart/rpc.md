# RPC Endpoints

*In Progress*

The RPC endpoints exposed by an Iris node are used primarly in order to facilitate data ingestion and ejection from the network. 

## Ingestion

To realize the full flow of data ingestion into the network, we use two distinct endpoints. One endpoint, callable only by the node itself, allows a data owner to add data to its offchain client. Another endpoint allows authorized proxy nodes to fetch data from the offchain client. To elaborate, these endpoints are:

- `iris_addBytes`
- `proxy_fetchBytes`

## Ejection

For data ejection, proxy nodes require no specific RPC endpoint. In the ejection flow, after gaining authorization to data by successfully execute a [rule executor]() associated with an asset class, a proxy node is selected and is then authorized to call a data consumers RPC endpoint, thus streaming the authorized data to the consumer's offchain client. Additionally, a data consumer has an endpoint it can call in order to eject data from its offchain client. To elaborate, these endpoints are:

- `iris_fetchBytes`
- `proxy_addBytes`
