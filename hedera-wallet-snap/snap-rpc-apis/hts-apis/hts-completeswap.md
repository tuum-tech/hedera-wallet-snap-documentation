# hts/completeSwap

## How to call the API from an app

Hedera Wallet Snap connects to your currently connected Metamask account by default. To learn how apps can connect to Hedera Wallet Snap using a non-metamask(external) account, refer to this [documentation](../#connecting-to-a-non-metamask-external-account).&#x20;

Then, depending on whether you're trying to connect to a metamask account or a non-metamask account, you can call the snap API in the following way:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const initiateSwapAPI = async () => {
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
        method: 'hts/completeSwap',
        params: {
          network: 'testnet',
          scheduleId: '0.0.4285081',
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
* Before this API can be called, a corresponding [`hts/initiateSwap`](hts-initiateswap.md) API must first be called that will initialize the atomic swap between two parties
* This API must be called within 30 minutes after initializing the swap or the transaction will fail
{% endhint %}

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Parses the arguments that were passed
3. Uses [scheduled transaction](https://docs.hedera.com/hedera/sdks-and-apis/sdks/schedule-transaction/create-a-schedule-transaction) to implement the atomic swap feature whereby the `requester` initiates the swap with the `responder` by calling the [`hts/initiateSwap`](hts-initiateswap.md)API upon which the snap sends this transaction as a scheduled transaction to the ledger. Within 30 minutes, if the `responder`calls this API with the scheduleId of the transaction, the swap is complete.
4. Returns the transaction receipt as response

## Example of how the Atomic Swap is performed

Let's assume Alice wants to swap her 1 Hbar with 10 Tuum token that Bob has(basically a peer to peer swap)

1. Alice calls the snap API for [`hts/initiateSwap`](hts-initiateswap.md) and as part of the parameters, she says she wants to give her 1 Hbar to Bob if Bob can give Alice 10 Tuum tokens
2. Snap creates this atomic swap transaction and sends it to the network as a scheduled transaction with a max expiry of 30 minutes
3. Snap returns the schedule Id for this transaction
4. Alice lets Bob know about this atomic swap transaction and gives him the schedule Id
5. Bob queries the schedule Id and verifies everything looks good
6. Bob calls the snap API for `hts/completeSwap` with the schedule Id
7. The scheduled transaction is executed and the atomic swap transaction is complete

<figure><img src="../../../.gitbook/assets/Untitled (11).png" alt=""><figcaption></figcaption></figure>

An example response:

```json
{
    "currentAccount": {
        "metamaskEvmAddress": "0x0b3628d1b838993b5fceec8b2a26502e7a8e5241",
        "externalEvmAddress": "",
        "hederaAccountId": "0.0.3589358",
        "hederaEvmAddress": "0x0ca39034793f026127bcfb651b85515394fd21b1",
        "publicKey": "0x03d5f871cfe7134c67799dc6df75cdfc4b3f4fd797442350297efa9483661916d2",
        "balance": {
            "hbars": 346.70233551,
            "timestamp": "Fri, 26 Apr 2024 19:24:31 GMT"
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
            "cents": 333977,
            "expirationTime": "Fri, 26 Apr 2024 20:00:00 GMT",
            "exchangeRateInCents": 11.132566666666667
        },
        "topicSequenceNumber": "0",
        "topicRunningHash": "",
        "totalSupply": "0",
        "scheduledTransactionId": "0.0.3581604@1714159254.939190271?scheduled",
        "serials": [],
        "duplicates": [],
        "children": []
    }
}
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/qBwvMoz" %}

<details>

<summary>Some things to keep in mind while interacting with the above demo</summary>

* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work

</details>

{% hint style="info" %}
To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).

You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
