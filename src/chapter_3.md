# Assets

The main pallet we provide is built as a wrapper around the assets pallet.

## The Ticket Asset Class
When a node adds data to Iris it also constructs a new asset class backed by some initial amount of native tokens  (OBOL). 

The creator of this asset class is then authorized to mint new assets, which we refer to as `tickets`. Our initial use case makes a few assumptions that we will break in the future.
- Each owner and CID combination has at most one associated asset class
- Asset classes can correspond to at most one owner/CID combination
- Owning a non-zero quantity of assets in an asset class grants the owner access to the underlying data

### Asset Class Creation
The Asset class is created when an owner adds some data to the network via the `ipfs_add_bytes` extrinsic. The calling node submits all needed parameters, which are passed through to an OCW who then becomes responsible for creating the asset class on behalf of the original caller after it has process an IPFS request. To be explicit, apart from the file data's existence to be confirmed, to create the asset class we require:

- balance: The initial balance to back the asset (in the native token OBOL)
- assetId: A unique id to identify the asset

#### Asset Id generation


### Creating Tickets 
To be cute, I would like to call this "printing tickets" but we'll save that for later...
After an asset class has been created for some associated owner/cid combination, the owner of the asset class can then mint tickets (i.e. assets) within that asset class. This is done through another extrinsic: `mint_tickets`.

### The Asset Graveyard
In order to ensure that dead assets don't build up in runtime storage in the future, we implement a mechanism that destroys asset classes if the underlying data is unavailable for some amount of time. Or maybe even better, the asset class is deflationary: The owner must continue to resupply the underlying, supporting balance, otherwise the asset class collapses and is destroyed, and the underlying data is no longer protected from removal from the network. 
