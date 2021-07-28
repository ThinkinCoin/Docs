# Threshold Signature Scheme

## Introduction <a id="introduction"></a>

**Threshold Signature Scheme \(TSS\)** is a cryptographic protocol for distributed key generation and signing. TSS allows constructing a signature that is distributed among different parties \(for example three users\), and each user receives a share of the private signing key. To sign a transaction, at least two of these three users need to join. For individuals, threshold signatures allow for two-factor security or splitting the ability to sign between two devices so that a single compromised device won’t put the money at risk. For businesses, threshold signatures allow for the realization of access control policies that prevent both insiders and outsiders from stealing corporate funds. TSS technology allows us to replace all signing commands with distributed computations.The private key is no longer a single point of failure.

## Motivation <a id="motivation"></a>

A physical key must fit exactly into a keyhole to unlock a physical vault. But if this key is compromised or lost, the funds locked in the vault may no longer be safe. This simple approach of key management may make sense when a small sum is at stake. However, when the amount stored in the vault is large, it is wise to consider spreading the responsibility of key ownership between several trusted parties.

Traditional **MultiSig \(multi-signature\)** is a more refined unlocking system that requires _multiple_ independent keys to unlock the vault. MultiSig requires generating a larger private key and the vault has multiple locks - one for each key . More processing power is needed as participants have to sign additional signatures, which must then be checked individually by the network. This is not ideal, because a participant must leave traces showing exactly who signed and multiple parties must be online at the same time.

With **Threshold Signatures**, all of the parties must forge the vault’s lock together, in a modular way, where each party owns a share of the key. A TSS vault is indistinguishable from a regular vault and is hence universal, and it has the same privacy and verification cost of a regular vault. Even if only a subset of the keys is available, the vault may still be unlocked \(this is known as meeting a threshold of participation\).

Combining TSS feature with Binance Chain client will help users manage their funds in a much safer way. TSS will be offered in an independent binary, but it will have some impact on the existing functions of _bnbcli/tbnbcli_.

## Implementation <a id="implementation"></a>

Many development resources have been poured into implementing TSS, a cryptographic protocol for distributed key generation and signing. TSS is now compatible and reusable for ECDSA-based blockchains, including Binance Chain, Bitcoin, and Ethereum networks. We expect that members of the Binance ecosystem and partner community can integrate this TSS library with their applications, such as wallets and custodians, and further develop this exciting new technology.

With the support of the Binance Chain community, we are happy to share the open-source code at [https://github.com/binance-chain/tss-lib](https://github.com/binance-chain/tss-lib).

## Security Audit <a id="security-audit"></a>

The implementation of a multi-party threshold ECDSA [library](https://github.com/binance-chain/tss-lib) is open source so it can be publicly audited by anyone. An independent third party auditors from [Kudelski Security](https://www.kudelskisecurity.com/) are hired to validate the security of the cryptography in TSS solution. The latest report in October by can be found [here](https://docs.binance.org/assets/audit-binance-tss-lib-final.pdf).

Security checks are routinely and continuously planed for all parts of TSS lib implmentations and future audits will be reported to Binance Chain community.

## Workflow <a id="workflow"></a>

Let’s take a look at the major steps in TSS:

* **Vault Initialization**: the first step is for setting up tss parameters of each party. This will initialize the node's p2p listen address and setup a directory to save key. It's recommended that you should save your tss key in a different folder other than normal key info.
* **Key Generation**: the second step is also the most complex. We need to define the quorum policy: count of total parties \(n\) that holds secret shares and threshold \(t\) which means at least t + 1 parties need to take part in the signing process. We need to generate a key which will be public and used to verify future signatures. However, we also have to generate an individual secret for each party, which is called a secret share. The functions guarantee the same public key to all parties and a different secret share for each. In this way, we achieve: \(1\) privacy: no secret shares data is leaked between any parties, and \(2\) correctness: the public key is intact with secret share. They need to agree on the channel which they want to use for sending messages between each other. The channel will have its corresponding password. Both ID and password needs to be shared offline.
* **Signing**: this step involves a signature generation function. The input of each party will be its own secret share, created as output of the distributed key generation in the previous step. There is also public input known to all, which is the message to be signed. The output will be a digital signature, and the property of privacy ensures that no leakage of secret shares occurred during the computation.
* **Verification**: the verification algorithm remains as it is in the classical setting. To be compatible with single key signatures, Binance Chain validator nodes can be able to verify the signature with the public key. The transaction will be no different from others.
* **Vault Regroup**: Regroup will reset secret share and configs between all parties.It's recommend to switch the configuration periodically, say once a month. If some party lost his key, it's also necessory to reset the distribution once some party lost their key. Regroup will generate new\_n secret share with new\_t threshold. At least old\_t + 1 should participant

## Where can I download the Binance TSS CLI? <a id="where-can-i-download-the-binance-tss-cli"></a>

You can download tss client and Binance Chain Commandline here: \* Mainnet: [https://github.com/binance-chain/node-binary/tree/master/cli/prod/0.6.3](https://github.com/binance-chain/node-binary/tree/master/cli/prod/0.6.3) \* Testnet: [https://github.com/binance-chain/node-binary/tree/master/cli/testnet/0.6.3](https://github.com/binance-chain/node-binary/tree/master/cli/testnet/0.6.3)​

## How to Use <a id="how-to-use"></a>

* **Warning**: Please test your TSS setup before use this on mainnet.

> Please backup your bnbcli home before use this tool:

```text
cp -r ~/.bnbcli ~/.bnbcli_backup_tss (replace ~/.bnbcli with their bnbcli home)
```

Please refer to this [Example](threshold-signature-scheme.md) to help you understand the whole process

### Init <a id="init"></a>

`tss init` will create home directory of a new tss setup, generate p2p key pair.

* Here are the global transaction flags:
* Here are the flags for `tss init`:

### Describe <a id="describe"></a>

`tss describe` will show config and address of a tss vault

* Here are the flags for `tss describe`:
* Example

  ```text
  ./tss describe​> please set vault of this party:[input vault name]> Password to sign with this vault:[input password]address of this vault: bnb1config of this vault:{        "p2p": {                "listen": "/ip4/0.0.0.0/tcp/59968",                "bootstraps": null,                "relays": null,                "peer_addrs": [                        "/ip4/127.0.0.1/tcp/59748",                        "/ip4/127.0.0.1/tcp/60022"                ],                "peers": [                        "test3",                        "test2"                ],                "DefaultBootstap": false        },        "Id": "",        "Moniker": "tss1",        "vault_name": "vault1",        "Threshold": 1,        "Parties": 3,        "log_level": "info",        "profile_addr": "",        "Home": "~/.tss"}
  ```

### Channel <a id="channel"></a>

`tss channel` will generate a channel ID for bootstrapping. One party can generate a channel, then share the generated channel ID with others offline.

* Here are the flags for `tss channel`:

It's advised to refresh the channels regularly.

### Keygen <a id="keygen"></a>

This command will generated the private key and share the secret. Everyone needs to agree on the password of this private key. The lenght of password must be more than **eight**.

Note: you need to make sure that all the parties are online.

* Here are the flags for `tss keygen`:

if you want to add the generated key files in the bnbcli home, you can copy it to the home folder:

```text
bnbcli keys add --tss -t tss --tss-home ~/.test1 --tss-vault third test1_third
```

### Regroup <a id="regroup"></a>

This command will generate new\_n secret from the same private key, and it will be shared with new\_t threshold. At least old\_t + 1 should participante in signing

* Here are the flags for `tss regroup`:

## Changes to `bnbcli/tbnbcli` <a id="changes-to-bnbclitbnbcli"></a>

We added a new key type “tss” \(just like the existing types: “local”, “offline”, “ledger”\) to bnbcli which stands for tss secret share.

To add a tss key into bnbcli’s keystore: 1. Tss keygen command will automatically add generated secret share into default keystore \(~/.bnbcli\) with name “tss\_\_” 2. User can manually specify tss’s home, vault\_name and a customized bnbcli home like:

```text
bnbcli keys add --home ~/.customized_cli --tss -t tss --tss-home ~/.test1 --tss-vault “default” my_name
```

All other commands \(i.e. send token, place order, delete key etc.\) of bnbcli should support tss type key.

## Example <a id="example"></a>

In this example, A, B and C are the parties who decided to share a private key together. They decided that any two of them can sign a transaction. To complete a TSS signing process, they need to follow the following steps:

### Step 1: Init TSS <a id="step-1-init-tss"></a>

During this step, all parties from different machines have to initialite their P2P settings before generate the shared key.

### Step 2: Generate Channel ID for bootstraping <a id="step-2-generate-channel-id-for-bootstraping"></a>

In this step, the parties will create a secrect communication channel between them. One of then will generate the channel ID and share with others. In this example, A will generate the channel ID. B and C will not have to do anything. A can also specify the length for this channel session and the default time is 30 mins.

In this step, the private key will be generated and shared between these three parties. All the parties have to be online at the sme time.

### Step 4: Sign Transaction <a id="step-4-sign-transaction"></a>

In this steo, A and B decided to sign a transaction together. Both A and B will try to broadcast the transaction and only one of them will succeed.

### Step 5: Regroup Vault <a id="step-5-regroup-vault"></a>

First, please generate a new channel for messaging:

Then, we can switch to the new channel for sending messages to each others.

* New committee having different t-n from old committee
* Change 1-3 into 2-4 scheme.
* old parties \(A, B\) join new committee
* new parties \(D, E\) are newly-joined
* Regroup from 1-3 to 2-4, with 2 old parties \(A and B\) and 2 new parties \(D and E\)

