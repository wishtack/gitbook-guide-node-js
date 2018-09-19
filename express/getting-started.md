# Getting Started

Express est un framework web Node.js performant et **minimaliste**, accompagné d'un large écosystème.

Express fournit tous les outils pour l'implémentation d'applications web et de Restful APIs.

Express fait parti de la stack web **MEAN** _**\(Mongo/Express/Angular/Node\)**_ actuellement très répandue.

{% hint style="info" %}
Comme indiqué précédemment concernant Node.js, Express nécessite une logique d'implémentation asynchrone. En fonction de vos besoins, il peut être plus judicieux dans certains cas d'utiliser un framework web Python avec [gevent](http://www.gevent.org/) pour implémenter un serveur web asynchrone avec une logique d'implémentation synchrone. 🤭
{% endhint %}

### Installation

```bash
yarn add express
```

### Utilisation

```javascript
const express = require('express');
const app = express();

/* Routing. */
app.get('/', (req, res) => res.send('Welcome to Wishtack!'));

/* Run server and listen on port 3000. */
const server = app.listen(3000, () => {

    const host = server.address().address;
    const port = server.address().port;

    console.log(`App listening on http://${host}:${port}`);
    
});
```

Il suffit ensuite de lancer l'application :

```bash
node app.js
```

