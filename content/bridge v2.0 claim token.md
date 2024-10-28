---
title: Réclamer vos tokens
draft: false
tags:
---

Annoncement :

@discord : https://discord.com/channels/1212446221395042335/1212815856418164737/1300350344861061162

Pour utiliser le pont :
Utilisez qclient 2.0.1 pour obtenir votre identifiant de compte commençant par 0x :
./qclient-2.0.1-linux-amd64 token balance (utilisez la commande appropriée pour votre architecture/OS)
Visitez le site Web du pont et entrez votre compte à partir de l'étape 1 : https://quilibrium.com/bridge
Vous devrez connecter votre portefeuille ERC20 (c'est-à-dire MetaMask) et suivre les instructions à l'écran pour relever les défis du message. Une fois terminé, vous pourrez exécuter la transaction mint sur votre portefeuille ERC20.

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
	    