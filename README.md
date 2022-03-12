# Labo découverte Maltego

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

## Recherche d'une adresse email

Si vous n'avez pas le nom d'une personne, mais une adresse email, vous pouvez aussi commencer votre recherche directement par l'adresse en question. Dans ce cas là, le résultat de la recherche pourrait vous trouver l'identité associée à cette adresse ainsi que d'autres détails comme, par exemple, une organisation, un numéro de téléphone, etc.

Pour chercher une adresse email, il suffit d'utiliser l'entité **Email Address** dans la palette.

![Email search](images/email_search.png)

Réalisez des recherches avec quelques adresses que vous connaissez, de préférence liées à une organisation. Est-ce que ça vous permet de retrouver des liens intéressants avec l'organisation ? Qu'avez-vous retrouvé en plus ? Accompagnez vos réponses avec des captures d'écran et commentaires.


## Installation et utilisation de nouvelles transformations

Pour installer de nouvelles transforms, cliquez sur l'onglet "Transforms" et ensuite sur Transform Hub. Depuis le hub, vous pouvez installer de nouvelles transformations.

Commençons par VirusTotal Public API. VirusTotal peut analyser des fichiers et des URLs pour chercher des malwares. Cela permet, par exemple, de trouver des fichiers/URLs compromis chez une cible. Vous aurez besoin de [créer un compte]( https://www.virustotal.com/gui/join-us) pour avoir accès à une clé vous permettant d'utiliser l'API et donc, la transformation correspondante pour Maltego. Un lien pour trouver votre clé vous sera envoyé dans le même email utilisé pour l'activation du compte.

On va maintenant installer la Shodan Tranform. Shodan.io est un "analyseur d'Internet". Il donne des informations intéressantes (aussi de point de vue de la sécurité) sur des dispositifs connectés, des serveurs et services, etc. Pour comprendre ce que Shodan vous apporte à travers le Transform Maltego et comment ça marche, [vous pouvez lire cet article](http://maltego.blogspot.com/2016/04/abracadabra-its-shodan-time.html). Vous aurez besoin de [créer un compte](https://account.shodan.io/register) pour utiliser la transformation.

PassiveTotal est une plateforme de recherche de menaces. Le but est de contribuer à analyser la sécurité de systèmes pour prévenir les attaques avant qu'elles n 'arrivent. Pour activer cette transformation, il faut commencer par la [création d'un compte](https://community.riskiq.com/registration). Vous accédez ensuite à votre espace utilisateur (account) et révélez les valeurs cachées dans API ACCESS. Attention, la transformation vous demande un user et une clé (key). Ces deux valeurs correspondent respectivement à votre adresse email et à la valeur identifiée comme "secret" sur votre compte riskiq. Pour plus d'information sur cette transformation, ce référer à [cet article](https://blog.passivetotal.org/brand-new-maltego-transforms-and-code/).

Vous pouvez chercher vous même des informations sur d'autres transformations disponibles.

Procédez maintenant à relancer les recherches que vous avez déjà effectuées, mais utilisant exclusivement les transformations que vous venez d'installer. Est-ce que vous arrivez à trouver d'autres informations ? N'oubliez pas votre capture et commentaires.

## Et maintenant ?

Est-ce qu'il vous restent encore des transforms gratuites à installer ? Vous pouvez donc procéder à l'installation d'autres transformations intéressantes comme Have I Been Pwned?, dataprovider, Farsight DNSB, FullContact, etc. Avoir un plus grand nombre de transformations installés augmente considérablement les résultats. Par contre, le volume d'information peut être difficile à gérer et à comprendre. Vous pouvez dans tous le cas, appliquer les transformations une par une au lieu de toutes en même temps.

Faites une petite recherche sur Internet pour comprendre le type d'information que chaque transformation vous apporte (ce n'est pas toujours très clair...). Remplissez un petit tableau avec ces informations. Ça peut devenir utile quand vous avez beaucoup de transformations installées.

Utilisez donc ces nouvelles transformations que vous avez installé.

Tous les résultats sur le graph sont utilisables pour lancer des nouvelles recherches. Un clique-droit sur les différentes icônes vous permet de lancer des transformations à partir de cette entité. Vous pouvez lancer des transformations sur des numéros de téléphone, des services, des adresses IP, des coordonnées, des documents, etc.

Utilisez quelques résultats retrouvés lors de vos recherches précédentes pour lancer des transformations sur d'autres entités de types différents à celles que vous avez déjà testé (Person, Domain, email). Est-ce que vous arrivez à trouver quelque chose d'intéressant ? Est-ce que le graph devient difficile à gérer ? Documentez vos activités avec des captures et des commentaires.

[GitHub est aussi une source précieuse de transformations](https://github.com/search?q=maltego+transform) qui ne se trouvent pas dans le Hub. Est-ce que vous avez une idée pour une transformation ? Vous pouvez [les developper vous même](https://docs.maltego.com/support/solutions/articles/15000017605-writing-local-transforms-in-python) aussi en python ! 

# Livrable

Captures d'écran et commentaires en format PDF ou directement sur le README.md

Le rendu se fait à travers un "pull request". 

# Echéance

Le 14 avril 2022 à 10h25

# Rendu

## Une simple reconnaissance du réseau

Le nom de domaine choisi appartient à l'entreprise auditée dans le cadre du cours d'AST : *rollomatic.ch*

De manière générale, on voit que l'on obtient énormément d'informations de différents types (noms DNS, adresses mails, numéros de téléphone, sites web, etc...) en ayant fait seulement une recherche sur le nom de domaine :

![image-20220303105846459](figures\image-20220303105846459.png)

Par contre, cette recherche n'a pas retourné d'entités Person comparé à l'exemple avec le domaine *heig-vd.ch*. Cela veut peut-être dire que Maltego n'a retrouvé aucun nom complet de personne lui permettant de créer une entité Person. Il est cependant possible de relancer de nouvelles transformations sur les adresses mails qu'il a trouvé, associées à des personnes. Maltego nous retourne également des anciennes versions du site web www.rollomatic.ch enregistrées sur le site Wayback Machine.

En relançant de nouvelles transformations sur le site web www.rollomatic.ch, on obtient de nouvelles informations comme de nouvelles adresses mails, des liens vers d'autres sites ainsi que différents composants utilisés par le site (OpenSSL, Apache, PHP, etc...) :

![image-20220303190838757](figures\image-20220303190838757.png)



Des transformations ont également été lancées sur l'adresse mail d.wunderlin@rollomatic.ch, ce qui a généré une entité Person puis de nouvelles transformations ont été lancées sur cette entité :

![image-20220303191354956](figures\image-20220303191354956.png)

Cela a retourné différents résultats dont des sites web sur lesquels cette personne est peut-être enregistrée ou référencée, de nouvelles adresses mails ainsi que des numéros de téléphone. Cependant, comme dans ce cas nous n'avons pas le prénom de la personne (seulement la première lettre), les résultats obtenus sont moins fiables et peuvent concerner un plus grand nombre de personnes, toutes en lien avec le nom de famille "Wunderlin". L'entité Deliverability est calculé à partir d'un score IPQS (IPQualityScore) permettant d'évaluer la "qualité" d'une adresse mail en fonction de certains indicateurs, ceci afin d'obtenir plus d'informations sur celle-ci.



## Recherche d'une identité

J'ai commencé par me rechercher moi-même et j'ai obtenu les informations suivantes :

![image-20220303192948696](figures\image-20220303192948696.png)

Malgré les multiples résultats, la majorité ne me concerne pas. Aucune des adresses mails obtenues ne m'appartiennent, seuls les comptes LinkedIn, GitHub et RootMe me concernent. Une page d'une site d'informations www.arcinfo.ch sur laquelle mon nom est inscrit a également été référencée. J'ai également tenté de lancer une recherche sur le pseudonyme que j'ai utilisé (en partant d'une entité Alias) sur le site RootMe mais elle n'a donné aucune information intéressante.

J'ai également lancé une recherche sur Stéphane Teixeira Carvalho et j'ai pu obtenir différentes informations en lien notamment avec le site web de la HEIG-VD, GitHub ainsi que le Swatch Group (site www.eta.ch) :

![image-20220303200936160](figures\image-20220303200936160.png)

Comme pour la recherche précédente, le reste des informations ne concerne pas la personne ciblée. 



## Recherche d'une adresse email

J'ai effectué une première recherche avec mon adresse mail de la HEIG-VD mais cela n'a pas ressorti plus d'informations importantes que les recherches précédentes : 

![image-20220306131256704](figures\image-20220306131256704.png)

Cependant, il est évidemment possible d'obtenir beaucoup d'informations sur l'organisation en relançant une recherche sur son domaine associé (ici *heig-vd.ch*) :

![image-20220306131955017](figures\image-20220306131955017.png)

Comme pour le domaine *rollomatic.ch*, on observe que l'on obtient des informations de différents types (personnes, noms DNS, serveurs mails, documents, etc...).

J'ai également essayé d'obtenir le nom et le prénom d'une connaissance en fonction de son adresse mail car ils ne figurent pas dans celle-ci mais en vain :

![image-20220306133137391](figures\image-20220306133137391.png)

Ceci afin de voir s'il était possible d'identifier une personne (avec son nom et son prénom) en fonction de son adresse mail possédant un pseudonyme. J'ai testé la même chose avec une autre adresse mail et même résultat, je n'ai pas pu identifier la personne. Pour ce qui est des Tags IPQS, "Suspect" indique que le serveur mail n'est pas capable de vérifier si l'adresse mail est bien valide. Pour ce qui est de "Frequent Complainer", cela indique que cette adresse mail est souvent désabonnée de listes marketing (newsletters, etc...) ou reporte souvent des mails comme spams.



## Nouvelles transformations

Le graphe ci-dessous contient uniquement les résultats obtenus avec la transformation VirusTotal :

![image-20220306140510380](figures\image-20220306140510380.png)

On peut voir que, par rapport à la recherche précédente, on obtient en plus des certificats (comme par ex. *COMODO RSA Domain Validation Secure Server CA* pour les sous-domaines *\*.rollomatic.ch*), des catégories (*media sharing* par ex.) ainsi que des points de couleurs nous indiquant le résultat de l'analyse VirusTotal :

- Le point vert signifie *harmless* 
- Le point jaune signifie *undetected* mais un ou plusieurs fournisseurs de sécurité ont défini l'URL ou le fichier comme malicieux
- Le point gris signifie également *undetected* mais aucun fournisseur de sécurité n'a reporté l'élément comme malicieux selon le site de VirusTotal. 

En effet, le site définit le niveau de menace en fonction de l'analyse de différents fournisseurs de sécurité (Avira, Fortinet, etc...).

Par exemple avec le sous-domaine *rmonitor.rollomatic.ch* :

![image-20220312154426114](figures\image-20220312154426114.png)



Ou encore avec un fichier javascript :

![image-20220312154526864](figures\image-20220312154526864.png)



Avec Shodan, on obtient aucune information supplémentaire par rapport à la recherche précédente sur le domaine *rollomatic.ch*. On obtient juste le nom DNS du serveur mail :

![image-20220306142000161](figures\image-20220306142000161.png)



J'ai donc relancé une recherche mais cette fois avec le domaine *heig-vd.ch* et cette fois on obtient plus de résultats :

![image-20220312155511373](figures\image-20220312155511373.png)

On obtient par exemple que le fournisseur d'accès Internet est *SWITCH*, que le port 80 sur l'adresse IP 193.134.220.45 est ouvert, qu'il y a 3 noms de domaine associés à cette adresse IP (*robot15.ch*, *mas-eddbat.ch*, *mas-mobilite.ch*), qu'elle semble être localisée à Neuchâtel et que l'organisation liée est la Haute École d'Ingénierie. On apprend aussi que le serveur web ayant répondu sur le port 80 utilise le service *Microsoft HTTPAPI httpd* mais cette information a pu être volontairement falsifiée.



Avec PassiveTotal, on obtient quelques sous-domaines en plus, les deux nameservers associés (*nsany1.infomaniak.com* et *nsany2.infomaniak.com*) ainsi que la date de premier enregistrement du domaine qui est le 17.01.1999 :

![image-20220306142431942](figures\image-20220306142431942.png)

On observe différentes entités \<empty\> qui représentent quand le domaine expirera, quand le registre a été mis à jour et quel est le registrar. Le registrar peut être obtenu en tapant la commande `whois rollomatic.ch` dans un terminal :

![image-20220312162225403](figures\image-20220312162225403.png)

Il est intéressant d'observer que les dates de premier enregistrement ne concordent pas à 1 jour près entre le résultat fourni par PassiveTotal et le résultat de la commande `whois`.



## Autres transformations

| Titre              | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| Have I Been Pwned? | Permet de savoir si une adresse mail ou un mot de passe a fuité |
| Farsight DNSDB     | Permet de faire une analyse à l'aide d'une base de données contenant des IPs, des noms de domaines ainsi que d'autres enregistrements DNS |
| FullContact        | Permet d'obtenir des informations venant de Twitter, des adresses mails et des numéros de téléphone |
| Social Links CE    | Permet de rechercher les comptes associés à une adresse mail |

Bizarrement dataprovider n'était plus disponible dans le Transform Hub de Maltego et n'a donc pas pu être installé.



J'ai testé la transformation Have I Been Pwned? sur une adresse mail qui est apparue dans une fuite de données et effectivement on peut le voir ici : 

![image-20220306144505222](figures\image-20220306144505222.png)

Cette adresse mail est semblerait-il apparu dans une liste de spam.



J'ai également essayé de lancer une recherche sur mon adresse mail de l'école avec FullContact puis Social Links CE mais je n'ai rien obtenu d'intéressant : 

![image-20220312164856561](figures\image-20220312164856561.png)

On peut voir que l'on obtient différents résultats où mon prénom (ou nom) apparaît, notamment des personnes liées à leurs entreprises respectives ainsi que leurs adresses, des documents JSON venant de l'OCCRP (*Organized Crime and Corruption Reporting Project*) qui, selon Wikipédia est "*un regroupement de journalistes d'enquête et de centres d'enquête fondé en 2006. Les membres de l'OCCRP enquêtent sur différentes zones géographiques et sur différentes thématiques*". On obtient également des documents accessibles publiquement venant d'un cloud.
