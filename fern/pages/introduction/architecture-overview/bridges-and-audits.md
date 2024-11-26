---
description: This page covers the current state of Paradex's asset bridging architecture
---

# 🔐 Bridges & Audits

## Overview

In order to bridge assets over to Paradex's Starknet instance, users can read the reference provided by the developers of the bridge mechanism directly at the following links:

* [Starkgate Bridge mechanism](https://docs.starknet.io/documentation/architecture\_and\_concepts/L1-L2\_Communication/token-bridge/)
* [L1 to L2 messaging](https://docs.starknet.io/documentation/architecture\_and\_concepts/L1-L2\_Communication/messaging-mechanism/)

## Bridges & Audits

Starkgate is the bridge developed by Starkware, the entity behind Starknet and StarkEx. Users can find their public repository [here](https://github.com/starknet-io/starkgate-contracts/tree/main/src/starkware/starknet/apps/starkgate).

Paradex has forked this bridge and maintains this, users can request for access to the repository by posting in our Discord [here](https://discord.gg/paradex).

The Starknet smart contracts in their entirety have been audited at the file viewable below. This includes the bridge.

{% file src="../../.gitbook/assets/Starknet Core Summary Report - Sept 2022.pdf" %}

## Paradex & Audits

Paradex's smart contracts have not yet been audited as we are continuously deploying upgrades, but we plan to complete an audit in the next few months after we exit Beta with a functioning cross-margin system.&#x20;

At that point, we will begin smart contract audits as well as penetration testing (bug bounty) before removing developer-implemented limits on protocol TVL.\
\
In the meantime, feel free to check out our page on [L2 Beat](https://l2beat.com/scaling/projects/paradex) for more information on our smart contracts, locked volume, etc.