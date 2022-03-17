---
description: The system crate that defines the core types for runtimes.
---

# 📡 frame\_system

## frame\_system

You'll see this everywhere and wonder why. WHY!? WHAT IS THIS!? The same is true for `frame_support` but over time they start making sense.&#x20;

`frame_system` is the `System` crate that defines the core **types** for `runtime` such as Account ID, Header, Version, Hash, Origin, etc., as well as core [storage items](../frame-pallet/runtime-storage.md) such as Block Hash, Block Number, [Events](../frame-pallet/runtime-events.md), etc.

Luckily, substrate\_ makes it easy by including the `pallet_prelude` in both crates. Use this with the wildcard `*` and move on. You'll come back to it and it'll make more sense.

```rust
#[frame_support::pallet]
pub mod pallet {
    use frame_support::pallet_prelude::*;
    use frame_system::pallet_prelude::*;
    // other pallet dependencies...
```



## frame\_support
