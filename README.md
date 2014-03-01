Docker file for Infinispan server
=================================

This repo contains some basic Docker files for [Infinispan](http://infinispan.org) server 6.0.0.
All server configuration has turned off REST authentication.

###Building container images:

```
docker build -t <repo_name>/ispn-standalone ispn-server-standalone
docker build -t <repo_name>/ispn-cluster ispn-server-cluster
```

###Get IP and store some value via REST

```
export CONTAINER_ID="<container_id>"
export CONTAINER_IP=`curl -s -X GET http://127.0.0.1:4243/containers/$CONTAINER_ID/json | awk 'BEGIN{RS=",";FS=":"}/"IPAddress":".*"/{print substr($3,2,length($3)-2)}'` 
curl -X POST -d "test value" http://$CONTAINER_IP:8080/rest/namedCache/testKey
curl -X GET http://$CONTAINER_IP:8080/rest/namedCache/testKey
```