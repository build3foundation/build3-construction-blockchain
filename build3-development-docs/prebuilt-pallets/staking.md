---
description: Used to manage funds as stake by network maintainers.
---

# 🍶 Staking

## Overview

Manage funds at stake by network maintainers.

This allows a user to voluntarily place funds under deposit. These funds are rewarded under normal operation but are slashed should the staked maintainer be found not to be discharging duties properly.

### Validating

A `validator` is responsible for validating the block. In this scenario, the block is the contributing work entry being claimed.

Validators are chosen on rotation based on regular elections in each `era`.

### Nomination

A `nominator` votes on a set of \`validators to be elected. Once interest in nomination is stated by an account, it takes effect at the net election round. The funds in the nominator's stash account indicate the weight of its vote. The rewards and punishment that a validator earns are shared between the validator and its nominators.

{% hint style="info" %}
Since nominators and validators share punishment and rewards it incentivizes the nominator to NOT vote for misbehaving/offline validators as much as possible, simply because the nominators will also lose funds if they vote poorly.
{% endhint %}

An account can become a nominator via the `nominate` call.

### Voting

Actual validators are chosen from among all potential validators via election by the potential `validators` and nominators. The term `voters` is used to represent the union of `potential validators` and `nominators` all of whom participate in the election process.

The current election algorithm is implemented based on [Phragmén](elections-phragmen.md).

The election algorithm's first priority is to elect validators with the most stake value and votes.

Then it tries to divide the nominator votes among candidates in an equal manner.

Optional post-processing can be applied to iteratively normalize the nominator staked values until the total difference among voters of a particular nominator is less than a threshold.

### Rewards and Slash

The `Pallet` is attempting to embrace valid behavior while punishing any misbehavior or lack of availability.

Rewards must be claimed for each era before it gets too old by $HISTORY\_DEPTH using the `payout_stakers` call.&#x20;

#### Slash

Slashing can occur at any point in time, once misbehavior is reported. Once slashing is determined, a value is deducted from the balance of the validator and all nominators who voted for this validator.

The logic for slashing is further described in the `slashing` pallet documentation.

#### Reward

Validators and nominators are rewarded at the end of each era. The total reward is calculated using era duration and staking rate.

$$
points_{era(t)}+ \frac{$_{staked_n,staked_v}}{$_{supply}}=reward_{n,v}n
$$

t is `$HISTORY_DEPTH`

points\_{era(t)} are the reward points received by the team during an era

$\_{stakedn, stakedv} is the total validator and nominator stake

$\_{supply} is the total supply of the currency

The total reward is split among validators and their nominators depending on the **number of points** received during the era.&#x20;

{% hint style="info" %}
Reward points are issued to validators.

* 20 points to the block producer for producing a (non-uncle) block in the delay chain,
* 2 points to the block producer for each reference to a previous unreferenced uncle, and
* 1 point to the producer of each referenced uncle block
{% endhint %}

The `validator` and its `nominator` split their reward as follows:

The `validator` sets `commission` which is paid to the `validator` only. The `commission` =is deducted from the total reward paid to `validator` and its `nominators` and the remainder is split among `validator` and all of the `nominators` proportional to the value `staked` behind the `validator`.

### Chilling

Any role above can choose to step back temporarily and just chill for a while.



