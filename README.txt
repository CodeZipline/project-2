SET UP:
    A file .env must be made with the desired endpoint ports for each server to know and pull from the operating system.  
DOCKER:
    Due to usage of relative paths inside the go files, the Dockerfile build must be called within the directory to function.
        Commands:
            // Create a docker volume to be shared between host machine and container
            sudo docker volume create --name [volumeName] 
                - In this case we use:  sudo docker volume create --name myDB
            // Create a docker image of alpine with a badger BD hosted on 8081, located in the /app folder in the container
                - The settings for the docker file is set up and will be executed with: docker build .
            // Create a container with the volume attach
            sudo docker run -it --name [containerName] -v [volumeName]:[containersDirectory] [osDistribution] [applicationOnStartUp]
                - In this case we use:  sudo docker run -it --name dbserver -v myDB:/badger alpine /bin/bash

