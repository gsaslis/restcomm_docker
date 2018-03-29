# Intro

This docker image contains the [Restcomm JSS7](https://github.com/RestComm/jss7) stack deployed on 
[Restcomm JAIN SLEE](https://github.com/RestComm/jain-slee), together with its Resource Adaptors, as a JBoss service, 
as described in the [docs](https://www.restcomm.com/docs/core/ss7/SS7_Stack_Installation_Guide.html#installation-options). 

It also includes a test JSS7 Service which is deployed with the stack, to simulate some of the functionality.

## Instructions 

1. Clone this repo and switch to the `jss7` folder, or download both files into the same folder. 
2. Run `docker-compose up`. This should first start the docker image build process and then run the container itself, 
exposing the necessary ports on your host, for your easy access. 
