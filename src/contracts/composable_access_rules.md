# Composable Access Rules and Rule Executors

A **composable access rule** is a smart contract that allows data owners to define and specify unique business models which are executed when a consumer nodes attempts to fetch it from the network. Compo9sable access rules are executed within the context of a **rule executor** contract.

A **rule executor** allows a data owner to determine a unique collection of rules that shall be executed in order to provide authorization to data consumers to access their data. At a basic level, a rule executor makes cross contract calls to each composable access rule and then uses the `submit_execution_results` function exposed from our chain extension to report the results back on chain, which feeds into the locking mechanism managed by the [iris-ejection pallet](../pallets/pallets_iris_ejection.md).

## How?

All composable access rules are smart contracts which impement the ComposableAccessRule trait. In particular, each rule implements the function:

- `execute(asset_id, consumer_address) -> bool`: Execute the logic that determines if the consumer can or cannot access the data associated with the asset id.

A developer can then create their own rule executor, which instantiates the composable access rules that they want to execute and makes cross contract calls to get their results. A composable access rule contract can be simultaneously used by many rule executors. Finally, the `register_rule` extrinsic in the [iris-ejection pallet](../pallets/pallets_iris_ejection.md) allows the owner of an asset class to register a rule executor with their asset class, by supplying the rule executor's address and the asset id as parameters.

## Available Rules

We are in the process of developing several contracts that will be available in Iris. We intend to allows developers to deploy their own contracts as well. 

Composable Access Rules can be found in the [contracts](https://github.com/ideal-lab5/contracts/tree/main/composable_access_rules) repository

For now, we only have a single pre-defined rule available:

### Limited Use Rule

The limited use rule contract specifies some number of times N that a consumer can use their asset to access the data.

### Example

For an example rule executor, take a look at the [contracts](https://github.com/ideal-lab5/contracts/tree/main/composable_access_rules/rule_executor) repository.