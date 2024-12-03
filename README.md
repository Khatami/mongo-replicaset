# MongoDB Replica Set with Docker Compose for Local Development

This guide provides instructions for running a MongoDB replica set using Docker Compose for local development.

## Update /etc/hosts File

To ensure the MongoDB instances can be resolved, add these entries to your `hosts` file:

```bash
127.0.0.1 mongo1 
127.0.0.1 mongo2 
127.0.0.1 mongo3
```

## Run the following bash

```bash
docker compose up -d
```

## Direct Connections

To directly connect to individual MongoDB instances, use the following connection strings:

```bash
mongodb://mongo1:27017/?directConnection=true mongodb://mongo2:27018/?directConnection=true mongodb://mongo3:27019/?directConnection=true
```

## Connect to the Replica Set

To connect to the MongoDB replica set, use this connection string:

```bash
mongodb://mongo1:27017,mongo2:27018,mongo3:27019/?replicaSet=myReplicaSet
```

## Connect to Secondary Nodes

If you prefer to read from secondary nodes, use the following connection string with the read preference set to secondary:

```bash
mongodb://mongo1:27017,mongo2:27018,mongo3:27019/?replicaSet=myReplicaSet&readPreference=secondaryPreferred
```

## Identifying the Primary Node

To identify the primary node in your replica set, run the following command in the MongoDB shell:

```bash
print("Primary node: " + rs.status().members.filter(member => member.stateStr === "PRIMARY")[0].name);
```