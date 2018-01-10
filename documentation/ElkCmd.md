
https://elk-docker.readthedocs.io/

# config
  * ram - atleast 4gb to docker
  * nmap - aleast 262144
	##increase nmap count. elastic search need more than default
	sysctl -w vm.max_map_count=262144
	## update permanently
	/etc/sysctl.conf --> vm.max_map_count
  * TCP port 5044 - log emitting client need access to this port

# using prebuilt image for now
sudo docker pull sebp/elk
! need Dockerfile or alteast find out all the packages installed

# create one container with all three
sudo docker run -p 5601:5601 -p 9200:9200 -p 5044:5044 -it --name elk sebp/elk

ubuntu:5601	#kibana web interface
ubuntu:9200	#elasticsearch JSON interface
ubuntu:5044	#logstash beat interface to load log into elk container

# create 3 separate containers

##elasticsearch
docker run -d -p 9200:9200 -p 9300:9300 -t -h elasticsearch --name elasticsearch elasticsearch
  * verify elasticsearch is owrkinf
curl http://localhost:9200


-p = post forward
-h = hostname

## kibana
docker run -d -p 5601:5601 -h kibana --name kibana --link elasticsearch:elasticsearch kibana
  * kibana needs elasticsearch
  * verify https://ubuntu:5601

##logstash
logstash.conf #config file
docker run -h logstash --name logstash --link elasticsearch:elasticsearch -it --rm -v "$PWD":/config-dir logstash -f /config-dir/logstash.conf

--rm 
-v = mounting current working directory as config-dir in container
  * run logstash.conf 

#sample logstash config file

```
input {
beats {
   port => 5044
}
udp {
   port => 5514
   type => "syslog"
}
tcp {
   type => "WindowsEventLog"
   port => 5544
}
}
```

cisco routers 
logging host 10.0.0.0 transport udp port 5514
or
from asdm
https://jackhanington.com/blog/2014/07/30/sysloging-cisco-asa-firewall/

