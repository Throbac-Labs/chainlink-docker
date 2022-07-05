# Monitoring Setup

changes:

- create tls certificates
- create encrypted pws
- add encrypted pws to exporterweb.yml, prometheusweb.yml
- add plain txt pws prometheus.yml
- add remote write url, username, & pw to prometheus.yml
- add remote write url to promtail.yml
- add proper container log volume to promtail.yml

### Create tls certifications

Prometheus & Node Exporter
```
cd ~/chainlink-docker/.monitoring/.tls/.prometheus && openssl req -x509 -out   ~/chainlink-docker/.monitoring/.tls/.prometheus/prometheus.crt  -keyout  ~/chainlink-docker/.monitoring/.tls/.prometheus/prometheus.key -newkey rsa:2048 -nodes -sha256 -days 365 -subj '/CN=localhost' -extensions EXT -config <( printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth") && cd ~/chainlink-docker/.monitoring/.tls/.node-exporter && openssl req -x509 -out   ~/chainlink-docker/.monitoring/.tls/.node-exporter/node-exporter.crt  -keyout  ~/chainlink-docker/.monitoring/.tls/.node-exporter/node-exporter.key -newkey rsa:2048 -nodes -sha256 -days 365 -subj '/CN=localhost' -extensions EXT -config <( printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```

### Create encrypted pws + add them to exporterweb.yml, prometheusweb.yml

#### Install HTPASSWD
```
sudo apt install apache2-utils -y
sudo apt-get install httpd-tools
```
#### Prometheus auth
```
htpasswd -nBC 10 "" | tr -d ':\n'
```
---> add to prometheusweb.yml

#### Node exporter auth
```
htpasswd -nBC 10 "" | tr -d ':\n'
```
---> add to exporterweb.yml

  - Be careful to save each of these generated passwords and hashes separately, one group for node-exporter and one for prometheus
  - Check updated .yml and .ini files posted in this repo as those are what we've used (prometheus.yml, exporterweb.yml, prometheusweb.yml, grafana.ini)
  
### Add pws to prometheus.yml
 
 I typically use same pws as above, but these are plain text
 
 
### Add remote write url, username, & pw to prometheus.yml + Add remote write url to promtail.yml
 
 This is gathered from grafana.com after creating a grafana cloud account and navigating to the "my account" and then creating a stack
 
### Add proper container log volume to promtail.yml

```
# log in as root
sudo -i 
# get the correct container to export your logs via promtail
cat /var/lib/docker/containers
```




 
