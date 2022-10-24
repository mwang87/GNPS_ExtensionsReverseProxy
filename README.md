## GNPS Reverse Proxy 

This is the service to reverse proxy a bunch of services at the Wang Lab. 

### Different Types

1. nginx-basic - this is the most basic reverse proxy without TLS enabled - meant for internal services or those proxied purely through cloudflare and security is not a big deal
1. nging-tls - this includes TLS automatically done - this is meant for most client facing activities

### Header Pass Through

We enable a header passthrough for specific websites so that we can enable rate limiter on a source ip basis. 
