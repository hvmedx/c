## Exercice 4

`make` utilisé : GNU Make 3.81 (celui de macOS).

`make clean` puis `make` :

```
rm -f main.o liste.o demo
gcc -Wall -Wextra -std=c11 -g -c main.c
gcc -Wall -Wextra -std=c11 -g -c liste.c
gcc -Wall -Wextra -std=c11 -g -o demo main.o liste.o
```

Second `make`, sans rien modifier :

```
make: `demo' is up to date.
```

| Question | Réponse |
| --- | --- |
| A | `make` compare les dates de modification. `demo` est plus récent que `main.o` et `liste.o`, qui sont eux-mêmes plus récents que leurs dépendances (`main.c`, `liste.c`, `liste.h`). Aucune cible n'est plus ancienne qu'une de ses dépendances : il n'y a rien à refaire. |
| B (message exact) | Sur la commande de `demo`, **aucun message** : `make` compile `main.o` et `liste.o`, renvoie 0, mais ne crée pas `demo`. Sans tabulation, la ligne n'est plus une commande. Comme elle contient un `=` (dans `-std=c11`), `make` la lit comme une affectation de variable : `gcc -Wall -Wextra -std = c11 -g -o demo main.o liste.o` (visible avec `make -p`). La règle `demo` se retrouve sans commande. Sur une commande sans `=`, par exemple celle de `clean`, on obtient le message classique : `Makefile:11: *** missing separator.  Stop.` |
