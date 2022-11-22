# Instructions
## pre-requisite
1. Install Docker 
2. Your publish instance should be running on localhost:4503. If not you can change the values in "dispatcher.any" file.
3. Follow the instructions peacfully.

## Run the below commands one by one to use
1. Create an docker image 
``
docker build -t di .
``
"di" is name of image
"." is mandatory at end followed by space and denotes current directory.

2. Create container and run the dispatcher 
``
docker container run --publish 8080:80 --detach --name dc di
``
"dc" is name of container 
"di" is reference to existing image

3. Check `http://localhost:8080` in your browser.

4. If you want to ssh to your dispatcher to check the details
``
docker exec -it dc /bin/bash
``
"dc" is reference to container name 

5. If you want to check the logs in case of any issue facing while starting the docker
``
docker logs dc
``
check docker logs for container name "dc"

6. Try `docker ps` to check docker container running status.

### For more info about maintaining dispatcher look in to 
1. Adobe doc: https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html .
2. For cloud: https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html

# Note : 
1. The below code is at dispatcher.any file near to line 30-45.
```
#The load will be balanced among these render instances
/renders
{
    /rend01
    {
        # Hostname or IP of the render
        #/hostname localhost                #<<<--- 1. Enable this incase you are not using docker
        # Hostname or IP of the render in case docker access to Host localhost
        /hostname host.docker.internal      #<<<--- 2. Disable this incase you are not using docker
        # Port of the render
        /port "4503"
        # Connect timeout in milliseconds, 0 to wait indefinitely
        # /timeout "0"
    }
}
```
In the above code the host name is "host.docker.internal" used for docker to access host's localhost IP. 
The config needs modification as mentioned in above comments (1 and 2) to point to any external IP. 

# important:
1. `httpd` folder contains all sample files and do not replace with servers /etc/httpd folder!