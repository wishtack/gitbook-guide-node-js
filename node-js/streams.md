# Streams

Pour simplifier l'implémentation asynchrone du traitement d'un flux de données, Node.js propose l'utilisation de la notion de **stream**.

NodeJS définit des interfaces d'implémentation de **stream** : Readable, Writable, Duplex et Transform.

[https://nodejs.org/api/stream.html\#stream\_api\_for\_stream\_implementors](https://nodejs.org/api/stream.html#stream_api_for_stream_implementors)

{% embed data="{\"url\":\"https://nodejs.org/api/stream.html\#stream\_api\_for\_stream\_implementors\",\"type\":\"link\",\"title\":\"Stream \| Node.js v10.10.0 Documentation\",\"icon\":{\"type\":\"icon\",\"url\":\"https://nodejs.org/favicon.ico\",\"aspectRatio\":0}}" %}

## NodeJS implémente quelques streams et fonctionnalités de transformation

```javascript
const crypto = require('crypto');
const fs = require('fs');
const zlib = require('zlib');

const password = new Buffer(process.env.PASS || 'password');
const encryptStream = crypto.createCipher('aes-256-cbc', password);

const gzip = zlib.createGzip();
const readStream = fs.createReadStream('secret-data.txt');
const writeStream = fs.createWriteStream('encrypted-secret-data.gz');

/* Read current file. */
readStream

    /* Encrypt data. */
    .pipe(encryptStream)

    /* Compress data. */
    .pipe(gzip)

    /* Write data to output file. */
    .pipe(writeStream)

    /* We are done. */
    .on('finish', function () {
        console.log('done');
    });
```

