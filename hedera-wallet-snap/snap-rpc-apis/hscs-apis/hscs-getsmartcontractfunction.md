# hscs/getSmartContractFunction

## How to call the API from an app

Hedera Wallet Snap connects to your currently connected Metamask account by default. To learn how apps can connect to Hedera Wallet Snap using a non-metamask(external) account, refer to this [documentation](../#connecting-to-a-non-metamask-external-account).&#x20;

Then, depending on whether you're trying to connect to a metamask account or a non-metamask account, you can call the snap API in the following way:

```tsx
const snapId = `npm:@hashgraph/hedera-wallet-snap`

type SmartContractFunctionParameter = {
    type: 'string' | 'bytes' | 'boolean' | 'int' | 'uint';
    value: string | number | boolean | Uint8Array;
}

const getSmartContractFunctionAPI = async () => {
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
        method: 'hscs/getSmartContractFunction',
        params: {
          network: 'testnet',
          contractId: '0.0.4409710',
          functionName: 'getGreeting',
          functionParams?, // Optional param - type: SmartContractFunctionParameter[]
          gas?, // Optional param - type: number
          senderAccountId?: // Optional param - type: string
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
* The call can use at maximum the given amount of gas – the paying account will not be charged for any unspent gas.
{% endhint %}

## What the API does

1. Retrieves the currently connected account the user has selected on Metamask. If it's the first time, a new [snap account](../../snap-account.md) is created and the account info is saved in snap state.
2. Parses the arguments that were passed such as the gas, bytecode, adminKey, etc.
3. Calls the [Hedera SDK Get Smart Contract Function API](https://docs.hedera.com/hedera/sdks-and-apis/sdks/smart-contracts/get-a-smart-contract-function) to query a function of the given smart contract instance, giving it function parameters as its inputs. This is performed locally on the particular node that the client is communicating with. It cannot change the state of the contract instance.
4. Returns the transaction receipt as response

<figure><img src="../../../.gitbook/assets/Untitled (16).png" alt=""><figcaption></figcaption></figure>

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
    "result": {
        "contractId": "0.0.4409710",
        "bytes": "000000000000000000000000000000000000000000000000000000000000d903",
        "bloom": "00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "gasUsed": 800000,
        "errorMessage": "",
        "logs": "",
        "signerNonce": null,
        "evmAddress": "",
        "gas": -1,
        "amount": -1,
        "contractNonces": ""
    }
}
```

## Live Demo on CodePen

{% embed url="https://codepen.io/kpachhai/pen/YzbVjOo" %}

{% hint style="info" %}
* **Note**: Visit [https://pulse.tuum.tech/](https://pulse.tuum.tech/) to activate your hedera account before you interact with the demo
* If you're getting any errors with the live demo, make sure you go through the [FAQs](../../../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work.&#x20;
* To ease the integration of Hedera Wallet Snap on an application, we have created a template web application that you can run locally and check out the code in its entirety to learn how you can integrate and interact with various APIs exposed by Hedera Wallet Snap. Check out the full source code at [template application github repository](https://github.com/hashgraph/hedera-metamask-snaps/tree/main/packages/hedera-wallet-snap/packages/site).
* You can also check out the [API reference](../) to learn how each API works.
{% endhint %}
