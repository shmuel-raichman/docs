##### B"H
# Configure docker
To be able to pull images from our private registry server.
Create file `/etc/docker/daemon.json`
And put this block in
```json
{                                                                                          
  "insecure-registries": ["${registry-host}:${registry-port}"],      
  "registry-mirrors": ["http://${registry-host}:${registry-port}"]   
}                                                            
```
Test if you can pull images:
```bash
docker run dockerhub/hello-world
```
expected output:
```
Unable to find image 'dockerhub/hello-world:latest' locally                      
latest: Pulling from dockerhub/hello-world                                       
1b930d010525: Pull complete                                                      
Digest: sha256:92c7f9c92844bbbb5d0a101b22f7c2a7949e40f8ea90c8b3bc396879d95e899a  
Status: Downloaded newer image for dockerhub/hello-world:latest                  
                                                                                 
Hello from Docker!                                                               
This message shows that your installation appears to be working correctly.       
                                                                                 
To generate this message, Docker took the following steps:                       
 1. The Docker client contacted the Docker daemon.                               
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.        
    (amd64)                                                                      
 3. The Docker daemon created a new container from that image which runs the     
    executable that produces the output you are currently reading.               
 4. The Docker daemon streamed that output to the Docker client, which sent it   
    to your terminal.                                                            
                                                                                 
To try something more ambitious, you can run an Ubuntu container with:           
 $ docker run -it ubuntu bash                                                    
                                                                                 
Share images, automate workflows, and more with a free Docker ID:                
 https://hub.docker.com/                                                         
                                                                                 
For more examples and ideas, visit:                                              
 https://docs.docker.com/get-started/                                            
 ```
