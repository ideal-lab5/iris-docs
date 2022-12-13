# Iris Quickstart

This guide shows you the easiest way to get an iris node up and running.

Note: Iris is designed specifically for linux based operating systems. If you are using Windows, it is heavily advised that you use wsl2 and install an Ubuntu distribution to run your node. It is not guaranteed to work on Windows.

## Prerequisites

- [install Docker](https://docs.docker.com/getdocker/)
- [install IPFS](https://docs.ipfs.tech/install/)

## Configure IPFS

First, we will configure IPFS so that it is reachable by our node and can be discovered in the DHT. This is a crucial step that will allow Iris to find your data. If not done correctly, you will not be able to interact with the data layer.

``` bash
# fetch the swarm.key and copy it to your .ipfs folder
wget https://raw.githubusercontent.com/ideal-lab5/iris/main/swarm.key
# ensure your IPFS node is reachable
ipfs config Addresses.API "/ip4/0.0.0.0/tcp/5001"
ipfs config Addresses.Gateway "/ip4/0.0.0.0/tcp/8080"
ipfs config --json API.HTTPHeaders.Access-Control-Allow-Origin "[\"*\"]"
ipfs config --json API.HTTPHeaders.Access-Control-Allow-Credentials "[\"true\"]"
# reconfigure bootstrap nodes
ipfs bootstrap rm --all
ipfs bootstrap add /ip4/18.118.65.202/tcp/4001/p2p/12D3KooWJ5wuqGnr6u8XV6FeBbP1MBBamUpavwfotRag2JnTrF9p
# start the daemon
ipfs daemon 
# verify connection by listing peers (may have to be done in new terminal)
ipfs swarm peers 
```

## Run Iris

The code snippet below shows you how to run an Iris validator node using the well-known 'Alice' account, which is predefined in the 'development' chain spec. If you're interested in running from other chain specs (e.g. connecting to a testnet) or building your own, see the [development guide](../developers/development_guide.md#generating-a-custom-chain-spec)

``` bash
# pull the latest iris docker image
docker pull ideallabs/iris
# pull the latest chain spec
wget https://raw.githubusercontent.com/ideal-lab5/iris/main/iris.json
# run an iris node
docker run --add-host host.docker.internal:host-gateway -p 9944:9944 -p 9933:9933 -p 30333:30333 -p 9615:9615 -v ~/iris.json:/mnt/iris.json -it --rm --name iris-node ideallabs/iris --chain=/mnt/iris.json --rpc-cors all --unsafe-ws-external --rpc-external --rpc-methods=unsafe
```

If you want to connect to a different chain, you can use [your own chainspec](../developers/development_guide.md#generating-a-custom-chain-spec) or specify the chain as `--chain=dev` or `--chain=local`, which are both available to all nodes.