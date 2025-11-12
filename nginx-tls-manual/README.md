## Certs

Get certs at Cloudflare

Put them in the certs folder with the naming scheme

```
<domain>.key # This is the private one
<domain>.crt # This is the public cert
```

We can also self sign them this way:

```
openssl genrsa -out ./certs/immich.key 2048
openssl req -new -key ./certs/immich.key -out ./certs/immich.csr \
  -subj "/C=US/ST=State/L=City/O=Organization/OU=IT Department/CN=immich.wanglab.science"
  openssl x509 -req -days 365 -in ./certs/immich.csr \
  -signkey ./certs/immich.key -out ./certs/immich.crt

mv ./certs/immich.key ./certs/immich.wanglab.science.key
mv ./certs/immich.crt ./certs/immich.wanglab.science.crt
mv ./certs/immich.csr ./certs/immich.wanglab.science.csr
```

## Using DNS Challenge

mkdir -p ./certbot_config
docker run -it --rm \
  -v "${PWD}/certbot_config:/etc/letsencrypt" \
  certbot/certbot \
  certonly --manual \
  --preferred-challenges dns \
  -d immich.wanglab.science

### rename the files for nginx-proxy
sudo cp ./certbot_config/live/immich.wanglab.science/fullchain.pem \
    ./immich.wanglab.science.crt

sudo cp ./certbot_config/live/immich.wanglab.science/privkey.pem \
    ./immich.wanglab.science.key