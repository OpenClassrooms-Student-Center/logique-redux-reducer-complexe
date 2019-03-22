Bienvenue !

Dans la continuité de l'écriture des `actions`, nous allons maintenant coder votre premier `reducer`. Ne vous inquiétez pas, l'exercice est accompagné d'aide régulière. La prochaine et dernière étape sera le dispatch des `actions` !

Afin de vous faciliter la tâche, nous avons pris soin de vous créer le fichier `./reducers/todos.js` et d'importer les actions nécessaires à l'écriture du reducer pour les todos.

1. Préparer la structure du `reducer` :

Dans le fichier `/src/reducers/todos.js` :

## Étape 1 :

Commencez par créer une constante nommée `initialState` qui décrira l'état initial de `todos` : il s'agira d'un tableau d'objet qui aura pour clés respectives `text`, `completed` et `id` et pour valeurs `'Apprendre Redux'`, `false`, `0`.

** Exemple :**
```javascript
const initialState = [{
	text: 'Je dois créer mon state initial',
	completed: false,
	id: 10
}]
```

## Étape 2 :

Créez une fonction nommée `todos` qui prendra deux arguments :
- `state` : qui aura comme valeur par défaut `initialState`
- `action` : qui n'aura aucune valeur par défaut

**Important :** N'oubliez pas d'exporter la fonction par défaut

```javascript
export default function reducerName (state = initialState, action) {
	// Le code du reducer
}
```

## Étape 3 :

Dans la fonction `todos`, créez un `switch` sur `action.type` puis préparez la structure du `switch` en créant chaque `case` pour chacune des valeurs importées depuis `ActionTypes` que vous laisserez vide.

⚠ **Attention :** N'oubliez pas d'ajouter `default` dans votre `switch` qui retournera simplement le `state`.

**Exemple :**
```javascript
import { ADD_USER, DELETE_USER, EDIT_USER } from '../constants/ActionTypes'

export default function users (state = {}, action) {
	switch (action.type) {
		case ADD_USER:
			// ...
		case DELETE_USER:
			// ...
		case EDIT_USER:
			// ...
		default:
			return state
	}
}
```

> L'essentiel du travail consistera à décrire chaque `case` du `switch`. Étant donné les similarités, nous vous les avons groupés par 2 : on vous fera copier-coller un `case`, on vous l'expliquera, puis ce sera à vous de coder le `case` très similaire. Allons-y !

1. Avez-vous décrit le `case ADD_TODO` ?

Dans `case ADD_TODO`, copiez-collez le bloc de code ci-dessous :

```javascript
return [
	...state, // Spread operator
	{
		id: state.reduce((maxId, todo) => Math.max(todo.id, maxId), -1) + 1,
		completed: false,
		text: action.text,
	},
]
```

Ce code utilise le **spread operator** qui va reprendre le `state` actuel auquel on rajoute un nouvel élément à la liste.

2. Avez-vous décrit le `case CLEAR_COMPLETED` ?

Dans `case CLEAR_COMPLETED`, copiez-collez le bloc ci-dessous :

```javascript
return state.filter((todo) => todo.completed === false)
```

Ce code utilise la méthode `filter` qui retourne un nouveau tableau contenant tous les éléments du tableau d'origine. Ceux-ci remplissent une condition déterminée par la fonction `callback`. Dans le code ci-dessus, nous retournerons seulement les todos remplissant la condition `completed` égale `false`.

3. Avez-vous décrit le `case DELETE_TODO` ?

Dans `case DELETE_TODO`, retournez simplement un nouveau tableau en utilisant la méthode `filter` utilisée précédement. Pour ce faire, écrivez une fonction qui retourne toutes les todos, sauf celle où l'`id` coïncide avec l'`id` de l'action.

**Exemple :**
```javascript
return state.filter((user) => user.id !== action.id)
```

4. Avez-vous décrit le `case EDIT_TODO` ?

Dans le `case EDIT_TODO`, copiez-collez le bloc de code ci-dessous :

```javascript
return state.map((todo) => {
	return todo.id === action.id ? {
		...todo, // Spread operator
		text: action.text,
	} : todo
})
```

Ce code, de la même manière que pour `ADD_TODO`, utilise un **spread operator**. Il utilise également un fonction ternaire afin d'éditer uniquement la todo correspondant à l'`id`.

**Exemple de fonction ternaire :**
```javascript
return user.year >= 18 ? "Vous êtes majeur" : "Vous êtes mineur"
```

5. Avez-vous décrit le `case COMPLETE_TODO` ?

Écrivez le `case COMPLETE_TODO`, en utilisant la méthode `map` et une fonction ternaire comme nous venons de le voir avec `EDIT_TODO`. La seule différence est que nous allons éditer la clé `completed` en donnant comme valeur l'inverse de `todo.completed`.

6. Avez-vous décrit le `case COMPLETE_ALL_TODOS` ?

Dans `case COMPLETE_ALL_TODOS`, copiez-collez le bloc de code ci-dessous. Il ne présente aucune difficulté particulière, mais prenez le temps d'essayer de comprendre ce code si besoin :

```javascript
case COMPLETE_ALL_TODOS: {
	const areAllMarked = state.every((todo) => todo.completed)

	return state.map((todo) => ({
		...todo,
		completed: !areAllMarked,
	}))
}
```

Nous vous invitons à lire la documentation MDN concernant la méthode [`every`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/every) si vous ne la connaissez pas.

**FÉLICITATIONS !** Vous êtes arrivez à bout du plus long des exercices de ce cours 😉