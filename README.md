# bakery-docker-scripts
Dockerfiles and instructions how to deploy Vaadin Bakery app starter Flow into AWS

Dockerfiles are put into three different folder

## docker-db

Dockerfile for deploying postgresql database into AWS to be used as a database for Bakery App Starter

## docker-server

Dockerfile for deploying Bakery App Starter into AWS with db configured to previously set up db.

## docker-gatling

Dockerfile for running Gatling tests in the AWS against above server.

## Quick start guide

### Setup AWS Cluster and project

1. Log in your AWS account
2. Navigate to Elastic Container Service
3. Click Clusters
4. Create Linux Cluster with e.g. 2 nodes if you like to have db in the separate node:
5. Make sure you have ssh keypair setup (later your-ssh-keypair.pem)
6. Open appropriate ports (at least 22, 5432, and 8080)

### Setup Bakery app starter

1. `git clone https://github.com/vaadin/bakery-app-starter-flow-spring.git`
2. `cd bakery-app-starter-flow-spring`
3. `mvn clean install -Pproduction -DskipTests`
4. copy docker-server and docker-db folder into root of the project

### Setup Postgresql db into first node

1. `cd docker-db`
2. `scp -i your-ssh-keypair.pem * ec2-user@db.node.ip.address:.`
3. `ssh -i your-ssh-keypair.pem ec2-user@db.node.ip.address`
4. `docker build . --rm -t bakery-db && docker run -it --rm -p 5432:5432 bakery-db`

### Setup an application server into second node

1. `cd docker-server`
2. `cp ../target/bakery-app-starter-flow-spring-1.0-SNAPSHOT.war bakery-app.war`
3. `scp -i your-ssh-keypair.pem * ec2-user@appserver.node.ip.address:.`
4. `ssh -i your-ssh-keypair.pem ec2-user@appserver.node.ip.address`
5. `docker build . --rm -t bakery-server --build-arg dbip=db.node.ip.address && docker run -it --rm --ulimit nofile=90000:90000 -p 8080:8080 bakery-server`

In addition you can edit default db name, username, and password in the `docker-db/Dockerfile`. Docker file `docker-server/Dockerfile` accepts following build args: `dbip`, `dbname`, `dbuser`, `dbpw`.

# Remember to delete your cluster when you do not need it anymore
