---
description: The proposed frames to handle stamping engineered
cover: ../.gitbook/assets/Black on White.png
coverY: 0
layout: editorial
---

# 🫔 Proof of Supervision with Blockchain

## Collective (Licensing Boards, Working Groups)

{% content-ref url="../build3-development-docs/prebuilt-pallets/collective.md" %}
[collective.md](../build3-development-docs/prebuilt-pallets/collective.md)
{% endcontent-ref %}

Allows a set of account IDs to raise proposals, motion to vote, vote, and execute proposals. This might be useful for committees within organizations for planning and approving budgets, proposing new standards, etc.

{% hint style="info" %}
## Board of Directors

**Scope\<License Registrar::Virginia>**

## Objective

A board of directors with the same voting authorities issued by the local legislation, but now all voting would be on the blockchain, including approval and review of license applications.
{% endhint %}

{% hint style="warning" %}
## Working Group

**Scope\<Standard of Care::Electrical>**

#### Discipline\<Electrical>

## Objective

A standard of care working group organized around the objective to establish a standard of care for a discipline type. In this case, Electrical.&#x20;

It is the responsibility of the working group to establish a minimum standard of care for electrical design in a manner that

* helps assure public safety&#x20;
* without imposing erroneous administrative work on the community that would discourage engagement in compliance
* members of the working group should propose a `standard`\_`of_care` and internally vote on the final version.&#x20;
  * this final version would then go to the network as the proposed standard of care for the network
  * submissions will implement the `staking` mechanism (ie the group would collectively bond the proposal, receiving the bond back if adopted by the community
  * only one formal `standard_of_care` may exist per category.
  * `standard_of_care` era is set to six months and is voted for adoption by network every six months. Any working group may submit an updated standard of care during that time if they have a better version. The network will vote on the standard of care.

&#x20;
{% endhint %}

## Identity (The License)

{% content-ref url="../build3-development-docs/prebuilt-pallets/identity.md" %}
[identity.md](../build3-development-docs/prebuilt-pallets/identity.md)
{% endcontent-ref %}

This `Pallet` allows a user to put forth a proposed identity and ask for a review by any number of registrars.&#x20;

![Example Identity Records Representing a Professional and their Active Licensure Authority](../.gitbook/assets/engineer\_license\_example\_2.png)

{% hint style="info" %}
## Credential Registry

An engineering board of directors may become a registrar on the network.&#x20;

Adding registrars are currently done through the master admin (sudo); but will eventually be converted to a council decision.

Registrar has the authority to review the identity and validate it.&#x20;

A user may assign an identity to their prime account which would represent their main user information (name, email, etc).

When applying for a license, a user creates an account and adds it as a sub-account. The user then submits the sub-account to the board to make a judgment (approve) the identity. The board can change the state of the identity.

Once the license (sub identity) is approved, the engineer uses this license address to seal drawings.
{% endhint %}

{% content-ref url="../build3-development-docs/prebuilt-pallets/membership.md" %}
[membership.md](../build3-development-docs/prebuilt-pallets/membership.md)
{% endcontent-ref %}

Members of the standards of care committee are added and removed through this pallet.&#x20;

## Contract (Construction Documents)

{% content-ref url="../build3-development-docs/prebuilt-pallets/contracts.md" %}
[contracts.md](../build3-development-docs/prebuilt-pallets/contracts.md)
{% endcontent-ref %}

Using this `Pallet` would allow general smart contracts to deploy into the framework between parties.

{% hint style="warning" %}
## Construction Document Records

### Minimum Required Specification

Each professional enters into a `Contract of Supervision` when they begin working on a project.&#x20;

This connects the licensed agents to the record of supervision for the project.&#x20;

#### Deploying Contract

Because many jurisdictions require both the firm and the individual to be licensed, this contract may require authorization by both licensed parties: the `firm` and the `individual`.

Each individually permitted document should be deployed as a separate contract.

#### Description of Supervision&#x20;

This `Contract of Supervision` should also store the state of the work contract including&#x20;

* `deliverables` - the list of deliverables and their state (percent completion).
* `discipline` - the discipline associated with the supervision (elec, mech, etc)
* `standard_of_care` - the standard of care implemented for the supervision

#### Record of Work

* For the sake of practical implementation, we will limit the record of work to any substantial deliverable sent from professional outward which would increase the amount of completed effort by a minimum of 10 percent.
* The `Record of Work` is a record of all major deliverable points, who performed the design, who checked the work, and who verified proof of the standard of care for the block entry.
* For each record of work parties sign:&#x20;
  * the designer submits work for review under a `Minimum Standard of Care` `Configuration Trait`
  * a reviewer checks work against the`Minimum Standard of Care` `Configuration Trait`
  * the professional signs that the document has been designed and backchecked per the `Standard of Care`

### Proposed Future Specification

#### Record of Payment

The contact may also be capable of recording payment history and terms. In the event of payment default, the contract would set the state of record drawings to `invalid` thereby prohibiting continued use of the construction documents (ie they would no longer be permitted for use in construction.

#### Handling Payment Defaults

In the event of default, any queries to construction document status would&#x20;

* return an Error: Invalid Contract, Payment Default. NOT FOR CONSTRUCTION and&#x20;
* the contract would also engage the IPFS storage utility to encrypt the data to prevent further download until payment is remedied.
{% endhint %}

{% hint style="danger" %}
## Construction Document Records

### Proposed Future Specification

#### Record of Payment

The contact may also be capable of recording payment history and terms. In the event of payment default, the contract would set the state of record drawings to `invalid` thereby prohibiting continued use of the construction documents (ie they would no longer be permitted for use in construction.

#### Handling Payment Defaults

In the event of default, any queries to construction document status would&#x20;

* return an Error: Invalid Contract, Payment Default. NOT FOR CONSTRUCTION and&#x20;
* the contract would also engage the IPFS storage utility to encrypt the data to prevent further download until payment is remedied.
{% endhint %}

## Off-Chain Worker

{% content-ref url="../build3-development-docs/prebuilt-pallets/off-chain-worker.md" %}
[off-chain-worker.md](../build3-development-docs/prebuilt-pallets/off-chain-worker.md)
{% endcontent-ref %}

{% hint style="warning" %}
### Verify Document Authenticity

A user submits files (or links to files) to check their authenticity. The off-chain worker downloads the file, hashes and compares it to the state on contract, and emits and `Event` describes the findings.
{% endhint %}

[Documentation](https://docs.substrate.io/how-to-guides/v3/ocw/local-storage/) on how to implement.

## Multisig

{% content-ref url="../build3-development-docs/prebuilt-pallets/multisig.md" %}
[multisig.md](../build3-development-docs/prebuilt-pallets/multisig.md)
{% endcontent-ref %}

A module for doing multi-signature dispatches.

{% hint style="warning" %}
### Enforcing Standard of Process for Construction Documentation

This could be used to optionally enforce multi-signature dispatches of construction documents to ensure there has been a minimum standard of process (design, reviewer, engineer all stamp the document before it can be final).
{% endhint %}

## Offenses

{% content-ref url="../build3-development-docs/prebuilt-pallets/offences.md" %}
[offences.md](../build3-development-docs/prebuilt-pallets/offences.md)
{% endcontent-ref %}

This pallet tracks the reported offenses.&#x20;

{% hint style="warning" %}
### Disciplinary Action by Board of Directors

A supervisory board regulating some issued credentials could submit disciplinary action against the `Validator` in accordance with their own regulations.
{% endhint %}

{% hint style="warning" %}
### Failure to Comply to Standard of Care

The community itself could check on the implemented standards of care and any violation would be reported as an `Offense`.

_example: PermitZIP requires checklists as part of the process for every project, every deliverable. If the reviewer `Validated` a design without completing the checklist, this would be an `Offence`._
{% endhint %}

## Recovery (of Stolen or Lost License)

{% content-ref url="../build3-development-docs/prebuilt-pallets/recovery.md" %}
[recovery.md](../build3-development-docs/prebuilt-pallets/recovery.md)
{% endcontent-ref %}

Allows account recovery if lost credentials based on M-of-N social recovery.

{% hint style="warning" %}
### Stolen Professional License

When a license is lost or stolen, this `Pallet` provides for a means of recovery which also secures the license.

#### Recovery Process

The recovery process is protected by trusted "friends" and a specific threshold of that list is required to recover.

This helps to address the idea of an engineer losing "control" of their license.&#x20;

* the board could temporarily `lock` the license&#x20;
* any use of an illegal or invalidated license would notify the board&#x20;
* the engineer could go through the recovery process, and notify the board when recovered
* when the account is recovered, the engineer can request it to be re-authorized (paying board fees as needed)
{% endhint %}

##
