# PostgreSQL docker example

This repository show how to init a postgres database during the startup.

The SQL files which needs to be run during the startup process need to be 
placed in `/docker-entrypoint-initdb.d/*`. If you update the sql script,
just rebuild the image with the new files and start the new container.

The SQL examples are from the postgres documentation about creating databases
and tables.

Please keep in mind the the order of the scripts are important, that's why
they are prefixed with an index. If no prefix is present, it will order the 
files alphabetically.

## Build

To build the image:

```
docker build -t some-name-for-it .
```

That's it, pretty simple :) 

## Run

Like the official postgres image, you can start the image via:

```
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d some-name-for-it
```

## what's happening?

* The postgres image contains a init shell script, which will run all
  scripts inside the `/docker-entrypoint-initdb.d/*` directory.
* This will create a your database, based on your sql migration script
* you can also use shell scripts, just have a look here [1]



# Links
[1] https://github.com/docker-library/postgres/blob/aaf209829e072bec11bca1f6f0b52e756dfc096e/docker-entrypoint.sh#L126