# hscs/getSmartContractInfo

## How to call the API from an app

Hedera Wallet Snap connects to your currently connected Metamask account by default. To learn how apps can connect to Hedera Wallet Snap using a non-metamask(external) account, refer to this [documentation](../#connecting-to-a-non-metamask-external-account).&#x20;

Then, depending on whether you're trying to connect to a metamask account or a non-metamask account, you can call the snap API in the following way:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

const getSmartContractInfoAPI = async () => {
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
        method: 'hscs/getSmartContractInfo',
        params: {
          network: 'testnet',
          contractId: '0.0.4409710'
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
2. Parses the arguments that were passed such as the gas, bytecode, adminKey, etc.
3. Calls the [Hedera SDK Get Smart Contract Info API](https://docs.hedera.com/hedera/sdks-and-apis/sdks/smart-contracts/get-smart-contract-info) to query the network that returns the current state of a smart contract instance, including its balance.
4. Returns the transaction receipt as response

<figure><img src="../../../.gitbook/assets/Untitled (18).png" alt=""><figcaption></figcaption></figure>

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
    "info": {
        "contractId": "0.0.4409710",
        "accountId": "0.0.4409710",
        "contractAccountId": "0ca39034793f026127bcfb651b85515394fd21b1",
        "adminKey": "03d5f871cfe7134c67799dc6df75cdfc4b3f4fd797442350297efa9483661916d2",
        "expirationTime": "Mon, 02 Sep 2024 14:57:53 GMT",
        "autoRenewPeriod": 7776000,
        "autoRenewAccountId": "",
        "storage": 128,
        "contractMemo": "updating contract on June 4 2024",
        "balance": 0,
        "isDeleted": false,
        "tokenRelationships": {},
        "ledgerId": "testnet",
        "stakingInfo": {
          "declineStakingReward": false,
          "stakePeriodStart": null,
          "pendingReward": "0 tℏ",
          "stakedToMe": "0 tℏ",
          "stakedAccountId": null,
          "stakedNodeId": null
        }
    }
}
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/eYaWjwr" %}

{% hint style="info" %}
* **Note**: Visit [https://pulse.tuum.tech/](https://pulse.tuum.tech/) to activate your hedera account before you interact with the demo
* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work.&#x20;
* To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).
* You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
