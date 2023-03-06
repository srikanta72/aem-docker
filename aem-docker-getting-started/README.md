# AEM & Docker getting started guide

Getting started guide for development with [Adobe Experience Manager](https://www.adobe.com/nl/marketing-cloud/experience-manager.html) together with Docker. The configuration contains an AEM author, publisher and dispatcher environment, running in three separate containers. Docker images also have support for installing AEM packages during build.

## Note : 
In case you are using the AEM as cloud please follow below link to setting up the default dispatcher as part of the cloud.
[Dispatcher Docker](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html)

## Prerequisites

This tutorial assumes running on a Mac. Installation on Windows might differ for certain steps. The following items are required:

- [Docker](https://www.docker.com) with at least 4GB memory allocated (Recommended for 8GB)
- AEM installation file, name it `aem-quickstart.jar`. **Name has to match as mentioned**. 
- AEM license file, named `license.properties`.  **Name has to match as mentioned**. 
- Recommended: [Homebrew](https://brew.sh) package manager

## Getting started: running AEM

1. Clone this repository to a local directory and put the AEM installation file, license file in the root.
2. Put AEM quickstart jar file in `./aem_instance/` 
3. Put AEM packages that need to be installed during build in `./aem_packages/`. Order of installation will be alphabetically, based on package file name.
4. run `start-aem-docker.sh` 
or 
5. 
- Build the Docker images with `docker build -t aem-base -f base/Dockerfile . && docker-compose build` inside "aem-docker-getting-started" folder. This will take time depending on the number of packages, as the author and publisher are started during build to be able to install packages.
- Start the Docker containers with `docker-compose up`. This will also mount the `./logs` directory on your local system to the containers, so you have easy access to the logs of all containers.

6. Wait until AEM has fully started. To check for the author, open the [bundles page](http://localhost:4502/system/console/bundles) and when all bundle status are either `Active` or `Fragment` the AEM environment has fully started.
7. 
Author URL: [http://localhost:4502](http://localhost:4502)
username: `admin` 
password: `admin`
Dispatcher URL: [http://localhost](http://localhost)
Publisher: [http://localhost:4503](http://localhost:4503)

~ Starting and stopping containers preserves AEM content. 
~ Images need to be rebuild when changing packages in the `aem_packages` directories.
~ After stopping a container, or after a system reboot, you can use `docker-compose up` to start the containers.

to Start use `start-aem-docker.sh` and to reset,delete everything use `reset-aem-docker.sh`
## Folder Structure
```
/aem-docker-getting-started
  |- aem_instance
  |  |- aem-quickstart.jar
  |  |- license.properties
  |- aem_packages
  |  |- aem-service-pkg-6.5.2.zip
  |- base
  |  |- Dockerfile
  |- author
  |  |- Dockerfile
  |- publish
  |  |- Dockerfile
  |- dispatcher
  |  |- Dockerfile and other files
  |- logs
  |- other files as per this repo

```

## Getting started: set-up development environment

1. Install Java 8/11 SDK: 
For MAC: `brew cask install java8/11`. 
For Windows use installer version .msi/.exe file and set up the Environment path.
2. Install Maven: 
For MAC: `brew install maven`. 
For windows: Download the bin file form apache maven and follow environment path setup.
3. Download and install IntelliJ IDEA from [JetBrains](https://www.jetbrains.com/idea/download) or install with `brew cask install caskroom/cask/intellij-idea-ce`.
4. Clone the [AEM WKND Sites](https://github.com/adobe/aem-guides-wknd) repository to a local directory.
5. Open the folder with the AEM WKND Sites sample in IntelliJ. In IntelliJ, click on the right-top corner on the dropdown and select `Edit Configurations`. Add a `New Configuration` with the plus-icon on the top-left corner, select `Maven`. Set the name as `Deploy author`, set the working directory as `aem-guides-wknd`, command line `clean install -e` and profiles `autoInstallPackage`. Now save the configuration.
6. Click on the play button on the top-right corner to run the `Deploy author` configuration. You might get an error that the Java JDK can't be found: `Project JDK is not specified`. When this occurs, click on `Configure` next to the error and specify the location of your Java SDK (for instance, `/Library/Java/JavaVirtualMachines/jdk1.8.0_162.jdk/`). Now try again to run the `Deploy author` configuration and you should see a success message.
7. Navigate to the [AEM Package Manager](http://localhost:4502/crx/packmgr/index.jsp) and you should see the `aem-guides-wknd.*` packages on top of the list.

## Other tools

- [aem-front](https://github.com/kevinweber/aem-front) can be used to significantly speed-up your AEM front-end development workflow, as code changes will hot-reload in your browser.

## Docker commands you may require
- `docker ps` for checking the docker/container status
- `docker container ls -a` shows all available docker containers
- `docker container rm <container id1> <container id2>` to delete a container(s).
- `docker images` shows list of docker images available.
- `docker rmi <image id1> <image id2>` to delete image(s)
- `docker-compose build` to build the container with docker-compose yaml file.
- `docker-compose up` to start runiing all the docker containers with docker-compose.
- `docker start <container id> or docker stop <container id>` to start/stop a container. 
- `docker stop <container id> or docker stop <container id>` to start/stop a container. 
- `docker build -t aem-test .` build a docker image out of the Dockerfile at current directory. `"."` symbol is mandtory for docker build command.
- `docker exec -it <container id> /bin/bash` to access docker container from terminal window. Use `CTRL+D` to exit the terminal.

## Credits

Inspiration and code examples are taken from the following projects:

- [https://github.com/remcorakers/aem-docker-getting-started](https://github.com/remcorakers/aem-docker-getting-started)
- [https://github.com/AdobeAtAdobe/aem_6-1_docker](https://github.com/AdobeAtAdobe/aem_6-1_docker)
- [https://hub.docker.com/r/ggotti/aem-base](https://hub.docker.com/r/ggotti/aem-base)
- [https://github.com/adfinis-sygroup/aem-docker](https://github.com/adfinis-sygroup/aem-docker)
