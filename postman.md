- [scripts](#scripts)
- [fix](#fix)

# scripts

doc <https://learning.postman.com/docs/postman/scripts/test-examples/>

- set env var: `pm.environment.set("varName", "something");`
- get env var: `pm.environment.get("varName");`

## examples

- pre

```javascript
// body
const body = {
  email: 'isaac@kubi.cl',
  password: 'admin',
  device_type: 'I',
  device_token: 'b4bUEQHwh1Szlzp72I8iD17JchM9BDR6-gRv0bR8b0Y',
  uuid: '8897A265-3D1D-4C24-AC28-59AEDD7EB6CD',
  os_version: '12.4.5',
  device_name: 'Isaac’s iPhone',
  model_name: 'iPhone 6',
  ip: '127.0.0.1',
};
const { enc, AES } = CryptoJS;
const key = enc.Utf8.parse(pm.environment.get('key'));
const iv = enc.Utf8.parse(pm.environment.get('iv'));
var encBody = AES.encrypt(JSON.stringify(body), key, { iv: iv });
pm.environment.set('body', `${encBody}`);
// headerds
const apiKey = pm.environment.get('apiKey');
const token = pm.environment.get('token');
const encApiKey = AES.encrypt(apiKey, key, { iv: iv });
pm.request.headers.upsert({ key: 'api-key', value: `${encApiKey}` });
const encToken = AES.encrypt(token, key, { iv: iv });
pm.request.headers.upsert({ key: 'token', value: `${encToken}` });
```

- test

```javascript
const resCode = pm.response.code;
if (resCode === 200 || resCode === 401) {
  const { enc, AES } = require('crypto-js');
  const key = enc.Utf8.parse(pm.environment.get('key'));
  const iv = enc.Utf8.parse(pm.environment.get('iv'));
  const res = pm.response.json();
  const bytes = AES.decrypt(res, key, { iv: iv });
  const decRes = JSON.parse(bytes.toString(enc.Utf8));
  console.log('😉 decryptedData:\n' + JSON.stringify(decRes));
  // update token😎
  if (decRes.data && decRes.data.device.token) {
    const newToken = decRes.data.device.token;
    pm.environment.set('token', `${newToken}`);
  }
}
```

# fix

- when error `Could not get the lock, quitting`, run `pkill -fl Postman`
