# The syntax for detaching a Network are 
# --network disconnect <network identifier> <container identifier>
# for example 
--docker network disconnect skynet hello-dock

# to delete the network we can you docker network rm <network identifier>
# for us 
-- docker network rm skynet 
# we can also use the network prune command to remove any unused networks from your system. The command also has the -f or --force and -a or --all options