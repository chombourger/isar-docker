# isar-docker
Dockerfile to work with Isar (github.com/ilbers/isar)

## Usage
The container may be built and started with:
```
docker-compose up
```
This will pull a "debian" image from the public registry and augment it
with packages required by Isar. You may then start a remote shell:
```
ssh -p 8020 docker@localhost
Password: docker
```
Once in, a workspace may be created as follows:
```
$ cd /work
$ sudo install -o docker -g docker -d isar
$ cd isar
$ git clone https://github.com/ilbers/isar master
$ cd master
$ . isar-init-build-env ../build
$ bitbake isar-image-base
```
