# Error Management

## Convention Node.js

Si le premier paramètre est non `null` alors une erreur s'est produite et les informations de l'erreur sont dans ce paramètre.

Si le premier paramètre est `null` alors il s'agit d'un succès.

```javascript
fs.readFile('wishtack.txt', function (error, data) {

    if (error !== null) {
        /* Something went wrong. */
        return;
    }

    /* Everything is just fine. */
    ...

});

```

Si l'erreur a une solution alternative _\("retry" ou solution de backup\)_ alors gérez l'erreur immédiatement sinon il faut remonter l'erreur à l'utilisateur.

{% hint style="warning" %}
Aucune erreur ne doit être ignorée.
{% endhint %}

## Détection d'erreur avec l'objet `EventEmitter`

```javascript
const EventEmitter = require('events');

const emitter = new EventEmitter();

emitter.on('error', error => {
    /* Handle error case. */
});
```

{% hint style="danger" %}
Avec un `EventEmitter`, si l'erreur n'est pas capturée, une exception sera levée et interrompra le programme.
{% endhint %}

