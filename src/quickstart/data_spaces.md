# Data Spaces

## What is a data space?

A data space is a user created and owned 'space' that data can be associated with. Data spaces allows nodes to group together disparate data sets based on ownership of the data asset classes that the data is associated with. A data space allows the owner to specify which nodes are authorized to associate data with their space. Data spaces form the basis for moderation within the network. You can think of it like a DAO, where membership to the DAO (owning an NFT) allows you to associate your data with it. Or in other terms, a 'Dataspace' is like a directory the is read-only for all users unless they have special write permission.

For example, a dapp developer may want all data added to iris that should be associated with their application to be both easily found within Iris and also subject to additional checks specific to their application, such as only allowing certain types of file extensions or moderating data in some specific way (more on this in the moderation and governance section). By creating their own data space, the owner can authorize users of their dapp to associate data with the space.

## The Role of Dataspaces

Dataspaces allow dapp developers to have a modicum of control of what types of data is available within their applications and allows them to only allows data that they want. In essence, it provides the framework for moderation without censorship in a decentralized way. For example, suppose that you want to develop a decentralized marketplace to buy and sell the rights to music. Most likely, you would specifically only want files to be included in your marketplace if they are in specific formats for audio files (e.g. .mp3, .wav, etc). By creating a new dataspace, tokens can be minted and distributed to trusted nodes who must agree to the rules of the dataspace (e.g. only associating data with the given extension). If the rules are not followed, the node can be punished or access revoked, as per the rules of the dataspace. Presently, we have not yet designed or implemented the moderation or rule definition for dataspace members, however it will be part of the next iteration of Iris. 

## Creating a Data Space

A data space is really an asset class mapped to a set of configuration items. The creation of a dataspace is the creation of a new asset class and an entry in the 'Dataspaces' storage map, which maps the dataspace id to the dataspaces metadata, which is just the name of the dataspace currently. 

## Granting access

To grant access to your data space to another address in the network, mint new assets from the asset class and assign them to the given address. This can be done in several different ways with varying degress of control over how the holder of the asset can associate their own data assets the data space. In general, either the owner of the asset class can:

- lock transfers of the asset, meaning the holder cannot transfer it to any other accounts
- retain rights to revoke the asset, meaning the data space administrator can block previously authorized users

![data spaces](../../resources/data_spaces.png)
