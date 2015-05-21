# Percheron consul Stack

This repo contains a consul stack for use with [Percheron](https://github.com/ashmckenzie/percheron).

## Containers included

* master - Runs consul server + UI
* agent (2) - Runs consul agent

## Dependancies

* [Percheron](https://github.com/ashmckenzie/percheron)
* [Boot2Docker v1.6.x+](https://docs.docker.com/installation)
* [Docker client](https://docs.docker.com/installation) (nice to have)

## Quickstart

Start boot2docker

````shell
boot2docker up && eval $(boot2docker shellinit) && export BOOT2DOCKER_IP=$(boot2docker ip)
```

Clone the percheron-consul repo

```shell
git clone https://github.com/ashmckenzie/percheron-consul
```

Run Percheron!

```shell
cd percheron-consul && bundle install && bundle exec percheron start consul-stack
```

Ensure consul is running

```bash
curl http://boot2docker:8500/v1/catalog/nodes

[{"Node":"agent1","Address":"172.17.0.5"},{"Node":"agent2","Address":"172.17.0.6"},{"Node":"master","Address":"172.17.0.4"}]
```

Perform some DNS lookups

```bash
dig @boot2docker -p 8600 master.node.consul agent1.node.consul agent2.node.consul +short

172.17.0.7
172.17.0.8
172.17.0.9
```

Bring up the consul UI

```bash
open http://boot2docker:8500/ui
```
