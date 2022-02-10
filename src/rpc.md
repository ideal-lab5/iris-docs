# RPC

## Spec

- `iris_retrieveBytes`
- Description: This RPC endpoint allows external origins to access data to which they have been granted access. The account id should be the account id of the caller node.
- Parameters:
  - message: The CID to of the content to fetch encoded in hex

## Implementation

The RPC endpoint reads from offchain storage to fetch the bytes. Data is added to a unqieu node's offchain storage when the following conditions are met:

1. The node owns an asset minted from some asset class
2. A node is storing the data
3. The node invoked the `request_bytes` extrinsic

## Example

Assume that you have requested access to some CID: `QmVsbXUbr5JwUDibTBmmh224GhWy1FWguTbHb3DTU3ahTE`.
First, convert the CID to hex: `0x516d56736258556272354a775544696254426d6d6832323447685779314657677554624862334454553361685445`

and use it as the `message` field value, passing empty bytes to the other fields.

`curl http://localhost:9933 -H "Content-Type:application/json;charset=utf-8" -d '{"jsonrpc": "2.0", "id": "1", "method": "iris_retrieveBytes", "params":  ["0x516d56736258556272354a775544696254426d6d6832323447685779314657677554624862334454553361685445"]}'`
