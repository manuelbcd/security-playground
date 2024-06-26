# Security Playground

The security playground is a HTTP web server to simulate security breaches in
run time.

## Installation

Use the docker image to deploy it in your Kubernetes cluster or locally in a
container.

```bash
$ docker run --rm -p 8080:8080 sysdiglabs/security-playground
```
Or kubernetes
```bash
# Test workload security-playground 
kubectl create deployment playground --image=manuelbcd/security-playground:1.0.6

# Expose workload with an LB
kubectl expose deployment playground --port=80 --target-port=8080 --name=playground --type=LoadBalancer
# or
# Expose workload via ClusterIP
# kubectl expose deployment playground --port=80 --target-port=8080 --name=playground --type=ClusterIP
```





## Usage

The HTTP API exposes tree endpoints to interact with the system.

### Reading a file

You can read a file using just the URL.

```bash
$ curl localhost:8080/etc/shadow
```

This will return the content of the /etc/shadow file.

### Writing a file

You can write to a file using the URL and POSTing the content.

```bash
$ curl -X POST localhost:8080/bin/hello -d 'content=hello-world'
```

This will write to /bin/hello the hello-world string

### Executing a command

You can execute a command using the /exec endpoint and POSTing the command.

```bash
$ curl -X POST localhost:8080/exec -d 'command=ls -la'
```

or

```bash
$ curl -X POST localhost:8080/exec -d 'command=chmod 0755 /bin/hello'
```

This will capture and return the STDOUT of the command executed.

# Sample scenario

https://github.com/sysdig-workshops/aws-workshops-resources/blob/main/offensive/attack-playground.md
