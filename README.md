


# docker-prunpinpointing-experiments

Docker image for pruning pinpointing experiments.
It runs a simple HTTP server using which the experiments can be started.

# Prerequisites: 

- [docker](https://www.docker.com) for running the experiments container
- [java v.8+](http://java.com) and [maven v.3+](https://maven.apache.org/) for compiling the docker image

# How to build

1. Clone the repository
   ```
   git clone https://github.com/marnadir/docker-prunpinpointing-experiments.git
   ```

1. Invoke the following command in the root directory of the repository:
    ```
    mvn clean install docker:build
    ```
    This command will create a docker image with name 'liveontologies/pinpointing',
    from which docker containers can be created and started.

# How to run

1. Invoke the following command:

    ```
    mvn docker:start
    ```

    This creates and runs the container with the experiments called
    `pinpointing-container`, which is accessible on the port `3030`.
    
    Alternatively, one can create and start the container using the 
    docker command shown in [Quick Start](#quick-start).
    There one can also change the port value `3030` or the name 
    `pinpointing-container` to different values.
    
    If access to the files generated by the experiments is needed, the following
    option can be added to the command shown in [Quick Start](#quick-start)
    before the last argument:
    ```
    --mount type=bind,source=/absolute/path/on/host/machine,target=/home/pinpointing/workspace
    ```
    The directory under `/absolute/path/on/host/machine` must exist. The
    experiments will save all the generated files into it and then they can be
    accessed from the host machine. According to the
    [Docker documentation](https://docs.docker.com/engine/admin/volumes/) this
    is a better solution than leaving the files in the container. Potential
    problem is that this is a huge amount of small files, so if they are not
    removed after the experiments, there may be space problems on the host
    machine. If this option is not used, generated files are removed when the
    container is removed.

1. Point your browser to the address of the host machine with the configured port,
    e.g., http://localhost:3030/.
    
    If the server is not available, or there are other problems, one can inspect the
    container output log using
    ```
    docker logs pinpointing-container
    ```

1. Use the web interface to configure and run the experiments.

   While the container is running, one can connect to it from the shell,
   which is useful for inspecting the files in case of problems:

    ```
    docker exec -it pinpointing-container bash
    ```

 1. To stop the web server run:

    ```
    mvn docker:stop
    ```    
    
    If the contaner was started using the docker command, use:
    
    ```
    docker stop pinpointing-container
    ```
    
    Replace the name accordingly. To see all running use:
    
    ```
    docker ps
    ```
    
 1. To remove the container in case it is no longer needed run:
 
    ```
    mvn docker:remove
    ```
    
    or using the docker command:
    
    ```
    docker rm -v pinpointing-container
    ```
    
    Removing the container may take asome time. Please be patient.
    To see all available containers use:
    
    ```
    docker ps -a
    ```    
    
# See also

  - A complete list of [maven docker commands](https://dmp.fabric8.io/#maven-goals)
  - Run `docker --help`
  - Official [docker documentation](https://docs.docker.com)
  
