# There are two way to ataching a Container with a network 

# the first way is to youse the network connect command. the syntax are 
# docker network connect <network identifier> <container identifier> 

# in oure example 
-- docker network connect skynet hello-dock

# after them we yuse 
docker network inspect --format='{{range .Containers}} {{.Name}} {{end}}' skynet
# and het hello-dock the right result 
docker network inspect --format='{{range .Containers}} {{.Name}} {{end}}' bridge
hello-dock 
# and the same in the bridge network 

# The second way is to use the --network <network identifier> option if you use the run command 
# for example 
-- docker container run --network skynet --rm --name alpine-box -it alpine sh
/ # ping hello-dock
PING hello-dock (172.19.0.2): 56 data bytes
64 bytes from 172.19.0.2: seq=0 ttl=64 time=2.664 ms
64 bytes from 172.19.0.2: seq=1 ttl=64 time=0.098 ms
64 bytes from 172.19.0.2: seq=2 ttl=64 time=0.209 ms
64 bytes from 172.19.0.2: seq=3 ttl=64 time=0.188 ms
64 bytes from 172.19.0.2: seq=4 ttl=64 time=0.220 ms
