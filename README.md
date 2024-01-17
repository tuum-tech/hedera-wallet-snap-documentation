# Introduction

## Overview

Hedera Wallet Snap is a Metamask application that developers can incorporate into a variety of third party platforms to enhance MetaMask's functionality beyond its native capabilities. Specifically, Hedera Wallet Snap makes it possible to interact with Hedera Hashgraph natively without relying on Hedera JSON-RPC Relay. It can be seamlessly installed as a JavaScript npm package on web applications, thereby offering a range of advanced native features of Hedera to users.

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

## Official Snap Release

* Install from Metamask Snap Directory: [https://snaps.metamask.io/snap/npm/hashgraph/hedera-wallet-snap/](https://snaps.metamask.io/snap/npm/hashgraph/hedera-wallet-snap/)
* Stable Version: v0.1.3: [https://github.com/hashgraph/hedera-metamask-snaps/tree/v0.1.3/packages/hedera-wallet-snap](https://github.com/hashgraph/hedera-metamask-snaps/tree/v0.1.3/packages/hedera-wallet-snap)
* Snap Npm Package: [https://www.npmjs.com/package/@hashgraph/hedera-wallet-snap](https://www.npmjs.com/package/@hashgraph/hedera-wallet-snap)
* Snap Audit Report: [Hedera Wallet Snap Audit Report by Cure53](https://cure53.de/pentest-report\_tuum-hedera-snap.pdf)
* Demo Video showcasing Hedera Wallet Snap integration on an example website: [https://youtu.be/wzHn9z3CWpM](https://youtu.be/wzHn9z3CWpM)

## _Disclaimer_

_This snap is developed by Tuum Tech while the code for the snap is managed by Swirlds Labs. Furthermore, this wallet is neither created nor sponsored by Hedera and is built specifically for Metamask_
