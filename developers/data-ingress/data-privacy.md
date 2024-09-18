---
description: >-
  The Vana network strives to ensure personal data remains private and is only
  shared with trusted parties.
---

# Data Privacy

## Encrypting Data

Vana uses a patented non-custodial encryption technique to encrypt personal data. Data does not leave the user's browser unencrypted. A user's file is symmetrically encrypted with their encryption key, and if the encryption key is shared with another party, the key is encrypted with that party's public key so only the intended recipient can decrypt the key and the data.

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Encrypting user data, and sharing with a trusted party</p></figcaption></figure>

The steps are as follows:

1. The user uploads a decrypted file (F).
2. They are prompted to sign a fixed message with their wallets, creating a unique signature that can only be recreated by signing that same message using that same wallet.
3. The generated signature is used as the encryption key (EK) to encrypt the file F using a symmetric encryption technique, creating an encrypted file EF.
4. The encryption key EK is then encrypted with the trusted party's public key, making an encrypted encryption key (EEK).
5. The encrypted file EF and encrypted encryption key EEK can be safely shared with the intended recipient.

## Decrypting Data

Once the data has been encrypted, it can be decrypted by either a dApp or trusted party.

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption><p>A dApp, or trusted party can decrypt user data</p></figcaption></figure>

### Decryption by dApp

1. The dApp prompts the user to sign the same fixed message, to retreive the same EK as above
2. The EK is used to decrypt the encrypted file EF and retreive F

### Decryption by Trusted Party

1. The trusted party receives the encrypted file EF and the encrypted encryption key EEK
2. They decrypt the EEK using their private key, to retreive the encryption key EK
3. The EK is used to decrypt the encrypted file EF and retreive F

## Code Samples

Data DAOs can use the encryption technique described above to efficiently encrypt large files (up to several gigabytes in size) in the browser.&#x20;

{% embed url="https://github.com/vana-com/vana-dlp-ui-template/blob/098b8eebb3d06864bcd94a0e469a21f2b834dc2f/app/utils/crypto.ts#L4" %}

If the encryption key EK needs to be shared with a trusted party, it can be encrypted with their public key. To generate a new public/private keypair, see the instructions [here](https://github.com/vana-com/vana-dlp-ui-template/blob/098b8eebb3d06864bcd94a0e469a21f2b834dc2f/keys.md).&#x20;

```typescript
import * as openpgp from "openpgp";

const encryptionKey = "0x0a34ab7..."; // This is a secret (EK)
const publicKeyBase64 = "LS0tL..."; // Trusted party's public key, base64 encoded
const publicKey = await openpgp.readKey({
  armoredKey: atob(publicKeyBase64),
});
const encryptedEncryptionKey = await openpgp.encrypt({
  message: await openpgp.createMessage({ text: encryptionKey }),
  encryptionKeys: publicKey,
  format: "armored",
});
// encryptedEncryptionKey (EEK) is safe to share with the trusted party 
```

The trusted party can now receive and decrypt EEK, resulting in EK which can then be used to decrypt the user file F. A Python code example of this is shown [here](https://github.com/vana-com/vana-dlp-chatgpt/blob/main/chatgpt/utils/proof\_of\_contribution.py#L60).
