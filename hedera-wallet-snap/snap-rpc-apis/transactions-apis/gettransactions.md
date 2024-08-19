# getTransactions

## How to call the API from an app

Hedera Wallet Snap connects to your currently connected Metamask account by default. To learn how apps can connect to Hedera Wallet Snap using a non-metamask(external) account, refer to this [documentation](../#connecting-to-a-non-metamask-external-account).&#x20;

Then, depending on whether you're trying to connect to a metamask account or a non-metamask account, you can call the snap API in the following way:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const getTransactionsAPI = async () => {
  const externalAccountParams = {
    externalAccount: {
      accountIdOrEvmAddress: '0.0.12345',
      curve: 'ED25519'
    }
  }

  /*
    If you want to retrieve all the transactions for your account, 
    transactionId can be empty
  */
  const getTransactionsParams = {
    transactionId: '0.0.4228598@1706816923.997995813'
  }

  await window.ethereum.request({
    method: 'wallet_invokeSnap',
    params: {
      snapId,
      request: {
        method: 'getTransactions',
        params: {
          network: 'testnet',
          transactionId: getTransactionsParams.transactionId,
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
If you pass in an empty transactionId or don't pass anything to this API, it'll retrieve all the transactions associated with your account.
{% endhint %}

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Parses the arguments that were passed such as `transactionId` to retrieve info for. If this is not passed, the API will fetch all the transactions for the account.&#x20;
3. Calls the [Hedera Mirror Node REST API for transactions](https://docs.hedera.com/hedera/sdks-and-apis/rest-api#transactions) to retrieve transactions history.
4. Return the transactions details

An example response:

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
  "transactions": [
    {
      "bytes": null,
      "charged_tx_fee": 65919908,
      "consensus_timestamp": "Wed, 24 Jan 2024 21:58:32 GMT",
      "entity_id": null,
      "max_fee": "100000000",
      "memo_base64": "",
      "name": "CRYPTOTRANSFER",
      "nft_transfers": [],
      "node": "0.0.8",
      "nonce": 0,
      "parent_consensus_timestamp": "",
      "result": "SUCCESS",
      "scheduled": false,
      "staking_reward_transfers": [],
      "token_transfers": [],
      "transaction_hash": "lbF/gV2X5IDZBjRVdqiR+AAxKP0Kop8Z51Xt9DcNqGHgMI7PGSR1BoBCPR0aE2jz",
      "transaction_id": "0.0.4235873-1706133501-928562334",
      "transfers": [
        {
          "account": "0.0.8",
          "amount": 5679,
          "is_approval": false
        },
        {
          "account": "0.0.98",
          "amount": 59322807,
          "is_approval": false
        },
        {
          "account": "0.0.800",
          "amount": 6591422,
          "is_approval": false
        },
        {
          "account": "0.0.4235873",
          "amount": -65919918,
          "is_approval": false
        },
        {
          "account": "0.0.4551503",
          "amount": 10,
          "is_approval": false
        }
      ],
      "valid_duration_seconds": "120",
      "valid_start_timestamp": "Wed, 24 Jan 2024 21:58:21 GMT"
    }
  ]
}
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/XWGEPJK" %}

{% hint style="info" %}
* **Note**: Visit [https://pulse.tuum.tech/](https://pulse.tuum.tech/) to activate your hedera account before you interact with the demo
* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work.&#x20;
* To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).
* You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
