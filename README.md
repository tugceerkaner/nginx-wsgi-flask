# Application Details

## Project structure

```text
.
├── compose.yaml
├── flask
│   ├── app.py
│   ├── Dockerfile
│   ├── requirements.txt
│   └── wsgi.py
└── nginx
    ├── default.conf
    ├── Dockerfile
    ├── nginx.conf
    └── start.sh
```

## About

By following the steps above, you will have an NGINX Reverse Proxy and a Flask backend. The general traffic flow will look like the following:

`Client -> NGINX -> WSGI -> Flask`

### NGINX

With this deployment model, we use NGINX to proxy and handle all requests to our Flask backend. This is a powerful deployment model as we can use NGINX to cache responses or even act as an application load balancer between multiple Flask backends. You could also integrate a Web Application Firewall into NGINX to protect your Flask backend from attacks.

### WSGI

WSGI (Web Server Gateway Interface) is the interface that sits in between our NGINX proxy and Flask backend. It is used to handle requests and interface with our backend. WSGI allows you to handle thousands of requests at a time and is highly scalable. In this `docker-compose` sample, we use Gunicorn for our WSGI.

### Flask

Flask is a web development framework written in Python. It is the "backend" which processes requests.

A couple of sample endpoints are provided in this `docker-compose` example:

* `/` - Returns a "Hello World!" string.
* `/cache-me` - Returns a string which is cached by the NGINX reverse proxy. This demonstrates an intermediary cache implementation.
* `/info` - Returns informational headers about the request. Some are passed from NGINX for added client visibility.
