# deleteAccount

## How to call the API from an app

Hedera Wallet Snap connects to your currently connected Metamask account by default. To learn how apps can connect to Hedera Wallet Snap using a non-metamask(external) account, refer to this [documentation](../#connecting-to-a-non-metamask-external-account).&#x20;

Then, depending on whether you're trying to connect to a metamask account or a non-metamask account, you can call the snap API in the following way:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const deleteAccountAPI = async () => {
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
        method: 'deleteAccount',
        params: {
          network: 'testnet',
          transferAccountId: '0.0.67890', 
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
Note that deleting an account is an irreversible action and the user can never re-activate it again and the user is prompted with a MetaMask dialog box to confirm their choice for additional security.
{% endhint %}

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Calls the [Hedera SDK Delete Account API](https://docs.hedera.com/hedera/sdks-and-apis/sdks/accounts-and-hbar/delete-an-account) that deletes an existing account from the Hedera Token. Before deleting an account, the existing HBAR is transferred to the account defined by `transferAccountId`. NOTE: Deleting an account is an irreversible action.
3. Returns the transaction receipt as response.

Some example responses:

For a hedera account id `0.0.4559`:

```json
{
  "currentAccount": {
    "hederaAccountId": "0.0.4559",
    "hederaEvmAddress": "0x3ba201df50314e4702d4d92b52d304ee63bfca23",
    "balance": {
      "hbars": 0,
      "timestamp": "2024-02-01T21:40:21.826Z",
      "tokens": {}
    },
    "network": "testnet"
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
      "hbars": 1,
      "cents": 12,
      "expirationTime": "Mon, 25 Nov 1963 17:31:44 GMT",
      "exchangeRateInCents": 12
    },
    "topicSequenceNumber": "0",
    "topicRunningHash": "",
    "totalSupply": "0",
    "scheduledTransactionId": "",
    "serials": [],
    "duplicates": [],
    "children": []
  }
}
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/WNmJwLE" %}



{% hint style="info" %}
* **Note**: Visit [https://pulse.tuum.tech/](https://pulse.tuum.tech/) to activate your hedera account before you interact with the demo
* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work.&#x20;
* To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).
* You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
