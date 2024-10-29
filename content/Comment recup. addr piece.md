---
title: Comment récupérer l'adresse de votre pièce après l'échec d'une opération de pontage
draft: true
tags:
  - quilibrium
  - crypto
  - mainnet
  - release
  - solution
creation_date: 2024-10-29 17:38
modification_date: 2024-10-29 17:39
sources:
  - https://docs.quilibrium.one/start/tutorials/qclient/how-to-retrieve-your-coin-address-after-a-failed-bridging-operation
  - https://discord.com/channels/1212446221395042335/1212815856418164737/1300826971802177557
---
# Comment récupérer l'adresse de votre pièce après l'échec  d'un 'bridge'*

Usually, you can retrieve your coin address with the qclient token coins command. See [qclient commands for token transfers](https://docs.quilibrium.one/start/qclient-commands-for-token-transfers)

But in most cases, after a failed bridging operation, that command won't be able to query your coin address anymore.

This is because your coin has been taken out of the Quilibrium network and reserved for minting on Ethereum, but because you did not finish the bridge successfully, the coin has remained in a sort of "limbo".

This is why you should ALWAYS take note of your coin address before attempting to bridge.

So, if you can't query your coin address directly anymore (when `qclient token coins` doesn't work), here are 4 alternative methods to find your coin address.

En général, nous pouvons récupérer l'adresse de nos pièces avec la commande 
`qclient token coins`

Mais dans la plupart des cas, 
après l'échec de l'opération consitant à fait un pont "bridging",
cette commande ne pourra pas retrouver l'adresse de votre pièce.
 
 En effet, vous pouvez imaginez que votre pièce a été retirée du réseau Quilibrium afin d'être réservée à la frappe sur Ethereum, mais comme vous n'avez pas terminé le pont avec succès, la pièce est restée dans une sorte de « limbes ». 
C'est pourquoi vous devez TOUJOURS prendre note de l'adresse de votre pièce avant de tenter un pont. Donc, si vous ne pouvez plus interroger directement l'adresse de votre pièce (lorsque `qclient token coins` ne fonctionne pas), voici 4 méthodes alternatives pour trouver l'adresse de votre pièce.

/!\ je n'ai pas encore eu ce problème. Donc je ne fait que reporter ce que j'ai glané. 
## 1ère méthode: Décodage du premier format

Dans ce format, l'adresse de votre pièce est intégrée entre des chaînes de charactères statiques.
#### Structure

```
0x7472616e73666572[adresse_de_votre_pièce_sans_0x]1ac3290d57e064bdb5a57e874b59290226a9f9730d69f1d963600883789d6ee2
```

#### Exemple

```
# chaine de charactère originale:
0x7472616e73666572230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a21ac3290d57e064bdb5a57e874b59290226a9f9730d69f1d963600883789d6ee2

# adresse:
0x230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a2
```

> **Note**: The `0x` prefix is omitted in the cross-mint string.

###  2ème méthode: Décodage du deuxième format

This format combines your Ethereum address and coin address.

#### 

Structure

```
[your_ethereum_address][your_coin_address_without_0x]
```

#### 

[](https://docs.quilibrium.one/start/tutorials/qclient/how-to-retrieve-your-coin-address-after-a-failed-bridging-operation#example-1)

Example

```
# Original string:
0xc0ffee254729296a45a3885639AC7E10F9d54979230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a2

# Breakdown:
Ethereum address: 0xc0ffee254729296a45a3885639AC7E10F9d54979
Coin address: 0x230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a2
```

### 

[](https://docs.quilibrium.one/start/tutorials/qclient/how-to-retrieve-your-coin-address-after-a-failed-bridging-operation#where-to-find-these-strings-in-your-terminal-after-a-failed-bridging-operation)

Where to find these Strings in your terminal after a failed bridging operation

You can find the cross-mint hex strings in either:

- Your `.bash_history` file
    
- By using the up arrow key in your terminal to browse command history
    

---

### 

[](https://docs.quilibrium.one/start/tutorials/qclient/how-to-retrieve-your-coin-address-after-a-failed-bridging-operation#method-3-using-etherscan)

Method 3: Using Etherscan

If you have a failed transaction:

1. Go to Etherscan
    
2. Find your transaction
    
3. Click on "+ Click to show more"
    
4. Select "Decode Input Data"
    
5. Look for the `uid` value in the decoded data
    

---

### 

[](https://docs.quilibrium.one/start/tutorials/qclient/how-to-retrieve-your-coin-address-after-a-failed-bridging-operation#method-4-using-a-fresh-node)

Method 4: Using a fresh node

I have not tested this method, but it's been suggested by other that it coudl work

Spin up a fresh node, install the qclient and import the .config folder for the keys that you want to query for your coin address.

After your node begin syncing, try using the `qclient token coins` command again.

Because your node is not fully synced, it should in theory be able to "look into the past" and find your coin address even if, when querying that info from a fully synced node, you cannot see it.

---

### 

[](https://docs.quilibrium.one/start/tutorials/qclient/how-to-retrieve-your-coin-address-after-a-failed-bridging-operation#the-bridge-advanced-mode-shows-unknown-amount-when-i-paste-my-coin-address)

The bridge "Advanced" mode shows "Unknown Amount" when I paste my coin address.

If you have retrieved your coin address and are trying to finish the bridging process by pasting it directly via the "Advanced" bridge mode, you will see an "Unknown Amount" message.

This is normal, as the bridge doesn't know the amount in QUIL for that coin, since it no longer exists on the Quilibrium network but is already reserved for minting on Ethereum.

You can proceed with finishing the bridge, even if the amount is unknown, and your coin should be bridged successfully.
