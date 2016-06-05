# Alpine pause container

This container is an alpine based container which does nothing except stays alive even without being run with `-it`.
It can be used to replace the kubernetes `pause` container with one that has a shell, e.g. when testing some
part of kubernetes in an interactive manner.

## Usage

Run this container using `docker run karlherler/pause`, this will call the `pause` program (which does nothing but idle).
If you want to override the `pause` application you can postfix the docker run command with any other command as the program
is started using the `CMD` dockerfile parameter.

After the container is started you can investigate it by running `docker exec -it containername sh`

## Usage from kubernetes

Simply replace `image: kubernetes/pause` with `image: karlherler/pause` in your pod spec and the new pod will support `kubectl exec podname -i -t sh`

## Building

The simplest way to build this container is to call `make` using the make utility. This container relies on a
small c program and thus building will require a c compiler of some sort, specifically one supporting `gcc`
like flags. It is tested with gcc (version 6.1.1) and clang (version 3.8.0).

Using the docker container does not require any building.
