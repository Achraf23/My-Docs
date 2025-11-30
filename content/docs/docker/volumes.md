---
title: Volumes
type: docs
prev: docs/docker/
---

### Backup a Docker Volume
`docker run --rm --volumes-from infra-db-1 -v $(pwd):/backup mysql tar czvf /backup/backup.tar.gz -C /var/lib/mysql .`

- [ ] /opt/test : la ou va etre le backup dans le host
- [ ] --volumes-from : option to specify the container of the volume we want to backup
- [ ] /opt/test est monté sur `/backup` qui est dans le conteneur
	- [ ] Tjrs dans le conteneur, on execute `tar cvf` pour créer `backup.tar` dans `/backup`. Comme `/backup` est monté dans /opt/test (avec l'option `-v`), on backup.tar dans le host



### backup database docker data
```bash
## tar czvf if we want to compress backup with gzip
docker run --rm -v vboxuser_db_data:/var/lib/mysql   -v $(pwd)/backup:/backup   mysql   sh -c "cd /var/lib/mysql && tar cvf /backup/my_volume_backup.tar ."
```


<br>
Usually we want to backup the `/var/lib/mysql` folder for a MySQL database

```
docker run --rm --volumes-from infra-db-1 -v $(pwd)/backup:/backup mysql tar cvf /backup/backup.tar /var/lib/mysql
```

- [ ] `mysql` is the name of the image that must be indicated in the command (instead of the name of the container) 

### Clean docker volume environement and restart from scratch

`docker rm -f $(docker ps -aq)`

`docker volume rm $(docker volume ls -q)`

### docker volumes location

On most systems:

| Platform                     | Path to volume data                                                                                                          |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **Linux**                    | `/var/lib/docker/volumes/db_data/_data/`                                                                                     |
| **macOS (Docker Desktop)**   | Inside a **VM**, not directly accessible on the host filesystem (you can access it via `docker exec` or `docker run` though) |
| **Windows (Docker Desktop)** | Same as macOS — stored inside a Docker-managed VM (e.g., WSL2 or Hyper-V)                                                    |
|                              |                                                                                                                              |

	if we change the compose yaml file and add another volume, we have to run docker compose up to make sure data is created
Running `docker compose up` creates the volume if it doesn't already exist


### inspect all docker volumes
`docker volume ls -q | xargs docker volume inspect --format='{{.Name}}: {{.Mountpoint}}'
`

