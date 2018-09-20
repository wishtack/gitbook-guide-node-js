# WebSocket

Le protocole WebSocket RFC6455 est standardisé depuis décembre 2011 et implémenté par les navigateurs suivants : Chrome 16, Firefox 11, Internet Explorer 10, Opera 12.10 et Safari 6.

[https://tools.ietf.org/html/rfc6455](https://tools.ietf.org/html/rfc6455)

{% embed data="{\"url\":\"https://tools.ietf.org/html/rfc6455\",\"type\":\"link\",\"title\":\"The WebSocket Protocol\",\"icon\":{\"type\":\"icon\",\"url\":\"https://tools.ietf.org/images/rfc.png\",\"aspectRatio\":0}}" %}

Les WebSockets permettent d'établir une **connexion bi-directionnelle entre le client et le serveur**.

Il devient alors possible d'envoyer des messages en temps réel du client vers le serveur mais surtout du serveur vers le client en utilisant la même connexion.

A titre d'exemple, comparons la bande passante nécessaire pour une application web qui affiche les résultats temps réel d'un match de sport par **polling** puis en utilisant les **WebSockets**.

**Polling :** 1 000 000 d'utilisateurs =&gt; 1 000 000 requêtes toutes les 5 secondes =&gt; 1KB \* 1 000 000 / 5 =&gt; 200 MBPS**.**

**WebSocket :** 1 000 000 d'utilisateurs =&gt; un message serveur/client à chaque évènement _\(en moyenne, une fois toutes les 10 secondes\)_ =&gt; 50B \* 1 000 000 / 10 =&gt; 5 MBPS.

{% hint style="info" %}
Pour émettre des données du serveur au client, pensez à utiliser les **Server-Sent Events** qui s'avèrent généralement plus simple à mettre en place.

[https://developer.mozilla.org/en-US/docs/Web/API/Server-sent\_events/Using\_server-sent\_events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)
{% endhint %}

Une connexion WebSocket est établie suite au handshake HTTP suivant :

### Requête du client

```http
GET /users/123456/wishes/abcdef HTTP/1.1
Host: www.wishtack.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
Sec-WebSocket-Protocol: comments
Sec-WebSocket-Version: 13
Origin: https://www.wishtack.com
```

### Réponse du serveur

```text

HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: HSmrc0sMlYUkAGmm5OPpG2HaGWk=
Sec-WebSocket-Protocol: comments
```

## Socket.IO

[https://socket.io/](https://socket.io/)

{% embed data="{\"url\":\"https://socket.io/\",\"type\":\"link\",\"title\":\"Socket.IO\",\"description\":\"SOCKET.IO 2.0 IS HERE     FEATURING THE FASTEST AND MOST RELIABLE REAL-TIME ENGINE                            ~/Projects/tweets/index.js                                  var io = require\(\'soc\",\"icon\":{\"type\":\"icon\",\"url\":\"https://socket.io/images/favicon.png\",\"aspectRatio\":0}}" %}

Socket.IO est une couche d'abstraction des WebSockets.

En l'absence de l'implémentation de WebSockets, Socket.IO peut utiliser du polling par exemple.

Socket.IO fournit également un module pour simplifier l'implémentation des WebSockets côté serveur avec Node.js.

### Code Node.js

```javascript
const express = require('express');
const app = express();
const http = require('http');
const server = http.createServer(app);
const io = require('socket.io')(server);

/* Listen! */
app.listen(80);

/* Messaging. */
io.on('connection', (socket) => {

    socket.on('comment', (data) => {

        console.log(data);

        socket.emit('thanks', 'Thank you for your comment.');

    });

});
```

### Code Client

```javascript
const socket = io.connect('http://localhost/comment');

socket.on('connect', () => socket.emit('message', 'hi!'));

socket.on('thanks', (data) => socket.emit('message', data));
```

### Pensez à utiliser les _rooms_ pour diviser les clients en différents groupes

```javascript
io.on('connection', (socket) {

    socket.on('comment', (data) {

        socket.join(socket.handshake.url);

        socket.to(socket.handshake.url).emit('comment', data);

    });

});
```

