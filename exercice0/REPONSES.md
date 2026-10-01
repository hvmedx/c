## Exercice 0

**Pourquoi ne versionne-t-on jamais les `.o` ni l'exécutable ?**
Ce sont des fichiers générés : on les reconstruit à tout moment à partir des sources avec le compilateur. Ils sont binaires (illisibles dans un diff) et dépendent de la machine et du compilateur (un `.o` macOS ne sert à rien sous Linux). Les versionner alourdit le dépôt, crée des conflits inutiles et risque de livrer un binaire qui ne correspond plus aux sources.
