# tèminal : aliases

> Introduction course to shell basic commands : useful aliases

* * *

**tèminal** is an educational project, which will be used for an introduction to shell courses.

**Note:** the school where the course is given, the [HEPL](http://www.provincedeliege.be/hauteecole) from Liège, Belgium, is a french-speaking school. From this point, the instruction will be in french. Sorry.

* * *

Lors du cours, nous avons vu ensemble le moyen de créer des *alias*, des raccourcis personnels pour écrire une commande.

Vous trouverez ci-dessous une série d'alias utiles. Pour les utiliser, ajoutez-les à la fin de votre fichier `~/.bashrc` (sous linux) ou `~/.profile` (sous mac).

Pour prendre en compte vos nouveaux alias, vous pouvez soit quitter puis relancer votre terminal, ou entrer la commande suivante : `. .bashrc` ou `. .profile`.

* * *

Affiche tout le contenu du dossier courant, sous forme de liste, incluant les fichiers cachés, avec des tailles dans un format *lisible par un humain*.

    alias l="ls -Falh"

Affiche une réprésentation graphique de l'arborescence du dossier courant.
    
    alias tree="find . | sed 's/[^/]*\//|   /g;s/| *\([^| ]\)/+--- \1/'"

Affiche la taille des éléments du dossier courant, ainsi que sa taille totale, dans un format *lisible par un humain*.

    alias duh='du -h --max-depth=1'

Remonte d'un niveau dans l'arborescence.

    alias ..='cd ..'
    alias cd..="cd .."

Revient au chemin précédent dans la navigation.

    alias ...='cd ~-'

La commande `mkdir` créé par défaut les répertoires intermédiaires, et listera les dossiers créés.

    alias mkdir="mkdir -pv"

Lance la vagrant box associée à ce dossier.

    alias vup='vagrant up'
    
Détruit (de force) la vagrant box associée à ce dossier.

    alias vdestroy='vagrant destroy --force'
    
Se connecte en ssh à la vagrant box associée à ce dossier.
    
    alias vssh='vagrant ssh'
    
Combinaison des trois commandes précédentes : détruit, recrée puis se connecte.
    
    alias vdeploy='vagrant destroy --force && vagrant up && vagrant ssh'

Utilise le miroir npm Européen pour l'installation de packages (utile dans les cas où le miroir global est *dans les choux*).

    alias enpm='npm --registry registry.npmjs.eu'

Liste les ports réseaux ouverts sur la machine.

    alias ports='netstat -tulanp'

Efface l'écran.

    alias c='clear'

* * *

Mais les *aliases* ne sont que le bout visible de l'immense Iceberg de la configuration de votre environnement.

Toute cette configuration, qui s'adresse principalement aux utilisateurs des systèmes UNIX (Linux & Mac OS X), passe par des fichiers cachés qui commencent par un `.`, c'est pourquoi on les appelle "dotfiles".

Vous pouvez aller très loin en terme de personnalisation avec les dotfiles.  
Si vous avez envie de creuser le sujet, je vous invite à lire ce [tutoriel d'introduction](https://medium.com/@webprolific/getting-started-with-dotfiles-43c3602fd789), et vous référer à cette [liste de ressources](https://github.com/webpro/awesome-dotfiles) particulièrement complète. Vous pouvez aussi vous inspirez [des miens](https://github.com/leny/pwendok), si le cœur vous en dit...
