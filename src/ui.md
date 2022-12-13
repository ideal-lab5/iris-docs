# Iris UI

The UI is hosted at https://iris.idealabs.network. In order to use the hosted UI, you will need to be able to communicate with your IPFS over https.

The Iris UI provides a mechanism to add and retrieve data from Iris, to create an asset class, mint assets, privision data access, and manage both asset classes and assets.

If you intend to add data to Iris, you must also run an IPFS node locally. This holds for running from sources as well as the docker image. Run IPFS with `ipfs daemon`.

## Running from Sources

``` bash
git clone https://github.com/ideal-lab5/ui.git
cd ui
npm i
npm start
```

## Running from Docker

``` bash
docker pull ideallabs/iris-ui
docker run -it --rm -p 3000:3000 ideallabs/iris-ui
```

## PolkadotJs

The [polkadotjs apps](https://polkadot.js.org/) user interface is a useful tool for interacting with and monitoring the network state.

## Light Client

*Coming Soon*

- relay chain deployed
- parachain registered
- chain spec generation and distribution
- Configuration in iris ui