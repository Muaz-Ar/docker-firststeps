# to generate custom identifiers for images wit --tag or -t 
-- syntax is docker image build --tag <image repository>:<image tag> 
# in oure case 

docker image build --tag my-first-image:V1.1 .

# to run the Image 
docker container run --rm --detach --publish --name first-container1.1 my-first-image:V1.1 

# if you forgot to tag an Image you can do it with the image tag 
-- syntax docker image tag <image id> <image repository>:<image tag>

# if you want to rename your Image you can also use the image tag 
-- syntax docker image tag <image repository>:<image tag> <new image repository>:<new image tag>

# for the Listening of Images you need 
-- docker image ls

# delete the image 
-- docker image rm <image id> / <image tag>

# with docker image prune you can clean up all un-tagged dangling images as follws 
# The --force or -f option skips any confirmation questions. You can also use the --all or -a option to remove all cached   images in your local registry

# docker image history <Image repository>