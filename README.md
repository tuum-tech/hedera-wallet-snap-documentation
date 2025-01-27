# Introduction

## Overview

Hedera Wallet Snap unlocks wallet functionality for Hedera via MetaMask that any other apps can interact with, thereby turning MetaMask into a native Hedera wallet without relying on Hedera JSON-RPC Relay.

With Hedera Wallet Snap, users can send HBAR to another HBAR account id and an EVM address, retrieve account info from either the Hedera Ledger node or Hedera Mirror node.&#x20;

## What is a Snap?

Metamask Snaps is an open source system that allows anyone to safely extend the functioanlity of Metamask, creating new web3 end user experiences. A Snap can add new API methods to MetaMask, add support for different blockchain protocols, or modify existing functionalities using the [Snaps JSON-RPC API](https://docs.metamask.io/snaps/reference/rpc-api/).

Snaps enable users to interact with new blockchains, protocols, and decentralized applications (dApps) beyond what is natively supported by MetaMask. The goal of the MetaMask Snaps system is to create a more open, customizable, and extensible wallet experience for users, while fostering innovation and collaboration within the blockchain and decentralized application ecosystem.

Developers can write MetaMask Snaps using JavaScript, making it accessible and convenient for a broad range of developers to create custom solutions. Users can then opt to install these snaps to enhance their MetaMask experience, provided they trust the source of the snap.

To learn more about Snaps, visit [Metamask Snap Guide](https://docs.metamask.io/guide/snaps.html).

## How does the Hedera Wallet Snap work?



<figure><img src=".gitbook/assets/How does Hedera Wallet Snap work.drawio.png" alt=""><figcaption></figcaption></figure>

## &#x20;What are some of the Hedera Wallet Snap features?

* Control Hedera Accounts that deal with both Account Ids and EVM addresses via Metamask wallet
* Retrieve account info from Hedera Ledger Node(this will incur some costs)
* Retrieve account info from a Hedera Mirror Node(the URL of the Mirror node can be passed as part of the API request)
* View HBAR balance&#x20;
* View tokens balance and other token info
* Send HBAR to another HBAR account associated with an Account Id
* Send HBAR to another HBAR account associated with an EVM address
* Import any Hedera account(both ECDSA and ED25519) using private key and store in Snaps persistent storage inside [Snaps execution environment](https://docs.metamask.io/snaps/concepts/execution-environment/).
* Interact with [Hedera Token Service](https://docs.hedera.com/hedera/sdks-and-apis/sdks/token-service)
* Interact with [Hedera Smart Contract Service](https://docs.hedera.com/hedera/sdks-and-apis/sdks/smart-contracts)
* Interact with [Hedera Consensus Service](https://docs.hedera.com/hedera/sdks-and-apis/sdks/consensus-service)

## Official Snap Release

* Install from Metamask Snap Directory: [https://snaps.metamask.io/snap/npm/hashgraph/hedera-wallet-snap/](https://snaps.metamask.io/snap/npm/hashgraph/hedera-wallet-snap/)
* Stable Version: v0.6.2: [https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/snap](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/snap)
* Snap Npm Package: [https://www.npmjs.com/package/@hashgraph/hedera-wallet-snap](https://www.npmjs.com/package/@hashgraph/hedera-wallet-snap)
* Snap Audit Report: [Hedera Wallet Snap Audit Report by Cure53](https://cure53.de/pentest-report_hedera-snap.pdf)

## Demos

### Hedera Wallet Snap:

* \[Jul 22, 2024] Hedera Consensus Service Demo: [https://youtu.be/80qwlpCrVMM](https://youtu.be/80qwlpCrVMM)
* \[Jun 11, 2024] Hedera Smart Contract Service Demo: [https://youtu.be/ELx7CtRRBK8](https://youtu.be/ELx7CtRRBK8)
* \[Apr 5, 2024] Hedera Token Service Demo: [https://youtu.be/0omBQWvx728](https://youtu.be/0omBQWvx728)
* \[Feb 1, 2024] Webinar: Hedera Wallet Snap On MetaMask Snaps: [https://www.youtube.com/watch?v=4ItGGy1F6rc](https://www.youtube.com/watch?v=4ItGGy1F6rc)
* \[Nov 10, 2023] Introduction to Hedera Wallet Snap: [https://youtu.be/wzHn9z3CWpM](https://youtu.be/wzHn9z3CWpM)

### Pulse:

* \[Jun 20, 2024] Pulse on Hedera | Powered by MetaMask Snaps: [https://youtu.be/UD1zMybS0nU](https://youtu.be/UD1zMybS0nU)

## _Disclaimer_

_This snap is developed by Tuum Tech while the code for the snap is managed by Swirlds Labs. Furthermore, this wallet is neither created nor sponsored by Hedera and is built specifically for Metamask_
