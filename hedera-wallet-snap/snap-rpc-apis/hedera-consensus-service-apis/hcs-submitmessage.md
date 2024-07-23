# hcs/submitMessage

## How to call the API from an app

Hedera Wallet Snap connects to your currently connected Metamask account by default. To learn how apps can connect to Hedera Wallet Snap using a non-metamask(external) account, refer to this [documentation](../#connecting-to-a-non-metamask-external-account).&#x20;

Then, depending on whether you're trying to connect to a metamask account or a non-metamask account, you can call the snap API in the following way:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const snapAPI = async () => {
  const externalAccountParams = {
    externalAccount: {
      accountIdOrEvmAddress: '0.0.12345',
      curve: 'ED25519'
    }
  }

  await window.ethereum.request({
    method: 'wallet_invokeSnap',
    params: {
      snapId,
      request: {
        method: 'hcs/submitMessage',
        params: {
          network: 'testnet',
          topicId: '0.0.4617270',
          message: 'first message',
          maxChunks?, // Optional param - type: number
          chunkSize?, // Optional param - type: number
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
* Max size of an HCS message is 1024 bytes(1 kb).
* If you pass in `maxChunks`, it will set the max number of chunks in the transaction to this number.
* If you pass in `chunkSize`, it will set the max size for each chunk in the transaction to this number.
{% endhint %}

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Parses the arguments that were passed.
3. Calls the [Hedera SDK Submit Message API](https://docs.hedera.com/hedera/sdks-and-apis/sdks/consensus-service/submit-a-message) to submit a topic message to the network. You can subscribe to the topic via a mirror node or you can also retrieve these messages from a mirror node using [`hcs/getTopicMessages` API](hcs-gettopicmessages.md).
4. Returns the transaction receipt as response

<figure><img src="../../../.gitbook/assets/Untitled (2).png" alt=""><figcaption></figcaption></figure>

An example response:

```json
 {
    "currentAccount": {
        "metamaskEvmAddress": "0x0b3628d1b838993b5fceec8b2a26502e7a8e5241",
        "externalEvmAddress": "",
        "hederaAccountId": "0.0.3581604",
        "hederaEvmAddress": "0xca53f9c93d30e0b7212d67901e5a24fb090d542b",
        "publicKey": "0x0206022cea4c6dd6d2e7263b8802253971de922f5380661d97cba82dee66f57ad6",
        "balance": {
            "hbars": 86.77660179,
            "timestamp": "Tue, 23 Jul 2024 18:25:20 GMT",
            "tokens": {
                "0.0.3582047": {
                    "balance": 1,
                    "decimals": 1,
                    "tokenId": "0.0.3582047",
                    "name": "PACHHAI",
                    "symbol": "PACHHAI",
                    "tokenType": "FUNGIBLE_COMMON",
                    "supplyType": "INFINITE",
                    "totalSupply": "100",
                    "maxSupply": "0"
                }
            }
        },
        "network": "testnet",
        "mirrorNodeUrl": "https://testnet.mirrornode.hedera.com"
    },
    "receipt": {
        "status": "SUCCESS",
        "accountId": "",
        "fileId": "",
        "contractId": "",
        "topicId": "",
        "tokenId": "",
        "scheduleId": "",
        "exchangeRate": {
            "hbars": 30000,
            "cents": 202259,
            "expirationTime": "Tue, 23 Jul 2024 19:00:00 GMT",
            "exchangeRateInCents": 6.741966666666666
        },
        "topicSequenceNumber": "1",
        "topicRunningHash": "bba97100c674775f6f87618273980d182971cea41e2b665ded3668ac0d9689a68a1a510d37b9d8b43024b4cfb42f2ed3",
        "totalSupply": "0",
        "scheduledTransactionId": "",
        "serials": [],
        "duplicates": [],
        "children": []
    }
}
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/RwzRvvy" %}

<details>

<summary>Some things to keep in mind while interacting with the above demo</summary>

* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work

</details>

{% hint style="info" %}
To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).

You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
