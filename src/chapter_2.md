# Adding Data
The basic flow when adding data:

Let C be a consumer node and S be an iris validator node. Then data ingestion works by:
1) S disconnects from the private network
2) S connects to a multiaddress provided by C
3) S fetches a CID provided by C 
4) S disconnects from the multiaddress provided by C
5) S adds the data to its local node
6) S updates runtime storage to map ownership to new ticket configuration
7) S connects to the private network

## Tickets
When a node adds data to the network we let them provide any necessary data/configuration to construct and sell a ticket that lets others access their data.

### Ticket Configuration
Ticket configuration is intended to be extensible. 
In the future, accepted fields in a ticket will be determined by the network via a governance module, but for now we keep it as simple as possible.

```
{
    name: Vec<u8>,
    cost: i32,
}
```

When a node invokes the `ipfs_add_bytes` (name TBD + add link) extrinsic, they provide this minimum set of information needed to mint a ticket later on. 

### Ticket Creation and Purchase


### Ticket Usage and Validation