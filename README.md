# otrs-nginx
Nginx Alpine docker container with OTRS configuration included.

This image is based on the official nginx alpine image and is mainly included as a demonstration or quick-start to get you up and running. The included config files are an example of how to serve OTRS' static web content and how to proxy the perl files to the otrs-fcgi container. This image could be swapped out for your own nginx image or other frontend webserver that supports fast-cgi passing, or used in conjunction with another webserver running SSL for example.

## How to deploy

Please see my main [otrs-docker][1] repository for full instructions and the docker-compose file that automates the deployment of these images.

If you would like to run this image manually for testing purposes, then this docker run command will start it in the same way as the docker-compose file:
```
docker run -dt --restart unless-stopped --name otrs-nginx --mount source=otrs-config,target=/data --mount source=otrs-dir,target=/opt/otrs --network otrs-backend snw35/otrs-nginx:latest
```
Note that you will need the otrs-fcgi container for the required volumes, the OTRS installation files, and the fast-CGI process for nginx to pass the perl scripts to for execution.

## Building

If you would like to build this image yourself, then the process is straightforward: simply download/clone the repository somewhere and run the below command:
```
docker build -t otrs-nginx:1.13.8-alpine .
```

## About my images

All of my containers follow my take on containerization best-practice:

 * __No unmaintainable gunk.__ No hand-hacked custom scripts or glue code that would need to be updated later.
 * __Small and simple.__ Based on official Alpine Linux with as minimal Dockerfiles and images as possible.
 * __One process, one container.__ No process supervisor daemons or hacks. Allow the container runtime to have full visibility of each running process.
 * __Disposable and immutable.__ Only user data is kept in persistent volumes. All application data is kept inside the container. Any container can be stopped and replaced without affecting the configuration state of the application.
 * __Security focused.__ All processes (that can be) are run by a dedicated application user with minimal permissions. All containers are tested and intended for use with docker user namespace remapping.
 * __True to the application.__ Defaults are not altered in any way, and no additions or subtractions are made to the application's functionality.

If you like these guidelines, then please check out my other images here or on Dockerhub.

[1]: https://github.com/snw35/otrs-docker
