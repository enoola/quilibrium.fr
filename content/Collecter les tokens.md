---
title: Collecter les token
draft: true
tags:
  - quilibrium
creation_date: 2024-10-28 11:33
modification_date: 2024-10-29 01:08
---

Avec la sortie de la v2.0 de Quilibrium et de son réseau

Les mineurs ont la possibilité de faire valoir leur travail en mettant à jour leur(s) noeud(s), afin de prouver que l'on détient ces preuves qui se doivent valident, et contribuer à la constitution des premiers block de la version v2.0.



Annonce :
[annonce liée sur le @discord](https://discord.com/channels/1212446221395042335/1212815856418164737/1300350344861061162)

⚠️ à date il n'est pas possible d'envoyer des portions de coins
en somme lorsque vous 


# Commandes pour transférer vos token(s)

Avec la sortie de Quilibrium 2.0, **Qclient** est mis à disposition sous forme de  binaires directement. 
### Méthode pour récupérer les fichiers constituant le client
1. Obtenir la liste des fichiers : https://releases.quilibrium.com/qclient-release
	exemple contenu :
```
qclient-2.0.1-darwin-arm64
qclient-2.0.1-darwin-arm64.dgst
qclient-2.0.1-darwin-arm64.dgst.sig.1
qclient-2.0.1-darwin-arm64.dgst.sig.2
qclient-2.0.1-darwin-arm64.dgst.sig.3
...
qclient-2.0.1-linux-arm64
qclient-2.0.1-linux-arm64.dgst
...
qclient-2.0.1-linux-amd64
qclient-2.0.1-linux-amd64.dgst
...
```
2. Télécharger un par un les fichiers
3. vérifier les l'intégrité du fichier
	4.a. obtenir la signature du binaire de qclient
```
$openssl dgst --sha256 qclient-2.0.1-linux-amd64
SHA2-256(qclient-2.0.1-linux-amd64)= f25bcc9e48e7d5c4d1ac8687ef924951f35bb10e30e787f223b78536c0c05f66
```
4.b 

4. gpg --verify qclient-2.0.1-linux-amd64.dgst.sig.1 qclient-2.0.1-linux-amd64.dgst




5. Collecter un par un les fichiers 
Il faut récolter la liste des fichiers ayant trait au client **qclient** 
https://releases.quilibrium.com/qclient-release

client de votre 

### 

How to run the qclient commands

For the commands to work you need to be in your "ceremonyclient/client" folder: `cd ~/ceremonyclient/client/`

To run the qclient commands, you need to execute your qclient binary, followed by the command and optional flags. One important flag is `--config /path/to/config`, without this flag the command will fail, unless you run it from inside the "node" directory (or whichever directory contains your .confg folder). Here is an example of a command:

```
./qclient-version-os-arch command --config /path/to/config
```

This translates to the following for v2.0.1 on Linux:

```
./qclient-2.0.1-linux-amd64 token balance --config $HOME/ceremonyclient/node/.config
```

Every time you see "qclient" in the commands below, it actually refers to something like `./qclient-version-os-arch`

### 

[](https://docs.quilibrium.one/start/qclient-commands-for-token-transfers#id-1.-general-command-syntax)

1. General Command Syntax

The CLI tooling itself will be relatively straightforward, and the commands can be executed as follows (assuming a build in the accompanying _/client_ folder rather than `go run ./...`:

```
client [--config=<other path than ../node/.config/>] <app> <cmd> <param1> <param2> <...>
```

### 


2. Querying Balance

The command line tool accepts arguments in either decimal (xx.xxxxx) format or raw unit (0x00000) format. Note that raw units are a multiple of QUIL: 1 QUIL = 0x1DCD65000 units

Command:

```
qclient token balance
```

Response:

```
$ qclient token balance
50.0 QUIL (Account 0x23c0f371e9faa7be4ffedd616361e0c9aeb776ae4d7f3a37605ecbfa40a55a90)
```

### 

[](https://docs.quilibrium.one/start/qclient-commands-for-token-transfers#id-3.-querying-individual-coins)

3. Querying Individual Coins

Users may want to view the individual coins:

Command:

```
qclient token coins
```

Response:

```
$ qclient token coins
25.0 QUIL (Coin 0x1148092cdce78c721835601ef39f9c2cd8b48b7787cbea032dd3913a4106a58d)
25.0 QUIL (Coin 0x2dda9dc9770a1e5a01974fcd5af2a77147d0f19fb4935a1df677ec6050be0a9e)
```

### 

[](https://docs.quilibrium.one/start/qclient-commands-for-token-transfers#id-4.-creating-a-pending-transaction)

4. Creating a Pending Transaction

Quilibrium's token application has two modes: a two-stage transfer/accept (or reject), or a single-stage mutual transfer.

Command (2 options: _Amount_ or _OfCoin_)

In Qclient version 2.0.x it's only possible to send an entire coin, not an amount. The amount feature will be added in version 2.1.x

```
qclient token transfer <ToAccount> <RefundAccount> <Amount|OfCoin>
```

Response: _Amount_ option (only available from version 2.1.x of the Qclient)

```
$ qclient token transfer <ToAccount> <RefundAccount> <Amount>

<Amount> QUIL (Pending Transaction 0x0382e4da0c7c0133a1b53453b05096272b80c1575c6828d0211c4e371f7c81bb)
```

_OfCoin_ option

```
$ qclient token transfer <ToAccount> <RefundAccount> <OfCoin>

<Amount> QUIL (Pending Transaction 0x0382e4da0c7c0133a1b53453b05096272b80c1575c6828d0211c4e371f7c81bb)
```

Omitting the RefundAccount will simply provide your own originating account. The option to specify exists so that you can maintain anonymity when sending by creating a fresh account to receive the refund. The RefundAccount cannot be the same as the ToAccount.

The first is a user-friendly version of a transfer, similar to what account-based networks like Ethereum and Solana do, where you operate on a balance. Behind the scenes, the client is actually splitting and/or merging coins as needed to create the required amount to send as a discrete coin. The second is an application-aware version of a transfer, similar to what UTXO-based networks like Bitcoin do, where you operate on the raw coin balance under a specific address. If you have good reason to manage coins separately (yet under the control of the same managing account), you will want to use the second option in conjunction with split/merge operations if needed:

```
$ qclient token split <OfCoin> <LeftAmount> <RightAmount>
<LeftAmount> QUIL (Coin 0x024479f49f03dc53fd702198cd9b548c9e96004e19ef6a4e9c5211a9795ba34d)
<RightAmount> QUIL (Coin 0x0140e01731256793bba03914f3844d645fbece26553acdea8ac4de4d84f91690)
```

```
$ qclient token merge <LeftCoin> <RightCoin>
<Total> QUIL (Coin 0x151f4ae225e20759077e1724e4c5d0feae26c477fd10d728dfea962eec79b83f)
```

### 

[](https://docs.quilibrium.one/start/qclient-commands-for-token-transfers#id-5.-accepting-a-pending-transaction)

5. Accepting a Pending Transaction

To accept a pending transaction, you simply run:

```
$ qclient token accept <PendingTransaction>
<Amount> QUIL (Coin 0x2688997f2776ab5993894ed04fcdac05577cf2494ddfedf356ebf8bd3de464ab)
```

The same applies for rejecting a pending transaction

```
$ qclient token reject <PendingTransaction>
<Amount> QUIL (PendingTransaction 0x27fff099dee515ece193d2af09b164864e4bb60c19eb6719b5bc981f92151009)
```

This creates a separate pending transaction because if the refund address is specified by the originator, and were they to specify another of your own addresses, it would be no different from accepting.

### 

[](https://docs.quilibrium.one/start/qclient-commands-for-token-transfers#id-6.-performing-a-mutual-transfer)

6. Performing a Mutual Transfer

Pending transactions introduce friction, but without that friction, users can be spammed coins they don't want, or sent coins from an address they do not wish to interact with. If both parties agree in advance to transact, they can perform a mutual transfer, where both parties must be online, but can avoid having to deal with the two-phase transaction. This is great for maintaining privacy (each party's account is private) as well as ensuring a timely completion of a transaction:

On the receiver's side:

```
$ qclient token mutual-receive <ExpectedAmount>
Rendezvous: 0x2ad567e4fc1ac335a8d3d6077de2ee998aff996b51936da04ee1b0f5dc196a4f
Awaiting sender...
```

and after the sender connects:

```
Awaiting sender... OK
<Amount> QUIL (Coin 0x0525c76ecdc6ef21c2eb75df628b52396adcf402ba26a518ac395db8f5874a82)
```

On the sender's side:

```
$ qclient token mutual-transfer <Rendezvous> <Amount>
Confirming rendezvous... OK
<Amount> QUIL (Coin [private])
```

or if using the raw Coin address:

```
$ qclient token mutual-transfer <Rendezvous> <OfCoin>
Confirming rendezvous... OK
<Amount> QUIL (Coin [private])
```

This will likely be the first unique experience Quilibrium provides to users already familiar with other networks, as privacy preservation is an immediately obvious and first class experience here by showing the user what it can (or _cannot_) see.

### 

[](https://docs.quilibrium.one/start/qclient-commands-for-token-transfers#id-7.-claiming-rewards)

7. Claiming Rewards

Tokens issued after 1.5.0 are issued by nodes providing their proofs to the Mint Authority functionality of the token application. Claiming those rewards can be configured to be performed automatically (default, generates a new Coin every claim and merges them), or in lump sums at intervals, manually. It is recommended for ease of management that the defaults are applied, so that in the event of hardware failure no rewards go unclaimed.

If you wish to do it manually, however, you will need to run:

```
$ qclient token mint all
<Amount> QUIL (Coin 0x162ad88c319060b4f5ea6dbf9a0c2cd82d3d70dfc22d5fc99ca5371083d68416)
```

---






Pour utiliser le pont :
Utilisez qclient 2.0.1 pour obtenir votre identifiant de compte commençant par 0x :
./qclient-2.0.1-linux-amd64 token balance (utilisez la commande appropriée pour votre architecture/OS)
Visitez le site Web du pont et entrez votre compte à partir de l'étape 1 : https://quilibrium.com/bridge
Vous devrez connecter votre portefeuille ERC20 (c'est-à-dire MetaMask) et suivre les instructions à l'écran pour vérifier et valider la signature des messages.
Je vous invite à faire attention au frais de gaz.

Une fois terminé, vous pourrez exécuter la transaction mint sur votre portefeuille ERC20.

Notez que la mise à jour de la balance à l'aide de qclient peut prendre un peu de temps, mais soyez assuré que la mise à jour de la balance se produit immédiatement lors de la frappe.

Pour ceux qui tentent de consolider les récompenses sur un seul portefeuille à l'aide du transfert de jetons qclient, certains rapports indiquent que cela ne fonctionne pas de manière cohérente (le message n'est pas diffusé sur le réseau). Vous ne perdrez pas vos tokens, mais le transfert risque de ne pas s'effectuer comme prévu. Dans ce cas, il peut être préférable d'attendre le RPC public qui sera bientôt publié, permettant les menthes et les transferts sans nœud entièrement synchronisé.


depuis mon serveur/noeud quilibrium :

.. token balance


![[Pasted image 20241028092012.png]
![[bridge v2.0 réclamer vos tokens.20241028.png]]
ou:
pic
![[bridge v2.0 token balance.20241028.png]]

ouvrir un navigateur rendez-vous 
https://quilibrium.com/bridge


![[bridge v2.0 claim token.20241028.png]]

en your account in my case : 0x1a77b3e73163e429641bef9841df902f06943941717751ba487b14ca7c398b85

it displays your coins
![[Screenshot 2024-10-28 at 09.44.51.png]]
you can verify from your node with the following command :
![[bridge v2.0 claim token coins.20241028.png]]
![[bridge v2.0 claim token coins verify.20241028.png]]

cliquer sur connect
.... captures


../client/qclient-2.0.1-linux-amd64 cross-mint 0x7472616e73666572167e5ea5ecc36ea9d16e34787fb5d74ac7a5e7693a161ecdeb9d5d890abef9761ac3290d57e064bdb5a57e874b59290226a9f9730d69f1d963600883789d6ee2

CAPTURES
j'btien
{"peerPublicKey":"bn6Bx8TgY8PPm1zX66UoVSEewvojsIIJc14rPn8sJdXZ7HUSOn+gGTU8saLnKa6Obr5RrhWnYh4A","peerSignature":"6tJ+lP62/o9lyJ2JKLSAd7q6k4YW1AR1m8aXoz+Eo4bRTphfYQtfJuId6UvxDUIfjVKnfqEqsyCAOyuhhHKFugHWAomMliioRP3gVOHEHKtuT1FXAsfXnRquL5Jv4u2E+NzVP8g+clxCDcPqw13aLgEA","proverPublicKey":"Nc8KTNoAyu51DJygQV+MRTVPF+FXk+qe6cuNPYqsllJydkLZbNtDjAGkOck2hYtFUSHvrxlL6AUA","proverSignature":"KU5bYWbjq+FsdNPBYcFgu+pCb3dkLidIHM1o+5gKlO5cbuyiDYZGm/ApBbgeA3A691jBMv3Vqs2AF8crfi3zyqW5AJ3Y2QSsCnLc+yNo461Sp9+XwMVyjI9fX3ivHmruKLIWvR3hEYUQ6gcnNAozMgQA"}




![[Pasted image 20241028091946.png]]

![[bridge v2.0 claim.20241028.png]]


now I would like to guide user ...

1. check value of : listenGrpcMultiaddr field
    1.a. if value equal ""; then tell user : "GRPC isn't set would you like to set it ? (y/n)"
        1.a. if "y" then apply sed command :
            sed -i.bak 's#listenGrpcMultiaddr: "/ip4/127.0.0.1/tcp/8337"#listenGrpcMultiaddr: ""#' config.yml
        1.a. if "n" exit 0
    1.b. else 
	    tell user : "GRPC is set would you like to unset it ? (y/n)"
		1.b. if "y" then apply sed command to replace line listenGrpcMultiaddr: "" with line containing : listenGrpcMultiaddr: "/ip4/127.0.0.1/tcp/8337"
	    