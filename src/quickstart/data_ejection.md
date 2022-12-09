# Data Ejection

## Step 1: Configure Data Authorization Mechanism

In this initial step, the data owner is responsible for configuring a mechanism to authorize access to their data. Through the 'Authorization' pallet, a data owner can register an account id with their asset id, delegating that account id the ability to grant data access to other participants in the network. There is no limitation, only that it be a valida account id. The simplest way to do this is to register your own id, in which case you would have to manually approve requests to access the data. Another approach would be to deploy a rule executor contract (or use one that is already deployed) to the chain and to register the contract's address withy our asset id. This will let you configure any conditions that you want a potential consumer to meet and also setup the mechanisms needed to automatically verify these conditions. 

To deploy a contract, we use the polkadotJS user interface and the Contracts pallet. For more info, see th e guide written by Parity [here](https://wiki.polkadot.network/docs/build-smart-contracts). You can read more about composable access rules and rule executors [here](../developers/contracts/composable_access_rules.md) for more information.

## Step 2: Generate Keys

During the data reencryption process, a proxy node generates a new keypair whose secret must be known (along with recovered capsule fragments) at the time of decryption. To secure this secret key, we allow the data consumer to pass a 32-byte public key built on curve 25519 that will be used to encrypt the newly generated secret. The corresponding secret key will be needed when we call decrypt in step 4.

Using javascript, the easiest way to generate the keypair is with tweetnacl:

``` javascript
const tweetnacl = require('tweetnacl');
let keyPair = tweetnacl.box.keyPair();
```

## Step 3: Invoke Contract

As a consumer, the registered rule executor is retrievable via the `Regsistry` runtime storage map in the 'Authorization' pallet.

Call the contract, passing your newly generated public key and the asset id of the asset 

## Step 4: Decrypt and Download data

In this final step, we finally decrypt ciphertext with the `iris_decrypt` RPC and then download the decrypted plaintext. We will also use the secret key from the keypair generated in step 2. 

First, ensure that the ciphertext is available in your IPFS instance (i.e. ensure `ipfs get <CID>` returns a value)

Then, the `iris_decrypt` RPC endpoint can be invoked with the following, where the message signing is the same process as when we [called the iris_encrypt rpc](./data_ingestion.md#step-1-encryption).

``` javascript
await api.rpc.iris.decrypt(ciphertext, signature, signer, message, assetId, secretKey)
    .then(res => successCallback(res))
    .catch(err => errorCallback(err));
```

And Voila! If successful, then the plaintext is recovered!