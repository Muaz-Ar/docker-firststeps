# In the first step we only start a Container with the  Image nginx Image

-- mkdir <foldername>
-- cd <foldername>

--  docker container run --rm --detach --name default-nginx --publish 8080:80 nginx

# --rm : if you stop the Container  will be delet
# --detach : it´s running in the background 
# --name : We give the Container a Name 
# --publish : it opens a port for the cominication <Port for hostsystem>:<Port of the Container> 
# --nginx : Image 

# We want to build an Image from a source. this shoud start Nginx automatically running
# We need an Dockerfile with sources how has the instructions for our image 

-- vi Dockerfile                                # we put thies inside 
    -->  1 FROM ubuntu:laest                      # Every Dockerfile beginns with FROM the basic image for oure 
  2                                               # result image <bios>:<version>
  3 EXPOSE 80                                     # indicate our Port that need for publish 
  4
  5 RUN apt-get update && \                       #RUN is an comand to executes inside of an Container 
  6     apt-get install nginx -y && \               
  7     apt-get clean && rm -rf /var/lib/apt/lists/* # to clean our Image from package cache 
  8
  9 CMD ["nginx", "-g", "deamon off;"]            # this is an exec comand CMD executes the nginx commant in the shell 

# to build an Image you can youse the same commands options like to build an Container 
-- docker image <command> <options> <PATHFILE> #in oure case build

[+] Building 1.9s (4/5)                                                                                                                      docker:default
 => [internal] load .dockerignore                                                                                                                      0.0s
 => => transferring context: 2B                                                                                                                        0.0s
 => [internal] load build definition from Dockerfile                                                                                                   0.0s
[+] Building 10.5s (6/6) FINISHED                                                               docker:default
 => [internal] load .dockerignore                                                                         0.0s
 => => transferring context: 2B                                                                           0.0s
 => [internal] load build definition from Dockerfile                                                      0.0s
 => => transferring dockerfile: 213B                                                                      0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                          0.0s
 => CACHED [1/2] FROM docker.io/library/ubuntu:latest                                                     0.0s/ => [2/2] RUN apt-get update &&     apt-get install nginx -y &&     apt-get clean && rm -rf /var/lib/ap  10.2s
 => exporting to image                                                                                    0.2s
 => => exporting layers                                                                                   0.2s
 => => writing image sha256:b13749864f93c8f244feaf2450886df157ddb4880389fb85b82cccabbaf1408c              0.0s

# your terminal shows this an you get the Image sha256 =  b13749864f93c8f244feaf2450886df157ddb4880389fb85b82cccabbaf1408c
# now you can start your Container with run 
-- docker container run --rm --detach --name my-first-Image --publish 3080:80 b13749864f93c8f244fe............