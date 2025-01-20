---
title: "Linux : Une visite guidée de votre maison numérique"
date: 2025-01-20
tags:
 - "linux"
 - "système de fichiers"
 - "FHS"
categories:
 - "Linux"
---

"Mais pourquoi ils ont mis ce fichier là ?" C'est probablement la question que vous vous êtes posée en découvrant Linux. Entre `/bin`, `/etc`, `/usr` et compagnie, on dirait un vrai labyrinthe ! 

Et si je vous disais que c'est en fait aussi simple que de se promener dans une maison ?

## Bienvenue chez vous !

Imaginez que vous venez d'emménager. Comme dans toute maison, il faut savoir où sont rangées les choses. On fait la visite ensemble ?

### 1. Les fondations (/)

C'est le socle de la maison. On note ça avec un simple `/`. Sans fondations solides, pas de maison ! C'est la base de tout le système.

```bash
# Voyons ce qu'il y a dans les fondations
ls /
bin   dev  home  lib    media  opt   root  sbin  sys  usr
boot  etc  init  lib64  mnt    proc  run   srv   tmp  var
```

### 2. La chambre (/home)

Comme toute bonne chambre, c'est VOTRE espace personnel. Personne n'y met le nez sans permission !

```bash
/home/alice/
    └── Documents/
        └── recettes.txt
    └── Images/
        └── vacances.jpg
    └── Téléchargements/
        └── film.mp4
```

Ici, vous pouvez :
- Ranger vos documents
- Garder vos photos
- Installer vos programmes personnels
- Faire ce que vous voulez !

### 3. Le tableau électrique (/etc)

🚨 ATTENTION : Zone sensible ! 

C'est comme le tableau électrique de la maison. On y trouve :
```bash
/etc/
    └── network/        # Configuration réseau
        └── interfaces  # Comment se connecter à Internet
    └── ssh/           # Sécurité des connexions distantes
    └── passwd         # Liste des habitants de la maison
```

Un conseil : ne touchez à rien ici sans savoir ce que vous faites !

### 4. La boîte à outils (/bin et /sbin)

Comme dans toute maison, on a :
- Une boîte à outils basique (`/bin`) pour tout le monde
- Une boîte à outils pro (`/sbin`) pour les experts

```bash
/bin/
    └── ls     # Pour voir le contenu des pièces
    └── cp     # Pour copier des choses
    └── mv     # Pour déplacer des meubles

/sbin/
    └── fdisk  # Pour gérer les espaces de stockage
    └── iptables  # Pour gérer le pare-feu
```

### 5. La boîte aux lettres (/var)

C'est là que tout ce qui change arrive :
```bash
/var/
    └── log/   # Journaux d'activité
    └── mail/  # Courrier électronique
    └── spool/ # Files d'attente (impression...)
```

### 6. L'établi (/tmp)

Le garage où on bricole ! Attention, il est nettoyé régulièrement.

```bash
/tmp/
    └── téléchargement-en-cours.zip
    └── fichier-temporaire.txt
```

Conseil : Ne laissez rien d'important ici !

### 7. La bibliothèque (/usr)

La plus grande pièce de la maison ! C'est ici que vivent la plupart des programmes.

```bash
/usr/
    └── bin/     # Programmes installés
    └── lib/     # Bibliothèques de code
    └── share/   # Données partagées
    └── local/   # Vos installations manuelles
```

### 8. Le placard des extras (/opt)

Vous avez acheté un nouveau gadget ? C'est ici qu'il s'installe !

```bash
/opt/
    └── google/
        └── chrome/    # Votre navigateur
    └── discord/       # Votre messagerie
```

### 9. Le local technique (/dev)

Les "prises" où on branche tout :
```bash
/dev/
    └── sda           # Votre disque dur
    └── usb/          # Vos clés USB
    └── video0        # Votre webcam
```

### 10. Les compteurs (/proc)

Envie de savoir comment va votre maison ?
```bash
/proc/
    └── cpuinfo      # État du processeur
    └── meminfo      # État de la mémoire
    └── temperature  # Températures système
```

### 11. L'entrée (/mnt et /media)

Le hall où on accroche les manteaux... euh, les disques externes !
```bash
/media/
    └── usb/         # Clés USB branchées
/mnt/
    └── disque_externe/  # Disques montés manuellement
```

## Alors, on s'y retrouve mieux ?

Cette organisation n'est pas un hasard. Elle suit le FHS (Filesystem Hierarchy Standard), comme un plan d'architecte standardisé pour toutes les distributions Linux.

### Petit exercice pour finir

Trouvons où sont rangées nos affaires :
```bash
# Voir toutes les pièces principales
tree -L 1 /

# Explorer le contenu du tableau électrique
tree -L 2 /etc

# Voir ce qu'il y a dans notre chambre
tree -L 2 ~/
```

La prochaine fois que quelqu'un vous dit que Linux est compliqué, rappelez-vous : c'est juste une maison bien rangée ! 🏠

_PS : Et comme dans toute maison, n'oubliez pas de garder une copie des clés (sauvegarde) quelque part..._