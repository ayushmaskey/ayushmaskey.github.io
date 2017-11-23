---
layout: bigdata
type: bigdata
published: true
image: images/elk.png
title: cisco asa to ELK
permalink: bigdatas/data-asa-elk
date: 2017
labels:
  - cisco asa 5510
  - elk stack
summary: asa data collection - ELK.
---

what is elk stack?
what is elastic, logstash, kibana


There are few options when it comes to setting up ELK containers.
 * use base ubuntu and create ELK image from scratch
 * download images with all three in one which are available in docker hub.
 * donwload images for each of elasticsearch, logstash and kibana individually

For this project I chose to download the official image of each and create a container for each. Having separate container allows us to mimic a cluster of machines with each of those three apps running in separate machine.

```bash
docker pull elasticsearch
docker pull logstash
docker pull kibana
```

After the images have been downloaded, it is time to create a container of each with necessary settings. It is of utmost importance to create elasticsearch container before kibana or logstash since the later two need to be linked to former upon creation.

#### elasticsearch

```bash
docker run -d -p 9200:9200 -p 9300:9300 -t \
-hostname elastic1 --name elastic1 \
 elasticsearch
```
The above command uses elasticsearch image as base to create a container with hostname elastic1 and name the container elastic1. Moreover, the comand binds port 9200 and 9300 of the container to the same port numbers of the docker host machine. **-p** is the option we use to publish the ports. Port 9200 is for RESTful service that publishes basic information about the elasticsearch in JSON format. We can use a web browser or curl to download the content in port 9200 which can be used to verify whether elasticsearch is working as expected. While publishing port 9200 is optional, port 9300 is a necessity for elastic container. Port 9300 is used for communication between nodes.

#### kibana

```bash
docker run -d -p 5601:5601 -h kibana --name kibana \
--link elasticsearch:elasticsearch \
kibana
```

The command to run container is very similar to that of elasticsearch with couple of key differences. The command above uses kibana as base image to create a container named kibana and same hostname. **-h** is the same as **--hostname** and is used to give hostname to a docker container. The command also publishes port 5601 to the docker host and opens up the web interface to manipulate underlying data in elasticsearch. **-d** in kibana command is to simply create a container in detached mode. Finally, **--link** is the most important option when creating kibana container. Since kibana is a web interface to elasticsearch, we need to point kibana container to elasticsearch.

#### logstash

I kept logstash for the end as it requires more configuration. Command to create logstash container is similar to the other two up to contain extent, the biggest difference being the config file for logstash. 

```bash
docker run -h logstash --name logstash \
--link elasticsearch:elasticsearch \
-it --rm -v "$PWD":/config-dir logstash \
-f /config-dir/logstash1.conf
```
The above command uses logstash image to create a container named logstash and same hostname. Like kibana, logstash needs to be linked to elasticsearch as well. The above command has three more options, **-rm, -v, -f**. Those three commands were added specifically to to run and test config files. The biggest problem I had when creating cluster of ELK stack was getting the config files working as expected. 

Option **-v** mounts a folder in docker host as a volume in the container. Having a shared volume between host and container simplifies the process of modifying the config files. Once the config file is in the container, we can use option **-f** to point the logstash to the our config file rather than the default that ships with logstash image. 

The other option to point logstash to the correct config file would be to use Dockerfile. First copy the file  from host to container and then point.

```bash
COPY logstash.conf /config-dir/
CMD ["-f", "/config-dir/logstash1.conf"]
```

Regardless of how the config file is set, we will have to teat the file incrementally to achieve the desired result. I was creating container with a config file, stop the container, remove the container, tweak my config file and create the container again. This is a tedious process but docker option **--rm** simplifies the process of testing config file. We create the container with **--rm** option while we test and tweak the config file. Once we have a config file to our liking, the same command without **--rm** can be used the create a stable container.

#### logstash.config








