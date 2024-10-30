---
title: Comment récupérer l'adresse de votre pièce après l'échec d'une opération de pontage
draft: false
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
# Comment récupérer l'adresse de votre pièce après l'échec  d'un 'bridge'


En général, nous pouvons récupérer l'adresse de nos pièces avec la commande 
`qclient token coins`

Mais dans la plupart des cas, 
après l'échec de l'opération consitant à fait un pont "bridging",
cette commande ne pourra pas retrouver l'adresse de votre pièce.
 
 En effet, vous pouvez imaginez que votre pièce a été retirée du réseau Quilibrium afin d'être réservée à la frappe sur Ethereum, mais comme vous n'avez pas terminé le pont avec succès, la pièce est restée dans une sorte de « limbes ». 
C'est pourquoi vous devez TOUJOURS prendre note de l'adresse de votre pièce avant de tenter un pont. Donc, si vous ne pouvez plus interroger directement l'adresse de votre pièce (lorsque `qclient token coins` ne fonctionne pas), voici 4 méthodes alternatives pour trouver l'adresse de votre pièce.

/!\ je n'ai pas encore eu ce problème. Donc je ne fait que reporter ce que j'ai glané. 
### 1ère méthode: Décodage du premier format

Dans ce format, l'adresse de votre pièce est intégrée entre des chaînes de charactères statiques.
#### Structure

```
0x7472616e73666572[adresse_de_ta_pièce_sans_0x]1ac3290d57e064bdb5a57e874b59290226a9f9730d69f1d963600883789d6ee2
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

#### Structure

```
[ton_adresse_ethereum][adresse_de_ta_pièce_sans_0x]
```

#### Exemple

```
# adresse initiale:
0xc0ffee254729296a45a3885639AC7E10F9d54979230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a2

# découpage:
adress Ethereum : 0xc0ffee254729296a45a3885639AC7E10F9d54979
adress de ta pièce : 0x230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a2
```


### Méthode 3 : Utiliser Etherscan

Si tu as une transaction échouée :

1. Va sur Etherscan.
2. Trouve ta transaction.
3. Clique sur « + Click to show more ».
4. Sélectionne « Decode Input Data ».
5. Cherche la valeur uid dans les données décodées.

### Méthode 4 : Utiliser un nœud frais

&nbsp;&nbsp;&nbsp;Je n’ai pas testé cette méthode, mais d’autres suggèrent qu’elle pourrait fonctionner.

&nbsp;&nbsp;&nbsp;Lance un nœud frais, installe le qclient et importe le dossier .config pour les clés que tu souhaites interroger pour obtenir ton adresse de coin.

&nbsp;&nbsp;&nbsp;Une fois que ton nœud commence à se synchroniser, essaie à nouveau la commande qclient token coins.

&nbsp;&nbsp;&nbsp;Comme ton nœud n’est pas entièrement synchronisé, il devrait théoriquement être capable de « consulter le passé » et de trouver ton adresse de coin, même si, en interrogeant cette information depuis un nœud complètement synchronisé, tu ne peux pas la voir.

&nbsp;&nbsp;&nbsp;Le mode « Avancé » du pont affiche « Unknown Amount » lorsque tu colles ton adresse de coin.**

&nbsp;&nbsp;&nbsp;Si tu as récupéré ton adresse de coin et que tu essaies de finaliser le processus de pont en la collant directement via le mode « Avancé » du pont, tu verras le message « Unknown Amount ».

&nbsp;&nbsp;&nbsp;Cela est normal, car le pont ne connaît pas le montant en QUIL pour ce coin, puisque celui-ci n’existe plus sur le réseau Quilibrium mais est déjà réservé pour le minting sur Ethereum.

&nbsp;&nbsp;&nbsp;Tu peux continuer et finaliser le pontage, même si le montant est inconnu, et ton coin devrait être transféré avec succès. 😊