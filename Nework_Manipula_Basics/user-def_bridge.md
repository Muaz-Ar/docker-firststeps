# NETWORK ID     NAME      DRIVER    SCOPE
# c2e59f2b96bd   bridge    bridge    local
# 124dccee067f   host      host      local
# 506e3822bf1f   none      null      local

# all containers you create wit docker gets automaticly an bridge Network 
# now create an container and look #

docker container run --rm --detach --name hello-dock --publish 8080:80 fhsinchy/hello-dock
# a37f723dad3ae793ce40f97eb6bb236761baa92d72a2c27c24fc7fda0756657d

docker network inspect --format='{{range .Containers}}{{.Name}}{{end}}' bridge
# hello-dock

# Container how are concted to the Bridg network can comunicate to eachother using the ip adress
# container ho has a user defined brigt can comunicaate over the networkname, there are better isolated and can be attached and detached from user-defined networks on the fly. 

# with the command docker network ctreate you can an network 
-- docker network create <network name> 
docker network ls
NETWORK ID     NAME                                          DRIVER    SCOPE
4fdc2bd74bc1   bridge                                        bridge    local
c5708dd2d26d   fullstack-notes-application-network-backend   bridge    local
e66ec3bc59c5   host                                          host      local
4c42a303206c   none                                          null      local
bdb9eea8021c   skynet                                        bridge    local



