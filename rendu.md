Lucas Gianinetti - 31.03.2022
___
# Labo Découverte Maltego

## Une simple reconnaissance de réseau

J'ai fait la reconnaissance sur le domain **ascenseurs.lsm.swiss**, les dates utilisées pour lancer les transformations sont les suivantes :
* Début: Date par défaut -  01.01.2010
* Fin: Date de réalisation du labo - 31.03.2022

Il ressort différents types de documents de la recherche :
* Des sites web
  ![](.rendu_images/siteweb.png)
* Des snapshots
  ![](.rendu_images/snapshots.png)
* Des numéros de téléphone
  ![](.rendu_images/phones.png)
* Une adresse email
  ![](.rendu_images/email.png)
* Des noms de domaine
  ![](.rendu_images/domain.png)
* Des documents
  ![](.rendu_images/docs.png)
* Des DNS
  ![](.rendu_images/dns.png)

Il y a beaucoup d'informations dont un certain nombre sont erronées. Par exemple parmi les sites web il n'y a que le site **ascenseurs.lsm.swiss** qui correspond au nom de domaine recherché. Les noms de domaine aussi sont faux, comme le nom de domaine recherché comprenait un "mot générique" (ascenseurs) cela a donné beaucoup de faux positifs.

___
Reconnaissance sur le domaine **heig-vd.ch**

On voit qu'il y a directement beaucoup plus d'informations disponibles, dont par exemple des personnes liées à la heig ce qu'il n'y avait pas pour la recherche ci-dessus
![](.rendu_images/51978b84.png)

## Recherche d'une identité

On peut voir que me concernant, Maltego a réussi à trouver des repos gits auxquels j'ai contribué ainsi que mon compte facebook. Le reste des informations sont soit complétement fausses tels que les adresses et mails et la majorité des sites. Soit des faux positifs comme un homonyme qui a un compte twitter.com/LucasGianinetti2 où encore une personne dont le nom me ressemble fortement *facebook.com/lucasgiannetti

![](.rendu_images/moi.png)

## Recherche d'une adresse email

J'ai recherché l'adresse email heig de Nicolas. On peut voir qu'elle a directement été associée avec le domaine heig-vd.ch ainsi qu'à son identité

![](.rendu_images/nico.png)

## Virus total

J'ai appliqué la transformation sur le domaine **heig-vd.ch**

On retrouve entre autres des certificats TLS:
![](.rendu_images/tls.png)
Des adresses IPs
![](.rendu_images/IPs.png)
Des phrases
![](.rendu_images/phrases.png)

## Shodan
J'ai run toutes les transormations de Shodan sur le domaine **heig-vd.ch**.
Une adresse IP a été trouvée :

![](.rendu_images/828abf5b.png)

En effectuant un `whois 193.134.220.45` on voit bien que l'adresse ip est liée à la heig et aussi à un certain Fabrice Demierre

![](.rendu_images/2bdb27fb.png)

## PassiveTotal

Résultat sur le domaine **heig-vd.ch**, pas d'informations supplémentaires très intéressantes

![](.rendu_images/09d5911a.png)

## Farsight DNSB

Collections passives de données DNS

En faisant la transformation sur le domaine heig-vd.ch on peut voir qu'il trouve plus de DNS, serveur mail et adresses IPs

![](.rendu_images/f56fa187.png)

![](.rendu_images/5f008d7b.png)

## Have I Been Pwned ?

Regarde si une adresse email a été compromise / Comparaison avec des DB d'emails compromises connues

On peut voir que mon mail de l'heig ne fait pas parti des listes d'emails compromises

![](.rendu_images/82e17f58.png)


## Dataprovider

## FullContact
Trouve toutes les informations de contacts, tel que num de téléphone, adresse, page web d'infos, compte twitter

Pour heig-vd.ch

![](.rendu_images/5193e652.png)


## Conclusion

Si j'effectue toutes les transformations (de base + les transformations ajoutées) sur le domaine de la heig-vd on peut voir que les informations sont nombreuses et que le graphe devient difficile à lire

![](.rendu_images/05657603.png)

Mais en sélectionnait l'affiche par liste et en triant les informations par types nous arrivons à trouver notre chemin.

L'outil est très puissant et la combinaison des différentes transformations permet d'avoir une vue d'ensemble de l'organistion recherchée.


