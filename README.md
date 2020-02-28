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


# Deployment Steps:

### Intitialize Docker Swarm
    docker swarm init

### Run OpenFaas:

#### without authentication 
    cd open-faas && ./deploy_stack.sh --no-auth
    
#### With authentication 
    cd open-faas && ./deploy_stack.sh
    
    
    
# TearDown steps:

## Remove OpenFaas

    docker stack rm func
    docker secret rm basic-auth-user && docker secret rm basic-auth-password
    
## Leave Swarm

    docker swarm leave --force
    

# References

    https://medium.com/@pavithra_38952/openfaas-on-docker-440541d635a2
