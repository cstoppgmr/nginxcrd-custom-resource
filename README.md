# Kubernetes Nginxconf Controller - Nginxconf Resource Handling

**Note**: the source code is _verbosely_ commented, so the source is meant to be read and to teach

## What is this?

An example of a custom Kubernetes controller that's only purpose is to watch for the creation, updating, or deletion of all custom resource of type `Network` (in the all namespaces). This was created as an exercise to understand how Kubernetes controllers work and interact with the cluster and resources.

## Running

Clone repo:

```
$ git clone https://github.com/cstoppgmr/nginxcrd-custom-resource
$ cd nginxcrd-custom-resource
```

Prepare build environment:

```
$ go get github.com/tools/godep
$ godep restore
```

Build and run:

```
$ go build -o nginxcrd-controller .
$ ./nginxcrd-controller -kubeconfig=$HOME/.kube/config -alsologtostderr=true -nginxhome=/usr/local/nginx
```

You can also use `nginxcrd-controller` to create a Deployment and run it in Kubernetes. Note in this case, you don't need to specify `-kubeconfig` in CMD as default `InClusterConfig` will be used.

## Usage

You should create the CRD of Network first:

```
$ kubectl apply -f crd/nginxcrd.yaml
```

You can then trigger an event by creating a Network API instance:

```
$ kubectl apply -f example/www.demo.com.conf.yaml
```

CURD the Nginxconf API instance, and check the logs of controller. 

Enjoy!
