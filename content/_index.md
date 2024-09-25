---
title: "Bienvenue sur PypTech Chronicles"
description: "Blog sur Linux, Réseau, DevOps et la vie d'un tech en reconversion."
---

# PypTech Chronicles

Bienvenue sur mon blog dédié à **Linux**, **Réseau**, **DevOps** et **la reconversion dans le secteur IT**. Découvrez mes articles ci-dessous.

## Sections

- **Linux** : [Découvrez les articles](./categories/linux/)
- **Réseau** : [Articles sur le réseau](./categories/reseau/)
- **DevOps** : [Apprendre l'automatisation](./categories/devops/)
- **Reconversion** : [Mon parcours et réflexions](./categories/reconversion/)

## Articles Récents

### Articles de Reconversion

{{ range first 5 (where .Pages "Section" "posts" "Category" "Reconversion") }}

- [{{ .Title }}]({{ .RelPermalink }}) - {{ .Summary }}
  {{ end }}

### Articles sur Linux

{{ range first 5 (where .Pages "Section" "posts" "Category" "Linux") }}

- [{{ .Title }}]({{ .RelPermalink }}) - {{ .Summary }}
  {{ end }}

### Articles sur le Réseau

{{ range first 5 (where .Pages "Section" "posts" "Category" "Réseau") }}

- [{{ .Title }}]({{ .RelPermalink }}) - {{ .Summary }}
  {{ end }}

### Articles sur DevOps

{{ range first 5 (where .Pages "Section" "posts" "Category" "DevOps") }}

- [{{ .Title }}]({{ .RelPermalink }}) - {{ .Summary }}
  {{ end }}

---

© 2024 PypTech-Chronicles. Tous droits réservés.  
[Politique de confidentialité](#) | [Contact](#)
