---
description: FRAMPallets are individual pieces of runtime logic for us in FRAME runtimes.
coverY: 0
---

# 🏗 FRAME Pallet

substrate\_ _has a long list of pre-packages pallets, but you can also build your own or modify one built by the substrate_\_ team.

## Pallet Structure

A pallet is composed of a few building blocks. These are:

1. [Imports](./#imports-and-dependencies)
2. [Declaration of Pallet Type](./#declaration-of-the-pallet-type)
3. [Runtime Configuration Trait](./#runtime-configuration-trait)
4. [Runtime Storage](./#runtime-storage)
5. [Runtime Events](./#runtime-events)
6. [Hooks](./#hooks)
7. [Extrinsics (Dispatchable Calls)](./#dispatchable-call)

### No Std

The first line of code, always. It tells the rust compiler not to use Rust's standard library except when explicitly told so.

{% hint style="warning" %}
Substrate runtimes are compiled to WASM and a regular native binary so you **do not have access to rust's standard library**.&#x20;

This means simple things like printing to the command line using `println!` will not compile.&#x20;

[Learn more here](https://substrate.recipes/runtime-printing.html#printing-from-the-runtime).
{% endhint %}

### [Imports](https://app.gitbook.com/o/VlWTV0GJXmoHRKrDvk52/s/3UKO6MPPEQpqMJk5aWx1/\~/changes/2r7eGDMAwFdUD41dlSl4/frame-pallet/imports)

This is where crates are imported, especially the substrate\_ framework crates.&#x20;

All pallets will import `frame-support` and `frame-system`&#x20;

```rust
pub use pallet::*;
// other global dependencies...

#[frame_support::pallet]
pub mod pallet {
    use frame_support::pallet_prelude::*;
    use frame_system::pallet_prelude::*;
    // other pallet dependencies...
```

### Declaration of the Pallet Type

A placeholder to implement traits and methods.

```rust
    #[pallet::pallet]
    #[pallet::generate_store(pub(super) trait Store)]
    #[pallet::generate_storage_info]
    pub struct Pallet<T>(_);
```

### [Runtime Configuration Trait](https://app.gitbook.com/o/VlWTV0GJXmoHRKrDvk52/s/3UKO6MPPEQpqMJk5aWx1/\~/changes/xXqaDNctfMMobhev7VOT/pallet/configuration-trait)

This is used to access features from other pallets, or constants that impact the pallet's behavior.

{% hint style="info" %}
This is the part of the code where you say "hey I'm going to create some functions that do with something I'll call `coin` and I'm going to have the be the `coin` that's defined in the other pallet....but I'm going to also cast votes, so my `votes` will be the ones defined in that other voting pallet"
{% endhint %}

The `Config` trait allows you to do the above while keeping `Generic Types` so you can change define and use something called `coin` or `votes` from some other `Pallet` defined at runtime, but swapped with some other pallet with a runtime update later on.

### [Runtime Storage](runtime-storage.md)

Have some custom data you want on the chain for users or otherwise?

`Runtime Storage` is where you do that. You declare storage items you'd like to make accessible to runtime.

### [Runtime Events](runtime-events.md)

Events are how you communicate back to people using the block chain like "transaction confirmed!" or "error! not enough cash!"

### [Hooks](hook.md)

This is  where you'd build some logic that can be executed regularly in some context, for e.g. on\_initialize.&#x20;

Basically, your blockchain's equivalent to handling webhooks.

### [Extrensics (Dispatchable Calls)](https://app.gitbook.com/o/VlWTV0GJXmoHRKrDvk52/s/3UKO6MPPEQpqMJk5aWx1/\~/changes/HQOUCVHJR1sNlGKXFbuy/frame-pallet/extrinsics-dispatchable-calls)

These are functions that blockchain users can call. This is often called a `Dispatchable Call`.

#### decl\_module!

This is the macro where dispatchable calls are composed.

## A Little More on Each Topic

{% content-ref url="imports.md" %}
[imports.md](imports.md)
{% endcontent-ref %}

{% content-ref url="runtime-configuration-trait.md" %}
[runtime-configuration-trait.md](runtime-configuration-trait.md)
{% endcontent-ref %}

{% content-ref url="runtime-storage.md" %}
[runtime-storage.md](runtime-storage.md)
{% endcontent-ref %}

{% content-ref url="runtime-events.md" %}
[runtime-events.md](runtime-events.md)
{% endcontent-ref %}

{% content-ref url="hook.md" %}
[hook.md](hook.md)
{% endcontent-ref %}

{% content-ref url="extrinsics-dispatchable-calls.md" %}
[extrinsics-dispatchable-calls.md](extrinsics-dispatchable-calls.md)
{% endcontent-ref %}
