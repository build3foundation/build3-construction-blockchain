---
description: >-
  Allows control of membership of a set of AccountId's. Useful for managing
  membership of a collective.
---

# 🧜 Membership

This allows control of membership of a set of `AccountId`'s.&#x20;

This pallet stores&#x20;

* the list of members
* the `prime` member (master admin account for the membership)

Events are emitted when members are&#x20;

* added
* removed
* swapped
* reset
* changed

Users of authorized origin can

* add members
* remove members
* swap members
* reset members _not sure what this is yet_
* change key (user can change they key associated with membership to a different address)
* set prime (assign the prime member, must be by current member)
* clear prime (remove the prime member, can only be released by prime member)
