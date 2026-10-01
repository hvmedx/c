## Exercice 2

Commandes :

```bash
gcc -Wall -Wextra -c main.c
gcc -Wall -Wextra -c liste.c
gcc -o demo main.o liste.o
./demo
```

Sortie du programme :

```
liste     : 50 -> 40 -> 30 -> 20 -> 10 -> NULL
longueur  : 5
contient 30 : oui
liberee
```

| Question | Réponse |
| --- | --- |
| A | Deux : `main.o` et `liste.o`, un par fichier `.c` compilé. Il n'y a pas de `liste.h.o` : un `.h` n'est jamais compilé seul. Le préprocesseur recopie son contenu dans chaque `.c` qui l'inclut (`#include`), et il est compilé dans `main.o` et dans `liste.o`. Il ne contient d'ailleurs que des déclarations, donc aucun code à produire. |
| B | Elle recompile tout à chaque fois, et ne garde aucun `.o`. Avec les deux étapes, si on ne modifie que `main.c`, on ne recompile que `main.c` et on réutilise `liste.o` tel quel. Sur trois fichiers c'est négligeable, sur un projet de centaines de fichiers c'est la différence entre quelques secondes et plusieurs minutes. C'est exactement ce que `make` automatisera. |
