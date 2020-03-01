# OpenFaas

OpenFaaS is a framework and infrastructure preparation system for building serverless applications. It originated from the serverless framework in the Docker Swarm and now supports other kinds of infrastructure backends, such as Kubernetes or Hyper.sh. Functions in OpenFaaS are containers. Any program written in any language can be packed as a function by leveraging the container technologies of Docker. This enables us to fully reuse the existing code to consume a wide range of web service events without rewriting the code. OpenFaaS is a great tool for modernizing old systems to run on a cloud-based infrastructure.

The driving factor behind the making of the framework is shaping the following, features:

    Ease of use
    Portable
    Simplicity in architecture and design
    Open and extensible platform
    Language agnostic
    
    
# OpenFaaS components

The components are the API gateway, the function watchdog, and an instance of Prometheus. All are running on top of Docker Swarm or Kubernetes orchestration engines. The API gateway and the instance of Prometheus run as services, while the function watchdog runs as the part of function containers.

![alt text](https://github.com/dipsscor/OpenFaas-Serverless-Framework/blob/master/screenshots/architecture.png)



## Function watchdog
The function watchdog is an OpenFaaS component. It is responsible for wrapping the real working code around a function program. The function program’s requirement is only to accept input via the standard input (stdin) and print out the result, of course, to the standard output (stdout).
The API gateway (gateway) connects to function containers through an overlay network. Each function container contains the following:

    Function watchdog, fwatchdog
    A certain function program written in any language

![alt text](https://github.com/dipsscor/OpenFaas-Serverless-Framework/blob/master/screenshots/watchdog.png)


# Deployment Steps:

### Intitialize Docker Swarm
    docker swarm init

### Run OpenFaas:

#### without authentication 
    cd open-faas && ./deploy_stack.sh --no-auth
    
#### With authentication 
    cd open-faas && ./deploy_stack.sh
 
 
 ![alt text](https://github.com/dipsscor/OpenFaas-Serverless-Framework/blob/master/screenshots/OpenFaas.png)
    
### Grafana:

For adding Grafana as separate service

    docker service create --name=grafana --network=func_functions -p 3000:3000 grafana/grafana

In this project , Additional Grafana configurations and dashboard has been added in open-faas-->docker-compose*.yml files
Also, OpenFaas Grafana dashboard is added -->Dashboard_id-->3434

![alt text](https://github.com/dipsscor/OpenFaas-Serverless-Framework/blob/master/screenshots/Grafana.png)


# URL Access:

### OpenFaas Dashboard URL:

    http://localhost:8080/ui
    
### Prometheus URL:

    http://localhost:9090 
    
    
### Grafana URL:

    http://localhost:3000     
    
    
    
# TearDown steps:


## Remove function on OpenFaas
Remove all the functions from OpenFaas dashboard

## Remove OpenFaas

    docker stack rm func
    docker secret rm basic-auth-user && docker secret rm basic-auth-password
    
## Leave Swarm

    docker swarm leave --force
    

# Address of the API Gateway on functions.yml

### On Kubernetes
    The default address for the gateway on Kubernetes is http://gateway.openfaas:8080.

### On Docker Swarm
    The default address for the gateway is http://gateway:8080
    

# References

    https://medium.com/@pavithra_38952/openfaas-on-docker-440541d635a2
    https://docs.openfaas.com/deployment/docker-swarm/
    
