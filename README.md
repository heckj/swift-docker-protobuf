# swift-docker-protobuf

extends the swift-docker image with protobuf

Hosting on Docker Hub: [heckj/swift-docker-protobuf](https://hub.docker.com/repository/docker/heckj/swift-docker-protobuf)

## building locally

    docker build -f 5.2/18.04/Dockerfile . -t swift-docker-protobuf:5.2-bionic -t swift-docker-protobuf:5.2 -t swift-docker-protobuf:latest
    docker build -f 5.2/16.04/Dockerfile . -t swift-docker-protobuf:5.2-xenial
