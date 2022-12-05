# Getting Started

This is a minimal guide on how to build and run a full Iris node *locally*, both from docker and sources. For a full guide on properly setting up an hosted Iris node, see [here](../nodes/ec2_setup.md) 

1. [Installation](#installation)
2. [Running](#running)
3. [Interacting with your Node](#interacting-with-your-node)
4. [Testing](#testing)

## Installation

There are three ways to install iris, either building the source code, building a docker image, or simply installing from docker. The easiest and most reliable way to run an Iris is node is to 

### Run from Sources

#### Prerequisites

- [install Rust](https://www.rust-lang.org/tools/install)
- [install IPFS](https://docs.ipfs.tech/install/)

#### Build

``` bash
git clone https://github.com/ideal-lab5/iris.git
cd iris
cargo +nightly build --release
```

#### Run

``` bash
# purge the local chain data
./target/release/node-template purge-chain --base-path /tmp/alice --dev -y
# run the build
./target/release/iris-node \
  --base-path /tmp/alice \
  --dev \
  --alice \
  --port 30333 \
  --ws-port 9944 \
  --rpc-port 9933 \
  --rpc-cors all \
  --ws-external \
  --rpc-external \
  --rpc-methods=unsafe \
  --validator \
  --node-key 0000000000000000000000000000000000000000000000000000000000000001
```

Note: to specify a bootnode, use the bootnodes parameter. ex: `--bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWEdUQFXhAF4fu9hqRTWqsigioyjatRKRZ7mwyQCBoWyK3`

### Run from Docker

#### Prerequisites

- [install Docker](https://docs.docker.com/getdocker/)

Install from the docker hub
`docker pull ideallabs/iris`

**OR**

From the latest sources, build the docker image:
`docker build -t ideallabs/iris -f /Dockerfile .`

#### Run

``` bash
# run as validator node (e.g. first node)
docker run -p 9944:9944 \
  -p 9933:9933 \
  -p 30333:30333 \
  -p 9615:9615 \
  -it \
  --rm \
  --name iris-alice \
  ideallabs/iris \
  --dev --ws-external --rpc-external --validator --alice \
  --node-key 0000000000000000000000000000000000000000000000000000000000000001
```

## Interacting with your node

See [here](../developers/data_ingestion/md) for a more in depth treatment of 

### IPFS configuration
Update your ipfs configuration to specify the IPFS bootstrap nodes exposed by the testnet. This step will allow Iris gateway nodes to find your data.

These values are publicly available in the 'bootstrap nodes' runtime storage map in the ipfs pallet.

``` bash
# e.g. in the iris testnet
ipfs bootstrap add /ip4/18.118.65.202/tcp/4001/p2p/12D3KooWJ5wuqGnr6u8XV6FeBbP1MBBamUpavwfotRag2JnTrF9p
ipfs bootstrap add /ip4/3.12.124.166/tcp/4001/p2p/12D3KooWK4ASu9ik6RWJv8cRJ6ypg2rUpgR369gZjAZRVPJ41KpD
ipfs bootstrap add /ip4/3.14.26.5/tcp/4001/p2p/12D3KooWJHvwXTX8hrkZnYpegHMbxazRUFU8zgd99nFqmqbjN6B6
```

### The Iris UI

The Iris UI provides a mechanism to add and retrieve data from Iris, to create an asset class, mint assets, privision data access, and manage both asset classes and assets.

If you intend to add data to Iris, you must also run an IPFS node locally. This holds for running from sources as well as the docker image. Run IPFS with `ipfs daemon`.

#### Running from Sources

``` bash
git clone https://github.com/ideal-lab5/ui.git
cd ui
npm i
npm start
```

#### Running from Docker

``` bash
docker pull ideallabs/iris-ui
docker run -it --rm -p 3000:3000 ideallabs/iris-ui
```

### PolkadotJs

The [polkadotjs apps](https://polkadot.js.org/) user interface is a useful tool for interacting with and monitoring the network state.

#### Light Client

*Coming Soon*

- relay chain deployed
- parachain registered
- chain spec generation and distribution
- Configuration in iris ui

## Generating a custom chain spec

``` bash
cargo +nightly build --release
./target/release/iris-node build-spec --chain=dev --raw --disable-default-bootnode > iris.json
```

## Testing

Run the unit tests with `cargo +nightly test iris`.

## Guidelines

We aim for a minimum of 80% coverage on new code.

## Manual Testing

Our manual testing approach largely consists of invoking extrinsics and checking runtime storage. We do this using the polkadot UI:
https://polkadot.js.org/apps/

### Useful Tools

#### Calling substrate RPC endpoints

To convert strings to hex, I like this tool:
https://onlinestringtools.com/convert-string-to-hexadecimal

#### Querying Substrate Storage

https://www.shawntabrizi.com/substrate-js-utilities/
