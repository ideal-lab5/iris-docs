# Extrinsics

### Iris Pallet
public 
`ipfs_add_bytes`
- entrypoint to add data to iris and create a ticket

permissioned
`submit_ipfs_results`
- only callable by offchain workers
- updates runtime storage to encode: owner -> cid -> ticket_config