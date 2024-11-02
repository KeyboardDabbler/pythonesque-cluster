### Gameserver with RCON-CLI-Tool

See [example docker-compose.yml](docker-compose.yml).

## Run RCON commands

> [!NOTE]
> Please research the RCON-Commands on the official source: https://tech.palworldgame.com/settings-and-operation/commands

You can use `docker exec palworld-dedicated-server rconcli <command>` right on your terminal/shell.

```shell
$ docker exec palworld-dedicated-server rconcli showplayers
name,playeruid,steamid

$ docker exec palworld-dedicated-server rconcli info
Welcome to Pal Server[v0.1.4.1] jammsen-docker-generated-20384

$ docker exec palworld-dedicated-server rconcli save
Complete Save
```

## Backup Manager

> [!WARNING]
> If RCON is disabled, the backup manager won't do saves via RCON before creating a backup and will report warnings.
> This means that the backup will be created from the last auto-save of the server.
> This can lead to data-loss and/or savegame corruption.
>
> **Recommendation:** Please make sure that RCON is enabled before using the backup manager.

> [!WARNING]
> Please use in the following part always the `-user steam` option or your files will written as root


Usage: `docker exec -user steam palworld-dedicated-server backup [command] [arguments]`

| Command | Argument           | Required/Optional | Default Value                     | Values           | Description                                                                                                                                                                          |
| ------- | ------------------ | ----------------- | --------------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| create  | N/A                | N/A               | N/A                               | N/A              | Creates a backup.                                                                                                                                                                    |
| list    | `<number_to_list>` | Optional          | N/A                               | Positive numbers | Lists all backups.<br>If `<number_to_list>` is specified, only the most<br>recent `<number_to_list>` backups are listed.                                                             |
| clean   | `<number_to_keep>` | Optional          | `BACKUP_RETENTION_AMOUNT_TO_KEEP` | Positive numbers | Cleans up backups.<br>If `<number_to_list>` is specified, cleans and keeps<br>the most recent`<number_to_keep>` backups.<br>If not, default to `BACKUP_RETENTION_AMOUNT_TO_KEEP` var |

Examples:

```shell
$ docker exec -user steam palworld-dedicated-server backup
> Backup 'saved-20240203_032855.tar.gz' created successfully.
```

```shell
$ docker exec -user steam palworld-dedicated-server backup list
> Listing 2 backup file(s)!
2024-02-03 03:28:55 | saved-20240203_032855.tar.gz
2024-02-03 03:28:00 | saved-20240203_032800.tar.gz
```

```shell
$ docker exec -user steam palworld-dedicated-server backup_clean 3
> 1 backup(s) cleaned, keeping 2 backups(s).
```

```shell
$ docker exec -user steam palworld-dedicated-server backup_list
> Listing 1 out of backup 2 file(s).
2024-02-03 03:30:00 | saved-20240203_033000.tar.gz
```

## Webhook integration

To enable webhook integrations, you need to set the following environment variables in the `default.env`:

```shell
WEBHOOK_ENABLED=true
WEBHOOK_URL="https://your.webhook.url"
```

After enabling the server should send messages in a Discord-Compatible way to your webhook url.

> You can find more details about these variables [here](/docs/ENV_VARS.md#webhook-settings).

### Supported events

- Server starting
  - This even is not server started. Just add like 5 seconds on top and the server is online
- Server stopped
- Server updating
- Server updating and validating
