# Snap Account

## Overview

While MetaMask Snaps can access the currently connected Metamask accounts, they cannot access the private key of these accounts directly. Rather, Hedera Wallet Snap gets a [deterministic 256-bit entropy value](https://docs.metamask.io/snaps/reference/rpc-api/#snap\_getentropy), specific to the Snap and the currently connected Metamask account and uses it to generate a new private key. Other snaps cannot access this entropy and it changes if the user's secret recovery phrase changes, which means even if the snap creates a new wallet for each Metamask account, users will always be able to access their snap wallet as long as they are connected to that same Metamask account on another browser/device.

In addition, Hedera Wallet Snap also enables developers and users to access both non-MetaMask accounts (imported using private keys directly) via [Snap dialog box](https://docs.metamask.io/snaps/reference/rpc-api/#snap\_dialog) which is a secure way of transferring data from Metamask to the snap.

In summary, users can connect to Hedera Wallet Snap using their currently connected MetaMask account or importing the private key directly.



<figure><img src="../.gitbook/assets/How does Hedera Wallet Snap API Request work.drawio.png" alt=""><figcaption></figcaption></figure>

### How Hedera Wallet Snap connects to a Metamask account

The architecture diagram below demonstrates how a new Snap wallet is created for Metamask accounts.

1. User connects to the Hedera Wallet Snap using their Metamask account
2. Snap gets a [deterministic 256-bit entropy value](https://docs.metamask.io/snaps/reference/rpc-api/#snap\_getentropy), specific to the Snap and the currently connected Metamask account and uses it to generate a Snap wallet
3. Snap imports the private key to this Snap wallet to the Snap storage for later use
4. For example, if your Metamask account is 0x35a0....9898, your Snap account address may be 0xda17....2792. The point is you are not accessing your Metamask account but rather you're accessing a Snap specific account that is associated with your Metamask account

<figure><img src="../.gitbook/assets/How Snap connects to a Metamask account.png" alt=""><figcaption></figcaption></figure>

### How Hedera Wallet Snap connects to a Non-Metamask account

The architecture diagram below demonstrates how a new Snap wallet is created for Non-Metamask(External) accounts.

1. User passes their Account id(eg. 0.0.633893) or EVM address(0xe75e....6B0D) as parameters to the `externalAccount` params. For example: `externalAccount: { accountIdOrEvmAddress: '0.0.633893', curve?: 'ED25519' }`
2. Snap knows that this is a non-metamask account due to the `externalAccount` params being passed. So, it tries to import the account directly onto Metamask
3. If this is the first time importing the account, Snap prompts the user to enter the private key to this account via Metamask dialog box. If the account was previously imported, it skips this step.
4. Once the user enters the private key, Snap imports the private key to this Snap wallet to the Snap storage for later use
5. For example, if your Non-Metamask account's EVM address is 0xe75e....6B0D, your Snap account address will also be 0xe75e....6B0D. Note that unlike a Metamask account whereby a new Snap wallet is created for each account, if you connect to a non-metamask account, Snap will not generate a new wallet and instead use the same account that was imported.&#x20;
6. This feature lets users import their existing wallets such as Hashpack, Blade Wallet, etc directly onto the Snap



<figure><img src="../.gitbook/assets/How Snap connects to a non-Metamask account.png" alt=""><figcaption></figcaption></figure>

