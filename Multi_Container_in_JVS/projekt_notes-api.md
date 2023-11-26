# In this Projekt we will have to containers and we will connect them with the Network
# Also we will have enviroment variables and learn to named volumes 

# Oure fist step is to attach an user definied bridge Network <notes-api-network 
-- docker network create notes-api-network 

# The Database server for this Projekt is an ProstgreSPL- Server and youse the official Prostgres Image
# For thies Image we need the envirement variables for the: 
# - POSTGRES_PASSWORD = you must use thist its in the documentation 
# - POSTGRES_DB : you have a name for the Standart DAtabase 
# - PostgreSQL listens on port 5432 you need to publish that as well 

docker container run \
    --detach \
    --name=notes-db \
    --env POSTGRES_DB=notesdb \
    --env POSTGRES_PASSWORD=secret \
    --network=notes-api-network \
    postgres:12

#  20:00 ╰─ docker container ls -all
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS          PORTS      NAMES
b4c551ff94e4   postgres:12   "docker-entrypoint.s…"   13 seconds ago   Up 12 seconds   5432/tcp   notes-db

# Databases as PostgreSQL, MongoDB und MySQL use the file-System save there data 
# PostgreSQL use the /var/lib/postgresql/data file 
# but now we must named oure Volume if we don´t want to lose data if somtihng will be happen 
# with the container 

            <-------------- Working With Named VOlumes --------------->

# With named Volumes we can work becours there are locical Objekts you can work on the CLI 
-- docker volume create <volume name> 
# now we put past command on the cli to create oure volume 
-- docker volume create notes-db-api 
# to controll it -- docker volume ls 

# This volume can now be mounted to /var/lib/postgresql/data inside the notes-db container. To do so, stop and remove the notes-db container
 
1. -- docker container stop notes-db
2. -- docker container rm notes-db

docker container run \
    --detach \
    --volume notes-db-data:/var/lib/postgresql/data \
    --name=notes-db \
    --env POSTGRES_DB=notesdb \
    --env POSTGRES_PASSWORD=secret \
    --network=notes-api-network \
    postgres:12

# we Inspect the container 
docker container inspect --format='{{range .Mounts}} {{ .Name }} {{end}}' notes-db
# Now the data will be safely stored inside the notes-db-data volume and can be reused in the futurean see that everytihng is ok and we can refrubish    

        <---------------- Accessing Logs From a Container ----------------->

# with docker container logs <conterneir identifier> you can look too the logs of your container 
-- docker container logs notes-db 

        <---------------- Attaching the Database Server ----------------->

# first we check is the notes-api-netwoer connected. We will do this with :
-- docker network inspect --format='{{range .Containers}}{{.Name}}{{end}}' notes-api-network
# if ther is no connection we can conect this with the command 
-- docker network connect notes-api-network notes-db

