# hscs/updateSmartContract

## How to call the API from an app

Hedera Wallet Snap connects to your currently connected Metamask account by default. To learn how apps can connect to Hedera Wallet Snap using a non-metamask(external) account, refer to this [documentation](../#connecting-to-a-non-metamask-external-account).&#x20;

Then, depending on whether you're trying to connect to a metamask account or a non-metamask account, you can call the snap API in the following way:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const updateSmartContractAPI = async () => {
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
        method: 'hscs/updateSmartContract',
        params: {
          network: 'testnet',
          contractId: '0.0.4409710',
          adminKey?, // Optional param - type: string
          contractMemo?, // Optional param - type: string
          expirationTime?, // Optional param - type: string
          maxAutomaticTokenAssociations?, // Optional param - type: number
          stakedAccountId?, // Optional param - type: string
          stakedNodeId?, // Optional param - type: number
          declineStakingReward?, // Optional param - type: boolean
          autoRenewPeriod?, // Optional param - type: number
          autoRenewAccountId?, // Optional param - type: string
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
* If you had not created your smart contract setting the `adminKey,`you will not be able to update your smart contract
{% endhint %}

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Parses the arguments that were passed such as the contractid, adminKey, etc.
3. Calls the [Hedera SDK Create Update Contract API](https://docs.hedera.com/hedera/sdks-and-apis/sdks/smart-contracts/update-a-smart-contract) to modify the smart contract entity state like admin keys, proxy account, auto-renew period, and memo.
4. Returns the transaction receipt as response

<figure><img src="../../../.gitbook/assets/Untitled (13).png" alt=""><figcaption></figcaption></figure>

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
        "contractId": "0.0.4409710",
        "topicId": "",
        "tokenId": "",
        "scheduleId": "",
        "exchangeRate": {
            "hbars": 30000,
            "cents": 358240,
            "expirationTime": "Tue, 04 Jun 2024 16:00:00 GMT",
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

{% embed url="https://codepen.io/kpachhai/pen/JjqNBWZ" %}

{% hint style="info" %}
* **Note**: Visit [https://pulse.tuum.tech/](https://pulse.tuum.tech/) to activate your hedera account before you interact with the demo
* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work.&#x20;
* To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).
* You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
