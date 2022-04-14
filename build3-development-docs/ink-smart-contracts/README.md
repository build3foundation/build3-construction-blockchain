---
description: The smart contract language and development tools for substrate_ frameworks.
---

# 🐙 ink! Smart Contracts

## What is ink!?

It's Solidity, but without the chains. Users can build smart contracts to deploy onto your blockchain, but they are also able to be deployed to other networks.&#x20;

Let's start with a review of the pre-built [examples](https://github.com/paritytech/ink/tree/master/examples) available by Parity. We'll offer some ideas of how to implement these into the Build3 blockchain to help provide context.

## Ready-to-Ship Examples

### [Delegator](https://github.com/paritytech/ink/tree/master/examples/delegator)

The delegator smart contract is the showcase for executing other smart contracts on-chain.&#x20;

It includes in total 4 different smart contracts

* Delegator (root): Delegates calls either to the Adder or Subber smart contract
* Adder: Increases a value in the Accumulator smart contract
* Subber: Decreases a value in the Accumulator smart contract
* Accumulator: Owns a simple `i32` value that can be incremented or decremented

#### Ideas

* An architect can be delegated the authority to submit product data for review on behalf of a trade contractor.

### [DNS Registration](https://github.com/paritytech/ink/tree/master/examples/dns)

Replace complicated, hard to remember addresses with simple domain names like `kenny.build3`

{% hint style="info" %}
`Note that all values are stored as hex and so a string must be converted to hex prior to registration.`

`The front end allows the user input`` `**`kenny.b3`**` ``but the storage is set at` 0x6b656e6e792e6233000000000000000 and assigned to the origin of the requester.&#x20;
{% endhint %}

### [Multisignature Authorization](https://github.com/paritytech/ink/tree/master/examples/multisig)

One origin with multiple signatories. The number of those parties signing can be configured and changed for each contract.  This can represent many things such as

* submittal approvals (trade contractor, general contractor, engineer, architect)
* general authorizations of work (hiring and working parties)
* certificates of occupancy (inspector, plan reviewer, engineer of record)

