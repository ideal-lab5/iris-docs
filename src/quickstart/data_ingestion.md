# Data Ingestion

This is a quick overview of how you can ingest data into the Iris network from a user interface and to create an owned data asset class. We won't go into details on specifics of the blockchain implementation or analyze runtime storage in this overview; if you're interested in a deeper look into the specifics take a look [here](../developers/data_assets.md). Examples are provided on how to use the polkadotjs SDK to interact with Iris.

*Note:* In the current version of Iris, only validator nodes are able to ingest data into the network.

## Data ingestion workflow

Data ingestion in Iris works through a multi-phase process. First, the data needs to be encrypted through the `iris_encrypt` RPC endpoint, which results in some encryption artifacts being encoded onchain while the caller is responsible for adding the generated ciphertext to IPFS and making their IPFS node discoverable by the iris gateway node IPFS network. Once added to IPFS, the data owner then invokes an extrinsic to 'complete' the ingestion of their data. Essentially, this sends a request to a gateway node to verify the data is properly encrypted, artifacts exists, the data is owned by the caller, and finally creates an data asset class on behalf of the caller, and we are done. 

### Step 0: Setup

Run an IPFS node and an Iris node. Either build your own network or connect to the testnet (as per the [quick setup guide](./quick_setup.md)). The only stipulation is that the network must have at least one proxy node and one gateway node availiable. Ensure that your IPFS node is properly configured as per the instructions [here](../developers/development_guide.md#ipfs-installation-and-configuration).

### Step 1: Encryption

In this first phase, we encrypt some plaintext using the `iris_encrypt` RPC endpoint exposed by each Iris node. The endpoint uses the umbral_pre TPRE library to generate new keys and encrypt your data. Subsequently, it sends an unsigned tx to include the generated 'capsule' and public key on-chain (see [iris protocol](https://github.com/ideal-lab5/whitepaper/blob/main/IRIS_PROTOCOL_DRAFT_0.0.1.pdf) for more details). To allow a valid address to be authenticated and used for signing, the endpoint requires the caller to pass their account id along with a signature and signed message, which is used to recover the caller's account.

**To choose a proxy node** query the x25519_public_keys runtime storage map in the 'Authorities' pallet and choose any validator with a key.

Messages can be signed with the polkadotJS library:

``` javascript
import { stringToU8a, u8aToHex } from '@polkadot/util';
// connect to node, create keyring and get 'account'
let message = 'random message';
let signature = account.sign(stringToU8a(message));
// convert the signature to hex before calling extrinsic
let sig_as_hex = u8aToHex(signature);
```

You can then call the iris_encrypt RPC with

``` javascript
 await api.rpc.iris.encrypt(plaintext, signature, signer, message, proxy)
        .then(res => success_callback(res))
        .catch(err => error_callback(err));
``` 

### Step 2: Add ciphertext to IPFS

First, ensure that your IPFS node is properly configured by attempting to find a peer who is mapped to a known validator (using `ipfs dht findpeer <peerID>`). This data is available in the 'SubstrateIpfsBridge' runtime storage map in the IPFS pallet.

Once the rpc call returns the generated ciphertext, the caller is responsible for choosing a gateway node and adding the ciphertext to an IFPS node that is reachable by the selected gateway. This would be handled within the `success_callback` that's called in the `then` block above by calling `ipfs add /path/to/ciphertext`. Once the data is in IPFS and the transaction submitted by the RPC call is encoded onchain, you can proceed to the next step.

### Step 2: Specify gateway node and complete request

Here we make a request to a gateway node to verify and ingest our data and to create a data asset class.
To do so, select a gateway node and call the `create_request` extrinsic exposed by the DataAssets FRAME pallet. This is the fist paid transaction for the caller, where they must pay the transaction fees as well as supply reserve currency to the requested gateway as incentive to process the transaction. Furturistically, we intent to add functionality to increase the priority of requests and to kill requests entirely. 

Using the polkadotjs SDK, this can be called as:

``` javascript
await api.tx.dataAssets.createRequest(gatewayAddress, gatewayReserveAmount, cid, multiaddress, existentialDeposit)
    .signAndSend(account, result => {
        if (result.status.isInBlock) {
            isInBlockCallback(result);
        } else if (result.status.isFinalize) {
            isFinalizedCallback(result);
        }
    });
```

### Step 3: Done!

If the gateway is able to successfully verify and ingest your data, then it will create a new data asset class on your behalf. See [here](../developers/nodes/gateway_node.md#asset_id_generation) for details on how asset ids are generated. 
