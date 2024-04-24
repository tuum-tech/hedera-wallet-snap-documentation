# getCurrentAccount

## How to call the API from an app

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const handleHelloAPI = async () => {
  await window.ethereum.request({
    method: 'wallet_invokeSnap',
    params: {
      snapId,
      request: {
        method: 'getCurrentAccount',
        params: {
          network: 'testnet'
        }
      }
    }
  })
}
```

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Returns the account info currently stored within the snap state. Note that this info may not be up-to-date with the info on the ledger. If you want to retrieve the most up-to-date info from the ledger, you will need to call [getAccountInfo snap API](../account-apis/getaccountinfo.md).

Some example responses:

For a hedera account id `0.0.3581604`:

```json
 {
    "currentAccount": {
        "metamaskEvmAddress": "0x0b3628d1b838993b5fceec8b2a26502e7a8e5241",
        "externalEvmAddress": "",
        "hederaAccountId": "0.0.3581604",
        "hederaEvmAddress": "0xca53f9c93d30e0b7212d67901e5a24fb090d542b",
        "publicKey": "0x0206022cea4c6dd6d2e7263b8802253971de922f5380661d97cba82dee66f57ad6",
        "balance": {
            "hbars": 5.67332072,
            "timestamp": "Wed, 13 Mar 2024 20:37:05 GMT",
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
                },
                "0.0.3581974": {
                    "balance": 0,
                    "decimals": 2,
                    "tokenId": "0.0.3581974",
                    "name": "WOODS",
                    "symbol": "WOODS",
                    "tokenType": "FUNGIBLE_COMMON",
                    "supplyType": "INFINITE",
                    "totalSupply": "100",
                    "maxSupply": "0"
                },
                "0.0.3590430": {
                    "balance": 1,
                    "decimals": 1,
                    "tokenId": "0.0.3590430",
                    "name": "Token1",
                    "symbol": "KP1",
                    "tokenType": "FUNGIBLE_COMMON",
                    "supplyType": "INFINITE",
                    "totalSupply": "100",
                    "maxSupply": "0"
                }
            }
        },
        "network": "testnet",
        "mirrorNodeUrl": "https://testnet.mirrornode.hedera.com"
    }
}
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/gOqBQLX" %}

<details>

<summary>Some things to keep in mind while interacting with the above demo</summary>

* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work

</details>

{% hint style="info" %}
To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).

You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
