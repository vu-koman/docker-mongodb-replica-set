# MongoDB Replica Set in docker-compose


## Generate new *mongodb-keyfile*

[***mongodb-keyfile***](https://docs.mongodb.com/manual/core/security-internal-authentication/#keyfiles)
> Keyfiles use SCRAM challenge and response authentication mechanism where the keyfiles contain the shared password for the members. 

Simple command to generate mongodb keyfile(depends on *openssl*): 

> `openssl rand -base64 756 > mongodb-keyfile`


## Change replica set name

In file [*docker-compose.yml*](./docker-compose.yml) change `buaa_mongo_replset` to your replica set name


## Change hostnames of containers

If you change hostnames of docker containers in [*docker-compose.yml*](./docker-compose.yml), you'll need to update following files:

- [*docker-compose.yml*](./docker-compose.yml):
  - Update *mongo-express* service environment variable **ME_CONFIG_MONGODB_SERVER**
- [*Dockerfile*](./mongo-connector/Dockerfile):
  - Update `--host` parametar in `CMD` dockerfile command
- [*initReplSet.js*](./mongo-connector/initReplSet.js):
  - Update `rs.add(<host_name>)` mongodb command on lines 2 and 3


## Build

Note that build is needed every time you change something mentioned above

> `docker-compose build`


## Start

> `docker-compose up -d`


## Stop and destroy containers

> `docker-compose down`


## Stop, destroy containers and delete volumes

> `docker-compose down -v`


## Connection string expamle for replica set

> mongodb://root:toor@buaa_mongodb_primary:27017,buaa_mongodb_secondary1:27017,buaa_mongodb_secondary2:27017/?replicaSet=buaa_mongo_replset&w=1&readConcernLevel=local
