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
  
# Creating Docker image from Spring Boot Application:
* Dockerfile:
We must create a Dockerfile in each service on our project with the following content:

```
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
ADD ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

* Spotify plugin:

```
<properties>
   <docker.image.prefix>springio</docker.image.prefix>
</properties>
<build>
    <plugins>
        <plugin>
            <groupId>com.spotify</groupId>
            <artifactId>dockerfile-maven-plugin</artifactId>
            <version>1.3.6</version>
            <configuration>
                <repository>${docker.image.prefix}/${project.artifactId}</repository>   
	<buildArgs>
		<JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
	</buildArgs>
            </configuration>
        </plugin>
    </plugins>
</build>
```

* You can build a tagged docker image using the following command line:

`mvnw install dockerfile:build`

* You can use docker-compose to start up multiple containers:

```
version: '2.0'
services:
  config:
    image: config
    ports:
        - "8888:8888"
    networks:
        - seted-network

  product:
    image: product
    
    depends_on:
        - config
    networks:
        - seted-network

  discovery:
    image: discovery
    ports:
        - "8761:8761"
    depends_on:
        - config
    networks:
        - seted-network

  proxy:
    image: proxy
    ports:
        - "9999:9999"
    depends_on:
        - config
    networks:
        - seted-network

networks:
  seted-network:
    driver: bridge
```
    
# [Getting started with Spring Boot and Docker](https://spring.io/guides/gs/spring-boot-docker/)




