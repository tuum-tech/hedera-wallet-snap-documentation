# getAccountInfo

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
        method: 'getAccountInfo',
        params: {
          network: 'testnet',
          mirrorNodeUrl: 'https://testnet.mirrornode.hedera.com'
          // Pass 'accountId' is useful if you want to retrieve account info 
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
If you don't pass in "mirrorNodeUrl", the snap will query the Hedera Ledger node to retrieve the account information and this may have some costs associated with the query. In addition, the token balance would also not be retrieved as that can only be retrieved from querying a mirror node.

If you want to retrieve the complete account data and want to do it for free, be sure to pass in "mirrorNodeUrl" in your parameter.

If you don't pass in "accountId", it will retrieve account info for the currently connected account.
{% endhint %}

Note that you can also call this API to retrieve account info for another account Id which you do not own. Think of this as fetching the account info of an arbitrary hedera account Id.\
To do that, you would just pass in `accountId` like this:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

  await window.ethereum.request({
    method: 'wallet_invokeSnap',
    params: {
      snapId,
      request: {
        method: 'getAccountInfo',
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

This would retrieve the account info of the account `0.0.1` from the Hedera Mirror Nodes.

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Calls the [Mirror Node Account Info REST API ](https://docs.hedera.com/hedera/sdks-and-apis/rest-api#api-v1-accounts-idoraliasorevmaddress) to get account info from the Hedera Mirror Node if `mirrorNodeUrl` is passed. If not, it calls the [Get Account Info API of the Hedera SDK](https://docs.hedera.com/hedera/sdks-and-apis/sdks/accounts-and-hbar/get-account-info)
3. Returns the result.&#x20;

Some example responses:

For a hedera account id `0.0.4235873`:

```json
{
  "currentAccount": {
    "hederaAccountId": "0.0.4235873",
    "hederaEvmAddress": "0x3ba201df50314e4702d4d92b52d304ee63bfca23",
    "balance": {
      "hbars": 0.75108133,
      "timestamp": "Wed, 24 Jan 2024 21:58:32 GMT",
      "tokens": {}
    },
    "network": "mainnet"
  },
  "accountInfo": {
    "accountId": "0.0.4235873",
    "alias": "HORADX2QGFHEOAWU3EVVFUYE5ZR37SRD",
    "createdTime": "Mon, 11 Dec 2023 05:42:32 GMT",
    "expirationTime": "Sun, 10 Mar 2024 05:42:32 GMT",
    "memo": "lazy-created account",
    "evmAddress": "0x3ba201df50314e4702d4d92b52d304ee63bfca23",
    "key": {
      "type": "ECDSA_SECP256K1",
      "key": "0380f14bf0a7c8c8c0bbae90e4f6d18b8a016fa945ec646943e8d56a1f7e4dd02a"
    },
    "balance": {
      "hbars": 0.75108133,
      "timestamp": "Wed, 24 Jan 2024 21:58:32 GMT",
      "tokens": {}
    },
    "autoRenewPeriod": "7776000",
    "ethereumNonce": "0",
    "isDeleted": false,
    "stakingInfo": {
      "declineStakingReward": false,
      "stakePeriodStart": "",
      "pendingReward": "0",
      "stakedToMe": "0",
      "stakedAccountId": "",
      "stakedNodeId": ""
    }
  }
}
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/abXWpea" %}

{% hint style="info" %}
* **Note**: Visit [https://pulse.tuum.tech/](https://pulse.tuum.tech/) to activate your hedera account before you interact with the demo
* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work.&#x20;
* To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).
* You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
