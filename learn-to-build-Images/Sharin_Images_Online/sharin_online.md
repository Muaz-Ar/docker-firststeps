# First create an accound at Docker 
# then login on Docker-hub desktop 
--docker login       Authenticating with existing credentials...    Login Succeeded

# to share you Image it must to be tagged  <docker hub username>/<image name>:<image tag> .
docker image build tag <reponame>:<image tag> <username>/<repo name>:<image tag> . 

docker image push <username>/<image repository>:<image tag>
