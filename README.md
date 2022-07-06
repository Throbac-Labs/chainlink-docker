# chainlink-docker

wip

## CL Node Notes

Changes:
- Create tls credentials
- Change .api and .password values
- Change chainlink.env to specs of desired blockchain & add proper database URL (using externally hosted db)
- Change docker-compose.yml eth-proxy endpoints to desired value

### Create tls credentials

```
openssl req -x509 -out  ~/chainlink-docker/.tls/server.crt  -keyout ~/chainlink-docker/.tls/server.key -newkey rsa:2048 -nodes -sha256 -days 365 -subj '/CN=localhost' -extensions EXT -config <( printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")

sed -i '/SECURE_COOKIES=false/d' ~/chainlink-docker/chainlink/chainlink.env
```
