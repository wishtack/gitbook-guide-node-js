# Databases

Node.js permet d'utiliser facilement toutes sortes de _databases_ : SQL, NoSQL etc...

[https://github.com/felixge/node-mysql](https://github.com/felixge/node-mysql)

{% embed data="{\"url\":\"https://github.com/felixge/node-mysql\",\"type\":\"link\",\"title\":\"mysqljs/mysql\",\"description\":\"A pure node.js JavaScript Client implementing the MySql protocol. - mysqljs/mysql\",\"icon\":{\"type\":\"icon\",\"url\":\"https://github.com/fluidicon.png\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://avatars1.githubusercontent.com/u/18713232?s=400&v=4\",\"width\":420,\"height\":420,\"aspectRatio\":1}}" %}

[https://github.com/mongodb/node-mongodb-native](https://github.com/mongodb/node-mongodb-native)

{% embed data="{\"url\":\"https://github.com/mongodb/node-mongodb-native\",\"type\":\"link\",\"title\":\"mongodb/node-mongodb-native\",\"description\":\"Mongo DB Native NodeJS Driver. Contribute to mongodb/node-mongodb-native development by creating an account on GitHub.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://github.com/fluidicon.png\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://avatars3.githubusercontent.com/u/45120?s=400&v=4\",\"width\":200,\"height\":200,\"aspectRatio\":1}}" %}

Pour la plupart des applications, il est préférable d'utiliser une base NoSQL telle que MongoDB pour bénéficier des avantages suivants :

* L'absence de schéma statique permet de s'adapter rapidement aux nouveaux besoins.
* La _scalability_ grâce au _sharding_.
* Syntaxe simplifiée.
* Map/Reduce.
* ...

## ORM \(Object-Relational Mapping\) / ODM \(Object-Document Mapping\)

Comme dans les autres langages, il est fortement recommandé d'utiliser une couche d'abstraction pour des raisons de factorisation, simplification et sécurité.

### ORM SQL

[http://sequelizejs.com](http://sequelizejs.com)

{% embed data="{\"url\":\"http://sequelizejs.com\",\"type\":\"link\",\"title\":\"Manual \|  Sequelize \| The node.js ORM for PostgreSQL, MySQL, SQLite and MSSQL\"}" %}

```javascript
const Sequelize = require('sequelize');
const sequelize = new Sequelize('database', 'username', 'password');

const User = sequelize.define('User', {
  firstName: Sequelize.STRING,
  lastName: Sequelize.STRING
});

const main = async () => {

    await sequelize.sync();
    
    const userModel = await User.create({firstName: 'Foo', lastName: 'BAR'});

    const user = user.get({plain: true})

};

main();
```

### ODM MongoDB

[http://mongoosejs.com/](http://mongoosejs.com/)

{% embed data="{\"url\":\"http://mongoosejs.com/\",\"type\":\"link\",\"title\":\"Mongoose ODM v5.2.16\"}" %}

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/test');

const User = mongoose.model('User', {
    firstName: String,
    lastName: String
});

const foo = new User({
    firstName: 'Foo',
    lastName: 'BAR'
});

await foo.save();
```



