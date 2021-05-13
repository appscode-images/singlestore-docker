# deployment-docker

This repository contains our official deployment Docker images for various products.
If you are interested in contributing, please read `CONTRIBUTING.md`.

| Image        | SingleStore Packages Installed                                    |
|--------------|-------------------------------------------------------------------|
| ciab         | singlestoredb-server, singlestoredb-studio, singlestoredb-toolbox |
| ciab-redhat  | singlestoredb-server, singlestoredb-studio, singlestoredb-toolbox |
| dynamic-node | (none)                                                            |
| node         | singlestoredb-server                                              |
| node-redhat  | singlestoredb-server                                              |
| tools        | singlestoredb-toolbox                                             |

# Running the Cluster in a Box image

To initialize a new cluster in a box:

```bash
docker run -i --init \
    --name singlestore-ciab \
    -e LICENSE_KEY=${LICENSE_KEY} \
    -e ROOT_PASSWORD=${ROOT_PASSWORD} \
    -p 3306:3306 -p 8080:8080 \
    singlestore/cluster-in-a-box
```

To manage your cluster in a box:

```bash
To start the container:
    docker start singlestore-ciab

To read logs from the container:
    docker logs singlestore-ciab

To stop the container (must be started):
    docker stop singlestore-ciab

To restart the container (must be started):
    docker restart singlestore-ciab

To remove the container (all data will be deleted):
    docker rm singlestore-ciab
```

# Automatically run SQL when Cluster in a Box initializes

If you want to automatically run SQL commands when creating a Cluster in a Box
container, you can mount a SQL file into the Docker container like so:

```bash
docker run -i --init \
    --name singlestore-ciab \
    -e LICENSE_KEY=${LICENSE_KEY} \
    -e ROOT_PASSWORD=${ROOT_PASSWORD} \
    -v /PATH/TO/INIT.SQL:/init.sql \
    -p 3306:3306 -p 8080:8080 \
    singlestore/cluster-in-a-box
```

**Replace `/PATH/TO/INIT.SQL` with a valid path on your machine to the SQL file
you want to run when initializing Cluster in a Box.**
