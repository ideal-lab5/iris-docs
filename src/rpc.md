# RPC

Iris only exposes one custom RPC endpoint. The retreiveBytes endpoint allows authorized nodes to fetch data from the iris network.

## Spec

- `iris_retrieveBytes`
- Description: This RPC endpoint allows external origins to access data to which they have been granted access.
- Parameters:
  - asset_id: The desired asset id

## Implementation

The RPC endpoint reads from offchain storage to fetch the bytes.

Invocation of this endpoint necessitates a few prerequisites:

1. The node owns an asset minted from some asset class
2. Some node is storing the data in the embedded IPFS node, be it a storage provider, the data owner, or just some other consumer who has already requested the data.
3. The node has invoked the `request_bytes` extrinsic, which fetches the data from IPFS and adds it to offchain storage

## Example

Assume that you have requested access to some CID: QmVsbXUbr5JwUDibTBmmh224GhWy1FWguTbHb3DTU3ahTE. First, convert the CID to hex: 0x516d56736258556272354a775544696254426d6d6832323447685779314657677554624862334454553361685445

and use it as the message field value, passing empty bytes to the other fields.

curl http://localhost:9933 -H "Content-Type:application/json;charset=utf-8" -d '{"jsonrpc": "2.0", "id": "1", "method": "iris_retrieveBytes", "params": ["392"]}'
