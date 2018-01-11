
# Snort
## [Installation and configuration](https://www.upcloud.com/support/installing-snort-on-ubuntu/)

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
```

comment out not in community version
```
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


## Option 3: subscriber version: pay


## Changes to snort.config
```
ipvar HOME_NET <server public IP>/32
ipvar EXTERNAL_NET !$HOME_NET
```


