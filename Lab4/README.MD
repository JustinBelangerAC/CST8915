# Lab 4
My youtube video link: https://www.youtube.com/watch?v=bhgZstem1Nk&feature=youtu.be 

1. What are the main differences between a Docker image and a Docker container?
    - A docker image is a binary file that was created based on the configurations in a cocker file, images can be built on top of other images, you can fetch images from a registry like DockerHub
    - a docker container is a running instance of the docker image
2. Explain how Docker's layered architecture improves efficiency.
    - the layered architecture lets us re-use layers that are the same between multiple docker containers. 
    - if we run multiple containers that are built on / expand upon an image that was already created, the layers that are the same are shared lowering the amount of space that the docker images use up
3. Why does each container get its own writable layer?
    - they do this so that they can make changes in their own container without affecting the other containers. this lets the containers store data that is based on their own instance
4. What are the benefits of using Docker Compose over running containers individually?
    - This greatly reduces the amount of time that is required to run multiple containers
    - we can run every container that is needed from the same compose file with a single command
