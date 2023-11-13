# Containerizing a JavaScript Application 
# The JavaScript code for this task can be found heare
# what we will do 
# Get a good base image for running JavaScript applications i.e. node.
# Set the default working directory inside the image.
# Copy the package.json file into the image.
# Install necessary dependencies.
# Copy rest of the project files.
# Start the vite development server by executing npm run dev command.

-- touch Dockerfile.dev 
-- vi Dockerfile.dev

FROM node:lts-alpine        # nodejs and use the lts-alpine tab https://hub.docker.com/_/node

EXPOSE 3000                 

USER node                   # here the USER if you put nothing it well be used as ROOT and thats not safety 

RUN mkdir -p /home/node/app # kreate an file app for an normal Linux 

WORKDIR /home/node/app     # all coming direktorys workt now in this folder bwcous we say everything will be happen in the app file

COPY ./package.json .  # Copy the package.json in /home/node/app

RUN npm install        #also this comand in app 

COPY . .               # Copy all other folders . for the folder . for the direktion 

CMD [ "npm", "run", "dev" ] # 

-- docker image build --file Dockerfile.dev --tag hello-dock:dev .
# we use file Dockerfile.dev becous we don´t use the standard Dockerfile
# for the run command we will take 
-- docker container run \
    --rm \
    --detach \
    --publish 3000:3000 \
    --name hello-dock-dev \
    hello-dock:dev1 
# as you can see we´re writing line by line, and that´s done using the \ 
# now oure aplication is runnin at localhost:3000 or http://127.0.0.1:3000 it´s the same  