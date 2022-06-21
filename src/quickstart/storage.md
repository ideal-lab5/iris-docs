# Storage

*currently under development - The storage system is not currently implemented*
Iris is capable of integrating with nearly any storage system, be it centralized or decentralized. We accomplish this through the use of a generic storage connector module.

## Hot Storage

Iris uses embedded instances of IPFS to enable hot-storage within the runtime. It runs a secondary runtime, which runs the ipfs daemon within proxy nodes, allowing them to add, remove, pin, and cat data, as well as share it with other nodes. Additionally, this enables Iris to use the full power of IPFS to deliver data to consumers.

## Cold Storage

Cold storage is configurable within Iris via the storage connector module. Iris allows for the storage connector to be developed to support nearly any storage system, centralized or decentralized.

In our local test environment we enable storage to a local server.

Once we deploy to Kusama, we will leverage Crust as our cold storage solution.
