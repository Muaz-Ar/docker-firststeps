# Performin Multi-Staged Builds 
# in the dev mod we need the Hot-Reload-Function but not in the production Mode 
# So to create an image where the application runs in production mode, you can take the following steps:

# 1. --> Use node as the base image and build the application.
# 2. --> Install nginx inside the node image and use that to serve the static files.

# now we Use node image as the base and build the application. Copy the files created using the node image to a nginx image.
# Create the final image based on nginx and discard all node related stuff.

FROM node:lts-alpine as builder  # The basic Image an as builder assigns a name to this stage so that it can be refferd to later on

WORKDIR /app                

COPY ./package.json ./
RUN npm install

COPY . .
RUN npm run build

FROM nginx:stable-alpine        # Line 11 starts the second stage of the build using nginx:stable-alpine as the base image.

EXPOSE 80

COPY --from=builder /app/dist /usr/share/nginx/html

--docker image build --tag hello-dock:prod .
