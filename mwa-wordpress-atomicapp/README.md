## What is micro-webapps?
The goal of the micro-webapps project is to allow simple deployment of web applications in the cloud (multi container) environment. Admin is able to choose the frontend which will serve the web applications and then install the web applications as separate containers. For each web application, he is able to configure the URI on which the web application will be served.

It is therefore possible to setup webserver with, for example, following structure:

- `http://domain.tld/` running static content.
- `http://domain.tld/blog` running wordpress in separate container.
- `http://bugs.domain.tld` running Bugzilla in separate container.
- `http://another-domain.tld` running completely different domain.

It also allows more advanced features like load-balancing. For more information, check the [micro-webapps home page](https://github.com/micro-webapps/micro-webapps).

## What is wordpress-atomicapp?
This Docker image contains [Atomic App](https://github.com/projectatomic/atomicapp) running Wordpress based on the official Wordpres Docker image.

## How to use wordpress-atomicapp?

At first, you have to have the micro-webapps frontend deployed on your cloud. There are three possible frontends:

* [microwebapps/httpd-frontend-atomicapp](https://hub.docker.com/r/microwebapps/httpd-frontend-atomicapp)
* [microwebapps/nginx-frontend-atomicapp](https://hub.docker.com/r/microwebapps/nginx-frontend-atomicapp)
* [microwebapps/haproxy-frontend-atomicapp](https://hub.docker.com/r/microwebapps/haproxy-frontend-atomicapp)

Please read the documentation on the frontend's Docker page for instructions how to deploy the frontend.

Once the frontend is deployed in the cluster, you just run following atomicapp command to deploy the Wordpress:

```
# atomicapp run microwebapps/wordpress-atomicapp
```

This downloads all the Docker images needed by the Wordpress and deploys it. It will also ask for the configuration variables with their description. You can also check the "answers.conf.sample" file generated by the "atomicapp", rename it to "answers.conf" and change some variables if you want.

You should now be able to use curl, wget or web browser to access the Wordpress on the domain and path you configured.

## Where to get more informations and documentation?

The micro-webapps documentation is available on [micro-webapps GitHub page](https://github.com/micro-webapps/micro-webapps/).
