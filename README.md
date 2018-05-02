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

***

 * [Travis CI: ![Build Status](https://travis-ci.org/snw35/otrs-nginx.svg?branch=master)](https://travis-ci.org/snw35/otrs-nginx)
