# Snap RPC APIs

## Connecting to a non-metamask(external) account

Users can connect to both metamask accounts and non-metamask accounts with Hedera Wallet Snap. For connecting to metamask accounts, everything is handled automatically as snap has direct access to Metamask APIs however for connecting to non-metamask accounts, some additional flags must be passed so the snap recognizes that the user is trying to connect to an external account.&#x20;

The flag for an external flag is as follows:

```tsx
const externalAccountParams = {
  externalAccount: {
    accountIdOrEvmAddress: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266',
    curve?: 'ECDSA_SECP256K1' | 'ED25519'
  }
}
```

In addition to Hedera EVM accounts, Hedera Wallet Snap also lets users connect to Hedera Accounts with account Ids directly.&#x20;

For that, the flag for an external flag is as follows:

```tsx
const externalAccountParams = {
  externalAccount: {
    accountIdOrEvmAddress: '0.0.12345',
    curve?: 'ECDSA_SECP256K1' | 'ED25519'
  }
}
```

Hedera Wallet Snap lets users connect to their Hedera accounts that were created using the following curves:

1. [**ECDSA\_SECP256K1**](https://docs.hedera.com/hedera/support-and-community/glossary#ecdsa-secp256k1): A cryptographic algorithm used for data integrity and widely used in cryptocurrencies. In this term, "secp256k1" refers to the specific parameters of the elliptic curve used, making it efficient for computations. Hedera supports this signature scheme for generating cryptographic keys and signing transactions.
2. [**ED25519**](https://docs.hedera.com/hedera/support-and-community/glossary#ed25519): In the context of Hedera, Ed25519 is one of the signature schemes supported for the creation and verification of digital signatures. It's often used for signing transactions, as it provides a strong level of security while still being efficient to compute.
