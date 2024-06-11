# FAQs

## How to install the Hedera Wallet Snap?

**For developers integrating the snap:**

1. To get started, make sure you have [MetaMask](https://metamask.io/) first and then install the Hedera Wallet snap from the [MetaMask Snaps Directory](https://snaps.metamask.io/snap/npm/hashgraph/hedera-wallet-snap/). Note that as of now, v0.4.2 is the most stable version so we recommend you use this in your application.
2. Note that snaps don't have user interface like MetaMask does so the snap needs to be installed by the user first and then the dapp can call Metamask API to interact with the snap. To learn more about how you can do this in your own app, look at an [example site code](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site) that has the Hedera Wallet Snap installation functionality or go through the live demos within the [Snap RPC APIs](../hedera-wallet-snap/snap-rpc-apis/) section where you can check out the working html/js code to do this.

**For users using the snap:**

1. You can install the Hedera Wallet snap from the [Metamask Snaps store](https://snaps.metamask.io/). However, you cannot interact with the snap directly from Metamask. Rather, you will need to visit applications that have integrated the snap.&#x20;
2. In the future, each snap will have a dedicated page within Metamask but that is not yet live on Metamask and will be coming later in 2024.

## What are Metamask Snaps?

MetaMask Snaps allow users to add features and functionality to their MetaMask wallet. Individual snaps are features created by third-party developers that MetaMask users can install directly into their wallet. Learn more about [Metamask snaps](https://metamask.io/snaps/).

## What is a Snap?

A Snap is an application built by a third-party developer that adds features and functionality to MetaMask. Snaps can connect to blockchain protocols beyond Ethereum, show insights about transactions, display notifications, add new privacy and identity features, and much more.

## Are Snaps safe to use?

Snaps run in a sandboxed environment and use a permissions model to protect your data and respect your consent. Snaps do not have access to your MetaMask account data. When installing a Snap, make sure you understand what permissions you are granting to stay secure.&#x20;

## Can I interact with Hedera Wallet Snap directly in MetaMask?

To interact with the snap and perform actions you need to go through a dapp. We have built a dedicated [dapp](https://pulse.tuum.tech/) that you can access here but you're also welcome to build your own dapps integrating with the Hedera Wallet Snap.

## Why is my Snap address different from my MetaMask address?

MetaMask does not allow Snaps to access the private keys of MetaMask accounts so Hedera Wallet Snap creates a new account with a private key. Note that neither you nor any Dapps will be able to view the private key of this Snap account as it's stored within snap sandboxed storage and is not accessible. This new Snap account is still associated with the currently connected MetaMask account however so you can always get back to your Snap account by connecting to this MetaMask account in the future.

## How can I export the private key of my snap account?

Check out the section: [Show Private Key](../hedera-wallet-snap/snap-rpc-apis/snap-state-apis/showaccountprivatekey.md) for more details on how to do this.

## How can I connect to my MetaMask account?

Since MetaMask does not allow Snaps to access the private keys of MetaMask accounts, Hedera Wallet Snap creates a new account. However, the Snap does offer flexibility in that it also lets you connect to an external account by directly importing your private key to the Snap. Note that the Snap creates a MetaMask dialog box for you to enter your private key so this key is not shared with any applications. Refer to [Snap RPC APIs](../hedera-wallet-snap/snap-rpc-apis/) on how to enable this in your Dapp.

## What happens if I delete the snap in MetaMask?

Reinstalling the snap will automatically recover your account provided you use the same Metamask account to configure the account again via your DApp.

## Is the Hedera Wallet Snap available on MetaMask Mobile?

Snaps are currently only available on MetaMask. MetaMask is a browser-based extension. This means the Hedera Wallet snap, or any other snap, is currently not available on MetaMask Mobile however, there are plans from the Metamask team to release the Snap feature on Metamask mobile in the near future.

##

##
