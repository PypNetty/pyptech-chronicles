---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
type: "articles"
layout: "single"
categories: ["Linux", "Réseau", "DevOps", "Reconversion Tech"]
tags: ["Introduction", "Guide", "Linux", "Réseaux", "DevOps"]
description: "Article sur {{ replace .Name "-" " " | title }} dans le cadre de PypTech Chronicles"
cover: "" # optionnel : chemin vers une image d’illustration
---
