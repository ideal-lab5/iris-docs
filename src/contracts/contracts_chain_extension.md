# Chain Extension

The iris chain extension provides functionality for dapp developers to hook into the iris runtime. More specifically, it exposes the ability to call extrinsics from the iris-assets pallet and the iris-ledger pallet to enable developers to manage assets via mint and transfer abilities and to lock, unlock, and transfer tokens to other accounts.

## Exposed Functions

### From the Iris-Assets pallet

See the [iris-assets](./pallets_iris_assets.md) for more details.

- create
- request bytes
- mint
- transfer_assets

## From the Iris-Ledger pallet

See the [iris-ledger](./pallets_iris_ledger.md) for more details.

- lock_currency
- unlock_and_transfer_currency

## Usage

To functions from the chain extension in your smart contract, register the chain extension:

``` rust
#[ink::chain_extension]
pub trait Iris {
    type ErrorCode = IrisErr;

    #[ink(extension = 0, returns_result = false)]
    fn transfer_asset(
        contract_account: ink_env::AccountId, 
        consumer_account: ink_env::AccountId, 
        asset_id: u32, 
        asset_quantity: u64
    ) -> [u8; 32];

    #[ink(extension = 1, returns_result = false)]
    fn mint(caller: ink_env::AccountId, target: ink_env::AccountId, asset_id: u32, amount: u64) -> [u8; 32];

    #[ink(extension = 2, returns_result = false)]
    fn lock(amount: u64) -> [u8; 32];

    #[ink(extension = 3, returns_result = false)]
    fn unlock_and_transfer(target: ink_env::AccountId) -> [u8; 32];
} 
```

and invoke the chain extension function:

``` rust
 self.env()
    .extension()
    .mint(
        caller, self.env().account_id(), asset_id, amount,
    ).map_err(|_| {}).ok();
```
