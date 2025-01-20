---
title: "Les processus sous Linux : la base de tout"
date: 2025-01-20
tags:
  - "linux"
  - "processus"
  - "système"
  - "conteneurs"
categories:
  - "Linux"
---



# Les processus sous Linux : la base de tout

Avant de plonger dans le monde fascinant des conteneurs, il faut comprendre ce qui se cache derrière. Et tout commence par une notion fondamentale : les processus.

## C'est quoi un processus ?

Imaginez votre ordinateur comme une cuisine. Chaque recette en cours de préparation serait un processus : il a besoin d'ingrédients (la mémoire), d'ustensiles (les ressources système), d'un plan de travail (l'espace CPU), et bien sûr, d'un chef cuisinier (le processeur).

Concrètement, un processus c'est :
- Un programme en cours d'exécution
- Un environnement isolé avec sa propre mémoire
- Une unité de base pour le système d'exploitation
- Un ensemble de ressources allouées

## L'ordonnancement des processus

Le système d'exploitation doit gérer tous ces processus qui s'exécutent en même temps. C'est le rôle de l'ordonnanceur (scheduler) :

### Le temps CPU
- Chaque processus obtient un quantum de temps
- L'ordonnanceur décide qui s'exécute quand
- Les priorités peuvent être ajustées (nice)
- Les processus peuvent être déplacés entre les cœurs CPU

### Les politiques d'ordonnancement
1. SCHED_OTHER : processus normaux
2. SCHED_FIFO : temps réel, premier arrivé premier servi
3. SCHED_RR : temps réel avec rotation
4. SCHED_BATCH : traitement par lots
5. SCHED_IDLE : uniquement quand le système est inactif

## La carte d'identité d'un processus

Chaque processus possède une identité unique :

### Le PID (Process ID)
- Numéro unique qui identifie le processus
- Géré par le kernel dans une table globale
- Le premier processus (init/systemd) a le PID 1
- Maximum configurable via /proc/sys/kernel/pid_max

### Le PPID (Parent Process ID)
- Identifie le processus parent
- Forme un arbre de processus
- Si le parent meurt, init/systemd devient le nouveau parent
- Visible avec `pstree` ou `ps f`

### Les identifiants de sécurité
- UID réel : qui a lancé le processus
- UID effectif : droits d'exécution actuels
- UID sauvegardé : pour les programmes setuid
- Groupes : appartenance aux groupes système

## Le cycle de vie détaillé

### La création (fork + exec)
1. fork() clone le processus parent :
   - Copie de l'espace mémoire (copy-on-write)
   - Duplication des descripteurs de fichiers
   - Héritage des signaux et ressources

2. exec() charge le nouveau programme :
   - Remplace l'image mémoire
   - Réinitialise les registres
   - Conserve les descripteurs de fichiers (sauf si close-on-exec)

### Les états possibles
- R (Running) : en cours d'exécution
- S (Sleeping) : en attente interruptible
- D (Disk Sleep) : en attente non interruptible
- T (Stopped) : arrêté ou tracé
- Z (Zombie) : terminé mais non récupéré
- X (Dead) : en cours de suppression

### La communication inter-processus (IPC)
1. Signaux
   - SIGTERM : demande de terminaison
   - SIGKILL : terminaison forcée
   - SIGSTOP : suspension
   - SIGCONT : reprise d'exécution

2. Autres mécanismes IPC
   - Pipes et FIFOs
   - Files de messages
   - Mémoire partagée
   - Sémaphores
   - Sockets Unix

## L'espace mémoire d'un processus

### Les segments mémoire
1. Text segment (code)
   - Instructions du programme
   - Lecture seule
   - Partageable entre processus

2. Data segment
   - Variables globales initialisées
   - Lecture/écriture
   - Privé au processus

3. BSS (Block Started by Symbol)
   - Variables globales non initialisées
   - Initialisé à zéro au démarrage
   - Pas stocké dans l'exécutable

4. Heap (tas)
   - Mémoire dynamique (malloc/free)
   - Croissance vers le haut
   - Fragmentable

5. Stack (pile)
   - Variables locales
   - Paramètres de fonction
   - Croissance vers le bas
   - Taille limitée

### La pagination
- La mémoire est divisée en pages
- Chaque processus a sa table des pages
- Permet la mémoire virtuelle
- Gère le swap si nécessaire

## Le système de fichiers /proc en détail

### Informations générales
```bash
/proc/[pid]/cmdline    # Ligne de commande
/proc/[pid]/cwd        # Répertoire de travail
/proc/[pid]/environ    # Variables d'environnement
/proc/[pid]/exe        # Lien vers l'exécutable
/proc/[pid]/fd/        # Descripteurs de fichiers
/proc/[pid]/maps       # Cartographie mémoire
/proc/[pid]/root       # Root directory
/proc/[pid]/status     # État du processus
```

### Contrôle et limites
```bash
/proc/[pid]/limits     # Limites de ressources
/proc/[pid]/oom_score  # Score Out-Of-Memory
/proc/[pid]/coredump   # Configuration du dump
```

### Statistiques
```bash
/proc/[pid]/io         # Statistiques I/O
/proc/[pid]/sched      # Infos d'ordonnancement
/proc/[pid]/stat       # Statistiques kernel
/proc/[pid]/statm      # Statistiques mémoire
```

## Les outils de monitoring

### ps : la base
```bash
# Tous les processus avec détails
ps aux

# Arbre des processus
ps auxf

# Processus d'un utilisateur
ps -u username

# Format personnalisé
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu
```

### top et htop
- Vue temps réel des processus
- Utilisation CPU et mémoire
- Possibilité de trier et filtrer
- Actions sur les processus (kill, renice)

### strace
- Trace les appels système
- Utile pour le debugging
- Montre les interactions avec le kernel
```bash
strace -p [pid]    # Attacher à un processus
strace cmd         # Tracer depuis le début
```

### lsof
- Liste les fichiers ouverts
- Montre les connexions réseau
- Identifie les processus bloquants
```bash
lsof -p [pid]      # Fichiers d'un processus
lsof file          # Qui utilise ce fichier
```

## Bonnes pratiques et pièges courants

### Gestion des ressources
1. Éviter les fuites mémoire
2. Fermer les descripteurs de fichiers
3. Gérer correctement les zombies
4. Limiter la fragmentation du heap

### Sécurité
1. Principe du moindre privilège
2. Validation des entrées
3. Gestion correcte des signaux
4. Protection contre les race conditions

### Performance
1. Optimiser l'utilisation mémoire
2. Éviter le thrashing
3. Utiliser les bonnes priorités
4. Gérer efficacement les I/O

## Pourquoi c'est important ?

Comprendre les processus est crucial car :
1. Les conteneurs sont basés sur l'isolation des processus
2. La gestion des ressources part des processus
3. La sécurité se gère au niveau des processus
4. L'orchestration manipule des processus

Cette compréhension est essentielle pour :
- Débugger des applications
- Optimiser les performances
- Gérer la sécurité
- Comprendre les conteneurs

## Pour aller plus loin

Dans le prochain article, nous verrons comment l'industrie est passée des processus "simples" aux conteneurs, et pourquoi cette évolution était nécessaire. Nous découvrirons l'histoire fascinante des conteneurs, de chroot à Docker, en passant par les innovations qui ont rendu tout cela possible.

Les processus sont la base de tout sous Linux. En comprenant leur fonctionnement, vous aurez une bien meilleure vision de ce qui se passe réellement dans votre système, et surtout, vous serez prêt à comprendre ce qui fait la magie des conteneurs.

N'hésitez pas à explorer par vous-même. La meilleure façon d'apprendre, c'est d'expérimenter !