- [redis-cli basic commands](#redis-cli-basic-commands)

# redis-cli basic commands

- install client: `sudo apt-get install redis-tools`
- connect: `redis-cli`
  - remote: `redis-cli -h <redis-host> -p <redis-port>`
- authentication: `AUTH <password>`
- get all keys: `keys *`
- set key: `set <keyName> <keyValue>`
- get key value: `get <keyName>`
- clear all redis: `FLUSHALL`

## examples:

### ping

- `redis-cli --tls -h vortex-scheduler-bull-stg-jfhn85nf-zof5ju.serverless.use1.cache.amazonaws.com -p 6379 ping`

### get

- `redis-cli --tls -h vortex-cache-stg-9cx7z42v-zof5ju.serverless.use1.cache.amazonaws.com -p 6379 get organization:3d7d549b-3fb4-434d-9c2e-e7ab4e9199d1`
- `redis-cli --tls -h vortex-cache-stg-9cx7z42v-zof5ju.serverless.use1.cache.amazonaws.com -p 6379 get campaign:ced966fb-f1c5-469e-ae12-032279e9fe19`
- `redis-cli --tls -h vortex-cache-prd-ipqmtaiv-wycuq2.serverless.use1.cache.amazonaws.com -p 6379 get campaign:6ba27c2a-dacf-40c5-adad-46975df8e427`
- `redis-cli --tls -h vortex-cache-stg-9cx7z42v-zof5ju.serverless.use1.cache.amazonaws.com -p 6379 HGETALL {email_notification_bucket}`

### delete

- `redis-cli --tls -h vortex-cache-stg-9cx7z42v-zof5ju.serverless.use1.cache.amazonaws.com -p 6379 DEL organization:3d7d549b-3fb4-434d-9c2e-e7ab4e9199d1`
- `redis-cli --tls -h vortex-cache-prd-ipqmtaiv-wycuq2.serverless.use1.cache.amazonaws.com -p 6379 DEL campaign:6ba27c2a-dacf-40c5-adad-46975df8e427`

### set

- `redis-cli --tls -h vortex-cache-stg-9cx7z42v-zof5ju.serverless.use1.cache.amazonaws.com -p 6379 SET test_key "test_value" `
