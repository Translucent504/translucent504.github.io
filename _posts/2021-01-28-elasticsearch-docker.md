---
title: "How to install Elasticsearch with docker"
excerpt_separator: "<!--more-->"
categories:
  - today-i-learned
tags:
  - til
---

> Installing elastic search with docker and also with docker-compose

<!--more-->

# Instructions

Just follow this [Link](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html).

## Get the image:

```
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.10.2
```

## Start the container:

This will run elasticsearch in a single node mode where there wont be replication and stuff 🤷.

```
docker run --name "elastic" -v elasticdata:/usr/share/elasticsearch/data -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.10.2
```

- the -v flag lets us create and attach a volume to persist data with elasticsearch at the given path inside the container `/usr/share/elasticsearch/data`.

## Verify

To check if its working, wait a couple of seconds until the terminal has stopped throwing random messages 😆. Then check the health by sending a get request with curl or whatever:

```
curl -XGET "localhost:9200/_cat/health?v=true&pretty"
```

You can send data to it with put or post requests like:

```
curl -XPOST "localhost:9200/school/_doc/1" -H 'Content-Type:application/json' -d '{"name":"asdasd"}'
```

## Starting multiple nodes

We can use docker compose to startup multiple nodes that will work together.

- [Install Docker-compose on Linux](https://docs.docker.com/compose/install/)
- [Follow the rest of the instructions here.](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#docker-compose-file)

## Incase of errors:

If you get this error:

> max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]

A temporary fix will be to run this on your machine:

```
sysctl -w vm.max_map_count=262144
```

For a permanent fix edit `/etc/sysctl.conf` and put `vm.max_map_count=262144`.
