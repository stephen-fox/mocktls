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
certificate chain into the program. Once the data has been pasted, simply close
stdin with Control+D (Control+C on Windows because I was not sure what else
to do). Please refer to https://pkg.go.dev/crypto/tls#LoadX509KeyPair for
details about certificate chain structure. Here is an example:

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

## Certificate chain versus a single certificate
For the purposes of this project, a "certificate chain" refers to a list of
certificates. This term is commonly used by many TLS implementations. If you
are using a single certificate, then it is still considered a "chain", and can
be used in place of the chain. The term is a bit of a misnomer because
certificate signing is more complicated than A signs B which signs C. For more
information on the subject, refer to [Ryan Sleevi's blog post](https://medium.com/@sleevi_/path-building-vs-path-verifying-the-chain-of-pain-9fbab861d7d6)
on the subject.
