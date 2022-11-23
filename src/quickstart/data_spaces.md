# Data Spaces

TODO:

- move RuleExecutor and composable access rules to dataspace level

## What is a data space?

A data space is a user created and owned 'space' that data can be associated with. Data spaces allows nodes to group together disparate data sets based on ownership of the data asset classes that the data is associated with. A data space allows the owner to specify which nodes are authorized to associate data with their space. Data spaces form the basis for moderation within the network.

For example, a dapp developer may want all data added to iris that should be associated with their application to be both easily found within Iris and also subject to additional checks specific to their application, such as only allowing certain types of file extensions or moderating data in some specific way (more on this in the moderation and governance section). By creating their own data space, the owner can authorize users of their dapp to associate data with the space.


## The Role of Dataspaces

- search/indexing/subindexing?
- TPRE
- availability
- moderation
- dataspace owners pay to maintain storage?
- dataspaces should have rules for who can deposit data (e.g. shareholders only)

## Creating a Data Space

A data space is really an asset class mapped to a set of configuration items.

## Granting access

To grant access to your data space to another address in the network, mint new assets from the asset class and assign them to the given address. This can be done in several different ways with varying degress of control over how the holder of the asset can associate their own data assets the data space. In general, either the owner of the asset class can:

- lock transfers of the asset, meaning the holder cannot transfer it to any other accounts
- retain rights to revoke the asset, meaning the data space administrator can block previously authorized users

![data spaces](../../resources/data_spaces.png)


 ## Data spaces and TPRE

Dataspaces allow the Iris network to perform TPRE without the need for the data owner (DO) to provide a new re-encryption key each time that a data consumer (DC) wants to access data associated with their asset class. Really, what we're accomplishing here is a mechanism to share a secret key without exposing it to the network. 

In the following, let $enc^{SK}_{PK_0, .., PK_m}(f)$ represent the data $f$ encrypted using the public keys $PK_0, ..., PK_m$ and secret key $SK$. When $SK = {PK_0,  ..., PK_M}$, we omit the superscript and simple write $enc_i(m)$, where $i$ represents some address with a public/secret key pair.

Let $DSO$ represent the owner of a dataspace $DS$ and $S = {s_1, ..., s_k}$ be the set of shareholders of the dataspace (addresses that hold some quantity of the asset minted from $DS$). Assume that a data owner, $DO$, owns some asset $A$ associated with some data $f$. Now, we will detail the process through which $DO$ can associated their asset with $DSO$ to enable the data to be retrieved from the network.

In the following, let $\delta, \theta > 0$ represent the shares of key fragments to create and threshold be the number of fragments needed to reconstruct the reencryption key, respectively. In order for the data associated with the asset $A$ to be accessible outside of the network, $DO$ must depsoit their data to a dataspace. By deposit we mean that $A$ must generate $\delta$ key fragments of the secret key used to encrypt the data $A$ and distribute each fragment to a distinct proxy node.

$DO$ generates a keypair $(PK_A, SK_A)$ and uses it to construct the ciphertext of their data $f -> enc_{PK_A}^{DO}(f) -> C_f$.
Next, $DO$ uses generates key fragments such that they enable us to perform $\{\delta, \theta\}$ -TPRE. So we perform:
$(C_f, \delta, \theta, SK_A, PK_{DO}) -> \{k_1, ..., k_\delta\}$. Each $k_i$ is then assigned to a distinct shareholder $s_i \in S$. For each $i = 1, ..., \delta$, $DO$ generates $enc_{PK_{s_i}}^{DO}(SK_A)$ and gossips the encrypted key fragments to the network. 

Now suppose some data consumer node, $DC$, wants to retrieve the data associated with the asset class that was deposited into the dataspace $D$. In order to do so, $DC$ requires the secret key $SK_A$ in order to recover the plaintext $enc_{SK_A}^{DO}(f) -> f$. To recover the secret key, $DC$ must collect $\theta$ key fragments from shareholders of the dataspace. The recovery process is triggered when $DC$ invokes the rule executor associated with the dataspace. If each composable access rule evaluates to true, then the data becomes unlocked for $DC$ within the dataspace $DS$. This authorizes $DC$ to request key fragments from up to $\theta$ shareholders. When each key fragment is recovered, $DC$ uses each fragments to recover the secret key $SK_A$, after which they use the secret key to decrypt the data.
