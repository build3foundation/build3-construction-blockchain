---
description: >-
  The configuration trait is a way for you to allow external pallets to define
  the element types being used on your internal pallet.
---

# ⚙ Runtime Configuration Trait

substrate\_ is taking full advantage of the [extensibility features of Rust](https://permitzip.gitbook.io/building-blockchain-applications/core-knowledge/data-structures/extensible-features) by implementing the `Config` object as a trait.

The best practice when building your pallet is to implement [Generic Types](https://permitzip.gitbook.io/building-blockchain-applications/core-knowledge/data-structures/extensible-features/generic-types).

This will allow you to create all the functionality you want while leaving the concrete types a decision made at runtime.

The `Configutation Trait` is the way that substrate\_ empowers the use of that extensible framework writing.

The `Configuration Trait` definition is a requirement for all [pallets](./).
