# Feedback 3

**#2 et #3 Lister tous les profs et tous les étudiants**

Quand on clique sur le menu ça fonctionne, une liste s’affiche avec soit les profs soit les étudiants.

L’affichage du tableau est propre, en revanche le menu disparait lorsqu’on entre dans une des vues liste.

Il manque dans tes views un dossier layout pour les couches graphiques qu’on retrouve sur toutes les pages. 

Tu peux aussi ajouter des sous-vues (partials) qui sont des “morceaux de vue” qui vont être présent dans plusieurs vue (par exemple le menu que l’ont retrouvera quand un user sera connecté).

D’une manière générale il faut toujours garder en tête qu’un template html est toujours un morceau de vue et ne représente pas la page final affiché sur le navigateur mais un morceau de celle-ci. Comme souvent en informatique des outils sont là pour nous éviter de recopier toujours le même code (par exemple le code du header que l’on retrouve sur tes templates list). 

**#4 Ajout d'un prof et ajout d’un étudiant**

Ça ne fonctionne pas pourtant tu n’était pas si loin d’avoir un résultat.

Pour les profs le bouton “ajouter” redirige vers l’ajout des étudiants 😅 donc tu es redirigé vers l’ajout des étudiants, je note ça comme une erreur d’inattention 🙂.

Ce qui est plus embêtant est que tu semble avoir mélanger l’ajout des étudiants et des profs (une fonction `studentAdd` dans le controller `TeacherController`, a voir si c’est le résultat de copier/coller malheureux car tu n’arriver pas à obtenir un résultat ou si tu as vraiment pas compris la logique.

En tout cas ce qu’il faut comprendre c’est que le code d’ajout des profs et des étudiants doivent être chacun dans leur controllers et vue respectifs.

Pour l’ajout d’un étudiant ça ne fonctionne pas car tu as une erreur SQL car tu n’insert pas de valeur pour `teacher_id` ce qui est obligatoire (un étudiant doit avoir un prof). Cela aurait pu fonctionner sinon avec tes valeur hardcoder dans le formulaire mais le mieux aurait été d’avoir la liste des profs sous la main dans la vue. Pour cela il faut dans la méthode `studentAdd::StudentController` appeller la fonction qui donne la liste des profs (`Teachers::findAll()`) pour ensuite partager cette valeurs à la vue dans la fonction show comme tu l’a déjà fait avec les étudiants.

**Bilan**

Des progrès à faire avec les Views et le fonctionnement de l’architecture MVC en général, notamment les liens entre les Controllers et la Vue. Pour info j’ai  ajouté un htaccess dans le dossier public pour que ça fonctionne n’as tu pas oublié de le committer ?