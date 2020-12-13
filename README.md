# mocktls
Package mocktls provides mock TLS functionality for testing purposes.

## Mock TLS server
A basic TLS server can be run with the following command:

```sh
go run cmd/mockserver/main.go
```

By default, a private key and certificate chain will be generated in memory.

#### Using an existing private key and certificate chain from stdin
An existing private key and certificate chain can be provided via standard
input. A general example of this feature can be pasting a private key and
certificate chain into the program. Once the data has been pasted, simply send
a `SIGINT` with Control+D (or Control+C on Windows). Please refer to
https://pkg.go.dev/crypto/tls#LoadX509KeyPair for details about certificate
chain structure:

```sh
go run cmd/mockserver/main.go -i
-----BEGIN CERTIFICATE-----
# PEM data.
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
# PEM data.
-----END CERTIFICATE-----
-----BEGIN ECDSA PRIVATE KEY-----
# PEM data.
-----END ECDSA PRIVATE KEY-----
```

#### Using an on-disk private key and certificate
An existing private key and certificate chain can also be specified from disk as
well. Please refer to https://pkg.go.dev/crypto/tls#LoadX509KeyPair for
details about certificate chain file structure:

```sh
go run cmd/mockserver/main.go -k /path/to/key.pem -c /path/to/certchain.pem
```
