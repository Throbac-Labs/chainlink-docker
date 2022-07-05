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

## Authentication

A .htpasswd file is used for the protection of the Prometheus credentials using HTTP authentication and is implemented into a .htaccess file.

#### Install HTPASSWD
```
sudo apt-get install httpd-tools
```
#### Prometheus auth
```
htpasswd -nBC 10 "" | tr -d ':\n'
```
#### Node exporter auth
```
htpasswd -nBC 10 "" | tr -d ':\n'
```
  - Be careful to save each of these generated passwords and hashes separately, one group for node-exporter and one for prometheus
  - Check updated .yml and .ini files posted in this repo as those are what we've used (prometheus.yml, exporterweb.yml, prometheusweb.yml, grafana.ini)
