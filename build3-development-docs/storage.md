---
description: >-
  The block size limitations make storing large values a challenge. How do we
  deal with that?
---

# 🛰 Storage

## The Blockchain Data Storage Problem

Storing boolean and integer values is easy. Decimals are a bit more challenging. And strings are extremely limited.&#x20;

To make things a bit more constrained, `ink!` contracting language only allows a single low-level primitive, `Mapping` , for access to contract storage.

This means the front-end developers will have to continuously transform data for most RPC requests.

In practice, the [substrate primitives](https://docs.rs/substrate-primitives/latest/substrate\_primitives/) do not normally exceed 32 bytes for reasons outside of cryptographic security. The `H12` Struct allows for up to 64 bytes.  This paragraph is larger than 64 bytes.

## Off-Chain Workers

Substrate has pallet which off-chain computational efforts to occur. This is great because more complicated work should be taken offline, or all nodes would have to perform the same computations causing a massive bandwidth problem.

The substrate\_ off-chain worker subsystem allows for tasks that are data and computationally intensive to be performed without slowing down the block production.&#x20;

This allows for an asynchronous element of producing blocks to exist where a node will go off-chain, produce their results, and report back with the cryptographic results representing the results.

Check out this [Off-chain Worker Callback Example](https://gnunicorn.github.io/substrate-offchain-cb/)

This does not solve the storage problem. After all, the final result is just a hash of the final data, not the data itself.  The data can be stored in a database, but that comes at the cost of trusting someone to maintain a central database.&#x20;

There are likely many private companies that would append the blockchain by offering these services, but how can we find a way to persist the data for a longer period of time?

* This multifront-end developer will have to continually transform data for most RPC requests

## IPFS

IPFS is a peer-to-peer data storage system that helps to solve the large format, immutable and persistent storage dilemma presented by traditional blockchain.

Luckily, the IPFS development team has already worked to start solving this problem and they have constructed an [off-chain worker manual](https://rs-ipfs.github.io/offchain-ipfs-manual/introduction.html).&#x20;

More on this later.
