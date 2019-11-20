---
layout: post
title: "Stop a docker-compose container without removal"
author: evanbrodie
date: 2017-06-01T16:06:01+00:00
---

Suppose you need to stop your docker-compose container but you don't want to remove the container. For example, this container runs your database, so removing the container would mean that you would also lose all your data.

Don't use `docker-compose down`. This will remove your container and you will have rebuild your database from scratch. Sad panda.

Instead, use `docker-compose stop`. You can then restart the container and have all the data back that you had before.

**Resources**:

- [Docker-Compose Down](https://docs.docker.com/compose/reference/down/)
- [Docker-Compose Stop](https://docs.docker.com/compose/reference/stop/)
