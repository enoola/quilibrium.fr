---
title: Annonce - 30 Novembre 2024 - 08h37
draft: false
tags:
  - quilibrium
  - annonces
  - majv2
creation_date: 2024-10-30 15:10
modification_date: 2024-10-30 15:12
Annonce original: https://discord.com/channels/1212446221395042335/1212815856418164737/1301087575292903485
---


**Informations sur le Minting et la Réparation des Preuves Pré-2.0**

La limite de numéro de cadre pour le minting des preuves accuse un retard important en raison d’une congestion extrême, ce qui entraîne une production de cadres lente.

Bien que nous travaillions à améliorer le taux de production des cadres, pour éviter que l’intervalle de minting pré-2.0 ne dure trop longtemps, **le réseau arrêtera d’accepter de _nouvelles_ séries de preuves pré-2.0 le 02 novembre 2024, à 5h00 UTC**, afin de maintenir correctement la fenêtre de sept jours depuis l’ouverture de l’accès au minting des preuves. Si vous avez une série de preuves en cours d’envoi, vous ne serez pas affecté par cette mesure, conformément à l’objectif initial de la fenêtre de sept jours.

Étant donné la forte congestion du réseau, assurez-vous de passer immédiatement à la version 2.0 si ce n’est pas déjà fait, afin de ne pas risquer de manquer la date limite.

Par ailleurs, certains utilisateurs ont exécuté des scripts ou utilisé du matériel défectueux lors des versions 1.4.19/20/21, ce qui a produit des données corrompues.

Nous avons créé un outil de réparation qui tente de corriger les données corrompues, **cependant, il y a un risque significatif de perte de données et l’outil pourrait ne pas réussir à finaliser le minting, donc utilisez cet outil uniquement en dernier recours**.

L’outil peut être téléchargé ici via wget/curl. Vous devrez ensuite l’exécuter sur votre nœud.
https://releases.quilibrium.com/node-repair-tool-linux-amd64
https://releases.quilibrium.com/node-repair-tool-linux-arm64
https://releases.quilibrium.com/node-repair-tool-darwin-arm64