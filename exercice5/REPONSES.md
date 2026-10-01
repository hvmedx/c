## Exercice 5

Note : `make` 3.81 compare les dates à la seconde près. Un `touch liste.h` lancé dans la même seconde que la compilation passe inaperçu (`demo' is up to date`). Il faut attendre une seconde avant le `touch` pour observer le comportement ci-dessous.

| Étape | Ce que make recompile |
| --- | --- |
| 2, avec la dépendance | `main.o` et `liste.o`, puis l'édition de liens de `demo` (3 commandes) |
| 4, sans la dépendance | `liste.o` seulement, puis l'édition de liens de `demo`. `main.o` n'est **pas** recompilé |

| Question | Réponse |
| --- | --- |
| A | Avec la dépendance, modifier `liste.h` recompile les deux fichiers qui l'incluent. Sans elle, `make` ne sait pas que `main.c` inclut `liste.h` : il ne voit que `main.c`, qui n'a pas changé, et garde l'ancien `main.o`. `make` ne lit pas les `#include`, il ne connaît que les dépendances qu'on lui écrit. |
| B | Un exécutable incohérent. `liste.o` est recompilé avec la nouvelle structure (plus grande, champs décalés), alors que `main.o` garde l'ancienne : les deux moitiés du programme ne sont pas d'accord sur la taille ni sur la position des champs de `Maillon`. Le lien réussit quand même, sans aucun message, parce que l'éditeur de liens ne vérifie que les noms des symboles, jamais les types. Le résultat est un comportement indéfini : valeurs fausses, corruption mémoire ou plantage, selon où le champ a été ajouté. Le bug disparaît « tout seul » après un `make clean`, ce qui le rend très difficile à comprendre. |

### Le Makefile complet

Le Makefile final (règle générique `%.o: %.c liste.h`, variables `CC`, `CFLAGS`, `OBJ`) produit les mêmes trois compilations, aux options `-o main.o` / `-o liste.o` près, et un programme à la sortie identique, vérifiée avec `diff`.
