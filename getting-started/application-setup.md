# Application Setup

## Add @hashgraph/hedera-wallet-snap to package.json

```bash
npm install @hashgraph/hedera-wallet-snap@0.1.3
or
yarn add @hashgraph/hedera-wallet-snap@0.1.3
```

## Check whether Metamask is installed(OPTIONAL)

It's optional but recommended to verify whether MetaMask is installed by the users because Snaps are only available within Metamask. The choice is up to developers on how they want to handle this aspect of the integration.

```tsx
async function isMetamaskInstalled() {
  // Check if the `window.ethereum` property exists on the window object
  return typeof window.ethereum !== 'undefined' && window.ethereum.isMetaMask;
}
```

Check out [Snap RPC APIs](../hedera-wallet-snap/snap-rpc-apis/) to learn about how to interact with the Hedera Wallet Snap from your website.

## Add the Connect to Hedera Wallet Snap button on your application

Note that before users can interact with the Hedera Wallet Snap, it needs to first be installed on the Metamask itself so you can have a button on your website that lets users do exactly this.

```tsx
// Get permissions to interact with and install the Hedera Wallet Snap
async function connect() {
  console.log("snap id", snapId);
  const isMetamaskDetected = await isMetamaskInstalled();
  if (!isMetamaskDetected ) {
    console.error(
      "You need to install Metamask for this demo to work. You can install it at https://metamask.io"
    );
    alert(
      "You need to install Metamask for this demo to work. You can install it at https://metamask.io"
    );
  }

  let snaps = await window.ethereum.request({
    method: "wallet_getSnaps"
  });
  console.log("Installed snaps...", snaps);
  try {
    if (!(snapId in snaps)) {
      console.log("Hedera Wallet Snap is not yet installed. Installing now...");
      const result = await ethereum.request({
        method: "wallet_requestSnaps",
        params: {
          [snapId]: {}
        }
      });
      console.log("result: ", result);
      snaps = await window.ethereum.request({
        method: "wallet_getSnaps"
      });
    }
  } catch (e) {
    console.log(
      `Failed to obtain installed snap: ${JSON.stringify(e, null, 4)}`
    );
    alert(`Failed to obtain installed snap: ${JSON.stringify(e, null, 4)}`);
  }

  if (snapId in snaps) {
    console.log("Connected successfully!");
    alert("Connected successfully!");
  } else {
    console.log("Could not connect successfully. Please try again!");
    alert("Could not connect successfully. Please try again!");
  }
}
```

<details>

<summary>Some things to keep in mind while interacting with the above demo</summary>

* If you're getting any errors with the live demo, make sure you go through the [FAQs](../basics/faqs.md) section to learn about what you may be missing. You need to install [Metamask](https://metamask.io/) in your browser for the live demo to work

</details>
