# Docker Enterprise Search

```shell
docker network create elastic
```

```shell
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.13.1
docker run -d --name elasticsearch \
--net elastic \
-p 9200:9200 -p 9300:9300 \
-e "discovery.type=single-node" \
docker.elastic.co/elasticsearch/elasticsearch:7.13.1
```

```shell
docker pull docker.elastic.co/enterprise-search/enterprise-search:7.13.1
docker run -d --name enterprise-search \
--net elastic \
-p 3002:3002 \
-e elasticsearch.host='http://elasticsearch:9200' \
-e allow_es_settings_modification=true \
-e secret_management.encryption_keys='[4a2cd3f81d39bf28738c10db0ca782095ffac07279561809eecc722e0c20eb09]' \
docker.elastic.co/enterprise-search/enterprise-search:7.13.1
```

```shell
docker pull docker.elastic.co/kibana/kibana:7.13.1
docker run -d --name kibana \
--net elastic \
-p 5601:5601 \
-e "ELASTICSEARCH_HOSTS=http://elasticsearch:9200" \
docker.elastic.co/kibana/kibana:7.13.1
```

Open http://localhost:3002 in browser