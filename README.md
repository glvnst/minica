# minica (kinda)

## IMPORTANT NOTE ABOUT THIS FORK

Please see [the official minica repo - jsha/minica](https://github.com/jsha/minica) rather than relying on this fork!

This fork mostly consists of me merging PRs that were submitted to jsha/minica but have not yet been accepted (nor rejected) there. This fork is for experimentation and personal use and probably most of these changes won't make it into upstream because they add complexity and use cases which may not be part of the original design goals. In these cases, minica's creator frequently directs people to the [mkcert](https://github.com/FiloSottile/mkcert) project.

## About minica

[Minica](https://github.com/jsha/minica) is a simple CA intended
for use in situations where the CA operator also operates each host
where a certificate will be used. It automatically generates both
a key and a certificate when asked to produce a certificate. It
does not offer OCSP or CRL services. Minica is appropriate, for
instance, for generating certificates for RPC systems or microservices.

On first run, minica will generate a keypair and a root certificate in the
current directory, and will reuse that same keypair and root certificate
unless they are deleted.

On each run, minica will generate a new keypair and sign an end-entity (leaf)
certificate for that keypair. The certificate will contain a list of DNS names
and/or IP addresses from the command line flags. The key and certificate are
placed in a new directory whose name is chosen as the first domain name from
the certificate, or the first IP address if no domain names are present. It
will not overwrite existing keys or certificates.

The certificate will have a validity of 2 years and 30 days.

### Installation

First, install the [Go tools](https://golang.org/dl/) and set up your `$GOPATH`.
Then, run:

`go get github.com/jsha/minica`

When using Go 1.11 or newer you don't need a $GOPATH and can instead do the
following:

```
cd /ANY/PATH
git clone https://github.com/jsha/minica.git
cd minica
go build
## or
# go install
```

### Example usage

```
# Generate a root key and cert in minica-key.pem, and minica.pem, then
# generate and sign an end-entity key and cert, storing them in ./foo.com/
$ minica --domains foo.com
```
