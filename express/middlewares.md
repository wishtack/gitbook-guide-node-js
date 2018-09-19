# Middlewares

Comme la plupart des frameworks web, Express permet d'utiliser des middlewares tiers ou implémenter des middlewares personnalisés.

## Rôle des middlewares

Les middlewares permettent :

* D'exécuter du code à chaque requête.
* Modifier la requête et/ou la réponse.
* Interrompre la requête.
* Appeler le middleware suivant ou interrompre la chaîne de middlewares.

## Types de middlewares

Il existe plusieurs types de middlewares :

### Application-level

Le middleware est appliqué à l'ensemble des requêtes avec la méthode `app.use` ou sur un type de requêtes en particulier avec les méthode `app.get` ou `app.post` etc... ou encore sur une URL en particulier :

```javascript
app.get('/users/:userId', (req, res, next) => {
    console.log(req.params.userId);
    next();
});
```

### Router-level

Ce middleware fonctionne similairement à l' application-level mais ne s'applique qu'au router en question et donc une partie des URLs.

### Error-handling

Ce middleware permet de capturer uniquement les erreurs. Il s'implémente en ajoutant simplement le paramètre `err` à la fonction du middleware.

```javascript
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Shit! Something went wrong!');
});
```

### Built-in

Express fournit des middlewares natifs comme `express.static` pour servir les fichiers statiques.

Le middleware `express.static` permet de définir les ressources statiques distribuées par l'application.

```javascript
app.use('/assets', express.static('public'));
```

{% hint style="info" %}
Il reste préférable d'utiliser un CDN _\(Content Delivery Network\)_ pour servir des ressources statiques ou encore mieux : Firebase Hosting [https://firebase.google.com/docs/hosting/](https://firebase.google.com/docs/hosting/), AWS Cloudfront + S3, Netlify [https://www.netlify.com/](https://www.netlify.com/)...
{% endhint %}

### Third-party

Tous les middlewares disponibles sur NPM**.**

