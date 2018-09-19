# Routing

Le _routing_ définit le **lien** entre les **URLs** d'une application et le **traitement** à effectuer pour chaque requête.

Express permet de définir le _routing_ en établissant un lien entre une méthode HTTP, un _path_ et la fonction qui sera exécutée à chaque requête.

```javascript
app.METHOD(path, callback);
```

### Exemples

```javascript
app.get('/', (req, res) => res.send('Welcome!'));

/* Activate body parser for both url-encoded and JSON data. */
const bodyParser = require('body-parser');
app.use(bodyParser.json());
app.use(bodyParser.urlencoded());

app.post('/users', (req, res) => {
    console.log(req.body.firstName);
    res.end();
});
```

### Il est possible de configurer le _routing_ avec des expressions régulières

```javascript
app.get(/^\/blogs\/(\d+)$/, (req, res) => {
    const blogId = req.params[0];
    ...
});
```

#### APIs des objets `request` et `response`

[http://expressjs.com/en/4x/api.html\#req](http://expressjs.com/en/4x/api.html#req)

{% embed data="{\"url\":\"http://expressjs.com/en/4x/api.html\#req\",\"type\":\"link\",\"title\":\"Express 4.x - API Reference\",\"icon\":{\"type\":\"icon\",\"url\":\"http://expressjs.com/images/favicon.png\",\"aspectRatio\":0}}" %}

  
[http://expressjs.com/en/4x/api.html\#res](http://expressjs.com/en/4x/api.html#res)

{% embed data="{\"url\":\"http://expressjs.com/en/4x/api.html\#res\",\"type\":\"link\",\"title\":\"Express 4.x - API Reference\",\"icon\":{\"type\":\"icon\",\"url\":\"http://expressjs.com/images/favicon.png\",\"aspectRatio\":0}}" %}

{% hint style="warning" %}
Express étant asynchrone, si aucune réponse n'est envoyée explicitement au client, la connexion sera maintenue jusqu'au timeout.
{% endhint %}

{% hint style="warning" %}
Certaines fonctions utilisent des callbacks distinctes pour gérer le cas de succès et le cas d'erreur. Si vous oubliez de gérer le cas d'erreur, on tombe dans le cas du "timeout".
{% endhint %}

