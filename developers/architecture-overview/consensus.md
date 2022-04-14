---
description: Notes about the chain spec, and launching nodes..
---

# 🥝 Consensus

## Separating Block Production and Finality

The build3 chain adopts the concept of separating block production and block finality.

{% hint style="info" %}
The hash function used in this blockchain currently follows the BLAKE2 secure hashing function.
{% endhint %}

### Aura: Proof of Authority

Aura (Authority Round) authors a block based on proof of authority protocol from substrate\_'s `aura` pallet which also extends the consensus by allowing offline reporting.

In Aura, each block is authored in a series of discrete steps of a given constant duration:

$$
StepNumber=\frac{UnixTime}{Duration}
$$

The leader of each step is the only step permitted to issue the single block and is determined by calculating the remainder of the quotient between the step number and number of authors.

$$
Leader=StepNumber\pmod{N}
$$

The leader chooses the longest chain seen so far and authors a new block to it.

This consensus mechanism follows the fork choice rules of GRANDPA finality.

{% hint style="info" %}
Proof of Authority networks are permissioned not public and only strictly defined authority nodes are allowed to seal blocks.
{% endhint %}

### Who Can Author Block for Build3?

The authorship rights are granted to Build3 researchers in accordance with their commitment to research of the technology for the industry. The security is introduced through the idea that attacking a network you worked to build would do harm to your efforts to contribute to the technology.&#x20;

A layer of governance may be included to add a delegated proof of stake similar to the Polkadot network.

## GRANDPA: Finality Gadget

The blockchain implements the GRANDPA (GHOST-based Recursive Ancestor Deriving Prefix Agreement) finality gadget discussed in the [GRANDPA paper](https://github.com/w3f/consensus/blob/master/pdf/grandpa.pdf) on deterministic finality.

The GRANDPA gadget imports blocks produced from the Aura consensus production to determine the final state of the block production deterministically.

With GRANDPA finality, the validators vote on the chains instead of the blocks. The chain with the highest block number and enough votes is considered to be final, finalizing several blocks in one round.

### The GRANDPA Round

#### Primary Node Proposes Block

A new round starts when the **primary node** **broadcasts** **blocks** they estimate might have been finalized within a specific chain from the previous round.

#### Nodes Pre-Vote

After a pre-determined time from the broadcast, validators broadcast a pre-vote. The validators cast a prevote for the **head** of the best chain containing the **broadcasted blocks.**&#x20;

{% hint style="success" %}
If the primary node broadcasts a new **finalized block** that is at or **before (or is) the header of the broadcasted chain** but is **after all estimated finalized blocks**, then the nodes use the best chain containing that newly finalized block instead.
{% endhint %}

#### Nodes Pre-Commit

The pre-commit occurs after a fixed time when a supermajority is possible for any complete-able round. When a node observes a chain with the **header block** from the **broadcasted chain** any time later than all the **estimated finalized blocks,** it broadcasts a pre-commit.&#x20;

When a **block header** receives a **pre-commit** that extends the existing chain and contains a **supermajority** then it is finalized and becomes the new header.

## Running, Configuring, and Developing Nodes

The CLI that ships with the installation is configured with chain specifications:

* Development - A single validator network where the node that starts is a validator. This is convenient for a quick test of a new local feature because it starts producing blocks immediately.
* LocalTestNet - A dual validator network that adds bob as a validator so producing blocks takes a bit more configuration. This setup is convenient for a test net to simulate a more accurate environment.&#x20;

## Configuring Nodes

[Great documentation](https://docs.substrate.io/tutorials/v3/private-network/) at the end of this tutorial, but the summary is:

* Use a password to generate an Sr25519 Key for Producing Blocks Using `aura`
* Use the secret phrase from the previous `aura` account to generate Ed25519 key for finalizing blocks using `grandpa`.
* Polkadot's [technical reasoning ](https://wiki.polkadot.network/docs/learn-keys#:\~:text=There%20are%20no%20differences%20in,implementing%20more%20complex%20protocols%20safer.)for these keys.
* Export the spec to json format on CLI

```json
./target/release/your-node-name build-spec --disable-default-bootnode --chain local > customSpec.json
```

* Edit json to add the keys created earlier or to make further customizations.
* Convert json to raw format.

```
./target/release/your-node-name build-spec --chain=customSpec.json --raw --disable-default-bootnode > customSpecRaw.json
```

* purge old chain data if needed with

```
./target/release/your-node-name purge-chain --base-path /tmp/node01 --chain local -y
```

* Fire up the nodes...

```
./target/release/substrate-contracts-node \
--base-path /tmp/blockchoy_1 \
--chain ./customSpecRaw.json \
--port 30333 \
--ws-port 9945 \
--rpc-port 9933 \
--telemetry-url "wss://telemetry.polkadot.io/submit/ 0" \
--validator \
--rpc-methods Unsafe \
--name BlockChoy_1
```

This will start the validator, but it is not authorized to mine blocks yet. Add the `aura` and `grandpa` keys to authenticate the validation.



