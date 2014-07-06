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
    
Nous avons repéré des options intéressantes. Appuyons sur la touche `q` pour quitter.

    $ ls -Falh
    
> ► Explication rapide de l'affichage, on reviendra sur les droits plus loin.
    
C'est bien mais tant qu'à faire, autant ne pas taper ça à chaque fois. Créons un alias.

    $ alias l="ls -Falh"
    
> ► Explication de la pérénité de l'alias, présentation rapide des fichiers de profil.

## 3. Navigation

Naviguons un peu.

    $ cd files
    $ pwd
    $ l
    
Revenons au dossier parent.

    $ cd ..
    
> ► Présentation du `.`, du `..`, du `~` et du `/`

Allons voir ailleurs, utilisons la touche `TAB`.

    $ cd web/www/
    $ pwd
    $ l
    
Mais quelle taille fait-il, ce répertoire ?

    $ du
    
Pas très clair... allons voir le manuel.

    $ man du
    
Maintenant qu'on a les bonnes options, allons-y.

    $ du -ha
    
Bon, c'est bien tout ça, mais moi, j'aime bien avoir un terminal tout propre. Vidons l'écran.

    $ clear
    
## 4. Lecture

Pour lire un fichier, on a l'embarras du choix.

    $ cat index.html
    
Ouais, bon, celle-ci est un peu *pif paf pof*. Essayons-en une autre.

    $ less index.html
    
Là, c'est tout de suite un peu plus pratiques : les flèches pour naviguer, `space` pour la page suivante, `b` pour la précédente, `q` pour quitter.

Et si je ne voulais voir que le début du fichier ?

    $ head index.html
    
Ou la fin ?

    $ tail index.html
    
Bon, 10 lignes, c'est peu...

    $ tail -n 20 index.html
    
## 5. Opérations sur les fichiers

Faisons quelques opérations sur les fichiers avant de les éditer.

D'abord, revenons à notre racine.

    $ cd
    $ pwd
    
Allons dans notre dossier `web`.

    $ cd web
    
Nous allons copier notre dossier `www` vers `tmp`, pour travailler sur une copie.

    $ cp web tmp
    
Hum... "`cp: omitting directory www`" ? C'est une erreur commune : on veut copier un dossier, on doit donc indiquer à la commande qu'on veut copier tout son contenu *récursivement*.

    $ cp -r
    $ ls
    
Notre dossier `tmp` existe, allons jouer un peu.

    $ cd tmp
    
Bon, le fichier `comments.php`, j'en ai rien à faire, on va le supprimer.

    $ rm comments.php
    
Pareil pour le dossier `images/`.

    $ rm images
    
Ah, zut, c'est un dossier, j'ai oublié...

    $ rm -r images
    
> ► Parler rapidement du fameux `rm -rf /`

Réorganisons un peu le dossier `styles/`.

    $ cd styles
    $ ls
    
Je ne suis pas fan de l'idée d'avoir notre fichier `bootstrap.css` à la racine de `styles`. On va le mettre dans un nouveau dossier rien que pour lui, `libs`.

    $ mkdir libs
    $ ls
    $ mv bootstrap.css libs
    $ ls
    $ cd libs
    $ ls
    
Et puis ce serait bien de mettre le numéro de version dans son nom.

    $ head bootstrap.css
    $ mv bootstrap.css bootstrap-2.1.1.css
    $ ls
    
## 6. Créer et éditer des fichiers

Retournons à la racine de notre site.

    $ cd ~/web/tmp
    
Créons un fichier vide.

    $ touch readme.md
    
Pour l'éditer, nous allons utiliser l'éditeur de texte `nano`.

> ► Petit mot rapide sur `vi` et `emacs`.

    $ nano readme.md
    
On sauve avec `CTRL+O`, on quitte avec `CTRL+X`.

On va en profiter pour modifier `index.html` et intégrer notre changement de chemin pour *bootstrap*.

## 7. Gestion des droits

Et si on allait un peu voir dans la config ?

    $ cd /etc
    $ ls
    
Ici, nous voyons tous les fichiers de config de notre serveur. Et si on rajouter un raccourcis dans les `hosts` ?

    $ nano hosts
    
Oh, *permissions denied*. Pourquoi ? Affichons quelques infos sur ce fichier.

    $ stat hosts
    
> ► Explication du système de droits.  
> ► Petit mot sur le `sudo`

Comparons avec un de nos fichiers

    $ cd
    $ stat web/tmp/readme.md
    
Les droits sont pareils, mais comme le `owner` est différent, forcément, ça coince pour le fichier `/etc/hosts`.

#### Petite synthèse des droits

* **aucun** `--- (0)`
* **exécution seulement** `--x (1)`
* **écriture seulement** `-w- (2)`
* **écriture & exécution** `-wx (3)`
* **lecture seulement** `r-- (4)`
* **lecture & exécution** `r-x (5)`
* **lecture & écriture** `rw- (6)`
* **tous** `rwx (7)`

> ► De l'importance de bien choisir ses droits.

On va modifier les doits de notre fichier readme pour que les membres de notre groupe puissent écrire dedans.

    $ chmod 664 web/tmp/readme.md
    
Maintenant, on va chacun écrire un mot dans le readme de quelqu'un d'autre.

    $ nano /home/userX/web/tmp/readme.md
    
On oublie pas de sauvegarder, puis on ferme.  
Allons voir notre fichier pour découvrir notre petit mot.

    $ cat web/tmp/readme.md
    
## 8. Informations sur les programmes

Nettoyons un peu tout ce désordre, pour commencer.

    $ clear
    
La plupart des programmes ont une option permettant de connaître la version installée sur le système.

    $ nano --version
    
On peut aussi savoir où se trouve un programme en utilisant la commande suivante.

    $ which nano
    
Ça nous permet aussi de savoir si un programme est installé ou non.

    $ which ruby
    
Si on ne reçoit rien, c'est que le programme n'existe pas sur la machine.

## 9. Informations sur le système

On peut aussi avoir quelques infos sur le serveur.

    $ uname -a
    
Et savoir depuis combien de temps il est lancé.

    $ uptime
    
> ► Petit mot rapide sur le *load average*

Regardons un peu l'état de notre serveur.

    $ top

