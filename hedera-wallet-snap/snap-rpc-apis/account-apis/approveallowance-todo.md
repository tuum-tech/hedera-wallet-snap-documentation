# approveAllowance(todo)

## How to call the API from an app

Hedera Wallet Snap connects to your currently connected Metamask account by default. To learn how apps can connect to Hedera Wallet Snap using a non-metamask(external) account, refer to this [documentation](../#connecting-to-a-non-metamask-external-account).&#x20;

Then, depending on whether you're trying to connect to a metamask account or a non-metamask account, you can call the snap API in the following way:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const getAccountInfoAPI = async () => {
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
        method: 'getAccountBalance',
        params: {
          network: 'testnet',
          mirrorNodeUrl: 'https://testnet.mirrornode.hedera.com'
          // Pass 'accountId' is useful if you want to retrieve account balance
          // for someone else rather than yourself
          accountId: '0.0.67890', 
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
If you don't pass in "accountId", it will retrieve account info for the currently connected account.
{% endhint %}

Note that you can also call this API to retrieve account balance for another account Id which you do not own. Think of this as fetching the account balance of an arbitrary hedera account Id.\
To do that, you would just pass in `accountId` like this:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

  await window.ethereum.request({
    method: 'wallet_invokeSnap',
    params: {
      snapId,
      request: {
        method: 'getAccountBalance',
        params: {
          network: 'testnet',
          mirrorNodeUrl: 'https://testnet.mirrornode.hedera.com'
          accountId: '0.0.1',
        }
      }
    }
  })
}
```

This would retrieve the account balance of the account `0.0.1` from the Hedera Network Nodes.

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Calls the [Get Account Balance API](https://docs.hedera.com/hedera/sdks-and-apis/sdks/accounts-and-hbar/get-account-balance) to get account balance.
3. Returns the result.

Some example responses:

For a hedera account id `0.0.4559`:

```json
{
  "currentAccount": {
    "hederaAccountId": "0.0.4559",
    "hederaEvmAddress": "0x3ba201df50314e4702d4d92b52d304ee63bfca23",
    "balance": {
      "hbars": 89.60420503,
      "timestamp": "2024-02-01T21:35:21.826Z",
      "tokens": {}
    },
    "network": "testnet"
  },
  "accountBalance": 89.60420503
}
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/WNmzaZj" %}

<details>

<summary>Some things to keep in mind while interacting with the above demo</summary>

* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work

</details>

{% hint style="info" %}
To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).

You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
