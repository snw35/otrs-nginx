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


## About my images

All of my containers follow these main guidelines:

 * __Follow best practice.__ Adhere as closely as possible to the [official docker library image guidelines.](https://github.com/docker-library/official-images)
 * __No version-dependent scripts.__ No custom scripts or glue code that would need to be updated alongside the hosted application.
 * __Small and simple.__ Based on official Alpine Linux with as minimal Dockerfiles and images as possible.
 * __One process, one container.__ No process supervisor daemons or hacks. Allow the container runtime to have full visibility of each running process.
 * __Disposable and immutable.__ Strict separation of user and application data means that any container can be stopped and replaced without affecting the configuration state of the application.
 * __Security focused.__ No docker socket bind mounts, ever. All processes are run by a dedicated application user with minimal permissions where possible.
 * __True to the application.__ The application's defaults are not altered in any way, and no additions or subtractions are made to functionality.

If you like these guidelines, then please check out my other images here or on Dockerhub.

[1]: https://github.com/snw35/otrs-docker
