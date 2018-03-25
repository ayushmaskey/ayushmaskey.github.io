
# [Snort](http://snort.org/)

## Tesing
**view snort file**
```
snort -r /var/log/snort/snort.log.
```
**verify snort**
```
sudo snort -T -c /etc/snort/snort.conf
```

**alert in local.rules**
```
alert icmp any any -> $HOME_NET any (msg:"ICMP test"; sid:10000001; rev:001;)
```
**start snort in console**
```
sudo snort -A console -i eth0 -u snort -g snort -c /etc/snort/snort.conf
```
**snort as service**
```
sudo nano /lib/systemd/system/snort.service
```
```
[Unit]
Description=Snort NIDS Daemon
After=syslog.target network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/snort -q -u snort -g snort -c /etc/snort/snort.conf -i eth0

[Install]
WantedBy=multi-user.target
```
```
sudo systemctl daemon-reload
```

## [Installation and configuration](https://www.upcloud.com/support/installing-snort-on-ubuntu/)
[secondary with pulled pork](#http://www.ubuntu-howtodoit.com/?p=138)

pre-requisites
```
sudo apt install -y gcc libpcre3-dev zlib1g-dev libpcap-dev openssl libssl-dev libnghttp2-dev libdumbnet-dev bison flex libdnet
```

installating from source

```bash
mkdir ~/snort_src && cd ~/snort_src

wget https://www.snort.org/downloads/snort/daq-2.0.6.tar.gz
wget https://www.snort.org/downloads/snort/snort-2.9.9.0.tar.gz

tar -xvzf daq-2.0.6.tar.gz
tar -xvzf snort-2.9.11.1.tar.gz
```

run configure using default value
compile with make
install DAQ
```bash
cd ~/snort_src/daq-2.0.6/
./configure && make && sudo make install
```

configure snort with sourcefire enabled
and compile the source code
```bash
cd ~/snort_src/snort-2.9.11.1/
./configure --enable-sourcefire && make && sudo make install
```

update shared libray
```
sudo ldconfig
```

default snort path
```
/usr/local/bin/snort
```

create symbolic link (shortcut): good practice
```
sudo ln -s /usr/local/bin/snort /usr/sbin/snort
```

new user and user group without root access to run safely
```
sudo groupadd snort
sudo useradd snort -r -s /sbin/nologin -c SNORT_IDS -g snort
```

necessary folders and permissions
```
sudo mkdir -p /etc/snort/rules
sudo mkdir /var/log/snort
sudo mkdir /usr/local/lib/snort_dynamicrules

sudo chmod -R 5775 /etc/snort
sudo chmod -R 5775 /var/log/snort
sudo chmod -R 5775 /usr/local/lib/snort_dynamicrules

sudo chown -R snort:snort /etc/snort
sudo chown -R snort:snort /var/log/snort
sudo chown -R snort:snort /usr/local/lib/snort_dynamicrules
```

copy config files
```
sudo cp ~/snort_src/snort-2.9.11.1/etc/*.conf* /etc/snort/
sudo cp ~/snort_src/snort-2.9.11.1/etc/*.map /etc/snort
```

## Option 1: community rules: free
```
wget https://www.snort.org/rules/community -O ~/community.tar.gz
sudo tar -xvf ~/community.tar.gz -C ~/
sudo cp ~/community-rules/* /etc/snort/rules

#comment out not in community version
sudo sed -i 's/include \$RULE\_PATH/#include \$RULE\_PATH/' /etc/snort/snort.conf
```

## Option 2: registered version: sign up
from snort.org
```
wget https://snort.org/rules/snortrules-snapshot-29110.tar.gz?oinkcode=604cb8e7c4753ad57fb387b90d40d5cee3f6529f -O snortrules-snapshot-29110.tar.gz
wget https://snort.org/rules/snortrules-snapshot-29111.tar.gz?oinkcode=604cb8e7c4753ad57fb387b90d40d5cee3f6529f -O snortrules-snapshot-29111.tar.gz
wget https://snort.org/rules/snortrules-snapshot-2990.tar.gz?oinkcode=604cb8e7c4753ad57fb387b90d40d5cee3f6529f -O snortrules-snapshot-2990.tar.gz
wget https://snort.org/rules/snortrules-snapshot-2983.tar.gz?oinkcode=604cb8e7c4753ad57fb387b90d40d5cee3f6529f -O snortrules-snapshot-2983.tar.gz
```
**content to snort folder**
```
sudo tar -xvf ~$PWD/snortrules-snapshot-29110.tar.gz -C /etc/snort
```

## Option 3: subscriber version: pay


## Changes to snort.config
**external IP**
```
# Setup the network addresses you are protecting
ipvar HOME_NET 192.168.1.1/24
```
```
# Set up the external network addresses. Leave as "any" in most situations
ipvar EXTERNAL_NET !$HOME_NET
```
```
# Path to your rules files (this can be a relative path)
var RULE_PATH /etc/snort/rules
var SO_RULE_PATH /etc/snort/so_rules
var PREPROC_RULE_PATH /etc/snort/preproc_rules
```
```
# Set the absolute path appropriately
var WHITE_LIST_PATH /etc/snort/rules
var BLACK_LIST_PATH /etc/snort/rules
```
**logs**
```
# unified2
# Recommended for most installs
output unified2: filename snort.log, limit 128, nostamp, mpls_event_types, vlan_event_types
```
**uncomment**
```
include $RULE_PATH/local.rules
```


## Install pulledpork

**pre req**
```
sudo apt-get install -y libcrypt-ssleay-perl liblwp-useragent-determined-perl
```
```
wget https://github.com/finchy/pulledpork/archive/patch-3.zip
unzip patch-3.zip
cd pulledpork-patch-3
sudo cp pulledpork.pl /usr/local/bin/
sudo chmod +x /usr/local/bin/pulledpork.pl
sudo cp etc/*.conf /etc/snort/
```
**test pull pork** 
```/usr/local/bin/pulledpork.pl -V```

**changes to pulledpork.config**
```sudo vim /etc/snort/pulledpork.conf```

**uncomment line 29**
```rule_url=https://rules.emergingthreats.net/|emerging.rules.tar.gz|open-nogpl```

**upate line 74**
```rule_path=/etc/snort/rules/snort.rules```

**update line 89**
```local_rules=/etc/snort/rules/local.rules```

**update line 92**
```sid_msg=/etc/snort/sid-msg.map```

96
```sid_msg_version=2```

119
```config_path=/usr/local/etc/snort/snort.conf```

133
```
distro=Ubuntu-12-04```

141
```black_list=/etc/snort/rules/iplists/black_list.rules```

150
```IPRVersion=/etc/snort/rules/iplists```
