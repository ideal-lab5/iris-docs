# Iris Asset Exchange

The Iris Asset Exchange is a decentralized exchange to facilitate the buying and selling of assets in Iris.

## Usage

The source code and README for the IAE is located [here](https://github.com/ideal-labs/contracts/tree/main/iris_asset_exchange).

The iris-ui exposes a user interface to interact with the contract.

## Functions

### publish_token_sale

Mint new tokens and gives ownership of them to the contract account. The owner specifies a static price that consumers pay in order to purchase the asset.

Parameters:

* asset_id: The id of some owned asset
* quantity: The quanity of assets to mint and transfer to the contract
* price: The price per minted asset

### purchase_tokens

1. lock price*amount tokens
2. transfer tokens to the caller (from the contract account)
3. unlock tokens
4. caller transfer tokens to the owner
