---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Working with Keys

## EVM Compatibility

The Vana network is EVM-compatible and supports Ethereum-compatible addresses. A Vana wallet holds the core ownership of assets on the Vana network, acting as the identity for all operations. Your wallet is also used to derive different encryption keys to secure your data.&#x20;

## Wallets

Network participants like DLP validators can use the CLI tool that comes with the [Vana cli](https://pypi.org/project/vana/) to manage their wallets.

This guide explains how to work with Vana wallet keys. For instructions on creating a Vana wallet, see [creating-a-wallet.md](creating-a-wallet.md "mention").

A Vana wallet consists of a coldkey and a hotkey, used for different operations in the Vana ecosystem.&#x20;

## **Key Pairings**

Each key is a pair of separate cryptographic keys. A coldkey has a private key and a public key, as does a hotkey.

## Coldkey

The coldkey is synonymous with the wallet name. For example, the `--wallet.name` option in a `vanacli` command accepts the coldkey as its value, while `--wallet.hotkey` accepts the hotkey. One coldkey can have multiple hotkeys.

### **Coldkey Uses**

* **Storage**: Holds VANA.
* **Delegation**: For delegating and undelegating VANA.
* **DLP Creation**: Used for creating a DLP.
* **Security**: Provides the highest level of security; always encrypted.

## Hotkey

You can create multiple hotkeys paired with a single coldkey. In a DLP, you are identified by your hotkey, keeping your coldkey secure. The same hotkey cannot be used for two nodes in the same DLP but can be used in different DLPs.

### **Hotkey Uses**

* **Transactions**: Signing transactions.
* **Operations**: Registering and running DLP nodes.
* **Delegation**: VANA holders can delegate their VANA to a validator’s hotkey.

## Security

* **Coldkey**: Highly secure and always encrypted, used for storing and managing VANA securely.
* **Hotkey**: Less secure, generally unencrypted, used for regular operational tasks.
