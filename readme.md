Create self signed tls certificates without OpenSSL.

## Install
```
npm install -g mkcert
```

## CLI

### Create a Certificate Authority
```
$ mkcert create-ca --help

  Usage: create-ca [options]

  Options:
    --organization [value]  Organization name (default: "Test CA")
    --country-code [value]  Country code (default: "US")
    --state [value]         State name (default: "California")
    --locality [value]      Locality address (default: "San Francisco")
    --validity [days]       Validity in days (default: 365)
    --key [file]            Output key (default: "ca.key")
    --cert [file]           Output certificate (default: "ca.crt")
    -h, --help              output usage information
```

### Create a Certificate

```
$ mkcert create-cert --help

  Usage: create-cert [options]

  Options:
    --ca-key [file]     CA private key (default: "ca.key")
    --ca-cert [file]    CA certificate (default: "ca.crt")
    --validity [days]   Validity in days (default: 365)
    --key [file]        Output key (default: "cert.key")
    --cert [file]       Output certificate (default: "cert.crt")
    --domains [values]  Comma separated list of domains/ip addresses (default: "localhost,127.0.0.1")
    -h, --help          output usage information
```

## API

```js
const mkcert = require('mkcert');

// create a certificate authority


async function createC(){
const ca = await mkcert.createCA({
  organization: 'Hello CA',
  countryCode: 'NP',
  state: 'Bagmati',
  locality: 'Kathmandu',
  validityDays: 365
});
return ca;
}

// then create a tls certificate

async function createG(m){
const cert = await mkcert.createCert({
  domains: ['127.0.0.1', 'localhost'],
  validityDays: 365,
  caKey: m.key,
  caCert: m.cert
});
return cert;
}

const ca = createC().then(res1 => {
	const cert = createG(res1).then(res2 => {
		console.log(res2.key, res2.cert); // create a full chain certificate by merging CA and domain certificates
	});
	
});


```
