# Dbmate Docker Usage

This README provides instructions on how to use Dbmate with Docker to manage database migrations. The commands below allow you to create new migration files, run migrations up, and roll back migrations using a named Docker container for easier housekeeping.

## Running Dbmate Commands

To see available Dbmate commands, run:

```bash
docker run --rm -it --name dbmate --network=host -e DATABASE_URL="protocol://username:password@host:port/database_name?options" amacneil/dbmate --help
```

## Creating a New Migration File

To create a new migration file, use the following command:

```bash
docker run --rm -it --name dbmate --network=host -e DATABASE_URL="protocol://username:password@host:port/database_name?options" -v "$(pwd)/db:/db" amacneil/dbmate new create_users_table
```

## Running Migrations Up

To run any pending migrations, execute:

```bash
docker run --rm -it --name dbmate --network=host -e DATABASE_URL="protocol://username:password@host:port/database_name?options" -v "$(pwd)/db:/db" amacneil/dbmate up
```

## Rolling Back Migrations (Migration Down)

To roll back the most recent migration, use:

```bash
docker run --rm -it --name dbmate --network=host -e DATABASE_URL="protocol://username:password@host:port/database_name?options" -v "$(pwd)/db:/db" amacneil/dbmate rollback
```

## Notes

- Make sure to replace `protocol`, `username`, `password`, `host`, `port`, and `database_name` with your actual database credentials and connection details.
- The `--network=host` option is used to allow the Docker container to connect to the host's network, enabling it to access databases running on the host machine. If your database is running elsewhere, you may need to adjust the network settings accordingly.
- The `--name dbmate` parameter assigns a specific name to the container, allowing for easier identification and management.
- The `--rm` flag ensures that the container is automatically removed when it exits, preventing lingering containers with the same name.

If you have any questions or need further assistance, please refer to the [Dbmate documentation](https://github.com/amacneil/dbmate) or consult the [Dbmate Docker Hub page](https://hub.docker.com/r/amacneil/dbmate).