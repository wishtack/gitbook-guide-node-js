# Modules

Un **module Node.js** est **une fonctionnalité** regroupée dans un fichier JavaScript _\(ou parfois plusieurs grâce aux fichiers `index.js`\)_ dans le but d'être réutilisée à différents endroits d'une application.

Chaque **module Node.js** dispose de son propre contexte et ne peut donc interférer avec d'autres modules ou polluer le **global scope**.

## Utilisation d'un module

### Importation d'un module standard

```javascript
const http = require('http');
const dns = require('dns');
```

### Importation d'un module provenant d'un package externe

Il faut tout d'abord installer le package associé...

```bash
yarn add express # ou npm install --save express
```

... puis importer le module tel un module natif.

```javascript
const exporess = require('express');
```

## Modules "custom"

### Création d'un module simple \(un seul fichier\)

```javascript
const settings = {
    hostname: 'www.wishtack.com',
    coolMode: true
};

module.exports = settings;
```

### Importation du module

Les modules faisant partie de l'application _\(hors modules natifs ou dépendances\)_ doivent être importés par chemin relatif.

```javascript
const settings = require('./settings');

console.log(settings.coolMode); // true
```

{% hint style="info" %}
Une fois le support des ES Modules \([https://nodejs.org/api/esm.html](https://nodejs.org/api/esm.html)\) stabilisé, `import` remplacera `require`.
{% endhint %}



