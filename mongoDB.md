- [start](#start)
- [dump](#dump)
- [restore](#restore)
- [delete actual database](#delete-actual-database)
- [log into MongoDB](#log-into-mongodb)
- [commands](#commands)
- [mongo and docker](#mongo-and-docker)

# start

- run daemon `mongod`
- show Primary db `db.serverStatus().repl.primary`

# dump

```bash
mongodump -h fxnuncheecore-shard-00-03-jdnc2.mongodb.net:27017 \
        -u nunchee \
        -p YJvUPKSOKTa9E0a5 \
        -d AUTHNunchee \
        -c User \
        -q '{ "__belong.Client": ObjectId("59b144a4b00a9c4abb55669e") }' \
        --authenticationDatabase=admin --ssl
```

```bash
mongodump -h 52.54.124.45:27017 -u kubi_pro_user -p kubi_pro_user -d kubi_app_desa -c minitrivia_messages
```

# restore

```bash
mongorestore -vvvvv -h 127.0.0.1 -d AUTHNunchee -c User dump/AUTHNunchee/User.bson
```

```bash
mongo "mongodb+srv://kubi.u3bvn.mongodb.net/kubi_app" --username root --password l6t7nsgC03OQ2e9b
mongorestore -vvvvv \
  --host=atlas-b9xt68-shard-0/kubi-shard-00-01.u3bvn.mongodb.net:27017,kubi-shard-00-02.u3bvn.mongodb.net:27017,kubi-shard-00-00.u3bvn.mongodb.net:27017 \
  --ssl \
  --username 'root' \
  --password 'l6t7nsgC03OQ2e9b' \
  --ssl \
  --sslAllowInvalidCertificates \
  --sslAllowInvalidHostnames \
  --nsExclude 'admin.system.*' \
  --authenticationMechanism kubi_app \
  --authenticationMechanism SCRAM-SHA-1
```

```bash
mongorestore -vvvvv \
  --host=127.0.0.1 \
  --port=27888 \
  --username 'mongoadmin' \
  --password 'secret' \
  --db kubi_app_desa \
  --nsExclude 'admin.system.*' \
  --authenticationMechanism SCRAM-SHA-1 \
  --authenticationMechanism kubi_app_desa \
  ./dump/
```

`docker exec local-mongo sh -c 'mongorestore -d kubi_app_desa -u mongoadmin -p secret --archive' < db.dump`

# delete actual database

```javascript
use temp
db.dropDatabase()
```

# log into MongoDB

- get into mongo on Shell `mongo`
- authentication database

```bash
mongo -u <username> -p <password> --authenticationDatabase <dbname>
```

# commands

- show all databases `show dbs`
- select database to work with `use [databaseName]`
- Authenticate `db.auth("username", "password");`
- Logout `db.logout()`
- List down collections of the current database `show collections;` `db.getCollectionNames();`
- List down all the users of current database `show users;` `db.getUsers();`
- List down all the roles `show roles`
- create a collection `db.createCollection("collectionName");`
- Insert single document `db.<collectionName>.insert({field1: "value", field2: "value"})`
- Insert multiple documents `db.<collectionName>.insert([{field1: "value1"}, {field1: "value2"}])` `db.<collectionName>.insertMany([{field1: "value1"}, {field1: "value2"}])`
- save (Matching document will be updated; In case, no document matching the ID is found, a new document is created) `db.<collectionName>.save({"_id": new ObjectId("jhgsdjhgdsf"), field1: "value", field2: "value"});`
- update

```javascript
db.getCollection('Asset').update({
    '__belong.Client': ObjectId('5a1dc4176b769850f7fb978c'),
}, {
    $addToSet: {
        '__belong.AccessGroup': ObjectId('5a6b49a00ad5d4217fec6434')
    },
}, {
    multi: true,
    upsert: false,
}, );
```

- display collection records

  - Retrieve all records `db.<collectionName>.find();`
  - Retrieve limited number of records; Following command will print 10 results; `db.<collectionName>.find().limit(10);`
  - Retrieve records by id `db.<collectionName>.find({"_id": ObjectId("someid")});`
  - Retrieve values of specific collection attributes `db.<collectionName>.find({"_id": ObjectId("someid")}, {field1: 1, field2: 1});` `db.<collectionName>.find({"_id": ObjectId("someid")}, {field1: 0}); // Exclude field1`

- Collection count `db.<collectionName>.count();`

- Find \$in "array" `db.getCollection('User').find({'username': {$in: ["daniel.gonzalez@aldea.tv","gabriel.martinez@aldea.tv","diego.lopez@aldea.tv"]}}, {_id: 1})`
- compare id `mongoose.Types.ObjectId('58a0625246cb87062919eb62').equals('another id')`
- grant read & write permission: `db.grantRolesToUser('user1', [{ role: 'readWrite', db: 'account' }]);`

## administrative commands

- Get the collection statistics `db.<collectionName>.stats()` `db.printCollectionStats()`
- Latency statistics for read, writes operations including average time taken for reads, writes and related umber of operations performed `db.<collectionName>.latencyStats()`
- Get collection size for data and indexes

  - Size of the `collectiondb.<collectionName>.dataSize()`
  - Total size of document stored in the `collectiondb.<collectionName>.storageSize()`
  - Total size in bytes for both collection data and `indexesdb.<collectionName>.totalSize()`
  - Total size of all indexes in the `collectiondb.<collectionName>.totalIndexSize()`

## Example query

```javascript
db.getCollection('News')
    .find({
        '__belong.Client': ObjectId('587c502d67e4ce42f74a7061'),
        $where: 'this.videos.length > 0',
    })
    .forEach(function(item) {
        var assetIds = [];
        for (i in item.videos) {
            db.getCollection('Asset')
                .find({
                    _id: item.videos[i]._id
                })
                .forEach(function(asset) {
                    assetIds.push(asset._id);
                });
        }
        db.getCollection('Video')
            .find({
                '__belong.Asset': {
                    $in: assetIds
                },
                jwplayerMediaId: {
                    $exists: true
                },
            })
            .forEach(function(video) {
                var output = {
                    title: item.title,
                    fecha: item.available,
                    jw: video.jwplayerMediaId,
                };
                print(output);
            });
    });
```

# mongo and docker

```bash
docker run -d --name local-mongo  -p 27888:27017 -e MONGO_INITDB_ROOT_USERNAME=mongoadmin -e MONGO_INITDB_ROOT_PASSWORD=secret mongo
mongodb://mongoadmin:secret@localhost:27888/?authSource=admin
```
