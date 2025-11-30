---
title: Apache
type: docs
# prev: docs/first-page
# next: docs/docker/leaf
sidebar:
  open: true
---

### 2 types de compilation pour Apache
- statique : modules d'apache compilés statiquement avec le binaire, 
	- si un truc change, on doit tout recompiler
	- a l'avantage d'être plus rapide
-  dynamique
	-  on change uniquement les .so si on veut mettre à jour des modules 
	-  plus flexible mais moins rapide à l'exécution (doit charger les librairies dynamiquement)

## Apache best practices
Néanmoins, il est à noter que l’existence de nombreux modules Apache complexifie la configuration du serveur web. En effet, les bonnes pratiques recommandent de ne charger que les modules utiles : de nombreuses failles de sécurité affectant uniquement les modules d’Apache sont régulièrement découvertes.

**Francois Goffinet** UN CRACK !! \
https://linux.goffinet.org/services/apache-http-server/

