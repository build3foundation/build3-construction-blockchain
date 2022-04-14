---
description: A record of signed and verified work transactions.
layout: editorial
---

# 🏔 Record of Work

## Qualitative Productivity as a Quantitive Measure

The quality and throughput have never been reliably measured. It works for specific talents and personality types.&#x20;

What we are talking about is a more true and revealing method of calculating what someone has contributed to their work. This allows for traditionally ignored traits of a worker can be made visible to the network.

The same protocols implemented in the [engineering supervision](proof-of-supervision-with-blockchain.md) use case also provide a more general-purpose proof of work for all players in the network. Any kind of work can be documented with this protocol.

### The Players

There are three humans in this interaction.

* **Worker -** The person that performs to the standard of care.
* **Reviewer -** The person that reviews the work against the standard of care.
* **Authenticity Validator -** The person that affirms both parties acted with good faith.

### Staking (Gamifying Quality Control)

{% content-ref url="../build3-development-docs/prebuilt-pallets/staking.md" %}
[staking.md](../build3-development-docs/prebuilt-pallets/staking.md)
{% endcontent-ref %}

#### Rewards a Function of n Reviews

The review checks the work against the claimed standard of care. If approved on

* Passes First Review: 10 tokens awarded to the worker
* Second Review: 2 tokens awarded to the worker
* Third Review: The total stake is lost and split between the network and burned
* Reviewer is paid 1 token per review
* The Authenticity Validator must affirm the authenticity of the transaction. If they reject the transaction, all parties lose rewards and stake.
