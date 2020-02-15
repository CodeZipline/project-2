SET UP:
    A file .env must be made with the desired endpoint PORTs,(B_ORIGIN_PORT) for each server to know and pull from the operating system.  
    A config.json file will be parse to become a struct for provisioning the setting for database start up.
DOCKER: Due to usage of relative paths inside the go files, the Dockerfile build must be called within the directory to function.
    
    Commands for execution of the container:
    
        // Create a docker volume to be shared between host machine and container
        sudo docker volume create --name [volumeName] 
        - In this case we use:  sudo docker volume create --name myDB
    
        // Create a docker image with a tag for dockerhub, with the format of [userName]/[repositoryName].
            - The settings for the docker file is set up and will be executed with: docker build -t codezipline/dbserver ./cmd
    
        // Create a daemon apline container with the volume, dbserver, attach, to /badger in the container, on port 8081
        sudo docker run -it --name [containerName] -v [volumeName]:[containersDirectory] [osDistribution] [applicationOnStartUp]
            - In this case we use:  sudo docker run -it --expose 8081 --name dbserverContainer -v myDB:/app/badger codezipline/dbserver
    
    Commands:
    
    // Obtain ip address of the container with Container_Name, in this example it is dbserverContainer
    sudo docker inspect -f "{{ .NetworkSettings.IPAddress }}" dbserverContainer


