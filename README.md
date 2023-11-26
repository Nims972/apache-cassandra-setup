# apache-cassandra-setup
This repo helps in setting up apache cassandra on single node as well as multiple node

## Download and install Apache Cassandra 
How to setup the apache Cassandra is given in official documentation as well (https://cassandra.apache.org/doc/stable/cassandra/getting_started/installing.html#installing-the-debian-packages)

1. check the java version and whether its installed properly in the system.
```
java -version
```
2. Add the Apache repository of Cassandra to the file cassandra.sources.list

```
echo "deb https://debian.cassandra.apache.org 41x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
```

The expected output will be as below.
```
deb https://debian.cassandra.apache.org 41x main
```
4. Add the Apache Cassandra repository keys to the list of trusted keys.

```
curl https://downloads.apache.org/cassandra/KEYS | sudo apt-key add -
```

5. Update the package index from sources and Install Cassandra
```
sudo apt-get update
sudo apt-get install cassandra
```

6. Check the status of Cassandra:
```
nodetool status
```
![image](https://github.com/Nims972/apache-cassandra-setup/assets/22131911/aec2f9ba-d1cc-416d-ac23-503fe3f0fc49)
nodetool status should be like as in image.
Note: cassandra may take some time get warmup and available depends on the machine. (but should not take several mins usually)

## Configure Apache Cassandra for Multiple nodes

1. go to /etc/cassandra directory , take backup of cassandra.yaml file and change below items in cassandra.yaml
```
cluster_name: 'MyCassandraCluster'
num_tokens: 256
seed_provider:
  - class_name: org.apache.cassandra.locator.SimpleSeedProvider
    parameters:
         - seeds: "<IP1>,<IP2>"
listen_address:<IP of that VM>
rpc_address: <IP of that VM>
endpoint_snitch: RackInferringSnitch
```
2. Allow ports for communications
```
sudo ufw allow 7000
sudo ufw allow 7001
sudo ufw allow 9042
sudo ufw allow 7199
```
