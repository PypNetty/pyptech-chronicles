---
title: "Bienvenue sur PypTech Chronicles"
description: "Blog sur Linux, Réseau, DevOps et la vie d'un tech en reconversion."
---

# PypTech Chronicles

Bienvenue sur mon blog dédié à **Linux**, **Réseau**, **DevOps** et **la reconversion dans le secteur IT**. Découvrez mes articles ci-dessous.

## Sections

- **Linux** : [Découvrez les articles](/categories/linux/)
- **Réseau** : [Articles sur le réseau](/categories/reseau/)
- **DevOps** : [Apprendre l'automatisation](/categories/devops/)
- **Reconversion** : [Mon parcours et réflexions](/categories/reconversion/)

## Articles Récents

### Articles de Reconversion

{{ range first 5 (where .Site.RegularPages "Params.categories" "intersect" (slice "reconversion")) }}

- [{{ .Title }}]({{ .RelPermalink }}) - {{ .Summary | truncate 100 }}
  {{ end }}

### Articles sur Linux

{{ range first 5 (where .Site.RegularPages "Params.categories" "intersect" (slice "linux")) }}

- [{{ .Title }}]({{ .RelPermalink }}) - {{ .Summary | truncate 100 }}
  {{ end }}

### Articles sur le Réseau

{{ range first 5 (where .Site.RegularPages "Params.categories" "intersect" (slice "reseau")) }}

- [{{ .Title }}]({{ .RelPermalink }}) - {{ .Summary | truncate 100 }}
  {{ end }}

### Articles sur DevOps

{{ range first 5 (where .Site.RegularPages "Params.categories" "intersect" (slice "devops")) }}

- [{{ .Title }}]({{ .RelPermalink }}) - {{ .Summary | truncate 100 }}
  {{ end }}

---

© {{ now.Format "2006" }} PypTech-Chronicles. Tous droits réservés.
[Politique de confidentialité](#) | [Contact](#)
