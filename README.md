# signcode

[![Travis Build Status](https://travis-ci.org/kevinsawicki/signcode.svg?branch=master)](https://travis-ci.org/kevinsawicki/signcode)
[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat)](http://standardjs.com/)
[![npm:](https://img.shields.io/npm/v/signcode.svg)](https://www.npmjs.com/packages/signcode)
[![downloads:](https://img.shields.io/npm/dm/signcode.svg)](https://www.npmjs.com/packages/signcode)


Sign Windows executables from a Mac using [osslsigncode](https://sourceforge.net/projects/osslsigncode).

Works with `.pem`, `.p12`, and `.pfx` code signing files.

Signs with `sha1` and `sha256` signatures by default.

## Installing

```sh
npm install signcode
```

## CLI

Run `signcode --help` for more usage details.

```sh
signcode ./myapp.exe --cert ~/cert.p12 --password s3cr3t
```

## API

```js
var signcode = require('signcode')

var options = {
  cert: '/Users/kevin/certs/cert.pem',
  key: '/Users/kevin/certs/key.pem',
  overwrite: true,
  path: '/Users/kevin/apps/myapp.exe'
}

signcode.sign(options, function (error) {
  if (error) {
    console.error('Signing failed', error.message)
  } else {
    console.log(options.path + ' is now signed')
  }
})
```

## Cert helpers commands

These commands are helpful to when working with certificates.

### Create cert and key with no password

```sh
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -nodes
```

### Create cert and key with a password

```sh
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem
```

### Create a p12 with no password

```sh
openssl pkcs12 -export -out ./test/fixtures/cert.p12 -inkey ./test/fixtures/key.pem -in ./test/fixtures/cert.pem
```

### Show fingerprint of a cert

```sh
openssl x509 -noout -in ./test/fixtures/cert.pem -fingerprint -sha1
```

```sh
openssl x509 -noout -in ./test/fixtures/cert.pem -fingerprint -sha256
```
