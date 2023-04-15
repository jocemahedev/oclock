# Feedback 1

**#2 Lister tous les profs**

Fonctionnellement ça marche bien.

L’affichage est propre.

**Le code**

Dans teacher::TeacherController findAll est une méthode Static et doit donc être appelée de façon statique avec les ::.

il faut donc remplacer

```bash
$newteacher = new Teacher();
$teacher = $newteacher->findAll();

//PAR

Teacher::findAll()
```

Une méthode static rend le même résultat sur tout les objets de la même class (ici peu importe quel Instance de Teacher est instancier le résultat de findAll sera le même)

**#3 Lister tous les étudiants**

Fonctionnellement c’est good et visuellement c’est propre 👏

**Le code**

Même remarque pour l’exemple précédent avec les Teachers 🙂

**#4 Ajout d'un prof**

Fonctionnellement l’ajout fonctionne bien.

Quelques remarques quand même :

Tu aurais pu garder les infos dans le formulaire quand la validation du formulaire ne passe pas pour éviter de tout réécrire.

Tu testes la validité de la variable $_POST dans teacherAddPost::TeacherController() mais tu utilise INPUT_POST, cela fonctionne mais cela n’aide pas à rendre le code clair.

Dans le if de la même fonction tu testes avec isset et !empty

```bash
if (isset($_POST) && !empty($_POST)) 
//le !empty est suffisant
```

**#5 Ajout d'un étudiant**

Ça fonctionne comme précédemment. On peut observer que le code à été réutiliser 😉, c’est une bonne pratique de dev. L’étape suivante du dev étant de factoriser ce code pour ne pas simplement le copier 🙂 (DRY).

**#6 Restreindre l'accès aux utilisateurs**

Fonctionnellement ça marche (vérification que le user existe, vérification de password)  mais un utilisateur désactiver peux se connecter.

Même remarque que précédemment avec les isset et !empty sur les $_POST.

**#7 Mettre en place les permissions**

Les permissions sont gérées à un détail près 😬, le rôle user n’a pas la permission de voir la liste des profs. Le rôle n’est pas présent dans le tableau $acl du CoreController.

BONUS:

**Validation des données**

La validation de la donnée ‘status’ invalide aurait pu être mieux testé (un statut = 3 est-il valide ?)

Sinon à part ça c’est bon !

**Mise à jour d'un prof et Mise à jour d'un étudiant**

Ça ne fonctionne pas pourtant la mécanique est pas loin d’être bonne.

Dans la view dans le formulaire la propriété action redirige vers une route qui n’existe pas (d’où une erreur 404). En effet la route d’update doit posséder un id (l’id du teacher à modifier). En ajoutant l’id dans la propriété action cela fonctionne.

```bash
<form action="<?= $router->generate('teacher_update_post'), [ 'teacherid' => $teacher->getId() ]?>" method="POST" class="mt-5">
```

Même souci pour les étudiants.

**Suppression d'un prof et d’un étudiant**

C’est Good 👌

**Bilan :**

Très bon travail dans l’ensemble, par contre j’ai dû ajouter un htaccess dans le dossier public pour que ça fonctionne n’as tu pas oublié de le committer ?