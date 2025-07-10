---
title: "Créer un serveur core pour mon infra DevOps/Fyndra"
date: 2025-07-10
description: "Présentation du nœud principal de l’infrastructure Fyndra : un serveur isolé dédié aux services critiques."
slug: "serveur-core"
tags: ["fyndra", "proxmox", "infra", "tailscale", "headscale"]
draft: false
---

# Pourquoi un serveur core ?
Dans Fyndra, mon objectif est de permettre à un utilisateur de déclencher un environnement cloud-native complet : VM, conteneur, outils installés, terminal accessible, tout ça en un clic.

Mais avant de faire tourner ces environnements, il faut une colonne vertébrale fiable.
C’est le rôle de ce serveur "core" : un nœud stable, isolé, qui ne sert pas à exécuter les VM, mais à piloter l'ensemble.

# Rôle du serveur core
Orchestration réseau privée avec Headscale (Tailscale auto-hébergé)

 - Sécurisation des accès avec Traefik + TLS

 - GitOps, versionning, CI/CD local (Gitlab, runners, etc.)

 - Observabilité (Grafana, Prometheus, logs)

 - Interface future avec API Fyndra (Fastify, etc.)

# Matériel utilisé
Serveur : KS-C (OVH Kimsufi)
CPU     : Intel Xeon E5-1650v2 - 6c/12t - 3.5/3.9 GHz
RAM     : 32 Go ECC DDR3 1333 MHz
Disque  : 1×120 Go SSD SATA
OS      : Proxmox VE 8 (dernière version LTS)

# Objectifs techniques de cette partie
1. Préparer le Proxmox (MàJ, SSH, templates)

2. Créer un conteneur LXC Debian 12 pour Headscale

3. Poser les bases du reverse proxy

4. (Facultatif) Ajouter un DNS public si besoin