# If you've been working with git for some time now, you may know about the .gitignore files in projects, containing a list of files and directories to be excluded from the repository. Well Docker has a similar concept. The .dockerignore file contains a list of files and directories to be excluded from image builds. You can find a pre-created .dockerignore file in the hello-dock directory.

.git
*Dockerfile*
*docker-compose*

# node_modules
# This .dockerignore file has to be in the build context. Files and directories mentioned here will be ignored by the COPY instruction but if you do a bind mount, the .dockerignore file will have no effect. I've added .dockerignore files where necessary in the project repository.