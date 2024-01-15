# Hello World

## Overview

Hedera Wallet Snap provides developers with a range of APIs, starting with the simple "hello" snap API. This API connects to the current account and displays content to the user via a MetaMask dialog box. By learning to integrate the "hello" API, developers can then seamlessly integrate more complex APIs such as transferring Hbar and retrieving account information. To explore available APIs, refer to the [Snap RPC APIs ](../hedera-wallet-snap/snap-rpc-apis/)section in the documentation.

## JavaScript function to interact with Hedera Wallet Snap API

Let's see how we can interact with the "hello" API of the Hedera Wallet Snap.

```tsx
const handleHelloAPIRequest = async () => {
  const snapId = `npm:@hashgraph/hedera-wallet-snap`
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
Note that you do not need to pass in "mirrorNodeUrl" but if you do, the snap will use that URL instead of the default mirror node which may have rate limits associated with it.
{% endhint %}

where `snapId` can be one of the following:

1. `npm:@hashgraph/hedera-wallet-snap`: This is what you'll have most of the time if you are going to be integrating with the Hedera Wallet Snap version from the npm registry.
2. `local:http://localhost:9001`: If you're running the Hedera Wallet Snap locally on your development environment via [Hedera Wallet Snap Local Environment](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap), the snap APIs are exposed on localhost:9001. Note that you would only use this if you're actively making some changes to the Hedera Wallet Snap code locally otherwise, you'll be interacting with the Hedera Wallet Snap npm package directly.

On the above `handleHelloAPIRequest`method, we can see that it's invoking the wallet\_snap\_\* method of Metamask. What this does is invoke the `hello` API of Hedera Wallet Snap. Hedera Wallet Snap has implemented how to handle this API including what arguments to take(if any). Refer to [hello snap API](../hedera-wallet-snap/snap-rpc-apis/basic-apis/hello.md) for more info on how this API works.&#x20;

Then, all we need to do now is to handle the `hello` snap API request on our application:

```tsx
  const handleSendHelloClick = async () => {
    try {
      await handleHelloAPIRequest();
    } catch (e) {
      console.error(e);
    }
  };

  <Card
    content={{
      title: 'Send Hello message',
      description: 'Display a custom message within a confirmation screen in MetaMask.',
      button: (
        <Button
          buttonText="Send message"
          onClick={handleSendHelloClick}
        />
      ),
    }}
  />
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/poGPRmw" %}

{% hint style="info" %}
To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).

You can also check out the [API reference](../hedera-wallet-snap/snap-rpc-apis/) to learn how each API works.
{% endhint %}

###
