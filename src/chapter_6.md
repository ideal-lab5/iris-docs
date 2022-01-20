# Tokenomics
Here we present a breakdown of the tokenomics of the iris blockchain.

In Iris, there are three types of nodes that we care about:
1) Content Owner: A node who has added some content to iris and owns the corresponding asset class and is capable of provisioning access to it.
2) Content Viewer: A node who holds some asset minted from the content asset class, but is not necessarily the owner of the asset class.
3) Storage Provider: A node who owns some asset class and static amount of tokens and is capable of pinning data to their embedded IPFS node.

# Storage Provider
A storage provider is synonymous with a validator node.

# Content Owner

# Content Viewer

With that said, we will discuss the interactions between: 
* content owner and content viewer
* content owner and storage provider

There will never be transactions between the content viewer and the storage provider.

## Content Owner/Content Viewer 
This is generally understood and complete, leaving for later...

## Content Owner/Storage Provider
We use a session based model to store data.

### The Storage Pool
A storage pool is an object that represents storage of some CID corresponding to an owned asset class in Iris. 
The storage pool contains a maximum level of redundancy (i.e. max number of nodes to pin the data), the owner node,  as well as two collections of validator nodes. First is the candidate storage providers, and secondly the active storage providers ().

Prior to a subsequent session, validator nodes can request to become storage providers for some specific storage pool in the next session. When the request is successful, the node is added to a collection of candidate storage providers. When the next session starts, nodes that are part of the candidate pool become active storage providers. They must pin the CID that 