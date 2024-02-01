# hello

## How to call the API from an app

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const handleHelloAPI = async () => {
  await window.ethereum.request({
    method: 'wallet_invokeSnap',
    params: {
      snapId,
      request: {
        method: 'hello',
        params: {
          network: 'testnet',
          mirrorNodeUrl: 'https://testnet.mirrornode.hedera.com'
        }
      }
    }
  })
}
```

{% hint style="info" %}
Note that you do not need to pass in "mirrorNodeUrl" but if you do, the snap will use that URL instead of the default public Hedera mirror nodes which may have rate limits associated with it.
{% endhint %}

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Displays an alert dialog blox on Metamask with some content.



<figure><img src="../../../.gitbook/assets/Untitled (2).png" alt=""><figcaption></figcaption></figure>

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/poGPRmw" %}

<details>

<summary>Some things to keep in mind while interacting with the above demo</summary>

* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work

</details>

{% hint style="info" %}
To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).

You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
