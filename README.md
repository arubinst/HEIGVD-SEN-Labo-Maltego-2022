# Labo découverte Maltego

Auteur : Axel Vallon

## Introduction

Maltego est un outil de data mining capable d'explorer une variété de ressources de données open-source et utilise ces données pour créer des graphs permettant d'analyser des éventuelles connexions identifiées entre ces différentes ressources.

Les graphs permettent de faire des connexions entre des informations comme le nom d'une organisation, les adresse email et son structure organisationnelle, des domaines, des documents, etc.

Maltego est écrit en Java, ce qui lui permet de fonctionner sur Windows, Mac et Linux. Il est pré-installé sur Kali.

Dans la pratique, Maltego recherche et parse des grandes quantités d'information à partir de sites publiques et produit un jolie graph pour vous aider à rassembler les pièces du puzzle.

Maltego peut être utilisé en tout moment pendant un audit. Pourtant, si la cible est un domaine, c'est raisonnable de mapper le réseau depuis le début avec Maltego.

## Téléchargement et installation

Il y a plusieurs version de Maltego :

- Maltego XL : version premium pour de grandes quantités de données
- Maltego Classic : version payante qui inclut toutes les "transformations"
- Maltego CE (Community Edition) : Version gratuite avec des "transformations" limitées
- Casefile : pour examiner des liens sur des données offline

Nous allons travailler avec la version gratuite, Maltego CE.

### Installation

- Kali : comme déjà mentionné, Maltego est déjà pré-installé sur Kali. Vous aurez quand-même besoin de vous rendre sur le [site de Maltego](https://www.maltego.com/ce-registration/) pour créer un compte CE. Une fois votre compte crée, vous recevrez une clé qui vous permettra d'utiliser la Community Edition.
- Téléchargement : si vous installez Maltego sur votre machine Windows, Mac ou autre version de Linux, vous pouvez le [télécharger ici](https://www.maltego.com/downloads/). Il vous faudra le [compte CE](https://www.maltego.com/ce-registration/) aussi pour cette version. 

## Transforms

![Transforms Hub](images/transform_hub.png)

Maltego utilise des API pour connecter à d'autres applications et services. Maltego appelle ces connexions "Transforms" (transformations). 

Vous remarquerez qu'avec la version CE, certaines transformations sont gratuites et d'autres sont payantes. En plus, seul un petit groupe de transformations sont pré-installées. Il faudra donc dans certains cas s'enregistrer sur chaque site pour obtenir un accès à l'API de la transformation et l'activer. Ça dépendra de vos besoins.

Quelques transformations sont gratuites mais elles ne peuvent pas être installées sur la version gratuite de Maltego.

Nous pouvons commencer à travailler utilisant la config de base. La transformation Paterva CTAS CE est pré installée et elle fourni pas mal de fonctionnalités. On va rajouter quelques transforms intéressantes plus tard. 

## Une simple reconnaissance de réseau

En partant d'un nom de domaine, on peut commencer à mapper la structure d'une organisation. C'est assez surprenant la quantité d'information qui peut être disponible à partir de rien d'autre qu'un nom de domaine.

Cliquer sur le bouton **new graph** en haut, à gauche pour commencer un nouveau projet vide.

![New graph](images/new_graph.png)

Depuis la palette d'entités (**Entity Palette**) à gauche, défilez vers le bas et trouvez l'entité **Domain**. Puis, faites-la glisser dans votre graph vierge. 

**Double-cliquez** sur l'icon **Domain** et changez le nom au domaine que vous voulez rechercher. Dans mon cas, j'ai choisi *heig-vd.ch*. Vous pouvez utiliser, par exemple, le domaine de l'entreprise que vous avez audité en AST, si vous avez suivi le cours. Sinon, sentez-vous libre de choisir un domaine qui vous paraît intéressant.

<img src="images/domain_heig.png" width="200">

Un click droit sur l'icône Domain ouvre la fenêtre d'execution de transformations, la **Run Transforms** box. On peut être assez spécifique ici et sélectionner seulement ce qui nous intéresse. Pourtant, nous allons devenir fous et simplement choisir **Run All Transforms** on sélectionnant la petite icône "fast forward" à côté. 

![Run all](images/run_all.png)

Dès que **Run Transform** est sélectionné, Maltego commence son travail en traçant la structure du réseau. **Remarque :** sur le côté gauche de l'interface du graphique, il existe plusieurs options pour visualiser le graphique sous différentes formes.

![HEIG scan](images/heig_scan.png)

Vous pouvez voir dans les images ci-dessous que toutes sortes d'informations apparaissent, y compris les serveurs DNS, intranet, les sites qui peuvent avoir une certaine relation avec la cible, les emails associés, les serveurs de messagerie. Qu'est-ce que vous trouvez pour votre cas ? Faites des captures d'écran pour votre rendu et ajoutez vos commentaires !

**Réponse**

Nous avons séléctionné la société BM-Emploi, la même que pendant le projet AST

![1_bm_emploi_gauche](images/1_bm_emploi_gauche.png)

Sur cette première image, la gauche du graphe complet, nous visualisons les différents noms de domaine et quelques adresses mail interne de l'entreprise.

![1_bm_emploi_milieu](images/1_bm_emploi_milieu.png)

Sur celle du milieu, quelques page et articles liées à BM-Emploi, leur site internet, l'hébergeur de leur site internet (Infomaniak), à nouveau quelques noms de domaine et certain numéro de téléphone.

![1_bm_emploi_droite](images/1_bm_emploi_droite.png)

Nous avons une répétions des autres types d'éléments découvert précédemment.



------



![Machines, names, emails](images/machines_names_emails.png)

![Servers](images/servers.png)

On peut utiliser ces connexions pour en faire des nouvelles encore plus détaillées. Par exemple, des noms associés avec des emails et même des numéros de téléphone (les numéros de téléphone sont difficiles à obtenir en Europe. La recherche pour les USA fonctionne correctement).

![People](images/people.png)

Regardons de plus près une personne qui apparaît comme étant connectée au domaine heig-vd.ch. Il s'agit de "Bastian Gardel". Je fais clique-droit sur l'icône de Bastien et **run All Transforms**. De votre côté, sélectionnez une identité trouvée pour votre domaine et exécutez vos transformations. N'oubliez pas de faire une capture et commenter. 

![Transforms Gardel](images/transform_gardel.png)

Lorsque les transformations seront terminées, nous aurons un graphique supplémentaire de quelques adresses email associées à Bastien Gardel. On y trouve aussi une clé PGP qui lui appartient, peut-être. J'ai vérifié avec Bastien et les adresses sont en effet des adresses email qu'il utilise ou il a utilisées. Dans certains cas, les résultats peuvent être assez étranges.

![email Bastien](images/results_gardel.png)

N'hésitez pas à tester d'autres domaines.

## Recherche d'une identité

Si vous avez déjà une identité d'une personne que vous voulez rechercher, vous pouvez procéder directement avec Maltego. Commencez avec un nouveau graphique et rajoutez une personne avec l'entité Person. 

![Person](images/person.png)

Je change l'identité de la personne en double cliquant sur l'icône et en introduisant mon nom.

![Person ARS](images/person_ars.png)

Ensuite, j'execute toutes les transformations sur la personne comme on l'a déjà fait pour les éléments du domaine.

![Run all Person](images/run_all_person.png)

Dans mon cas, je trouve mon adresse email de la HEIG-VD et l'une de mes adresses prives.

![Result ARS](images/result_ars.png)

Faites quelques recherches, avec des noms que vous connaissez (vous-même y-compris). Est-ce que vous arrivez à trouver des adresses email associées ? N'oubliez pas vos captures et commentaires.

**Réponses**

Premièrement, nous avons lancé un scan sur notre personne, et avons découvert très peu d'informations étonnantes. Cependant, nous avons approfondi certains points. 

![3_personne_vallon](images/3_personne_vallon.png)



Nous avons fait un nouveau scan supplémentaire sur rootme.org, et il a été possible de trouver mon profile rootme, avec mon nombre de point, ce qui n'est pas possible sur Google actuellement.

![3_rootme_profile](images/3_rootme_profile.png)



Sur l'image ci-dessous, Le dernier point intéressant trouvé est le lien entre 2 personnes. J'ai effectué une recherche sur Nicolas Hungerbühler, et Maltego a été capable de faire le lien être entre lui et moi. Les trois choses interéssante sont le fait qu'on soit les 2 sur rootme, qu'on ait les 2 un compte github, mais le plus intéressant est que nous 2 somme lié à thehugoawards, qui est prix littéraire américain créé en 1953 et décerné chaque année aux meilleures œuvres de science-fiction et de fantasy de l'année écoulée. Nous pouvons en déduire que nous 2 aimons ce genre de style litteraire, et exploiter ceci dans une attaque.

![3_trouver_lien](images/3_trouver_lien.png)

## Recherche d'une adresse email

Si vous n'avez pas le nom d'une personne, mais une adresse email, vous pouvez aussi commencer votre recherche directement par l'adresse en question. Dans ce cas là, le résultat de la recherche pourrait vous trouver l'identité associée à cette adresse ainsi que d'autres détails comme, par exemple, une organisation, un numéro de téléphone, etc.

Pour chercher une adresse email, il suffit d'utiliser l'entité **Email Address** dans la palette.

![Email search](images/email_search.png)

Réalisez des recherches avec quelques adresses que vous connaissez, de préférence liées à une organisation. Est-ce que ça vous permet de retrouver des liens intéressants avec l'organisation ? Qu'avez-vous retrouvé en plus ? Accompagnez vos réponses avec des captures d'écran et commentaires.

**Réponse : **

Le premier test sur les mails fait est sur mes deux boîtes mail. On voit dans les deux cas que ces mails existent, ce qui est déjà une information très intéressante. Deuxièmement, on voit la fiabilité de ces adresses, et c'est intéressant de voir si ce fournisseur a une certaine valeur, à l'inverse d'une adresse jetable.

![4_axel_vallon](images/4_axel_vallon.png)

Ensuite, nous avons utilisé différentes adresses à la HEIG, et très peu d'informations sont sorties, en dehors du faire que nous sommes dans la même organisation.

![4_heig-vd_webwail](images/4_heig-vd_webwail.png)


## Installation et utilisation de nouvelles transformations

Pour installer de nouvelles transforms, cliquez sur l'onglet "Transforms" et ensuite sur Transform Hub. Depuis le hub, vous pouvez installer de nouvelles transformations.

Commençons par VirusTotal Public API. VirusTotal peut analyser des fichiers et des URLs pour chercher des malwares. Cela permet, par exemple, de trouver des fichiers/URLs compromis chez une cible. Vous aurez besoin de [créer un compte]( https://www.virustotal.com/gui/join-us) pour avoir accès à une clé vous permettant d'utiliser l'API et donc, la transformation correspondante pour Maltego. Un lien pour trouver votre clé vous sera envoyé dans le même email utilisé pour l'activation du compte.

On va maintenant installer la Shodan Tranform. Shodan.io est un "analyseur d'Internet". Il donne des informations intéressantes (aussi de point de vue de la sécurité) sur des dispositifs connectés, des serveurs et services, etc. Pour comprendre ce que Shodan vous apporte à travers le Transform Maltego et comment ça marche, [vous pouvez lire cet article](http://maltego.blogspot.com/2016/04/abracadabra-its-shodan-time.html). Vous aurez besoin de [créer un compte](https://account.shodan.io/register) pour utiliser la transformation.

PassiveTotal est une plateforme de recherche de menaces. Le but est de contribuer à analyser la sécurité de systèmes pour prévenir les attaques avant qu'elles n 'arrivent. Pour activer cette transformation, il faut commencer par la [création d'un compte](https://community.riskiq.com/registration). Vous accédez ensuite à votre espace utilisateur (account) et révélez les valeurs cachées dans API ACCESS. Attention, la transformation vous demande un user et une clé (key). Ces deux valeurs correspondent respectivement à votre adresse email et à la valeur identifiée comme "secret" sur votre compte riskiq. Pour plus d'information sur cette transformation, ce référer à [cet article](https://blog.passivetotal.org/brand-new-maltego-transforms-and-code/).

Vous pouvez chercher vous même des informations sur d'autres transformations disponibles.

Procédez maintenant à relancer les recherches que vous avez déjà effectuées, mais utilisant exclusivement les transformations que vous venez d'installer. Est-ce que vous arrivez à trouver d'autres informations ? N'oubliez pas votre capture et commentaires.

**Réponse**

### VirusTotal

Nous avons lancé cette transformation uniquement, et avons récupéré ceci:

![5_bm_virustotal](images/5_bm_virustotal.png)

Les différents point supplémentaires sont :

- adresse IP du serveur disponible.
- Information liés à WhoIS, qui permet d'avoir des informations supplémentaire sur un nom de domaine, qui le possède, et depuis quand il existe.

Cette recherche sur des individus ou des adresses mail n'a rien donné 

## PassiveTotale

Nous avons lancé cette transformation uniquement, et avons récupéré ceci:

![5_bm_passivetotal](images/5_bm_passivetotal.png)

Les différents point supplémentaires par rapport à avant sont :

- adresse IP du serveur disponible.
- Informations sur les différents certificats. 
- Certaines informations sur la sécurité interne.

Cette recherche sur des individus ou des adresses mail n'a rien donné 

### Shodan

Shodan n'a donné aucun résultat sur BM-Emploi, ni l'HEIG. Cela doit signifier qu'aucun appareil connecté n'est connu pour ces organisations.

![5_bm_shodan](images/5_bm_shodan.png)

## Et maintenant ?

Est-ce qu'il vous restent encore des transforms gratuites à installer ? Vous pouvez donc procéder à l'installation d'autres transformations intéressantes comme Have I Been Pwned?, dataprovider, Farsight DNSB, FullContact, etc. Avoir un plus grand nombre de transformations installés augmente considérablement les résultats. Par contre, le volume d'information peut être difficile à gérer et à comprendre. Vous pouvez dans tous le cas, appliquer les transformations une par une au lieu de toutes en même temps.

Faites une petite recherche sur Internet pour comprendre le type d'information que chaque transformation vous apporte (ce n'est pas toujours très clair...). Remplissez un petit tableau avec ces informations. Ça peut devenir utile quand vous avez beaucoup de transformations installées.

Utilisez donc ces nouvelles transformations que vous avez installé.

Tous les résultats sur le graph sont utilisables pour lancer des nouvelles recherches. Un clique-droit sur les différentes icônes vous permet de lancer des transformations à partir de cette entité. Vous pouvez lancer des transformations sur des numéros de téléphone, des services, des adresses IP, des coordonnées, des documents, etc.

Utilisez quelques résultats retrouvés lors de vos recherches précédentes pour lancer des transformations sur d'autres entités de types différents à celles que vous avez déjà testé (Person, Domain, email). Est-ce que vous arrivez à trouver quelque chose d'intéressant ? Est-ce que le graph devient difficile à gérer ? Documentez vos activités avec des captures et des commentaires.

[GitHub est aussi une source précieuse de transformations](https://github.com/search?q=maltego+transform) qui ne se trouvent pas dans le Hub. Est-ce que vous avez une idée pour une transformation ? Vous pouvez [les developper vous même](https://docs.maltego.com/support/solutions/articles/15000017605-writing-local-transforms-in-python) aussi en python ! 

### Have I been Pwned

Le résultat était vide pour le nom de domaine BM-Emploi, donc il est possible de supposer que BM-Emploi n'a pas été pwned. Après différents essai sur entité comme la HEIG-VD ou même la commune de Rolle, cela n'a pas donnée de résultat

![image-20220331170026799](images/image-20220331170026799.png)

Cependant, après recherche, cette transformation est utile sur les numéro de téléphone et les adresse mail. Mon adresse mail personnelle a eu une "breach", ce qui signifie que mes données ont été dévoillée sur le site mangadex.org. 

### Dataprovider

Transformation non existante.

### DNSB

Transformation non existante.

 ### Farsight

Permet d'avoir une recherche DNS en interne d'une organisation plus intelligente. Il est vrai qu'il est possible d'avoir une meilleure vue de ce qui existe, en comparant la transformation de base et celle-ci. 

![6_farsight_gauche](images/6_farsight_gauche.png)

![6_farsight_droite](images/6_farsight_droite.png)

### IPInfo

Nous avons installé un transformer supplémentaire, et on y voit seulement la localisation de Infomaniak, qui héberge le site web de BM-Emploi. La localisation trouvée est (46.2022,6.1457), soit situé dans une Eglise. Cette donnée n'est pas très pertinante.

![image-20220331171549895](./images/image-20220331171549895.png)

## Fullcontact

Fullcontact permet de récupérer des informations sur une entité, et celle-ci m'a grandement étonnée par sa précision, on y voit des adresses, la date de création, et même le nombre approximatif d'employé. On peut avoir les informations de base d'une entreprise en même pas 10s avec cette API.

![6_fullcontact_bm](images/6_fullcontact_bm.png)

### Résultat final

En finalité, on se retrouve avec trop d'informations, et il devient compliqué de les gérer. Il est important de filtrer ce que l'on veut et ce que l'on ne veut pas pour pouvoir avancer.

![image-20220331172953325](images/image-20220331172953325.png)

# Livrable

Captures d'écran et commentaires en format PDF ou directement sur le README.md

Le rendu se fait à travers un "pull request". 

# Echéance

Le 14 avril 2022 à 10h25
