# ELKR (Elasticsearch, Logstash, Kibana, Redis)

## Elasticsearch 2.3.1

###Install JAVA First

* `sudo apt-get update`

###Setting the **'JAVA_HOME'** environment variable

* `sudo addd-apt-repository ppa:webupd8team/java`
* `sudo apt-get update`
* `sudo apt-get install oracle-java8-installer`

it return path of java. copy the path and paste on following file

* `sudo nano /etc/environment`
* `JAVA_HOME="JAVA PATH"`

And Reload it

* `source /etc/environment`

---
### Download Elasticsearch
* `wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.3.2/elasticsearch-2.3.2.tar.gz`
* `tar -xvf elasticsearch-2.3.2.tar.gz`
* `./bin/elastsicsearch`

### Insltall Plugin
#### ElasticHQ
Monitoring, Managerment, and Querying Web Interface for ElasticSearch instances and clusters.

* `./bin/plugin install royrusso/elasticsearch-HQ`

#### ElasticSQL
Query elasticsearch using familar SQL syntax.

* `./bin/plugin install https://github.com/NLPchina/elasticsearch-sql/releases/download/2.3.2.0/elasticsearch-sql-2.3.2.0.zip`

**CONFIG**

`vim config/elasticsearch.yml`
Add following lines

* `script.inline: on`
* `script.indexed: on`


## Kibana 4.5.0

Source code build

* `git init`
* `git pull https://github.com/bdh1011/kibana 4.5.0`

**Install NPM**

* `curl -sL https://dev.nodesource.com/setup_4.x | sudo -E bash -`
* `sudo apt-get install -y nodejs`
* `npm install`
* `./bin/kibana`


## Redis 3.0.5

**RDM(Redis Desktop Manager)**

**Install**

* `wget http://download.redis.io/releases/redis-3.0.5.tar.gz`
* `tar xvfz redis-3.0.5.tar.gz`
* `make`
* `./src/redis-server &`

**Ruby install**

* `wget https://download.elastic.co/logstash/logstash/logstash-5.0.0-alpha2.tar.gz`
### Collector Logstash

