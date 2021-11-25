# Getting Started

1. [Installation](#installation)
2. [Running](#running)
3. [Interacting with your Node](#interacting-with-your-node)
4. [Testing](#testing)

## Installation

There are two ways to install iris, either building the source code, building a docker image, or simply installing from docker.

### Sources
```
git clone https://github.com/iridium-labs/substrate.git
cd substrate
git checkout iris
cargo +nightly build --release
```

### Docker
(The easiest way to install) DNE... future state.
`docker install iridium/substrate`

**OR**

From the latest sources, build the docker image:
`docker build -t iridium/substrate -f ./.maintain/Dockerfile .`



## Running

### From Source
```
# purge the local chain data
./target/release/node-template purge-chain --base-path /tmp/alice --dev -y
# run the build
./target/release/node-template \
  --base-path /tmp/alice \
  --dev \
  --alice \
  --port 30333 \
  --ws-port 9944 \
  --rpc-port 9933 \
  --rpc-cors all \
  --ws-external \
  --rpc-external \
  --rpc-methods=unsafe
```

Note: to specify a bootnode, use the bootnodes parameter. ex: `--bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWEdUQFXhAF4fu9hqRTWqsigioyjatRKRZ7mwyQCBoWyK3`

### From Docker
```
docker run -p 9944:9944 \
  -p 9933:9933 \
  -p 30333:30333 \
  -p 9615:9615 \
  -it \
  --rm \
  --name iris-alice \
  iridium/substrate \
  --dev --ws-external --rpc-external \
  --node-key 0000000000000000000000000000000000000000000000000000000000000001
```

*note: node-key is only needed if you want this node to be a bootnode*

# Interacting with your node
*See the [tech overview](../src/chapter_3.md) for information on extrinsics, rpc, etc.*

## PolkadotJs
As the UI undergoes development, the most reliable way to interact with your node is to use the default polkadotjs ui: polkadot.js.org/ .

## The Iris UI

FUTURE URL: https://app.iridium.industries

The Iris UI is an example of how to integrate with an Iris node. It provides a mechanism to add and retrieve data to/from Iris, to create an asset class, mint assets, and manage both asset classes and assets.

If you intend to add data to Iris, you must also run an IPFS node locally:
`ipfs daemon`

```
git clone https://github.com/iridium-labs/ui.git
cd ui
npm i
npm start
```

# Testing

Run the test with `cargo test`.

## Guidelines
We aim for a minimum of 80% coverage on new code. 

## Manual Testing
Our manual testing approach largely consists of invoking extrinsics and checking runtime storage. We do this using the polkadot UI:
https://polkadot.js.org/apps/

### Useful Tools
#### Calling substrate RPC endpoints

To convert strings to hex, I like this tool:
https://onlinestringtools.com/convert-string-to-hexadecimal

`curl http://localhost:9933 -H "Content-Type:application/json;charset=utf-8" -d '{"jsonrpc": "2.0", "id": "1", "method": "iris_retrieveBytes", "params": ["", "", ""]}'`

#### Querying Substrate Storage
https://www.shawntabrizi.com/substrate-js-utilities/
