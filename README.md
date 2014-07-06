# tèminal

> Introduction course to shell basic commands

* * *

**tèminal** is an educational project, which will be used for an introduction to shell courses.

**Note:** the school where the course is given, the [HEPL](http://www.provincedeliege.be/hauteecole) from Liège, Belgium, is a french-speaking school. From this point, the instruction will be in french. Sorry.

* * *

**Note 2:** certains puristes tombés ici par hasard pourraient avoir à redire sur l'approche et la méthode. Sachez que ce cours est destiné à des étudiants qui n'ont rien d'informaticiens, et qui n'auront de la ligne de commande qu'un approche d'utilisateur ponctuel non-expert.  
Les plus intéressés apprendront les détails par eux-même, et le contenu de ce cours est suffisant pour couvrir les besoins du reste du cours de RIA.  
Si malgré tout, quelque chose vous chiffonne, n'hésitez pas à créer une **issue** qu'on puisse en discuter. Un grand merci.

* * *


## Introduction

Quand j'ai débuté dans le web, il était impensable d'avoir un jour besoin d'utiliser un terminal ; taper des lignes de commande, c'était réservé aux informaticiens, *Dieu nous en préserve*...

Mais de nos jours, avec tous les *frameworks* et outils actuels, il n'est pas rare de commencer un projet par une petite ligne de commande de déploiement, ce que vous avez sûrement déjà dû faire. Aujourd'hui, nous allons aller un peu plus loin en apprennant les bases de la ligne de commande.

Tôt ou tard, vous serez confrontés à un serveur web récalcitrant ou un langage un peu plus bas niveau qui nécéssite quelques manipulations en ligne de commande.

### Démarrage

Pour les besoins de ce cours, j'ai configuré un petit serveur mobile qui sera branché en classe, et accessible avec son propre réseau WIFI.  
Connectez-vous au réseau nommé **hepl-ria**. Ce réseau n'a pas de mot de passe.

Ensuite, nous commencerons le cours et seront prêts à nous connecter. Si vous êtes sur *mac* ou *linux*, il vous suffit d'ouvrir un **Terminal**, sur windows, le mieux est de télécharger le petit programme Putty, qui se télécharge à l'adresse suivante : [putty.org](http://www.putty.org/).

### Note importante

Le déroulement du cours et les commandes qui suivent sont données à titre de référence partielle, tout sera détaillé oralement pendant le cours.

Une **invite de commande** (ou *prompt*) se termine généralement par un `$`. Dans la suite du document, tout bloque de code commencant par un `$` signifie que la suite est une commande à entrer dans votre terminal. Le signe dollar ne fait bien sûr par partie de la commande en question. 

> Les blocs de citation commençant par un triangle (►) sont des indications personnelles sur le topic couvert par la commande. Ils sont là comme références pour moi-même, mais peuvent vous servir de rappel lors de la relecture du document.

Si vous souhaitez une référence pratique à consulter au quotidien, je vous conseille le ["Mémento Unix/Linux", aux éditions Eyrolles](http://www.eyrolles.com/Informatique/Livre/memento-unix-linux-9782212133066), et si vous voulez aller plus loin, je vous recommande le livre ["Parlez-vous Shell ?", aux éditions ellipses](http://www.editions-ellipses.fr/product_info.php?products_id=8981).

## 1. Connexion

Nous connaissons déjà l'adresse IP de notre serveur : `192.168.1.50`.  
Essayons de voir si le serveur est *live* en utilisant la commande `ping`.

    $ ping -c 4 192.168.1.50
    
> ► Présentation de la structure d'une commande.
    
Notre serveur nous ayant répondu, nous allons pouvoir nous y connecter, avec la commande `ssh`.

    $ ssl -l userX 192.168.1.50
    
Remplacez `X` par un nombre entre `1` et `20` (nous les attribuerons ensemble). Le mot de passe pour la connexion est `test`.

## 2. Position dans l'arborescence et listage

On vient d'arriver, autant savoir où nous sommes. La commande `pwd` va nous aider.

    $ pwd
    
> ► Présentation de l'arborescence de base d'un système UNIX.

On sait où nous sommes, regardons ce qui s'y trouve, avec `ls`.

    $ ls
    
C'est bien mais pas top. Je suis sûr qu'on peut en savoir un peu plus sur ce qu'il y a dans ce répertoire. Consultons le manuel de la commande `ls`, grâce à la commande `man`.

    $ man ls
    
Nous avons repéré des options intéressantes.

    $ ls -Falh
    
> ► Explication rapide de l'affichage, on reviendra sur les droits plus loin.
    
C'est bien mais tant qu'à faire, autant ne pas taper ça à chaque fois. Créons un alias.

    $ alias l="ls -Falh"
    
> ► Explication de la pérénité de l'alias, présentation rapide des fichiers de profil.
