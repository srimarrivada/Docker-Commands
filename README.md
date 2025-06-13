# DOCKER COMMANDS
Use `docker help` to get the list of commands being used:

**Syntax:**
```
docker help
```
## 1. Docker Common Commands
The common docker commands include:
* `docker version`: It displays the version details of all docker components installed on the host. For more options, use `docker version --help` command.
  
  **Syntax:**
  ```
  docker version
  ```
  If use the below command, it displays the Docker client version alone:
  ```
  docker --version
  ```
  
* `docker info`: It displays the system wide information. For more options, use `docker info --help` command.
  
  **Syntax:**
  ```
  docker info
  ```
  or
  ```
  docker system info
  ```

## 2. Docker Image Commands
Docker provides a set of handy commands to manage images. Some of these commands are listed below:
* `docker build`: It is used to build the Docker image using the `Dockerfile` available in the specified directory.  
  This command allows to provide various options such as: 
  * `-d` to enable debugging
  * `-f` to specify the name of Docker File. By default, it refers to the file named `Dockerfile`
  * `-q` to suppress the build output
  * `-t` to set the name and optionally a tag for the image
  
  Use `docker build --help` command for the complete list of options.  
  
  **Syntax:**
  ```
  docker build <Dockerfile_location> <options>
  ```
  or
  ```
  docker image build <Dockerfile_location> <options>
  ```
  
* `docker pull`: It pulls the given image from the official docker registry which is **Docker Hub**. By default, it pulls the `latest` image from the Docker Hub but specify the tag name (version) to pull the
  specific version of the image. For more options, use `docker pull --help` command.

  **Syntax:**
  ```
  docker pull <image_name>
  ```
  or
  ```
  docker image pull <image_name>
  ```
  Use the following command to pull an image with a specific tag:
  ```
  docker pull <image_name>:<tag>
  ```
  or
  ```
  docker image pull <image_name>:<tag>
  ```
  **For example:**  
  Run the following command to pull the latest image of `mysql` from Docker Hub _(You can login to Docker Hub at https://hub.docker.com/ and search for `mysql` to see the list of available tags)_
  ```
  docker pull mysql
  ```
  Run the following command to pull the `8.4` version (tag) of `mysql` image:
  ```
  docker pull mysql:8.4
  ```

* `docker images`: It lists out all available images that were built on host or pulled from Docker registry such as Docker Hub.
  This command allows to provide various options such as: 
  * `-a` to show all images
  * `-f` to filter output based on conditions provided
  * `-q` to show only image IDs

  Use `docker images --help` command for the complete list of options.
  
  **Syntax:**
  ```
  docker images
  ```
  or
  ```
  docker image ls
  ```

* `docker inspect`: It helps to debug the docker image if any errors occurred while building an image or pulling the image. For more options, use `docker inspect --help` command.

  **Syntax:**
  ```
  docker inspect <image_name or image_id>
  ```
  **For example:**  
  Run the following command to inspect `mysql` image:
  ```
  docker inspect mysql
  ```
  
* `docker push`: It is used to push the docker image built in local to the Docker registry which is Docker Hub, by default. For more options, use `docker push --help` command.

  **Syntax:**
  ```
  docker push <image_name>
  ```
  or
  ```
  docker image push <image_name>
  ```

* `docker save`: It saves the docker image in the form of docker file. It accepts `-o` flag to write to a specific output file instead of **STDOUT**. For more options, use `docker save --help` command.

  **Syntax:**
  ```
  docker save -o <output_file> <image_name>
  ```
  or
  ```
  docker image save -o <output_file> <image_name>
  ```
  **For example:**  
  Run the following command to save the `mysql` image to a tar file in the current directory:
  ```
  docker save -o .\docker_mysql_save.tar mysql:8.4
  ```
 
* `docker import`: It imports the contents from a tar file to create a file system image. For more options, use `docker import --help` command.

  **Syntax:**
  ```
  docker import <tar_file_name> <new_image_name>
  ```
  or
  ```
  docker image import <tar_file_name> <new_image_name>
  ```
  **For example:**  
  Run the following command to import the `docker_mysql_save.tar` file as `mysql_import` image:
  ```
  docker import docker_mysql_save.tar mysql_import
  ```

* `docker tag`: It creates a new image with a specific tag based on the given image. Tags in Docker images are used to identify and differentiate between different versions of an image.

  **Syntax:**
  ```
  docker tag <image_name> <image_name>:<tag>
  ```
  or
  ```
  docker image tag <image_name> <image_name>:<tag>
  ```
  **For example:**  
  Run the following command to tag `mysql:8.4` as `mysql:v1.0`.  
  ```
  docker tag mysql:8.4 mysql:v1.0
  ```

 * `docker history`: It displays the history of an image with details of layers created on top of the base image. For more options, use `docker history --help` command.

   **Syntax:**
   ```
   docker history <image_name_or_image_id>
   ```
   or
   ```
   docker image history <image_name_or_image_id
   ```
   **For example:**  
   Run the following command to check the history of the `mysql:8.4` image:
   ```
   docker history mysql:8.4
   ```

 * `docker rmi`: It removes the specified docker image. For more options, use `docker rmi --help` command.

   **Syntax:**
   ```
   docker rmi <image_name>
   ```
   or
   ```
   docker image rm <image_name>
   ```
   or
   ```
   docker image remove <image_name>
   ```
   **For example:**
   Run the below command to delete `mysql:v1.0` image.
   ```
   docker rmi mysql:v1.0
   ```
 
* `docker image prune`: It removes all unused images that are not referenced by any container on the Docker host. For more options, use `docker image prune --help` command.

  **Syntax:**
  ```
  docker image prune
  ```

# 3. Docker Container Commands
Docker Container commands are helpful to manage the lifecycle of containers such as create, start, stop, inspect, or remove containers. Some of these commands are listed below:
* `docker run`: This command is a combination of `docker create` and `docker start` commands. It is used to create a container (if not already exists) from the specified image and start it. If the container
  already exists, it simply launches the container.  
  This command allows to provide various options such as: 
  * `-c` to set CPU for the container to use
  * `-d` to run container in the background (detached mode) and print container ID
  * `-e` to set environment variables
  * `-h` to specify container host name
  * `-i` to run in interactive mode which keeps STDIN open even when not attached
  * `-l` to set metadata on a container
  * `-m` to set memory for the container to use
  * `--name` to assign a name to the container
  * `--network` to connect a container to the network
  * `-p` to publish all container ports to random port
  * `-t` to allocate a pseudo-TTY
  * `-u` to specify username or UID with or without group or GID
  * `-v` to bind mount a volume to the container
  * `-w` to set the working directory inside the container

  Use `docker run --help` command for the complete list of options.
  
  **Syntax:**
  ```
  docker run <image_id or image_name>
  ```
  By default, the container gets an ID with an imaginary name such as `zen_dubinsky`, `heuristic_villani`, etc. which can be changed using `--name` option.

  **Note:** Some images may expect additional parameters to start a container.  

  **For example:**  
  When `docker run mysql` command is run to start the container, it fails since `mysql` image expects one of the parameters `MYSQL_ROOT_PASSWORD` or `MYSQL_ALLOW_EMPTY_PASSWORD`
  or `MYSQL_RANDOM_ROOT_PASSWORD` to start. Read [Docker Hub MySQL](https://hub.docker.com/_/mysql) documentation for more details.
  
  Run the following command to create `mysql` container with a root password `root123`_(you can provide any password here)_.
  ```
  docker run --name mysql -e MYSQL_ROOT_PASSWORD=root123 mysql
  ```
  In the output, you can see that MySQL has been initialized successfully and ready to listen for connections. Do not close this window, else the container will be stopped.

* `docker ps`: It is used to get a list of all running containers on the host.
  This command allows to provide various options such as: 
  * `-a` to show all containers whether stopped or running
  * `-l` to show only latest containers
  * `-q` to show only id of the containers.

  Use `docker ps --help` command for complete options.

  **Syntax:**  
  ```
  docker ps
  ```
  or
  ```
  docker container ls
  ```
  or
  ```
  docker container list
  ```
  Open a new **Command Prompt** and run these commands:
  ```
  docker ps
  docker ps -l
  docker ps -a
  docker ps -q
  ```
  
* `docker inspect`: It is used to inspect the Docker containers. For more options, use `docker inspect --help` command.

  **Syntax:**
  ```
  docker inspect <container_id or container_name>
  ```
  **For example:**  
  Run the following command to inspect `mysql` container:
  ```
  docker inspect mysql
  ```
  
* `docker exec`: It allows to execute the commands in the running containers. This command allows to provide various options such as: 
  * `-d` to run command in the background (detached mode)
  * `-e` to set environment variables
  * `-i` to run in interactive mode which keeps STDIN open even when not attached
  * `-t` to allocate a pseudo-TTY
  * `-u` to specify username or UID with or without group or GID
  * `-w` to set the working directory inside the container

  Use `docker exec --help` command for complete options.
  
  **Syntax:**
  ```
  docker exec -it <container_id or container_name> <command>
  ```
  **For example:**  
  Run the following commands to enter into `bash` prompt inside `mysql` container and execute commands:
  ```
  docker exec -it mysql bash
  echo "Hello"
  exit
  ```
  
* `docker attach`: It is used to attach local host standard input, output, and error to the primary process of a running container so that it allows to interact with the process inside the container as if the
  process is running in the terminal. For more options, use `docker attach --help` command.

  **Syntax:**
  ```
  docker attach <container_id or name>
  ```
  or
  ```
  docker container attach <container_id or name>
  ```
  **For example:**  
  First, run the following command to start a new `mysql` container in interactive and detached mode with `bash` process running inside it.
  ```
  docker run -itd --name mysql_bash_it -e MYSQL_ROOT_PASSWORD=root123 mysql bash
  ```

  Then, run the below command to attach the terminal to the new container named `mysql_bash_it` and start interacting with container:
  ```
  docker attach mysql_bash_it
  echo "Hello"
  exit
  ```

* `docker cp`: It is used to copy files between a container and docker host. For more options, use `docker cp --help` command.
  
  **Syntax:**
  ```
  docker cp <local_file_path> <container_name or id>:<container_path>
  ```
  or
  ```
  docker container cp <local_file_path> <container_name or id>:<container_path>
  ```

  Open a new command prompt and run the following command to copy `tmp.txt` file to `mysql` container:
  ```
  docker cp .\tmp.txt mysql:/tmp
  ```
  **For example:**  
  Run the following commands to connect to `mysql` container and verify if the copied file exists:
  ```
  docker exec -it mysql bash
  ls /tmp/tmp.txt
  exit
  ```
 
* `docker diff`: It allows to find the differences between the container’s filesystem and it’s base image. For more options, use `docker diff --help` command.
  
  **Syntax:**
  ```
  docker diff <container_id_or_name>
  ```
  or
  ```
  docker container diff <container_id_or_name>
  ```
  **For example:**  
  Run the following command to see the changes in `mysql` container filesystem:
  ```
  docker diff mysql
  ```

* `docker commit`: It is used to take an image of a running container. When the image is taken, all processes are paused so that the image does not encounter any problems once it is used to create one more
  container. For more options, use `docker commit --help` command.

  **Syntax:**
  ```
  docker commit <container_id_or_name> <image_name_and_or_tag>
  ```
  or
  ```
  docker container commit <container_id_or_name> <image_name_and_or_tag>
  ```
  **For example:**  
  Run the following command to create a new image based on `mysql` container filesystem:
  ```
  docker commit mysql mysql:v1
  ```
   
* `docker export`: It is used to export the container’s file system as a tar archive which can be shared across different hosts. Specify the output file name using `-o` option.

  **Syntax:** 
  ```
  docker export -o <output_file_name> <container_id_or_name>
  ```
  or
  ```
  docker container export -o <output_file_name> <container_id_or_name>
  ```
  **For example:**  
  Run the following command to export `mysql` container filesystem as `mysql_container_export.tar` in the current directory:
  ```
  docker export -o mysql_container_export.tar mysql
  ```

* `docker stats`: It is used to display the live stream of running containers resource usage statistics. This command allows to provide various options such as: 
  * `-a` to show all containers live stream
  * `--no-stream` to disable streaming stats and only pull the first result
  * `--no-trunc` to not truncate output
  
  Use `docker stats --help` command for complete options.

  **Syntax:**
  ```
  docker stats
  ```
  or
  ```
  docker container stats
  ```

* `docker logs`: It is used to fetch the logs of a container. This command allows to provide various options such as: 
  * `--details` to show extra details of logs
  * `-f` to continuously streaming the new output from container’s STDOUT and STDERR
  * `-n` to display number of lines from the end of logs
  * `-t` to show timestamps of logs

  Use `docker logs --help` command for complete options.
    
  **Syntax:**
  ```
  docker logs <container_id_or_name>
  ```
  or
  ```
  docker container logs <container_id_or_name>
  ```
  **For example:**  
  Run the following command to get `mysql` container logs until now:
  ```
  docker logs mysql
  ```

* `docker kill`: It is used to kill one or more running containers by killing all processes abruptly inside the container. For more options, use `docker kill --help` command.

  **Syntax:**
  ```
  docker kill <container_id or name>
  ```
  or
  ```
  docker container kill <container_id or name>
  ```
  **For example:**   
  Run the following command to kill `mysql` container:
  ```
  docker kill mysql
  ```

* `docker start`: It is used to start one or more running containers. For more options, use `docker start --help` command.

  **Syntax:**
  ```
  docker start <container_id or name>
  ```
  or
  ```
  docker container start <container_id or name>
  ```
  **For example:**   
  Run the following command to start `mysql` container:
  ```
  docker start mysql
  ```
  
* `docker wait`: It is used to wait or halt the execution until one or more specified containers have stopped and print their exit codes the logs of a container. 

  **Syntax:**
  ```
  docker wait <container_id_or_name>
  ```
  or
  ```
  docker container wait <container_id_or_name>
  ```
  **For example:**  
  Run the following command to get the exit status of `mysql` container:
  ```
  docker wait mysql
  ```
  In another command prompt, run the following command to kill `mysql` container:
  ```
  docker kill mysql
  ```
  Then, you can see exit code `137` on docker wait terminal.

* `docker stop`: It is used to stop one or more running containers. For more options, use `docker stop --help` command.

  **Syntax:**
  ```
  docker stop <container_id or name>
  ```
  or
  ```
  docker container stop <container_id or name>
  ```
  **For example:**  
  Run the following command to stop `mysql` container:
  ```
  docker stop mysql
  ```
  
* `docker restart`: It is used to stop and start one or more containers. For more options, use `docker restart --help` command.

  **Syntax:**
  ```
  docker restart <container_id or name>
  ```
  or
  ```
  docker container restart <container_id or name>
  ```
  **For example:**  
  Run the following command to restart `mysql` container:
  ```
  docker restart mysql
  ```

* `docker rm`: It is used to delete the specified container. By default, it deletes the container that is not currently running.  
  This command allows to provide various options such as: 
  * `-f` to remove the container forcefully even if it is running
  * `-v` to remove volumes
  * `-l` to remove specific link mentioned

  Use `docker rm --help` command for complete options:
  
  **Syntax:**
  ```
  docker rm <container_name or ID>
  ```
  or
  ```
  docker container rm <container_name or ID>
  ```
  or
  ```
  docker container remove <container_name or ID>
  ```
  **For example:**  
  Run the following command to remove the container named `mysql_bash_it` which is in **Exited** state. If the container is removed successfully, it displays the container name that got deleted.
  ```
  docker rm mysql_bash_it
  ```
  
* `docker container prune`: It removes all stopped containers on the Docker host. For more options, use `docker container prune --help` command.

  **Syntax:**
  ```
  docker container prune
  ```

## 4. Docker Volume Commands
Docker Volume commands are used for data persistence and sharing between containers. They allow to store data independently of container lifecycles. Some of these commands are listed below:
* `docker volume create`: It is used to create a new Docker volume. For more options, use `docker volume create --help` command.

  **Syntax:**
  ```
  docker volume create <volume_name>
  ```
  **For example:**  
  Run the following command to create a new volume named `mysql_volume`:
  ```
  docker volume create mysql_volume
  ```
  
* `docker volume ls`: It is used to list all volumes available on the Docker host. For more options, use `docker volume ls --help` command.

  **Syntax:**
  ```
  docker volume ls
  ```
  or
  ```
  docker volume list
  ```
   
* `docker volume inspect`: It is used to get the details of a specified volume. For more options, use `docker volume inspect --help` command.

  **Syntax:**
  ```
  docker volume inspect <volume_name>
  ```
  **For example:**  
  Run the following command to inspect `mysql_volume`:
  ```
  docker volume inspect mysql_volume
  ```

*` docker volume rm`:  It allows to remove the specified volume from the Docker host. For more options, use `docker volume rm --help` command.
  
  **Syntax:**
  ```
  docker volume rm <volume_name>
  ```
  or
  ```
  docker volume remove <volume_name>
  ```
  **For example:**  
  Run the following command to remove the volume named `mysql_volume`:
  ```
  docker volume rm mysql_volume
  ```
  
* `docker volume prune`: It is used to remove all unused volumes from the Docker host to free up space. For more options, use `docker volume prune --help` command.

  **Syntax:**
  ```
  docker volume prune
  ```

## 5. Docker Network Commands
Docker Network commands are used to attach containers to a network. Some of these commands are listed below:
* `docker network create`: It is used to create a new Docker network. For more options, use `docker network create --help` command.
  
  **Syntax:**
  ```
  docker network create <network_name>
  ```
  **For example:**  
  Run the following command to create a new network named `mynetwork`:
  ```
  docker network create mynetwork
  ```
 
* `docker network ls`: It is used to list all networks created on the Docker host. For more options, use `docker network ls --help` command.

  **Syntax:**
  ```
  docker network ls
  ```
  or
  ```
  docker network list
  ```
  
* `docker network inspect`: It is used to get the details of a specified volume. For more options, use `docker network inspect --help` command.

  **Syntax:** 
  ```
  docker network inspect <network_name>
  ```
  **For example:**  
  Run the following command to inspect `mynetwork`:
  ```
  docker network inspect mynetwork
  ```

* `docker network connect`:  It allows to connect the specified container to a Docker network. For more options, use `docker network connect --help` command.

  **Syntax:**
  ```
  docker network connect <network_name> <container_id or name>
  ```
  **For example:**  
  Run the following command to connect `mysql` container to `mynetwork` network:
  ```
  docker network connect mynetwork mysql
  ```

* `docker network disconnect`:  It allows to disconnect the specified container from the given Docker network. For more options, use `docker network disconnect --help` command.

  **Syntax:**
  ```
  docker network disconnect <network_name> <container_id or name>
  ```
  **For example:**  
  Run the following command to disconnect `mysql` container from `mynetwork` network:
  ```
  docker network disconnect mynetwork mysql
  ```

* `docker network rm`:  It allows to remove the specified network from the Docker host. For more options, use `docker network rm --help` command.

  **Syntax:**
  ```
  docker network rm <volume_name>
  ```
  or
  ```
  docker network remove <volume_name>
  ```
  **For example:**  
  Run the following command to remove `mynetwork`:
  ```
  docker network rm mynetwork
  ```

* `docker network prune`: It is used to remove all unused networks from the Docker host to free up space. For more options, use `docker network prune --help` command.

  **Syntax:**
  ```
  docker network prune
  ```

## 6. Docker Registry Commands
Docker Registry commands are used to work with the configured Docker registry. Some of these commands are listed below:

* `docker login`: It is used to authenticate to a Docker registry. By default, it authenticates to **Docker Hub** using a device code flow which lets to authenticate to Docker Hub without entering the password
  by just visiting a URL and enter the confirmation code and authenticate. For more options, use `docker login --help` command.

  **Syntax:**
  ```
  docker login
  ```
  
  To authenticate with a specific user name and password use `-u` and `-p` options:
  ```
  docker login -u <username> -p <password>
  ```
  **For example:**  
  Run the following command to get authenticated to Docker Hub without providing credentials. It provides a confirmation code and press **Enter** to open the login URL in the browser.
  ```
  docker login
  ```
  * Verify the confirmation code and click on **Confirm** button:
  * You can enter your Docker Hub username or directly login with Google credentials.
  * It then confirms that device is successfully connected.
  * On the command prompt, it displays Login Succeeded message.

* `docker search`: It is used to search the specific image in the Docker Hub. For more options, use `docker search --help` command.

  **Syntax:**
  ```
  docker search <image_name>
  ```
  **For example:**  
  Run the following command to search `mysql` image:
  ```
  docker search mysql
  ```
  
* `docker logout`: It is used to log out from the Docker registry which is Docker Hub by default.

  **Syntax:**
  ```
  docker logout
  ```
<br/>

## 7. Docker Compose Commands:
Docker Compose commands are used to manage multi-container applications.
* `docker compose version`: It is used to display the version information of Docker Compose. For more options, use `docker compose version --help` command.

  **Syntax:**
  ```
  docker compose version
  ```
  
* `docker compose config`: It is used to validate and display the docker compose file configuration. For more options, use `docker compose config --help` command.

  **Syntax:**
  ```
  docker compose config
  ```
  
* `docker compose build`: It is used to build or rebuild services. Once services are built, they are tagged as project-service, by default. For more options, use `docker compose build --help` command.
  
  **Syntax:**
  ```
  docker compose build
  ```

* `docker compose pull`: It is used to pull the latest versions of images associated with a service defined in the Docker Compose file but does not start the containers based on those images.
  For more options, use `docker compose pull --help` command.
  
  **Syntax:**  
  ```
  docker compose pull
  ```  

* `docker compose push`: It is used to push images built locally for services to the respective registry/repository assuming access to the build key. For more options, use `docker compose push --help`
  command.

  **Syntax:**  
  ```
  docker compose push
  ```
  
* `docker compose images`: It is used to list images used by containers. For more options, use `docker compose images --help` command.

  **Syntax:**
  ```
  docker compose images <options>
  ```

* `docker compose create`: It is used to create containers for a service without starting them. For more options, use `docker compose create --help` command.

  **Syntax:**  
  ```
  docker compose create
  ```

* `docker compose containers`: It is used to list containers. For more options, use `docker compose containers --help` command.

  **Syntax:**  
  ```
  docker compose containers
  ```

* `docker compose ps`: It is used to list containers and services including their names, commands, states and ports.

  **Syntax:**
  ```
  docker compose ps
  ```
  
* `docker compose ls`: It is used to list all running compose objects. For more options, use `docker compose ls --help` command.

  **Syntax:**
  ```
  docker compose ls <options>
  ```
  
* `docker compose top`: It is used to display running processes. For more options, use `docker compose top --help` command.

  **Syntax:**
  ```
  docker compose top
  ```
  
* `docker compose run`: It is used to run a one-time command against a service. For more options, use `docker compose run --help` command.

  **Syntax:**
  ```
  docker compose run <options> <service_name> <command>
  ```
  
* `docker compose exec`: It is used to execute a command in a running container. For more options, use `docker compose exec --help` command.

  **Syntax:**
  ```
  docker compose exec <options> <service_name> <command>
  ```
  
* `docker compose logs`: It is used to view log output from containers. For more options, use `docker compose logs --help` command.

  **Syntax:**  
  _To view logs for specified service:_
  ```
  docker compose logs <service_name>
  ```
  _To view logs for all services:_
  ```
  docker compose logs
  ```

* `docker compose pause`: It is used to pause running containers of a service. For more options, use `docker compose pause --help` command.

  **Syntax:**  
  _To pause for specified service:_
  ```
  docker compose pause <service_name>
  ```
  _To pause all services:_
  ```
  docker compose pause
  ```
  
* `docker compose unpause`: It is used to unpause paused containers of a service. For more options, use `docker compose unpause --help` command.

  **Syntax:**  
  _To unpause for specified service:_
  ```
  docker compose unpause <service_name>
  ```
  _To unpause all services:_
  ```
  docker compose unpause
  ```
  
* `docker compose stop`: It is used to stop running containers without removing them. For more options, use `docker compose stop --help` command.

  **Syntax:**  
  _To stop specified service:_
  ```
  docker compose stop <service_name>
  ```
  _To stop all services:_
  ```
  docker compose stop
  ```
  
* `docker compose start`: It is used to start containers for all services or the specified service only. For more options, use `docker compose start --help` command.

  **Syntax:**  
  _To start specified service:_
  ```
  docker compose start <service_name>
  ```
  _To start all services:_
  ```
  docker compose start
  ```
  
* `docker compose restart`: It is used to restart all stopped and running services or the specified services only. For more options, use `docker compose restart --help` command.

  **Syntax:**  
  _To restart specified service:_
  ```
  docker compose restart <service_name>
  ```
  _To restart all services:_
  ```
  docker compose restart
  ```
  
* `docker compose kill`: It is used to force stop running containers. For more options, use `docker compose kill --help` command.

  **Syntax:**  
  _To kill specified service:_
  ```
  docker compose kill <service_name>
  ```
  _To kill all services:_
  ```
  docker compose kill
  ```
  
* `docker compose rm`: It is used to remove stopped service containers. By default, anonymous volumes attached to containers are not removed but can be removed with `-v` option. For more options, use
  `docker compose rm --help` command.

  **Syntax:**
  ```
  docker compose rm
  ```
  
* `docker compose up`: It is used to build, create, start and attach to containers for a service. Once services are built, they are tagged as project-service, by default. For more options, use
  `docker compose up --help` command.

  **Syntax:**
  ```
  docker compose up <options>
  ```
  
* `docker compose down`: It is used to stop and remove images, containers, networks, and volumes created by `docker compose up` command. For more options, use `docker compose down --help` command.

  **Syntax:**
  ```
  docker compose down <options>
  ```

## 8. Docker Swarm Commands:
Docker provides various commands to manage nodes, services and stacks in the Swarm cluster

### 8.1 Docker Swarm Commands:
Docker Swarm commands are used to manage the Docker swarm.
* `docker swarm init`: It is used to initialize a swarm. For more options, use `docker swarm join --help` command. 

  **Syntax:**
  ```
  docker swarm init <options>
  ```
  The node on which this command is executed becomes the manager in the newly created single-node swarm. It generates two random tokens, one is a worker token and other is a manager token. When the new node
  is added to the swarm, the node joins as either a worker or manager based upon the worker or manage token passed.
  
* `docker swarm join`: It is used to add the node to a swarm. The node can join as manager or worker based on the token passed to the `--token` flag. For more options, use `docker swarm join --help` command. 

  **Syntax:**
  ```
  docker swarm join --token <token>
  ```
  
* `docker swarm leave`: It allows the node to leave the swarm. It accepts `--force` option which can be used for a manger to remove from the swarm forcefully but the safe way to remove a manager from a swarm is
  to demote it to a worker and then direct it to leave the swarm. For more options, use `docker swarm leave --help` command.

  **Syntax:**
  ```
  docker swarm leave
  ```
  
* `docker swarm unlock`: It is used to unlock a locked manager using the provided unlock key. The unlock key is printed at the time when auto-lock is enabled, and is also available from the
  `docker swarm unlock-key` command. For more options, use `docker swarm unlock --help` command.

  **Syntax:**
  ```
  docker swarm unlock
  ```
  
* `docker swarm update`: It is used to update the swarm with new parameter values including manager autolocking setting, validity period for node certifications, dispatcher heartbeat period etc.
  For more options, use `docker swarm update --help` command.

  **Syntax:**
  ```
  docker swarm update 
  ```

### 8.2.	Docker Node Commands:
Docker Node commands are used to manage nodes in swarm.
* `docker node ls`: It is used to list all nodes connected in the swarm. For more options, use `docker node ls --help` command.

  **Syntax:**
  ```
  docker node ls
  ```
  
* `docker node ps`: It is used to list tasks that are running on the current node or on the specified node. For more options, use `docker node ps --help` command.

  **Syntax:**
  ```
  docker node ps
  ```
  or
  ```
  docker node ps <node_name>
  ```
  
* `docker node inspect`: It is used to get the detailed information of one or mode nodes. For more options, use `docker node inspect --help` command.

  **Syntax:**
  ```
  docker node inspect <node_name>
  ```
  Use the following command to inspect the current node:
  ```
  docker node inspect self
  ```

* `docker node promote`: It is used to promote a node to manager. For more options, use `docker node promote --help` command.

  **Syntax:**
  ```
  docker node promote <node_name>
  ```
  
* `docker node demote`: It is used to demote a node from the existing manager so that it is no longer a manager in a swarm. For more options, use `docker node demote --help` command.

  **Syntax:**
  ```
  docker node demote <node_name>
  ```
  
* `docker node update`:  It is used to update the node with new parameter values. For more options, use `docker node update --help` command.

  **Syntax:**
  ```
  docker node update <options> <node_name>
  ```
  
* `docker node rm`:  It allows to remove the specified node from the Docker swarm. For more options, use `docker node rm --help` command.

  **Syntax:**
  ```
  docker node rm <node_name>
  ```

### 8.3. Docker Service Commands:
Docker Service commands are used to manage the services in swarm.

* `docker service create`: It is used to create a new service as described by the specific parameter passed. For more options, use `docker service create --help` command.

  **Syntax:**
  ```
  docker service create <options>
  ```

* `docker service ls`: It is used to list all services running in the swarm. For more options, use `docker service ls --help` command.

  **Syntax:**
  ```
  docker service ls
  ```

* `docker service ps`: It is used to list tasks that are running under specified services in the swarm. For more options, use `docker service ps --help` command.

  **Syntax:**
  ```
  docker service ps <service_name>
  ```

* `docker service inspect`: It is used to get the details of a specified service. For more options, use `docker service inspect --help` command.

  **Syntax:**
  ```
  docker service inspect <service_name>
  ```

* `docker service logs`: It is used to fetch the logs of a container. For more options, use `docker service logs --help` command.

  **Syntax:**
  ```
  docker service logs <service_name>
  ```
  
* `docker service update`:  It is used to update the service with new parameter values. The parameters are the same as `docker service create` command. For more options, use
  `docker service update --help` command.

  **Syntax:**
  ```
  docker service update <service_name> <options>
  ```
  
* `docker service scale`:  It is used to scale one or more replicated services. For more options, use `docker service scale --help` command.

  **Syntax:**
  ```
  docker service scale <service_name>=<number_of_replicas>
  ```
  
* `docker service rollback`:  It is used to rollback changes to the service’s configuration. For more options, use `docker service rollback --help` command.

  **Syntax:**
  ```
  docker service rollback <service_name>
  ```
  
* `docker service rm`:  It allows to remove the specified service from the Docker swarm. For more options, use `docker service rm --help` command.

  **Syntax:**
  ```
  docker service rm <service_name>
  ```

### 8.4. Docker Secret Commands:
Docker Secret commands are used to manage the swarm secrets.

* `docker secret create`: It is used to create a secret from a file or from user input. For more options, use `docker secret create --help` command.

  **Syntax:**
  ```  
  docker secret create <secrete_name> <file>
  ```
  
* `docker secret ls`: It is used to list all secrets created in the swarm. This command must be executed on the manager node to get the list of all secrets. For more options, use `docker secret ls --help`
  command.

  **Syntax:**
  ```
  docker secret ls
  ```
  
* `docker secret inspect`: It is used to get the detailed information of a specified secret. For more options, use `docker secret inspect --help` command.

  **Syntax:**
  ```
  docker secret inspect <secret_name>
  ```
* `docker secret rm`:  It allows to remove the specified secret from the Docker swarm. For more options, use `docker secret rm --help` command.

  **Syntax:**
  ```
  docker secret rm <secret_name>
  ```

### 8.5. Docker Stack Commands:
Docker Stack commands are used to manage the Swarm stacks.
  
* `docker stack config`: It is used to output the final Compose file after doing merges and interpolations of the specified compose files. For more options, use `docker stack config --help` command.

  **Syntax:**
  ```
  docker stack config -c <compose_file>
  ```
  
* `docker stack deploy`: It is used to create a new stack or update existing stack in Docker Swarm as described by the specific parameters passed. For more options, use `docker stack deploy --help` command.

  **Syntax:**
  ```
  docker stack deploy -c <compose_file> <options>
  ```
  If the configuration is split between multiple Compose files such as a base configuration and environment-specific overrides, you can provide multiple `--compose-file` flags as below:
  ```
  docker stack deploy --compose-file docker-compose.yml -c docker-compose.prod.yml service_name
  ```
  
* `docker stack ls`: It is used to list all stacks available in the swarm. For more options, use `docker stack ls --help` command.

  **Syntax:**
  ```
  docker stack ls
  ```
  
* `docker stack ps`: It is used to list all tasks running as part of specified stack available in the swarm. For more options, use `docker stack ps --help` command.

  **Syntax:**
  ```
  docker stack ps <stack_name>
  ```
  
* `docker stack services`: It is used to list all services running as part of specified stack available in the swarm. For more options, use `docker stack services --help` command.

  **Syntax:**
  ```
  docker stack service <stack_name>
  ```
  
* `docker stack rm`:  It allows to remove the specified stack and its associated components including services, networks and secrets from the Docker swarm. For more options, use
  `docker stack rm --help` command.

  **Syntax:**
  ```
  docker stack rm <stack_name>
  ```
  
