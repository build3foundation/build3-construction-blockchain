---
description: How to tell someone using your blockchain something happened.
---

# 👍 Runtime Events

Users of the application need feedback about what happened when they clicked something or interacted on your chain through a [public endpoint](https://app.gitbook.com/o/VlWTV0GJXmoHRKrDvk52/s/3UKO6MPPEQpqMJk5aWx1/\~/changes/xXqaDNctfMMobhev7VOT/pallet/dispatchable-call) you've given them.

Transactions can fail for any number of reasons, so your users need to know and that is handled through and `Event`. Confirmations are similar: tell your user it went okay with an `Event`.

## Right, so my pallet should be able to emit Events?

Yep, pretty much without exception. Here's how:

## In the Pallet

### type Event

Add `Event` type to the \`Config:

```rust
// Note: this is the pallet-required `Configuration Trait`
pub trait Config: frame_system::Config {
    
    // copy the line below exactly as shown into the `Config` section
    // of your `Pallet`. You'll eventually be able to interpret that
    // if you don't lnow. Just keep truckin'.
    type Event: From<Event> + Into<<Self as frame_system::Config>::Event>;

}
```

### decl\_module!

And now add the `decl_module!` ("declare\_module") macro to give access to the `deposit_event()` method.

```rust
decl_module! {
pub struct Module<T: Config> for enum Call where origin: T::Origin {

    // This line is new
    fn deposit_event() = default;

    // More dispatchable calls that you compose woud go here
    }
}
```

{% hint style="info" %}
**Reminder**: the `decl_module!` macro is the same we used for creating `Dispatchable Calls` for a `Pallet`.
{% endhint %}

### decl\_event!

`decl_event!` ("declare event") macro is the way Rust implements an event

```rust
decl_event!(
    pub enum Event<T> where AccountId = <T as frame_system::Config>::AccountId {
        EmitInput(AccountId, u32),
    }
);
```

{% hint style="warning" %}
We are showing generic types in these examples. The syntax for generic events **requires** the `where`.
{% endhint %}

## In the Runtime

We've defined a `trait` in the `Pallet` for `Config` and so now it has to be implemented at runtime.&#x20;

In your runtime `lib.rs` file, add

{% code title="./runtime/src/lib.rs" %}
```rust
impl simple_event::Config for Runtime {
    type Event = Event;
}
```
{% endcode %}

The code above is simply specifying the type for `Event` . Note the `<T>` is not shown and that is because we are defining the concrete type to be implemented by the `Pallet` we're configuring.

Add the events to the runtime build macro `construct_runtime!` by adding:

```rust
construct_runtime!(
    pub enum Runtime where
        Block = Block,
        NodeBlock = opaque::Block,
        UncheckedExtrinsic = UncheckedExtrinsic
    {
        // --snip--
        YourEventName: your_pallet_name,
    }
);
```
