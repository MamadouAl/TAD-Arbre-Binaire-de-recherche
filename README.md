# TAD Arbre Binaire de recherche

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
> chercher(11) ; chercher(4) ; chercher(13).
> supprimer (1,7.4) ; insérer(5, 112); inserer(20,123); inserer(22,320); supprimer(12,1.3) ; afficher

Dans un second temps, et si toutes vos méthodes fonctionnent, vous pourrez tester cette fois
l'efficacité de vos méthode en travaillant sur des ensembles de grande taille, et comparer les
résultats avec ceux obtenus avec les listes chaînées.
Plus de détails dans le fichier de complément sur les modalités de tests.
