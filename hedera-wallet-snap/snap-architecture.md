# Snap Architecture

## What does Hedera Wallet Snap look like under the hood?

One of the primary benefits of developing and using a snap in an application is that it leverages the security of MetaMask itself. Snaps, like Hedera Wallet Snap, operate in an isolated environment inaccessible to other snaps, ensuring that data can only be accessed through the APIs exposed by the snap.

Hedera Wallet Snap's security is of utmost importance, as it stores private keys for both MetaMask and non-MetaMask(external) accounts that have been previously imported. By exposing only the essential APIs for interacting with the Hedera Ledger, the snap ensures that applications cannot access its internal state.

The private keys stored within Hedera Wallet Snap's state are used to sign transactions and interact with the snap's APIs. This security measure prevents applications from impersonating another user, as all actions are tied to the connected account's private key.

In summary, Hedera Wallet Snap takes advantage of MetaMask's inherent security to protect user data within an isolated environment, ensuring the integrity of actions related to Hedera transactions.



<figure><img src="../.gitbook/assets/Hedera Wallet Snap Architecture.drawio.png" alt=""><figcaption></figcaption></figure>
