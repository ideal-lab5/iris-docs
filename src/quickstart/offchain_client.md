# Offchain Client

*currently under development - The offchain client is not currently implemented*

Each data owner and data consumer runs an instance of an offchain client, which is embedded within the Iris node itself. The client acts both as a file staging server and as a means to retrieve files from proxy nodes. Communication with the offchain client is done solely through the Iris node's RPC endpoints. It also allows owners and consumers to fetch and injgest data into/from the network without having to run a full client. That is, it allows them to run a light client in the browser, which drastically increases the ease of use of Iris.

## Data Ingestion

The general idea is that data owners can place data within the offchain client to be fetched by proxy nodes when the data owners makes a request to ingest data into the network (and thereby creating a new data asset class).

## Data Ejection

The offchain client allows data consumers to receive data from proxy nodes when they request data from the network. Authorized users whose asset holdings pass the data asset classes composable access rules can accept connections from authorized proxy nodes to download data locally.
