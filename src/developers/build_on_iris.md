# Build on Iris

This document serves as a holistic guide on how to build an app and run it on Iris.This document is subject to radical change as the project continues to be developed.

## Key Generation

When a consumer invokes a rule executor to request decryption rights, a 32-byte X25519 public key must be passed to Iris (via the rule executor contract). The corresponding secret key is then used in the final decryption step in order to complete decryption of the data. We place no restrictions on reusing keys, and leave that at the discretion of the consumer as well. In essence, your keypair acts as your password required to decrypt the data. 

*Note*: If in the future the protocol is tweaked so that the proxy node does not generate an ephemeral keypair for the caller, then this will no longer be needed.

