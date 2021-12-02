# RPC

## Spec
- `iris_retrieveBytes`
- Description: This RPC endpoint allows external origins to access data that exists in Iris, to which they have been granted access. The account id should be the account id of the caller node.
- Parameters:
    - signature: A signature
    - account: An account id 
    - signed_message: A message signed by the account using the signature


## Implementation
1) verify signature
2) fetch data from offchain storage
3) return bytes