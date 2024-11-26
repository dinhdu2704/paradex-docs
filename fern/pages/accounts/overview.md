# 🗒️ Wallet Overview

Users are able to deposit and withdraw their funds on Paradex via the native bridge or our cross-chain bridge partners. Starknet wallets are also supported via our cross-chain bridging partners.

## **Native Bridge**

Our native Paradex bridge, StarkGate, provides a trust-less route for users to transfer assets between Ethereum and Paradex. This ensures a seamless and secure transaction process. _(See_ [_Deposits & Withdrawals_](deposits-and-withdrawals/ethereum-wallets.md) _for more info)_

## **Cross-Chain Bridge**

We have partnered with [Rhino.fi](http://rhino.fi/) and [Layerswap](https://layerswap.io/) to offer alternative flows for onboarding to Paradex. These partnerships ensure that onboarding is seamless, secure, and user-friendly, allowing users to easily fund their accounts with USDC. Bridge partners can offer fast transfer times and competitive fees with optimized gas usage, resulting in lower costs.

{% hint style="info" %}
Our app only displays available bridge paths between source and destination chains. For example — Rhino.fi does not currently support Non-EVM to Non-EVM bridge transfers (ie: Solana, Starknet -> Paradex)
{% endhint %}

## Starknet Wallets

We have extended key generation to Starknet accounts, enabling your connected Starknet wallet to [deterministically derive a Paradex Account](../introduction/architecture-overview/wallet-integration.md). Deposits and withdraws on Starknet Wallets would be done via our [Cross Chain Bridging](deposits-and-withdrawals/cross-chain-bridging.md).

## Accepted Collateral

Paradex currently supports USDC as collateral to fund margin obligations. Plans are in place to transition to a multi-collateral model in the future, where Paradex will accept various cryptocurrencies, each adjusted for specific risk levels.

## Transfer and TVL Limits

Please be aware of the following limits:

* <mark style="color:purple;">**Maximum Deposit per Transaction:**</mark> 500,000 USDC
* <mark style="color:purple;">**Maximum Total Value Locked (TVL):**</mark> 20 million USDC across all users

These limits are designed to manage risk and ensure platform stability.

## [Guardian Keys](../security/guardian-keys.md)

You may also use a [Guardian Key](../security/guardian-keys.md) to safeguard your withdrawals. More information can be found [here](https://github.com/tradeparadex/paradex-cli/wiki/Tutorial:-Hardening-Account-Security).