# TAD Arbre Binaire de recherche
# `Partie 1`

:computer: L'objectif est d'implémenter le type abstrait dictionnaire à l'aide des arbres binaires de recherche.
On prendra comme éléments les mêmes que pour le TP d’AP4 (clé entière + valeur réelle). On
supposera que chaque élément de l’ensemble a une clé distincte.
Les principales méthodes à implémenter sont :
 * **recherche** : retourne la position d'un élément à partir de sa clé, s'il existe dans le dictionnaire.
               Sinon retourne NULL
* **insertion** : insère un élément dans le dictionnaire
* **afficher** : affiche tous les éléments du dictionnaire, dans l’ordre croissant des clés.

Dans un second temps, vous implémenterez la méthode **suppression**, qui retire du dictionnaire un
élément passé en paramètre. L’utilisation de méthodes intermédiaires est évidemment permise.

Vous pouvez tester vos méthodes sur l'exemple suivant.
insertion des éléments successifs :
> (12,1.3) ; (25,2.1) ; (7,3.6) ; (9,4.3) ; (11,5.2) ; (4,6.8) ; (1,7.4);
> afficher;
> 
> chercher(11) ; 
> 
> chercher(4) ; 
> 
> chercher(13);
> 
> supprimer (1,7.4) ;
> 
>  insérer(5, 112); 
>  
>  inserer(20,123); 
>  
>  inserer(22,320); 
>  
>  supprimer(12,1.3) ; 
>  
>  afficher ;

Dans un second temps, et si toutes vos méthodes fonctionnent, vous pourrez tester cette fois
l'efficacité de vos méthode en travaillant sur des ensembles de grande taille, et comparer les
résultats avec ceux obtenus avec les listes chaînées.
# `Partie 2`

# Comment tester l’efficacité pratique des méthodes ajout et suppression ?
**Préambule :** comme pour le tri, les temps d’exécution sont très faibles pour de petites tailles. On va
donc travailler sur de grands ensembles de données, ce qui signifie soit obtenir des données réelles,
soit les construire grâce à la génération aléatoire. C’est ce que l’on va faire ici. Et on va mesurer des
temps de calcul pour un grand nombre d’opérations simples.

**A NOTER :** dans ce qui suit, les tailles sont données à titre indicatif. En effet les durées d’exécution
peuvent beaucoup varier en fonction des caractéristiques de votre machine.
Si vous n’avez pas implémenté suppression, vous pouvez quand même tester pour ajout.

**Les étapes du test.**
## 1- Construction d’un ensemble de 10000 éléments par génération aléatoire.
Vous prendrez les clés entre 0 et 1000000 (1 million). Vous pouvez utiliser une méthode de
génération aléatoire issue du TP sur la complexité des tris, pour stocker les éléments dans un
premier temps dans un tableau d’éléments.
Note : de la sorte, il y aura peu de doublons, c’est à dire d’éléments de même clé (l’espérance du
nombre de doublons dans ce cas est proche de 50, ce que vous pouvez vérifier assez facilement en
supposant l’indépendance des tirages aléatoires).

## 2- Construction d’un tableau ASUPPRIMER de 1000 :
Conserver dans un second tableau nommé **ASUPPRIMER** 1000 de ces éléments (ils seront
supprimés plus tard) , choisis ALEATOIREMENT parmi les 10000. Par exemple, parcourir le
premier tableau et recopier l’élément courant dans le second tableau avec une probabilité de 0.15
(légèrement supérieur à 0.1 pour être presque sûr d’en avoir assez). S’arrêter quand le second
tableau est rempli. Vous pouvez le faire même si l’insertion est au fur et a mesure, en faisant le
tirage après l’insertion.

## 3- Construction de l’ABR par insertions successives.
Prise en compte des doublons. 4 solutions sont possibles.
Sol1 : on les élimine avant. le plus efficace consiste à faire un tri puis retirer les doublons.
Problème, ensuite on insére les éléments dans l’ordre trié, ce qui paradoxalement est très mauvais
pour l’ABR.
**Sol2 :** Quand on compare deux éléments, on fait une double comparaison, d’abord sur la clé puis
sur la valeur. C’est un peu lourd et pas demandé (et pas sûr à 100%).
**Sol3 :** Au moment de l’insertion, si on se rend compte qu’un élément de même clé est présent, on
arrête l’insertion. **Le plus simple est de modifier légèrement la méthode d’ajout** : elle peut rendre
un booléen qui sera faux si l’insertion ne peut se faire car on a trouvé un élément de même clé.
**Sol4** : Lors de l’insertion, en cas d’égalité des clés on met l’élément à droite. On a donc un ABR qui
peut contenir des éléments de même clé. La conséquence, c’est que si l’on fait une recherche par clé
on s’arrête au premier élément trouvé. Ceci implique un problème pour supprimer : On s’arrête sur
un nœud qui n’est pas le bon. Et cela ne correspond pas à notre définition d’un dictionnaire : les clés
sont toutes distinctes.

**On vous propose de choisir la solution 3.** Attention, cela veut dire qu’un élément dans le tableau
ASUPPRIMER peut ne plus être dans l’ABR. Là encore, le plus simple est de modifier suppression
pour qu’elle rende un booléen faux si l’élément n’est pas dans l’arbre.

**Calculez la hauteur** de l’ABR obtenu. (une petite modification à la méthode affiche permet de la
calculer assez facilement).
## Mesure des temps d’exécution des opérations
**Objectif :** calculer la durée d’exécution moyenne des opérations ajout et suppression. Pour cela, on
doit partir d’un ensemble dont on connaît la taille, ici environ 10000. Si on ajoute ou supprime 1000
éléments, cela ne modifiera pas l’ordre de grandeur de cette taille. On va donc faire le test en deux
étapes. On suppose l’ABR construit avec l’ajout des au plus 10000 éléments
1. Effectuer 1000 insertions supplémentaires, toujours aléatoirement, et toujours avec votre
méthode ajout modifiée pour ne pas ajouter de doublons.
2. Supprimer les 1000 éléments conservés dans le tableau ASUPPRIMER.

**Note :** On doit vraiment choisir aléatoirement les éléments à supprimer. En effet si on ne supprime
que les éléments que l’on vient d’insérer, on a un biais : on supprime essentiellement des feuilles de
l’arbre.

**Analyse :** Conserver les temps d’exécution pour chaque étape. En déduire le temps moyen pour une
insertion, pour une suppression, dans un ensemble d’environ 10000 éléments stockés dans un ABR.

Faites la même chose en remplaçant l’ABR par une *liste chaînée*. Vous utiliserez la classe créée
pour le TP1. Soyez attentifs à utiliser les mêmes données.
Comparez les résultats obtenus. Sont ils cohérents avec la hauteur de l’arbre et la longueur de la
liste chaînée ?
