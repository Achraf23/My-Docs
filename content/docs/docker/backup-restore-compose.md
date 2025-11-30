## Backup and Restore Volumes and Bind mounts

### Back up a single volume

Using **docker documentation** commands
```bash
docker run --rm --volumes-from infra-db-1 -v $(pwd):/backup mysql tar cvf /backup/backup.tar /var/lib/mysql .
```

> [!Warning]
> The point *.* at the end of the command above is important. When you extract the backup later on, it will not recreate the leading directories /var/lib/mysql 

<br>

Using **Offen** docker backup software (Github)

`docker run --rm -v infra_db_data:/backup/data -v $(pwd)/test:/archive --entrypoint backup offen/docker-volume-backup:v2`

- `infra_db_data` : name of the volume to backup. Mounted on `/backup` which is by **default where Offen Image fetches created backups**
- `/archive` : by default where the backup is copied to **inside the container**  


### Backup multiple containers workflow


## Restore multiple Volumes using Docker Compose

```yaml
restore:
    image: alpine
    volumes:
      - data:/backup_restore
      - ./backup:/src_backup  # folder with data-backup
    command: >
      sh -c "
        echo 'Extracting backup archive...' &&
        mkdir -p /tmp/restore &&
        tar -xzf /src_backup/data-backup.tar.gz -C /tmp/restore &&

        echo 'Copying extracted folders...' &&
        for folder in /tmp/restore/*; do
          name=$(basename $folder);
          echo \"Restoring $name -> /backup_restore/$name\";

          mkdir -p /backup_restore/$name;
          cp -r \"$folder\"/* /backup_restore/$name/;
        done &&

        echo 'Restore complete'
      "
```
