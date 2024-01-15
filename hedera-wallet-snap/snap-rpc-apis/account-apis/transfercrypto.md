# transferCrypto

## How to call the API from an app

Hedera Wallet Snap connects to your currently connected Metamask account by default. To learn how apps can connect to Hedera Wallet Snap using a non-metamask(external) account, refer to this [documentation](../#connecting-to-a-non-metamask-external-account).&#x20;

Then, depending on whether you're trying to connect to a metamask account or a non-metamask account, you can call the snap API in the following way:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const transferCryptoAPI = async () => {
  const externalAccountParams = {
    externalAccount: {
      accountIdOrEvmAddress: '0.0.12345',
      curve: 'ED25519'
    }
  }

  const transfers = [
    {
      asset: 'HBAR',
      to: '0.0.4498148',
      amount: 1 // in Hbar
    }
  ]

  // If you're sending to an exchange account, 
  // you will likely need to fill this out
  const memo = '' 

  await window.ethereum.request({
    method: 'wallet_invokeSnap',
    params: {
      snapId,
      request: {
        method: 'transferCrypto',
        params: {
          network: 'testnet',
          transfers,
          memo,
          maxFee: undefined
          /* 
            Uncomment the below line if you want to connect 
            to a non-metamask account
          */
          // ...externalAccountParams
        }
      }
    }
  })
}
```

{% hint style="info" %}
If you pass an 'undefined' value to maxFee, the uses the default maxFee which is 1 Hbar.&#x20;
{% endhint %}

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Parses the arguments that were passed such as the asset to transfer, who to transfer to and the amount to transfer.&#x20;
3. Send the asset to the receiver address

An example response:

```json
{
  "status": "SUCCESS",
  "accountId": "",
  "fileId": "",
  "contractId": "",
  "topicId": "",
  "tokenId": "",
  "scheduleId": "",
  "exchangeRate": {
    "hbars": 30000,
    "cents": 177843,
    "expirationTime": "2023-11-09T20:00:00.000Z",
    "exchangeRateInCents": 5.9281
  },
  "topicSequenceNumber": "0",
  "topicRunningHash": "",
  "totalSupply": "0",
  "scheduledTransactionId": "",
  "serials": [],
  "duplicates": [],
  "children": []
}
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/eYxWvmM" %}

<details>

<summary>Some things to keep in mind while interacting with the above demo</summary>

* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work

</details>

{% hint style="info" %}
To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).

You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
