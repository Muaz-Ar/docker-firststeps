# Work with Bind Mounts means: If we change somting localy it will be change at the Homepage automaticly 
# with Bind Mounts you can easily mount one of your local file system directory inside a container 
# for thos we yous volumes 
--volume <local file system directory absolute path>:<container file system directory absolute path>:<read write access>

# for oure case 
docker container run \
    --rm \
    --publish 3000:3000 \
    --name hello-dock-dev \
    --volume $(pwd):/home/node/app \   #with volume pwd:... you say that the container can use all thinks in the pwd file 
    hello-dock:dev1

# but this ar not working we need anonym Volumes the syntax  
--volume <container file system directory absolute path>:<read write access>
docker container run \
    --rm \
    --detach \
    --publish 3000:3000 \
    --name hello-dock-dev \
    --volume $(pwd):/home/node/app \       #with volume pwd:... you say that the container can use all thinks in the pwd file
    --volume /home/node/app/node_modules \ # now container gets information from node_modules
    hello-dock:dev