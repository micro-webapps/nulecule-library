## What is micro-webapps?
The goal of the [micro-webapps](https://github.com/micro-webapps/micro-webapps) project is to allow simple deployment of web applications in the cloud (multi container) environment. Admin is able to choose the frontend which will serve the web applications and then install the web applications as separate containers. For each web application, he is able to configure the URI on which the web application will be served.

It is therefore possible to setup webserver with, for example, following structure:

- `http://domain.tld/` running static content.
- `http://domain.tld/blog` running wordpress in separate container.
- `http://bugs.domain.tld` running Bugzilla in separate container.
- `http://another-domain.tld` running completely different domain.

It also allows more advanced features like load-balancing. For more information, check the [micro-webapps home page](https://github.com/micro-webapps/micro-webapps).

## What is haproxy-frontend-atomicapp?
This Docker image contains Atomic App running HAProxy as frontend for other web applications in the cloud. It is intended to be used with Kubernetes or Openshift. It fetches the list of deployed micro-webapps from the Kubernetes or Openshift API server and sets up the reverse proxy for the web applications.

## How to use haproxy-frontend-atomicapp?

Using [Atomic App](https://github.com/projectatomic/atomicapp) is the preferred how to deploy micro-webapps Docker images, but it is also possible to deploy it without the Atomic App as described in the description of microwebapps/haproxy-frontend Docker image.

To deploy the haproxy-frontend-atomicapp using the Atomic App, all you have to do is running following command:

```
# atomicapp run microwebapps/haproxy-frontend-atomicapp
```


This downloads all the Docker images needed by the haproxy-frontend and deploys it. It will also ask for the configuration variables with their description.

You should now be able to use curl or wget to check that haproxy-frontend is responding on the $publicip or on the IP address showed in `kubectl get service` or `osc get service` output.

## Deploying micro-webapps web application

When haproxy-frontend is running, you can start deploying micro-webapps web applications. Check the [micro-webapps](https://hub.docker.com/u/microwebapps/dashboard/) Docker registry for list of supported web applications.