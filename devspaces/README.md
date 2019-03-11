# CockroachDB Development with DF Devspaces

## Install DF Devspaces

1. Create and install devspaces client as it is written in help guide https://support.devspaces.io/article/22-devspaces-client-installation.

2. Deploy your development environment into DF devspaces following this guide https://support.devspaces.io/article/23-support-guidelines 

3. Here is some details about DF Devspaces https://devspaces.io/devspaces/help

Here follows the main commands used in Devspaces cli. 

|action   |Description                                                                                   |
|---------|----------------------------------------------------------------------------------------------|
|`devspaces --help`                    |Check the available command names.                               |
|`devspaces create [options]`          |Creates a DevSpace using your local DevSpaces configuration file |
|`devspaces start <devSpace>`          |Starts the DevSpace named \[devSpace\]                           |
|`devspaces bind <devSpace>`           |Syncs the DevSpace with the current directory                    |
|`devspaces info <devSpace> [options]` |Displays configuration info about the DevSpace.                  |

Use `devspaces --help` to know about updated commands.


### Start Devspaces 

1.  Create DevSpaces.

```bash
devspaces create
```

2. Start your devspaces.
```bash
devspaces start cockroachdb
```

3. Start containers synchronization
Open terminal on folder you want to sync with devspaces and run:

```bash
devspaces bind cockroachdb
```
**Important Note**: Cockroach is a GoLang application. It is essentials to have a source code inside folder structure like this `$GOPATH/src/github.com/cockroachdb`. This is a recommend way to structure GoLang application and namely for CockroachDb project, since build will fail otherwise.

4. Grab some container info

```bash
devspaces info cockroachdb
```

Retrieve published DNS, endpoints using this command and 

5. Connect to development container

```bash
devspaces exec cockroachdb
```

6. Make sure the source code is synced and build the product

```bash
cd ./src/github.com/cockroachdb/cockroach
make build
```

7. You may run the tests.

```bash
make test
```

8. Run server
```bash
./cockroach start --insecure
```

## Running CockroachDB via Docker-Compose file

Currently, we have these command available to work using local docker compose.

```bash
devspaces/docker-cli.sh <command>
```

|action    |Description                                                               |
|----------|--------------------------------------------------------------------------|
|`build`   |Builds images                                                             |                                      
|`deploy`  |Deploy Docker compose containers                                          |
|`undeploy`|Undeploy Docker compose containers                                        |
|`start`   |Starts Docker compose containers                                          |
|`stop`    |Stops Docker compose containers                                           |
|`exec`    |Get into the container                                                    |


### Dockerfile
 Dockefile is created on top of `ubuntu:18.04` image.

### Requirements
 - The project should be cloned from https://github.com/trilogy-group/cockroach.git
 - Docker version 18.09.0-ce
 - Docker compose version 1.23.1 

### Quick Start
- Clone the repository
- Open a terminal session to that folder
- Run `./docker-cli.sh deploy`
- Run `./docker-cli.sh exec`
- At this point you must be inside the docker container. You can continue now from section `6. Download and extract packaged source code`
- When you finish working with the container, type `exit`
- Run `docker-cli.sh stop` to stop running service.
- Run `docker-cli.sh start` to start stopped container (should be used only after `stop` command).
- Run `docker-cli.sh undeploy` to stop and remove running service
