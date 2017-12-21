# SpringBootDocker
In this project, we're trying to provide a sample microservices running using Docker 

# Download Docker ToolBox
First, you must download and install Docker ToolBox from this URL (if you're using Microsoft): https://docs.docker.com/toolbox/toolbox_install_windows/

# Our microservices
We're trying to deploy the following microservices using Docker:

  Product Service: The main service, which offers a REST API for listing all products.

  Config Service: Configuration service, which role is to centralize configuration files' of all different microservices.
  
  Proxy Service: A gateway that handles the routing of a request to one of the instances of a service.

  Discovery Service: Service that records service instances for discovery by other services.
  
  
