# README 

## Objectif ##

Ce script sert à installer des logiciels sur une base Ubuntu 22.04LTS avec un très large choix de paquets.
Il y a plusieurs avantages :
- Ce large choix de logiciel est accessible directement au sein d'une interface graphique unifiée (via Zenity),
- Il y a une description de chaque logiciel directement dans l'interface ce qui vous permet de voir au premier coup d'oeil ce qui peux vous intéresser ou non,
- Simple à utiliser : pour installer les logiciels, il suffit juste de cocher les cases correspondantes,
- Intègre différentes méthodes d'installations (installation via apt install, installation d'un paquet deb récupéré sur le site de l'éditeur, installation via un PPA ou le dépot de l'éditeur, installation via un Snap, installation avec Flatpak et le dépot Flathub, récupération au format AppImage, installation via un script etc...
(À noter que pour ceux qui n'aiment pas les paquets universels, sachez qu'aucun n'est coché par défaut et que, quand un logiciel est proposé en paquet universel, c'est explicitement indiqué dans le nom lors du choix).

![alt text](https://nsa40.casimages.com/img/2020/02/19//200219111357203921.png)

Démo en vidéo :
[Peertube](https://video.ploud.fr/videos/watch/fb72b903-b504-4e34-a5e6-590d252ed2db) ou
[YT](https://www.youtube.com/watch?v=PYei6q2Ar38)

## Compatibilité ##

Le script est destiné principalement à la version de base d'Ubuntu (Gnome) pour la version 22.04LTS.
Cela ne veux pas dire qu'il ne peut pas être utilisé sur une autre configuration mais qu'il a été testé/validé surtout pour celle-ci.

- Ce script est fait pour "Bash" (shell par défaut sous Ubuntu) mais pas pour les autres Shell donc si vous l'avez modifié manuellement sur votre Ubuntu pour mettre, par exemple, "Zsh" à la place, le script ne fonctionnera pas correctement (certaines fonctions non-compatibles).

- Si vous souhaitez utiliser le script sur une variante d'Ubuntu plutôt que la version de base (par exemple Xubuntu, Kubuntu, Ubuntu Mate, Linux Mint, ElementaryOS...), je vous recommande fortement au lancement de bien choisir l'option "Tous les choix décochés" par défaut afin de ne pas avoir des paquets utiles pour Gnome uniquement cochés par défaut (ce qui n'aura aucun intérêt pour vous vu que vous n'utilisez pas Gnome avec votre variante). Si vous utilisez KDE (notamment avec Kubuntu ou KDENeon), attention à bien cocher des logiciels cohérents avec cet environnement.

- Si vous souhaitez utiliser le script pour une ancienne version d'Ubuntu, par exemple la 20.04LTS ou la 18.04LTS, cela fonctionnera mais pas pour tous les logiciels, en effet certains s'installent avec une méthode spécifique pour la 22.04 qui ne marchera pas pour les versions précédentes. A noté que les Snaps/Flatpak/AppImage ne devraient poser à priori aucun problème quelle que soit la version (et même sur les autres distributions).

- Si vous avez besoin d'utiliser le script à distance via SSH, pensez à utiliser la paramètre "-X" afin d'avoir l'export graphique et donc d'avoir l'interface graphique Zenity (ssh -X login@....)

## Récupération / Lancement du script

Il y a 2 méthodes :

- Télécharger le contenu du script (répertoire Ubuntu_22.04LTS_PostInstall) sur ce github (soit par l'interface web soit via la commande wget), décompresser le contenu, penser à mettre le droit d'execution sur le script et lancer le "Postinstall" à l'intérieur SANS sudo (les sudo se trouvent à l'intérieur du script). En ligne de commande, cela donne donc :

> wget https://github.com/simbd/Ubuntu_22.04LTS_PostInstall/archive/master.zip &&
> unzip master.zip && 
> cd Ubuntu_22.04LTS_PostInstall-master/ && chmod +x Postinstall*sh &&
> ./Postinstall_Ubuntu-22.04LTS_FocalFossa.sh

- 2ème solution : faire avec git clone (avec l'avantage de pouvoir faire la maj du script sans le retélécharger manuellement). Il vous faudra en pré-requis avoir installé git (sudo apt install git).

> git clone https://github.com/simbd/Ubuntu_22.04LTS_PostInstall.git && cd Ubuntu_22.04LTS_PostInstall/ &&
> ./Postinstall_Ubuntu-22.04LTS_FocalFossa.sh

Avec cette 2ème solution, si vous voulez réutiliser le script plus tard et vérifier si il y a pas eu une nouvelle maj du script entre temps, dans le dossier du script, il suffira de faire :
> git pull

## Origine

C'est un fork d'un fork que j'ai beaucoup modifié, la base vient de Devil505 (https://github.com/Devil505), celui-ci a été forké ensuite pour être un peu amélioré par "FroggyComputing" (http://computing.travellingfroggy.info/).
Enfin je l'ai reforké car il était très incomplet en terme de choix logiciel et il manquait des fonctions.
J'ai notamment ajouté un gros paquet de logiciels provenant de mon ancien script qui était entièrement en ligne de commande (cf partie Archives) et ajouté des nouvelles possibilités d'installation.
(Seul 10% environ des logiciels viennent du script d'origine, 90% ont été ajoutés)
J'ai aussi ajouté des optimisations venant de mon ancien script et des packs de thème graphique. 

## Pré-requis (automatique)

Pour fonctionner correctement, le script a besoin des logiciels suivants ; cependant, de votre coté vous n'avez rien à faire puisqu'ils seront automatiquement installés :

- Zenity (permet l'affichage de la fenêtre graphique)
- Notify-send (permet l'affichage de notifications)
- Curl (utilisé par plusieurs logiciels proposés)

## Précisions concernant les balises du type {PPA}, {SNAP}, {FLATPAK} etc...

Les logiciels proposés ne s'installent pas tous de la même manière car les éditeurs ne proposent parfois qu'un seul type d'installation. Cependant certains d'entre-vous peuvent ne pas vouloir par exemple de Snap ou de Flatpak ou de PPA, si c'est le cas, pas de problème, pour ce type d'installation c'est indiqué explicitement a coté du logiciel par une balise { }. Par exemple, si vous ne voulez aucun paquet Flatpak installé, il suffira de vous assurer de ne pas cocher de cases avec {FLATPAK}.

_Légende_
- {PPA} => Signifie que le logiciel s'installera depuis un dépot PPA (sudo add-apt-repository ppa:...)
- {SNAP} => Signifie que le logiciel n'est pas un paquet debian mais un paquet universel Snap (c'est à dire installé depuis le SnapStore (snap install....)
- {FLATPAK} => Un peu comme les Snap sauf que ça utilisera Flatpak à la place via le dépot Flathub (flatpak install flathub nomdulogiciel...)
- {APPIMAGE} => Signifie que le logiciel sera récupéré au format AppImage (donc pas installé), le droit d'execution sera déjà correctement positionné. Vos logiciels au format AppImage seront stockés dans un dossier "AppImages" dans votre home.
- {Script LinInstall} => Signifie que le logiciel sera installé avec un script bash qui sera automatiquement récupéré et lancé

(S'l n'y a rien de précisé, cela signifie qu'il s'installe de façon classique avec apt install ou en paquet debian manuel ou avec un dépot officiel de l'éditeur. A noté que pour les paquets universels, vous n'avez pas besoin d'installer de pré-requis, si par exemple vous cochez un logiciel Flatpak et que vous n'avez jamais installé/configuré Flatpak, le script s'en chargera à votre place au 1er logiciel nécessitant Flatpak lors de son installation).

Cas particulier :

- {Nécessite intervention !} => Indique que pour certains logiciels, l'installation n'est pas 100% non-interactive, dans ce cas vous êtes obligé d'intervenir pour que le script puisse continuer (en générale pour valider un contrat de licence ou faire un choix particulier pour un logiciel spécifique).
Par conséquent, si vous cochez un logiciel où il est indiqué "{Nécessite intervention !}", pensez à contrôler l'avancée du script puisqu'il sera interrompu pour ce logiciel et la suite des installations ne reprendra que quand vous serez intervenu pour valider ce logiciel.

- (cli) => C'est juste une précision sur le logiciel pour vous indiquer qu'il ne s'utilise qu'en CLI (Command Line Inteface) c'est à dire en ligne de commande (pas d'interface graphique et souvent pas de raccourci dans le menu/dash des applications). À noter que ce n'est pas précisé pour ceux classé dans la catégorie "outil en cli" puisqu'ils sont tous concernés de toute façon dans cette catégorie donc inutile de le remettre à chaque fois).

***Bonne installation ! ;-)***
