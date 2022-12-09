# Composable Access Rules and Rule Executors

A **composable access rule** is a smart contract that allows data owners to define and specify unique business models which are executed when a consumer nodes attempts to fetch it from the network. Composable access rules are executed within the context of a **rule executor** contract. In general, each composable access rule should be as small as possible and only check for one condition. The idea is that composable access rules can be deployed to the network and then used within many different rule executors (more on this below). Composable access rules are by no means the only way to write rules for your data and are just one potential, resuable approach that can be taken. 

A **rule executor** allows a data owner to determine a unique collection of rules that shall be executed in order to provide authorization to data consumers to access their data. At a basic level, a rule executor makes cross contract calls to each composable access rule and then uses the `submit_execution_results` function exposed from our chain extension to report the results back on chain, which feeds into the locking mechanism managed by the [iris-ejection pallet](../pallets/pallet_iris_ejection.md). 

## How it works

A rule exeuctor can theoretically be any contract that can make calls to the Iris runtime using the 'submit results' chain extension. The owner of a data asset class must register a rule executor contract address with their data through the 'Authorization' pallet after the exeuctor is deployed and their data asset class exists. This delegates rights to the rule executor to grant access to other nodes that meet the rules specified. That is, every rule exeuctor must call:

``` rust
#[ink::chain_extension]
pub trait Iris {
    type ErrorCode = CustomError;
    #[ink(extension = 4, returns_result = false)]
    fn submit_results(
        caller: ink_env::AccountId, 
        consumer: ink_env::AccountId, 
        asset_id: u32, 
        result: bool, 
        public_key: [u8;32],
    ) -> [u8; 32];
} 
```

and invoke the chain extension function:

``` rust
 self.env()
    .extension()
    .submit_results(
        contract_acct,
        caller.clone(),
        asset_id.clone(), 
        true,
        public_key.clone(),
    );
```

And also be registered in the Authorization pallet.

## Available Rules

Composable Access Rules can be found in the [contracts](https://github.com/ideal-lab5/contracts/tree/main/composable_access_rules) repository

### Examples

See the examples folder of the github repo. 

#### Trivial Rule Executor

The trivial rule executor applies no rules. Basically, this means your data is free and open to anyone.

#### Limited Use Rule

The limited use rule contract specifies some number of times N that a consumer can use their asset to access the data.

### Example

For an example rule executor, take a look at the [contracts](https://github.com/ideal-lab5/contracts/tree/main/composable_access_rules/rule_executor) repository.