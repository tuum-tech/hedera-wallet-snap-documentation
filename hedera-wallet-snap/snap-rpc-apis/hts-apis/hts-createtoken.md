# hts/createToken

## How to call the API from an app

Hedera Wallet Snap connects to your currently connected Metamask account by default. To learn how apps can connect to Hedera Wallet Snap using a non-metamask(external) account, refer to this [documentation](../#connecting-to-a-non-metamask-external-account).&#x20;

Then, depending on whether you're trying to connect to a metamask account or a non-metamask account, you can call the snap API in the following way:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const createTokenAPI = async () => {
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
        method: 'hts/createToken',
        params: {
          network: 'testnet',
          assetType: 'TOKEN', // TOKEN | NFT
          name: 'Tuum',
          symbol: 'TUUM',
          decimals: 1,
          supplyType: 'INFINITE', // FINITE | INFINITE
          initialSupply?, // Optional param - type: number
          kycPublicKey?, // Optional param - type: string
          freezePublicKey?, // Optional param - type: string
          pausePublicKey?, // Optional param - type: string
          wipePublicKey?, // Optional param - type: string
          supplyPublicKey?, // Optional param - type: string
          feeSchedulePublicKey?, // Optional param - type: string
          freezeDefault?, // Optional param - type: boolean
          expirationTime?, // Optional param - type: string
          autoRenewAccountId?, // Optional param - type: string
          tokenMemo?, // Optional param - type: string
          customFees?, // Optional param - type: TokenCustomFee
          /*
             type TokenCustomFee = {
                  feeCollectorAccountId: string; // Sets the fee collector account ID that collects the fee
                  hbarAmount?: number; // Set the amount of HBAR to be collected
                  tokenAmount?: number; // Sets the amount of tokens to be collected as the fee
                  denominatingTokenId?: string; // The ID of the token used to charge the fee. The denomination of the fee is taken as HBAR if left unset
                  allCollectorsAreExempt?: boolean; // If true, exempts all the token's fee collector accounts from this fee
              };
          */
          maxSupply?, // Optional param - type: number
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
* `supplyPublicKey` must be passed for the `NFT` assetType
* `maxSupply` cannot be passed for `INFINITE` supply type
* If you don't pass in `supplyPublicKey` you will not be able to mint or burn tokens
{% endhint %}

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Parses the arguments that were passed such as the name of the token, symbol, decimals, initialSupply, etc
3. Calls the [Hedera SDK Create Token API](https://docs.hedera.com/hedera/sdks-and-apis/sdks/token-service/define-a-token) to create a new fungible or non-fungible token (NFT) on the Hedera network.
4. Returns the transaction receipt as response

<figure><img src="../../../.gitbook/assets/Untitled (10).png" alt=""><figcaption></figcaption></figure>

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
            "hbars": 104.67332072,
            "timestamp": "Thu, 25 Apr 2024 17:54:55 GMT",
            "tokens": {}
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
        "tokenId": "0.0.4279119",
        "scheduleId": "",
        "exchangeRate": {
            "hbars": 30000,
            "cents": 358240,
            "expirationTime": "Thu, 25 Apr 2024 19:00:00 GMT",
            "exchangeRateInCents": 11.941333333333333
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

{% embed url="https://codepen.io/kpachhai/pen/QWPoyQa" %}

{% hint style="info" %}
* **Note**: Visit [https://pulse.tuum.tech/](https://pulse.tuum.tech/) to activate your hedera account before you interact with the demo
* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work.&#x20;
* To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).
* You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
