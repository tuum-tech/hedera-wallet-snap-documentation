# hcs/getTopicInfo

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
        method: 'hcs/getTopicInfo',
        params: {
          network: 'testnet',
          topicId: '0.0.4617270',
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

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Parses the arguments that were passed.
3. Calls the [Hedera SDK Get Topic Info API](https://docs.hedera.com/hedera/sdks-and-apis/sdks/consensus-service/get-topic-info) to retrieve details about the topic from the ledger.&#x20;
4. Returns the transaction receipt as response

<figure><img src="../../../.gitbook/assets/Untitled (3).png" alt=""><figcaption></figcaption></figure>

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
            "hbars": 86.77513646,
            "timestamp": "Tue, 23 Jul 2024 18:34:03 GMT",
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
    "topicInfo": {
        "memo": "KP version 2",
        "runningHash": "bba97100c674775f6f87618273980d182971cea41e2b665ded3668ac0d9689a68a1a510d37b9d8b43024b4cfb42f2ed3",
        "sequenceNumber": 1,
        "expirationTime": "Sun, 20 Oct 2024 18:00:45 GMT",
        "adminKey": {
            "key": "0206022cea4c6dd6d2e7263b8802253971de922f5380661d97cba82dee66f57ad6"
        },
        "submitKey": {
            "key": ""
        },
        "autoRenewAccountId": "",
        "autoRenewPeriod": "7776000",
        "ledgerId": "testnet"
    }
}
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/NWZroZV" %}

{% hint style="info" %}
* **Note**: Visit [https://pulse.tuum.tech/](https://pulse.tuum.tech/) to activate your hedera account before you interact with the demo
* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work.&#x20;
* To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).
* You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
