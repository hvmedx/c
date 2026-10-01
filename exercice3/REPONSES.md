## Exercice 3

Compilateur : `gcc` sous macOS, qui est en réalité Apple clang 21 (messages de clang et de l'éditeur de liens `ld` d'Apple).

| Cas | Premier message exact | Compilation ou lien |
| --- | --- | --- |
| 1 | `Undefined symbols for architecture arm64: "_liste_afficher", referenced from: _main in main.o` (puis `ld: symbol(s) not found for architecture arm64`) | Lien |
| 2 | `main.c:5:5: error: use of undeclared identifier 'Maillon'` | Compilation |
| 3 | `./liste.h:4:16: error: redefinition of 'Maillon'` | Compilation |

| Question | Réponse |
| --- | --- |
| 1 | Le cas 1. Le message ne cite aucun fichier source ni numéro de ligne, seulement des symboles (`_liste_afficher`) et un fichier objet (`main.o`). Il vient de `ld`, qui le dit lui-même : `ld: symbol(s) not found` et `linker command failed`. `main.c` s'est compilé sans erreur : c'est au moment d'assembler les `.o` qu'il manque le code des fonctions. |
| 2 | Le premier : `use of undeclared identifier 'Maillon'`. Les 12 autres en découlent : comme `Maillon` est inconnu, la déclaration de `liste` échoue, donc chaque usage de `liste` devient « undeclared », et chaque fonction du module est « undeclared » puisque son prototype venait du même `.h` oublié. La cause est unique : il manque `#include "liste.h"`. |
| 3 | Dès qu'un même `.h` est inclus deux fois dans une même unité de compilation, le plus souvent indirectement : par exemple un second module `pile.h` qui inclut `liste.h` (parce qu'il utilise `Maillon`), et un `main.c` qui inclut à la fois `pile.h` et `liste.h`. Le contenu de `liste.h` est alors recopié deux fois et `Maillon` est défini deux fois. Ici on l'a provoqué artificiellement en écrivant deux fois la même ligne `#include`. |
