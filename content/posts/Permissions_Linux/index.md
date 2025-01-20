---
title: "🔐 Les permissions Linux : Bienvenue dans la bibliothèque !"
date: 2025-01-20
tags:
 - "linux"
 - "permissions"
 - "sécurité"
categories:
 - "Linux"
---

"Permission denied" ... On a tous déjà vu ce message frustrant sous Linux ! Mais au fait, c'est quoi ces fameuses permissions ? 

Imaginez une bibliothèque municipale. Il y a le bibliothécaire en chef, son équipe, et les visiteurs. Chacun a des droits différents, et c'est normal. Vous ne voudriez pas qu'un visiteur puisse réorganiser tous les rayons, n'est-ce pas ? 

## 🏛️ Visite guidée de notre bibliothèque Linux

### 1. Les différentes sections de la bibliothèque

Faisons un tour avec la commande magique `ls -l` :
```bash
ls -l
drwxr-xr-x Documents/   # Une salle de la bibliothèque
-rw-r--r-- roman.txt    # Un livre ordinaire
lrwxrwxrwx lien.txt     # Un panneau d'indication
```

C'est comme si on avait :
- 📚 Des livres ordinaires (`-`)
- 🏷️ Des panneaux d'indication (`l` comme lien)
- 🚪 Des salles (`d` comme directory)
- 🖨️ Des équipements spéciaux (`b`, `c`)

### 2. Les cartes d'accès (r, w, x)

Dans notre bibliothèque, chacun a une carte d'accès avec différents droits :

```bash
r : read   (lecture)     # 📖 Pouvoir lire un livre
w : write  (écriture)    # ✍️ Pouvoir écrire dedans
x : execute (exécution)  # 🔑 Pouvoir ouvrir/utiliser
```

Par exemple :
- Un visiteur peut lire (`r`) un livre
- Le bibliothécaire peut le modifier (`w`)
- Le gardien peut ouvrir les salles (`x`)

### 3. Le personnel de la bibliothèque

Regardez ce badge d'accès :
```bash
-rwxr-xr--
 👑  👥  🌍
 │   │   └── Les visiteurs (others)
 │   └────── Les bibliothécaires (group)
 └────────── Le chef bibliothécaire (user)
```

C'est comme une hiérarchie :
1. 👑 Le bibliothécaire en chef (proprio)
2. 👥 L'équipe des bibliothécaires (groupe)
3. 🌍 Les visiteurs (autres)

### 4. Décoder les badges d'accès

Prenons un exemple concret :
```bash
-rwxr-xr--  roman.txt
```

C'est comme un livre (`-`) où :
- Le chef (rwx) peut :
  - 📖 Le lire (r)
  - ✍️ Le modifier (w)
  - 🔑 L'utiliser (x)
- Les bibliothécaires (r-x) peuvent :
  - 📖 Le lire (r)
  - ❌ Pas le modifier
  - 🔑 L'utiliser (x)
- Les visiteurs (r--) peuvent :
  - 📖 Juste le lire (r)
  - ❌ Rien d'autre

### 5. Modifier les accès

#### La méthode simple (comme les badges)
```bash
# Donner une clé au chef
chmod u+x fichier

# Retirer le stylo aux bibliothécaires
chmod g-w fichier

# Autoriser la lecture aux visiteurs
chmod o+r fichier
```

C'est comme distribuer des badges :
- `u` : pour le chef (user)
- `g` : pour l'équipe (group)
- `o` : pour les visiteurs (others)
- `+` : donner un droit
- `-` : retirer un droit

#### La méthode numérique (pour les geeks)
```bash
chmod 755 fichier  # rwxr-xr-x
```

Le code secret :
- 4 = lecture (r)
- 2 = écriture (w)
- 1 = exécution (x)

On additionne pour chaque groupe :
- 7 (chef) = 4+2+1 = lecture + écriture + exécution
- 5 (équipe) = 4+0+1 = lecture + exécution
- 5 (visiteurs) = 4+0+1 = lecture + exécution

### 6. Les pancartes et les copies

#### Les panneaux d'indication (liens symboliques)
```bash
ln -s roman.txt → référence
```
Comme un panneau "Ce livre est aussi en rayon 3" 📍

#### Les vrais doubles (liens durs)
```bash
ln roman.txt copie
```
Comme une vraie copie avec le même code-barres 📚

## 📝 Créer et écrire dans les livres (Heredoc)

Dans notre bibliothèque, parfois on veut créer un nouveau livre avec plusieurs pages d'un coup. C'est là qu'intervient le "Heredoc" :

```bash
# Créer un nouveau livre avec plusieurs pages
cat << 'EOF' > mon_livre.txt
Chapitre 1
Il était une fois...

Chapitre 2
La suite de l'histoire...

Chapitre 3
La fin !
EOF
```

Le Heredoc, c'est comme un assistant qui écrit tout ce qu'on lui dicte jusqu'à ce qu'on lui dise "EOF" (End Of File) !

Quelques variantes utiles :
```bash
# Ajouter des pages à un livre existant
cat << 'EOF' >> mon_livre.txt
Épilogue
Et ils vécurent heureux...
EOF

# Créer un script avec des commandes
cat << 'EOF' > mon_script.sh
#!/bin/bash
echo "Hello, World!"
ls -l
date
EOF
chmod +x mon_script.sh  # N'oubliez pas les droits d'exécution !
```

💡 Astuce : Les guillemets autour de 'EOF' empêchent l'interprétation des variables. Sans guillemets, on peut utiliser des variables :
```bash
nom="Alice"
cat << EOF > message.txt
Bonjour $nom !
La date est : $(date)
EOF
```

## 🎮 À vous de jouer !

Essayez par vous-même :
```bash
# Créer un nouveau "livre"
touch test.txt

# Voir son badge d'accès
ls -l test.txt

# Modifier les droits
chmod 644 test.txt     # rw-r--r--
chmod u+x test.txt     # rwxr--r--

# Changer le responsable
chown alice:staff test.txt
```

## 🎯 Les points clés à retenir

1. Chaque fichier a son badge d'accès
2. Trois groupes : chef, équipe, visiteurs
3. Trois droits : lire, écrire, exécuter
4. Deux façons de modifier : lettres ou chiffres
5. La sécurité avant tout !

Voilà, vous savez maintenant gérer l'accès à votre bibliothèque Linux ! N'oubliez pas : avec de grands pouvoirs viennent de grandes responsabilités... 📚✨