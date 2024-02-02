# approveAllowance(todo)

## How to call the API from an app

Hedera Wallet Snap connects to your currently connected Metamask account by default. To learn how apps can connect to Hedera Wallet Snap using a non-metamask(external) account, refer to this [documentation](../#connecting-to-a-non-metamask-external-account).&#x20;

Then, depending on whether you're trying to connect to a metamask account or a non-metamask account, you can call the snap API in the following way:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const approveAllowanceAPI = async () => {
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
        method: 'approveAllowance',
        params: {
          network: 'testnet',
          spenderAccountId: '0.0.67890', 
          amount: 25,
          assetType: 'HBAR', // 'HBAR' | 'TOKEN' | 'NFT'
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
For assetType TOKEN/NFT, you will need to pass in additional parameter `assetDetail` that contains the following:

```typescript
type ApproveAllowanceAssetDetail = {
  assetId: string;
  all?: boolean;
}
```
{% endhint %}

Note that you can also call this API to approve allowance for other tokens and nfts.&#x20;

For tokens, you would need to pass in additional parameters as shown below:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

  await window.ethereum.request({
    method: 'wallet_invokeSnap',
    params: {
      snapId,
      request: {
        method: 'approveAllowance',
        params: {
          network: 'testnet',
          spenderAccountId: '0.0.67890', 
          amount: 25,
          assetType: 'TOKEN', 
          assetDetail: {
            assetId: '0.0.45634' // This is token ID
          }
        }
      }
    }
  })
}
```

For nfts, you would need to pass in additional parameters as shown below:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

  await window.ethereum.request({
    method: 'wallet_invokeSnap',
    params: {
      snapId,
      request: {
        method: 'approveAllowance',
        params: {
          network: 'testnet',
          spenderAccountId: '0.0.67890', 
          amount: 25,
          assetType: 'NFT', 
          assetDetail: {
            assetId: '0.0.57894' // This is nft ID
            all: false, // If this is set to true, it will approve all the NFTs in the above collection
          }
        }
      }
    }
  })
}
```

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Calls the [Hedera SDK Approve Allowance API](https://docs.hedera.com/hedera/sdks-and-apis/sdks/accounts-and-hbar/approve-an-allowance) that allows a token owner to delegate a token spender to spend the specified token amount on behalf of the token owner. The owner can provide an allowance for HBAR, fungible(TOKEN) and non-fungible(NFT) tokens.
3. Returns the transaction receipt as response.

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

{% embed url="https://codepen.io/kpachhai/pen/oNVdgEq" %}

<details>

<summary>Some things to keep in mind while interacting with the above demo</summary>

* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work

</details>

{% hint style="info" %}
To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).

You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
