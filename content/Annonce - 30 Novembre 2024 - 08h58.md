---
title: Annonces - 30 Novembre 202s4 - 8h58
draft: true
tags:
  - quilibrium
  - annonces
  - majv2
creation_date: 2024-10-30 14:27
modification_date: 2024-10-30 15:28
source: https://discord.com/channels/1212446221395042335/1212815856418164737/1301092863777701908
---

source: 
- https://discord.com/channels/1212446221395042335/1212815856418164737/1301092863777701908

voici une autre, [[Annonce - 30 Novembre 2024 - 08h37]], salve d’informations sur les problèmes les plus courants recueillis par @LaMat.

#### Problèmes de Minting

&nbsp;&nbsp;&nbsp;La vitesse de minting est actuellement limitée, mais la capacité est en cours d’expansion. Si vous êtes bloqué, continuez simplement à réessayer le processus.

&nbsp;&nbsp;&nbsp;Voici un script que vous pouvez exécuter pour vérifier votre situation si vous faites le minting via le nœud.

&nbsp;&nbsp;&nbsp;Si aucune preuve n’a été soumise au cours des 60 dernières minutes, redémarrez le nœud (mais assurez-vous que vous n’avez pas en fait terminé le minting, car dans ce cas, <u>le script de @Lamatt [Quilibrium.one](https://quilibrium.one) donnera un **faux positif** en ne trouvant plus de messages de preuve dans le log</u>).

Script de @LaMat
```
curl -sSL -H "Cache-Control: no-cache" "http://raw.githubusercontent.com/lamat1111/QuilibriumScripts/main/test/qnode_monitor_proofs.sh" | bash
```
  
#### Erreurs de Recherche de Preuve

&nbsp;&nbsp;&nbsp;Lorsque les logs affichent `"can't find proof for peer id and increment"`, cela indique un manque dans vos enregistrements. Si vous avez envoyé au moins une preuve, une récupération pourrait être possible. Un outil de réparation est maintenant disponible ([voir l’annonce précédente]()).

#### Corruption de la Base de Données
&nbsp;&nbsp;&nbsp;Les erreurs mentionnant “pebble et invalid chunks” indiquent une corruption sévère de la base de données. Bien qu’une solution soit possible, elle peut nécessiter de revenir en arrière sur votre incrément. Ce problème nécessite une expertise pour gérer la corruption pebble.


#### Échecs des Opérations de Pont (Bridge)
&nbsp;&nbsp;&nbsp; Après un échec d’opération de "bridging" montrant un solde à zéro, enregistrez votre adresse de coin et utilisez le mode avancé du pont. Il suffit de ré-entrer votre compte et l’adresse du coin pour relancer le processus de pont. Pour des instructions sur la récupération de l’adresse du coin, consultez ce guide : https://docs.quilibrium.one/start/tutorials/qclient/how-to-retrieve-your-coin-address-after-a-failed-bridging-operation