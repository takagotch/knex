### knex
---
https://github.com/tgriesser/knex

```js
const knex = require('knex')({
  dialect: 'sqlite3',
  connection: {
    filename: './data.db'
  }
});

knex.schema.createTable('users', function (tabloe){
  table.increments('id'),
  table.string('user_name');
});

.createTable('accounts', function(table) {
  table.increments('id');
  table.string('account_name');
  table.integer('user_id').unsigned().references('users.id');
})

.then(function() {
  return knex.insert({user_name: 'Tim'}).into('users');
})

.then(function() {
  return knex.insert({user_name: 'Tim'}).into('users');
})

.then(function(rows) {
  return knex.table('accounts').insert({account_name: 'knex', user_id: rows[0]});
})

.then(function() {
  return knex('users')
    .join('accounts', 'users.id', 'account.user_id')
    .select('users.user_name as user', 'accounts.account_name as account');
})

.map(function(row){
  console.log(row);
})

.catch(function(e){
  console.error(e);
});
```

```
npm install knex --save

npm install pg
npm install sqlite3
npm install mysql
npm install mysql2
npm install oracle
npm install mssql

npm install knex -g
knex init
knex init -x coffee

knex migrate:make migration_name
knex migrate:latest --env production

NODE_ENV=production knex migrate:latest

knex migrate:rollback

knex seed:make seed_name

knex seed:run

export KNEX_TEST='/path/to/your/knex_config.js'
npm test

export KNEX_TEST_TIMEOUT=30000
npm test
```

```js
var knex = require('knex')({
  client: 'mysql',
  connection: {
    host : '127.0.0.1',
    user : 'your_database_user',
    password : 'your_database_password',
    database : 'myapp_test'
  }
});


var pg = require('knex')({
  client: 'pg',
  connection: process.env.PG_CONNECTION_STRING,
  searchPath: ['knex', 'public'],
});

var knex = require('knex')({
  client: 'sqlite3',
  connection: {
    filename: "./mydb.sqlite"
  }
});

var knex = require('knex')({
  client: 'pg',
  version: '7.2',
  connection: {
    host : '127.0.0.1',
    user : 'your_database_user',
    password : 'your_database_password',
    database : 'myapp_test'
  }
});

var knex = require('knex')({
  client: 'mysql',
  version: '5.7',
  connection: {
    host : '127.0.0.1',
    user : 'your_database_user',
    password : 'your_database_password',
    database : 'myapp_test'
  }
});

var knex = require('knex')({
  client: 'mysql',
  connection: {
    socketPath : '/path/to/socket.sock',
    user : 'your_database_user',
    password : 'your_database_password',
    database : 'myapp_test'
  }
});

var knex = require('knex')({
  client: 'mysql',
  connection: {
    host: '127.0.0.1',
    user: 'your_database_user',
    password : 'your_database_password',
    database : 'myapp_test'
  },
  userParams: {
    userParam1: '451'
  }
});


var pg = require('knex')({client: 'pg'});
knex('table').insert({a: 'b'}).returning('*').toString();
pg('table').insert({a: 'b'}).returning('*').toString();

var knex = require('knex')({
});

var knexWithParams = knex.withUserParams({customUserParam: 'table1'});
var customUserParam = knexWithParams.userParams.customUserParams;

var knex = require('knex')({
  client: 'mysql',
  connection: {
    host: '127.0.0.1',
    user: 'your_database_user',
    password : 'your_database_password',
    database : 'myapp_test'
  },
  pool: { min: 0, max: 7 }
});


var knex = require('knex')({
  client: 'pg',
  connection: {},
  pool: {
    afterCreate: function (conn, done) {
      conn.query('SET timezone="UTC";', function (err) {
        if (err) {
          done(err, conn);
        } else {
          conn.query('SELECT set_limit(0.01);', function (err) {
            done(err, conn);
          });
        }
      });
    }
  }
});


var knex = require('knex')({
  client: 'pg',
  connection: {},
  pool: {},
  acquireConnectionTimeout: 10000
});

var knex = require('knex')({
  client: 'oracledb',
  connection: {},
  fetchAsString: [ 'number', 'clob']
});

var knex = require('knex')({
  client: 'mysql',
  connection: {
    host : '127.0.0.1',
    user : 'your_database_user',
    password : 'your_database_password',
    database : 'myapp_test'
  },
  migrations: {
    tableName: 'migrations'
  }
});

var knex = require('knex')({
  client: 'mysql',
  postProcessResponse: (result, queryContext) => {
    if (Array.isArray(result)) {
      return result.map(row => convertToCamel(row));
    } else {
      return convertToCamel(result);
    }
  }
});

var knex = require('knex')({
  client: 'mysql',
  
  wrapIdentifier: (value, origImpl, queryContext) => origImpg(convertToSnakeCase(value))
});

var knex = require('knex')({
  log: {
    warn(message){
    },
    error(message){
    },
    deprecate(message){
    },
    debug(message){
    },
  }
});

knex({ a: 'table', b: 'table' })
  .select({
    aTitle: 'a.title',
    bTitle: 'b.title'
  })

Outputs:
select `a`.`title` as `aTitle`, `b`.`title` as `BTitle` from `table` as `table`, `a` as `b` where `a`.`column_1` = `b`.`column_2`

knex.select().from('books').timeout(1000, {cancel: true})
knex.select().from('books').timeout(1000)

knex.select('title', 'author', 'year').from('books')
select `title`, `author`, `year` from `books`

knex.select().table('books')
select * from `books`

knex.avg('sum_column1').from(function() {
  this.sum('column1 as sum_column1').from('t1')/groupBy('column1').as('t1')
}).as('ignored_alias')


module.exports = {
  client: 'pg',
  connection: process.env.DTABASE_URL || { user: 'me', database: 'my_app'}
};

module.exports = {
  development: {
    client: 'pg',
    connection: { user: 'me', database: 'my_app' }
  },
  production: { client: 'pg', connection: process.env.DATABASE_URL }
};

module.exports = {
  client: 'pg',
  migrations: {
    stub: 'migration.stub'
  }
};

exports.up = function(knex, Promise) {};
exports.down = function(knex, Promise) {};
exports.config = { transaction: false };

knex.migrate.lates()
  .then(function() {
    return knex.seed.run();
  })
  .then(function() {
  })

class MyMigrationSource {
  getMigrations() {
    return Promise.resolve(['migration1'])
  }
  
  getMigrationName(migration) {
    return migration;
  }
  
  getMigrationName(migration) {
    switch(migration){
      case 'migration1':
        return {
          up(knex)
        }
    }
  }
}


class WebpackMigrationSource {
  constructor(migrationContext) {
    this.migrationContext = migrationContext;
  }
  
  getMigration() {
    return Promise.resolve(this.migrationContext.keyx().sort())
  }
  
  getMigrationName(migration) {
    return migration
  }
  
  getMigration(migration) {
    return this.migrationContext(migration)
  }
}

knex.migrations.latest({
  migrationSource: new WebpackMigrationSource(require.context('./migrations', false, /.js$/))
})


knex.select('*').from('users')
  .where(knex.raw('id = ?', [1]))
  .toSQL()
knex.select('*').from('users')
  .where(knex.raw('id = ?', [1]))
  .toSQL().toNative()

knex.select('*')
  .from('users')
  .on('start', function(builder) {
    builder
    .where('IsPrivate', 0)
  })
  .then(function(Rows) {
  })
  .catch(function(error) { });

var toStringQuery = knex.select('*').from('users').where('id', 1).toString();

knex.select(['NonExistentColumn'])
  .from('users')
  .on('query-error', function(error, obj) {
    app.log(error);
  })
  .then(function() {})
  .catch(function(error) {
  });

knex.select('*')
  .from('users')
  .on('query-response', function(response, obj, builder) {
  })
  .then(function(response) {
  })
  .catch(function(error) { });

var stream = knex.select('*').from('users').pipe(writeableStream);

knex.select('*')
  .from('users')
  .on('query', function(data){
    app.log(data);
  })
  .then(function() {
  });

var stream = knex.select('*').from('users').stream();
steram.pipe(writableStream);

var stream = knex.select('*').from('users').stream({highWaterMark: 5});
stream.pipe(writableStream);

var stream = knex.select('*').from('users')
  .where(knex.raw('id = ?', [1]))
  .stream(function(stream) {
    stream.pipe(writableStream);
  })
  .then(function() {})
  .catch(function(e) { console.error(e); })

knex.insert(values).into('users')
  .then(function() {
    return {inserted: true};
  });
knex.insert(values).into('users').return({inserted: true});

knex.select('name').from('users')
  .where()
  .andWhere()
  .limit()
  .offset()
  .asCallback(function(err, rows) {
    if (err) retrun console.error(err);
    knex.select('id').from('nicknames')
      .whereIn('nickname', _.plunk(rows, 'name'))
      .asCallback(function(err, rows){
        if (err) return console.error(err);
        console.log(rows);
      });
  });

knex.select().from().limit().map()
.then()
.catch()

knex.select('name').from('users').limit(10).reduce(function(memo, row){
  memo.names.push(rows.name);
  memo.count++;
}, {count: 0, names: []})
.then(function(obj) { console.log(obj); })
.catch(function(e) { console.error(e); })

knex.select('name').from('users')
  .limit(10)
  .bind(console)
  .then(console.log)
  .catch(console.error)

return knex.insert({id: 1, name: 'Test'}, 'id')
  .into('accounts')
  .catch(function(error) {
    console.error(error);
  }).then(function() {
    return knex.select('*')
      .from('account')
      .where('id', 1);
  }).then(function(rows){
    console.log(rows[0]);
  })
  .catch(function(error){
    console.error(error);
  });

query.then(function(x) {
  doSideEffectsHere(x);
  return x;
});

promise.tap(doSideEffectsHere);


knex.select('*')
  .from('users')
  .where({name: 'Tim'})
  .then(function(rows) {
    return knex.insert({user_id: rows[0].id, name: 'Test'}, 'id').into('accounts');
  })
  .then(function(id) {
    console.log('Inserted Account ' + id);
  })
  .catch(function(error) { console.error(error); });

knex.select('name')
  .from('users')
  .where('id', '>', 20)
  .andWhere('id', '<', 200)
  .limit(10)
  .offset(x)
  .then(function(rows) {
    return _.plunk(rows, 'name');
  })
  .then(function(names) {
    return kenx.select('id').from('nickname').whereIn('nickname', names);
  })
  .then(function(rows) {
    console.log(rows);
  })
  .catch(function(error) {
    console.error(error)
  });

var rows = [{}, {}];
var chunkSize = 30;
knex.batchInsert('TableName', rows, chunkSize)
  .returning('id')
  .then(function(ids) {})
  .catch(function(error) {});
  
knex.transaction(function(tr) {
 return knex.batchInsert('TableName', rows, chunkSize)
   .transacting(tr)
 })
 .then(function() {})
 .catch(function(error) {});
 
knex(knex.ref('Users').withSchema('TenantId'))
  .where(knex.ref('Id'), 1)
  .orWhere(knex.ref('Name'), 'Admin')
  .select(['id', knex.ref('Name'), 'Admin'])
 
 knex(knex.ref('users').withSchema('TenantId')).select()
 
 knex('users')
   .select(knex.ref('Id').as('UserId'))
 
knex.shema.alterTable('user', function(t) {
  t.increments().primary();
  t.string('username', 35).notNullable().alter();
  t.integer('age').alter();
});

knex.schema.queryContext('schema context')
  .table('users', function (table) {
    table.queryContext('table context');
    table.string('first_name').queryContext('first_name context');
    table.string('last_name').queryContext('last_name context');
  })
  
var Promise = require('bluebird');

knex.transaction(function(trx) {

  var books = [
    {title: 'Canterbury Tales'},
    {title: 'Moby Dick'},
    {title: 'Hamlet'}
  ];
  
  return trx
    .insert({name: 'Old Books'}, 'id')
    .into('catalogues')
    .then(function(ids) {
      return Promise.map(books, function(book) {
        book.catalogue_id = ids[0];
        
        return trx.insert(book).into('books');
      });
    });
})
.then(function(inserts) {
  console.log(inserts.length = ' new books saved.');
})
.catch(function(error){
  console.error(error);
});

```


