- [redis-cli basic commands](#redis-cli-basic-commands)

# redis-cli basic commands

- install client: `sudo apt-get install redis-tools`
- connect: `redis-cli`
  - remote: `redis-cli -h <redis-host> -p <redis-port>`
- authentication: `AUTH <password>`
- get all keys: `keys *`
- set key: `set <keyName> <keyValue>`
- get key value: `get <keyName>`
