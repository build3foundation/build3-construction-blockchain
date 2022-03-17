---
description: The most critical imports for every Pallet
---

# ⬇ Imports

{% content-ref url="../other-important-crates/frame_system.md" %}
[frame\_system.md](../other-important-crates/frame\_system.md)
{% endcontent-ref %}

`frame_system` provides low-level types, storage, and functions for your blockchain.

{% content-ref url="../other-important-crates/frame_support.md" %}
[frame\_support.md](../other-important-crates/frame\_support.md)
{% endcontent-ref %}

`frame_support` is like a helper crate. It is a collection of macros, traits, and modules to simplify development of `FRAME Pallets`.

{% content-ref url="../other-important-crates/frame_executive.md" %}
[frame\_executive.md](../other-important-crates/frame\_executive.md)
{% endcontent-ref %}

The `frame_executive` acts as an orchestration layer for the runtime. It dispatches incoming extrinsic calls to the respective pallets in runtime.
