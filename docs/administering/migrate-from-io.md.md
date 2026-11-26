# Migrate from Sandstorm.io

Sandstorm.io was the original startup which created Sandstorm, founded by Kenton
Varda. The final Sandstorm.io build is version 0.308, and to receive new updates
a server must migrate to Sandstorm.org builds.

## Standard installation

If you installed Sandstorm using the `curl | bash` method, you can migrate via
another single `curl | bash` command!

```bash
curl https://install.sandstorm.org/migrate.sh | bash
```

You will need to run the migrate.sh script as root. The script will check that
your server has enough free space to likely succeed, and will ask you to confirm
that you have backed up your server.

## Docker installation

If you used the Docker-based installation method, you will need to run the script
inside the container. If you do not know your container's name or ID, you can run
`docker ps`, and then run the following command to launch the migration script
inside the container.

```bash
docker exec -it --user root CONTAINER_ID_OR_NAME \
  bash -o pipefail -c 'export PATH="/opt/sandstorm:$PATH"; curl -fsSL https://install.sandstorm.org/migrate.sh | bash'
```

## Manual migration

If you do not want to use the migration script, this is a short primer on what the
migration script does to perform the migration and what commands you will need to
do it yourself.

You will need to change your `UPDATE_CHANNEL` in sandstorm.conf to `none` so that
you can apply a manual update. Then you can `sandstorm stop` to shut down Sandstorm.

Then you can download the latest bundle from https://dl.sandstorm.org/ such as
sandstorm-310.tar.xz. Then run `sandstorm update sandstorm-310.tar.xz` to update
to the new bundle.

Run `sandstorm migrate-mongo` to migrate the database from Mongo 2.6 to Mongo 7.0.

Change the `UPDATE_CHANNEL` back to `dev` to enable automatic updates from the new
update channel, and then `sandstorm start` to get Sandstorm running again.

## Reverting to Sandstorm.io version

If the upgrade fails and you need to return to the previous version of Sandstorm,
you can `stop sandstorm`, and use the command `sandstorm rollback-mongo` to restore
the backed up version of the original database. You will lose any changes to the
database made while running the newer release of Sandstorm.

Then you must manually apply a Sandstorm bundle for the older version of Sandstorm,
such as `sandstorm update sandstorm-308.tar.xz`, and then you can `sandstorm start`
to bring Sandstorm back online.