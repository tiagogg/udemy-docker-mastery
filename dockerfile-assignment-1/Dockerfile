# Overview of this assignment
# use the instructions from developer below to create a working Dockerfile
# feel free to add command inline below or use a new file, up to you (but must be named Dockerfile)
# once Dockerfile builds correctly, start container locally to make sure it works on http://localhost
# then ensure image is named properly for your Docker Hub account with a new repo name
# push to Docker Hub, then go to https://hub.docker.com and verify
# then remove local image from cache
# then start a new container from your Hub image, and watch how it auto downloads and runs
# test again that it works at http://localhost


# Instructions from the app developer
# - you should use the 'node' official image, with the alpine 6.x branch
# The oldest branch on node is alpine 8.x, so I used that one
FROM node:8-alpine
# - this app listens on port 3000, but the container should launch on port 80
  #  so it will respond to http://localhost:80 on your computer
EXPOSE 3000
# - then it should use alpine package manager to install tini: 'apk add --update tini'
RUN apk add --update tini
# - then it should create directory /usr/src/app for app files with 'mkdir -p /usr/src/app'
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
# - Node uses a "package manager", so it needs to copy in package.json file
COPY package.json package.json
# - then it needs to run 'npm install' to install dependencies from that file
# - to keep it clean and small, run 'npm cache clean --force' after above
# Best practice to run the clean on the same RUN as the installation
#   -> we only get 1 image layer -> less image space!
RUN npm install \
    && npm cache clean --force
# - then it needs to copy in all files from current directory
COPY . .
# - then it needs to start container with command '/sbin/tini -- node ./bin/www'
CMD [ "tini", "--", "node", "./bin/www" ]