# Monitoring Setup

changes:

- create tls certificates
- add remote write url, username, & pw to prometheus.yml
- add remote write url to promtail.yml
- add proper container log volume to promtail.yml

### Create tls certifications

Prometheus & Node Exporter
```
cd ~/chainlink-docker/.monitoring/.tls/.prometheus && openssl req -x509 -out   ~/chainlink-docker/.monitoring/.tls/.prometheus/prometheus.crt  -keyout  ~/chainlink-docker/.monitoring/.tls/.prometheus/prometheus.key -newkey rsa:2048 -nodes -sha256 -days 365 -subj '/CN=localhost' -extensions EXT -config <( printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth") && cd ~/chainlink-docker/.monitoring/.tls/.node-exporter && openssl req -x509 -out   ~/chainlink-docker/.monitoring/.tls/.node-exporter/node-exporter.crt  -keyout  ~/chainlink-docker/.monitoring/.tls/.node-exporter/node-exporter.key -newkey rsa:2048 -nodes -sha256 -days 365 -subj '/CN=localhost' -extensions EXT -config <( printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```
### Add remote write url, username, & pw to prometheus.yml + Add remote write url to promtail.yml
 
 This is gathered from grafana.com after creating a grafana cloud account and navigating to the "my account" and then creating a stack
 
### Add proper container log volume to promtail.yml

```
# log in as root
sudo -i 
# get the correct container to export your logs via promtail
cat /var/lib/docker/containers
```




 
