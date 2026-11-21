# docker-alpine

Building small service containers often requires a minimal Linux base, predictable configuration, and a way to supervise more than one process. docker-alpine provides Alpine Linux images with s6 process management for that setup.

## Features

- Build small Docker images on Alpine Linux.
- Manage container processes with s6 and s6-overlay.
- Configure services with `confd` or `consul-template`.
- Connect Consul-based containers to a Consul cluster.
- Add the images to Docker Compose-based microservice environments.

## Installation

Clone this repository and build the image locally:

```sh
git clone <repository-url> docker-alpine
cd docker-alpine
docker build -t docker-alpine .
```

Use the image as a base in another Dockerfile:

```Dockerfile
FROM docker-alpine

CMD ["/bin/sh"]
```

Build the derived image with:

```sh
docker build -t my-service .
```

## Usage

Start an interactive container and open the Alpine shell:

```sh
docker run --rm -it docker-alpine /bin/sh
```

A service image can inherit from `docker-alpine` and provide its own command:

```Dockerfile
FROM docker-alpine

CMD ["/bin/sh"]
```

Run the derived image with:

```sh
docker run --rm my-service
```

For containers that use Consul for service discovery, connect them to the same Docker network as the Consul service and configure the service to use the Consul agent or templates provided by the image.

## License

This project is licensed under the MIT License. It is based on [smebberson/docker-alpine](https://github.com/smebberson/docker-alpine), which is also released under the MIT License. See `LICENSE` for the complete license text and attribution details.

