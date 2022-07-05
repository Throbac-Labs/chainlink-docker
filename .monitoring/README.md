# Monitoring Setup


## TLS Certificates 

Prometheus
```
cd ~/chainlink-docker/.monitoring/.tls/.prometheus && openssl req -x509 -out   ~/chainlink-docker/.monitoring/.tls/.prometheus/prometheus.crt  -keyout  ~/chainlink-docker/.monitoring/.tls/.prometheus/prometheus.key -newkey rsa:2048 -nodes -sha256 -days 365 -subj '/CN=localhost' -extensions EXT -config <( printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```
Node Exporter
```
cd ~/chainlink-docker/.monitoring/.tls/.node-exporter && openssl req -x509 -out   ~/chainlink-docker/.monitoring/.tls/.node-exporter/node-exporter.crt  -keyout  ~/chainlink-docker/.monitoring/.tls/.node-exporter/node-exporter.key -newkey rsa:2048 -nodes -sha256 -days 365 -subj '/CN=localhost' -extensions EXT -config <( printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```
