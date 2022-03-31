# Labo découverte Maltego

###### Blanc Jean-Luc

## Etape 1 - Simple reconnaissance de réseau

Scan de heig-vd.ch : 

![image-20220303110313623](C:\Users\jean_\AppData\Roaming\Typora\typora-user-images\image-20220303110313623.png)

Sur ce screen, on peut voir qu'on récupère plusieurs noms de domaines, des individus, des numéros de téléphone, des adresses emails et différents sites. 

## Etape 2 - Recherche sur un individu du domaine

Scan de Joel Schär : 

![image-20220303110720737](C:\Users\jean_\AppData\Roaming\Typora\typora-user-images\image-20220303110720737.png)

On peut voir que j'ai retrouvé plusieurs informations sur ce "Joel Schar" a commencé par diverses adresses emails, un compte Facebook, Instagram, Linkedin, Mobilière, un numéro de téléphone ainsi qu'une chaîne Youtube.



## Etape 3 - Recherche sur un individu quelconque

Recherche sur Jean-Luc Blanc : 

![image-20220303111724185](C:\Users\jean_\AppData\Roaming\Typora\typora-user-images\image-20220303111724185.png)

On récupère différent type d'informations, des adresses mails, des numéros de téléphones et des comptes sur certains sites.

Aucune des informations trouvées ne m'appartiennent.



Recherche sur Dylan Canton

![image-20220303112758619](C:\Users\jean_\AppData\Roaming\Typora\typora-user-images\image-20220303112758619.png)

On récupère différent type d'informations, des adresses mails, des numéros de téléphones et des comptes sur certains sites.

Il n'y a que son github qui lui appartient réellement.



Recherche sur Rafaël Zermatten : 

![image-20220303113052012](C:\Users\jean_\AppData\Roaming\Typora\typora-user-images\image-20220303113052012.png)

On récupère différent type d'informations, des adresses mails, des numéros de téléphones et des comptes sur certains sites.

La quasi totalité des informations sont correctes.



## Etape 4 - Recherche d'adresses mails

Recherche sur jean-luc.blanc2@heig-vd.ch : 

![image-20220303114055233](C:\Users\jean_\AppData\Roaming\Typora\typora-user-images\image-20220303114055233.png)

On retrouve le site internet de la HEIG-VD ainsi qu'une "identité" correspondant à mon login.

Le reste des informations sont fausses



Recherche sur jean_luc97@hotmail.com : 

![image-20220303114118131](C:\Users\jean_\AppData\Roaming\Typora\typora-user-images\image-20220303114118131.png)

Ici peu d'information sont découvertes



## Etape 5 - Nouvelles transformations

### VirusTotal Public API

Recherche sur heig-vd.ch : 



![image-20220310105332762](C:\Users\jean_\AppData\Roaming\Typora\typora-user-images\image-20220310105332762.png)



### Shodan

Recherche sur heig-vd.ch puis sur l'adresse IP :

![image-20220310105829702](C:\Users\jean_\AppData\Roaming\Typora\typora-user-images\image-20220310105829702.png)



### PassiveTotal

Recherche sur heig-vd.ch : 

![image-20220310110222911](C:\Users\jean_\AppData\Roaming\Typora\typora-user-images\image-20220310110222911.png)



### Have I Been Pwned

Recherche sur jean-luc.blanc2@heig-vd.ch : 



![image-20220310111436148](C:\Users\jean_\AppData\Roaming\Typora\typora-user-images\image-20220310111436148.png)



