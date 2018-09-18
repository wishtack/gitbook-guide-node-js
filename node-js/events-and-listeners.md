# Events & Listeners

## Exemple avec le package IRC

```bash
yarn add irc
```

```javascript
const { Client } = require('irc');

const client = new Client('irc.freenode.net', 'myIrcBot', {
    channels: ['#wishtack']
});

client.on('error', message => console.error(`error: ${message}`));

client.on('connect', () => console.log('connected to the irc server'));

client.on('message', (from, to, message) => {
    console.log(`${from} => ${to}: ${message}`);
});

client.on('pm', (from, message) => console.log(`${from} => ME: ${message}`));
```

## `EventEmitter`

```javascript
const EventEmitter = require('events');
const eventEmitter = new EventEmitter();

/* Listen to 'greetings' events. */
eventEmitter.on('greetings', name => console.log(`Hi ${name}!`));

/* Emit 'hello' event. */
eventEmitter.emit('greetings', 'Wishtack');            
```

