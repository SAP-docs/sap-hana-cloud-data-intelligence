<!-- loio163f5d9740474bd59682c6552daa71ef -->

# Dockerfile Library for Runtime Environment

Operators require a certain runtime environment. For example, if an operator executes some JavaScript code, then the operator requires an environment with a JavaScript engine.

The Modeler provides predefined environments for operators, and these environments are available as a library of Dockerfiles.

When you execute a graph, the application translates each operator in the graph into processes. It then searches the Dockerfiles for an environment suitable for the operator execution and instantiates a Docker image.

> ### Note:  
> The Docker image with the environment and the operator process is executed on a Kubernetes cluster.

