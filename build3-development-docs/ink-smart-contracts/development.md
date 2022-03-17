---
description: >-
  An overview of building and configuring smart contracts with build3 foundation
  blockchain.
---

# 🕊 Development

## Getting Setup

The build3 framework is built using the contracts pallet and is compatible with the contract language [`ink!`](https://paritytech.github.io/ink/).&#x20;

Install the most recent working build.

{% hint style="info" %}
Pre-alpha release not ready. After all minimum features have been implemented, it will be posted. Stay tuned!
{% endhint %}

Install the [`ink! CLI`](https://github.com/paritytech/cargo-contract) `to aid in developing smart contracts`.

## Develop

### Creating

{% hint style="warning" %}
1. Ensure the ink! CLI is installed!
2. Do not create contract projects in the node directory
{% endhint %}

Navigate to a new directory outside of the node source code. This directory would ideally be dedicated to developing and compiling contracts.

Create new a contract using:

```bash
cargo contract new my_new_contract
```

{% hint style="info" %}
WARNING!\
The contract CLI tool may not build with the same parity scale index configuration. The Cargo.toml file will have to be updated to match the parity-scale-codec version and scale-info version from the installed  node.
{% endhint %}

The out of the box TOML file is confi

```toml
[package]
name = "flipper"
version = "0.1.0"
authors = ["[your_name] <[your_email]>"]
edition = "2021"
rust-version = "1.56.1"

[dependencies]
ink_primitives = { version = "3.0.0-rc8", default-features = false }
ink_metadata = { version = "3.0.0-rc8", default-features = false, features = ["derive"], optional = true }
ink_env = { version = "3.0.0-rc8", default-features = false }
ink_storage = { version = "3.0.0-rc8", default-features = false }
ink_lang = { version = "3.0.0-rc8", default-features = false }

# MAKE SURE THIS CODEC INFORMATION MATCHES THE BUILD. OUT OF THE BOX CLI IS 
# CONFIGURED TO 2.1 WHICH CAUSES ERRORS!
scale = { package = "parity-scale-codec", version = "3.0.0", default-features = false, features = ["derive"] }
scale-info = { version = "2.0", default-features = false, features = ["derive"] }

[lib]
name = "flipper"
path = "lib.rs"
crate-type = [
	# Used for normal contract Wasm blobs.
	"cdylib",
]

[features]
default = ["std"]
std = [
    "ink_metadata/std",
    "ink_env/std",
    "ink_storage/std",
    "ink_primitives/std",
    "scale/std",
    "scale-info/std",
]
ink-as-dependency = []

```

### Testing

Testing contracts in the off-chain environment provided by ink! is easy with:

```bash
cargo +nightly test
```

### Building

To build (compile your contract to WASM), **navigate to the contract directory** and run:

```
cargo +nightly contract build
```

### Reading

metadata.json is distributed with each build and has information about

* types - data types used
* storage - storage values within the contract and how to access them
* spec - information about callable functions

## Deploy

### Start the Node

Navigate to the node directory where a working release is installed.

Start the node in dev mode using:

```bash
target/release/substrate-contracts-node --dev
```

### Use substrate\_ Hosted UI

Go to the [substrate UI ](https://paritytech.github.io/contracts-ui/)with your running local blockchain and follow the instructions to deploy the contract code.
