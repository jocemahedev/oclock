# Fetch

Le **fetch** est une fonctionnalité de JavaScript permettant d'envoyer une requête HTTP à un serveur et de récupérer la réponse. Il est souvent utilisé pour récupérer des données d'une API. Voici un exemple de code :

```
fetch('<https://monapi.com/donnees>')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

```

Dans cet exemple, nous envoyons une requête à l'adresse `https://monapi.com/donnees` en utilisant la méthode `fetch`. La réponse est ensuite convertie en JSON en utilisant la méthode `json()`. Nous pouvons ensuite accéder aux données avec la variable `data`. Si une erreur se produit, elle est capturée avec la méthode `catch`.

Dans notre cas nous pouvons utiliser **fetch** pour supprimer un utilisateur. L’utilisation du fetch nous permet de ne pas être obliger de rafraichir la page pour voir le résultat.

Par exemple si on ajoute un peu de Js dans la page list des profs (dans views/teacher/list.tpl.php)

```bash
<script type="text/javascript">
  function onDelete(teacherId){
		console.log('on delete '+teacherid);
    fetch('https://correction-app.lndo.site/teachers/'+id+'/delete')
		.then(function(response) {
			if(response.status === 200){
						console.log('Success');
						console.log(response);
					}else{
						console.log('Erreur');
						console.log(response);
			}
			})
		.catch(function(error) {
			console.log('Erreur');
			console.log(error);
		});}
</script>
```

On ajoute un bouton qui exécute la fonctionJS onDelete avec le teacherId en paramètre : 

```bash
<button type="button" class="btn btn-sm btn-warning" onclick="onDelete(<?= $currentTeacher->getId()?>)">
 <span>Fetch JS</span>
 <i class="fa fa-trash-o" aria-hidden="true"></i>
</button>
```

En testant cela on peut remarquer que lorsqu’on clique sur le bouton…ça ne fonctionne pas 😅.

On panique pas on regarde la réponse et on remarque un 403 car sur la correction il y a une protection csrf. On a donc deux solutions soit on enlève le csrf et on cela nous permet de tester rapidement (A ne pas reproduire en production 😬). Dans le cas ou l’on veut mieux faire les choses il faut transmettre le csrf dans un paramètre ‘header’ du fetch voir ici comment on ajoute [https://developer.mozilla.org/fr/docs/Web/API/Fetch_API/Using_Fetch](https://developer.mozilla.org/fr/docs/Web/API/Fetch_API/Using_Fetch)

Dans notre cas on a commenté le `teacher-delete`  dans `csrf.php`.

Et donc on retestant on obtient une réponse avec status 200 qui indique que ça fonctionne et le tout sans rechargement de la page 😁.

Sauf que l’élément que l’on a delete est toujours présent sur la page (même si il n’est plus en BDD) car la page n’a pas été rafraichi 😆. Pour remédier à ça sans faire de refresh de page il faut supprimer l’élement html lorsque le **fetch** renvoie un 200.

1/ on ajout un id à l’élément `<tr>` dans `list.tpl.php`

```bash
<tr id="teacher-<?php echo $currentTeacher->getId()?>">
```

2/ on le remove en cas de status 200 avec ce bout de code

```bash
//a ajouter de le OnDelete en cas de status 200
$('#teacher-'+id).remove();
```

Et miracle ou pas,  ça fonctionne 🎉.

On a donc un delete qui marche sans refresh, par contre on ne traite pas encore le cas ou cela ne marche pas l’idéal serait d’afficher un message toujours en l’ajouter directement au DOM Html pour que ce soit visible sans refresh.