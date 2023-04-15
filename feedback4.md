# Feedback 4

Le projet ne fonctionne pas. 

Il ya une erreur sur un controller Manquant (`MainController`).

En cas de blocages sur un projet le mieux est de s’aider des indication fournit par les erreurs, et d’avancer pas à pas.

Ici par exemple on remarque qu’on a deux solutions soit on ajoute le controller, soit on supprime les endroits ou on essaye de le charger. (Indice le controller est utile 🙂).

Quand on l’ajoute on a une autre erreur (signe que ça avance) avec un autre controller manquant le `CoreController`. Il faut l’ajouter aussi, d’autant plus que plusieurs de tes autres controllers `StudentsController` et `TeachersController` héritent de ces propriétés (voir le extends en haut de la Class de ces Controllers).

Concernant le code en lui même il y a plusieurs choses a revoir.

Notamment la façon d’instancier un  objet qui n’est pas bonne.

Pour instancier un objet `Teacher` il faut faire :

```bash
$teacher = new Teacher();
//et non teacher()
```

Dans le cas qui nous intéresse la méthode teachers du `TeachersController` il n’y avait pas besoin de créer un objet Teacher car la méthode findAll est static on l’utilise de la façon suivante :

```bash
$teacherList = Teacher::findAll()
```

Ensuite il faut faire attention aux lien entre le routage (dans lequel on fait référence aux fonctions du Controller) et les Vues (auquel on fournit avec le Controller les infos a afficher).

Autres remarques plus général, as-tu réussi à importer la BDD je vois que les fichiers sql sont présents dans le dossier `Utils` ce qui est inutile 🙂. Les fichiers sql contiennent des requêtes SQL qui doivent être exécutés pour créer ta base de données, ce ne sont donc pas la base de données mais permettent de l’exécuter.

J’ai vu aussi qu’il y avait un fichier composer.phar dans ton dépôt. Si composer est bien installer sur ton poste tu n’as pas besoin de se fichier, la commande ‘composer’ fonctionne t’elle bien partout sur ton poste, à tester.

**Bilan**

Beaucoup de choses ne fonctionne pas, cela peut sembler décourageant mais en faisant preuve de méthode (résoudre les erreurs pas à pas) et avec un peu plus de connaissances (Les routes, les constructeurs,..), tu pourras progresser et t’améliorer.