# Iris-Ledger

The ledger pallet is a utility pallet meant to facilitate locking and unlocking of funds to ensure existence of funds when buying and selling assets within the iris ecosystem.

## Runtime Details

### Extrinsics

- `lock` - lock some amount of native tokens
- `unlock_and_transfer` - unlock the locked tokens and transfer all to some specified account
