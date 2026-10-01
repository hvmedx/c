## Exercice 1

| Question | Réponse |
| --- | --- |
| A | `main.c` déclare des `Maillon *`, et les fonctions du module prennent et renvoient ce type. Le compilateur doit connaître le type quand il compile `main.c`, et il ne voit que ce que `main.c` inclut, donc le `.h`. S'il était dans `liste.c`, `main.c` ne le connaîtrait pas : erreur `unknown type name 'Maillon'`. |
| B | Pour que le compilateur vérifie que les définitions de `liste.c` correspondent aux déclarations du `.h` (un type de retour ou un paramètre différent donne une erreur `conflicting types`). Il en a aussi besoin pour connaître la définition de `Maillon`, que `liste.c` utilise. |
