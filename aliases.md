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

    alias c='clear'
    
    alias tree="find . | sed 's/[^/]*\//|   /g;s/| *\([^| ]\)/+--- \1/'"

    alias l="ls -Falh"
    alias duh='du -h --max-depth=1'

    alias ..='cd ..'
    alias cd..="cd .."
    alias ...='cd ~-'

    alias vup='vagrant up'
    alias vdestroy='vagrant destroy --force'
    alias vssh='vagrant ssh'
    alias vdeploy='vagrant destroy --force && vagrant up && vagrant ssh'

    alias enpm='npm --registry registry.npmjs.eu'

* * *