# Nginx Directory Lister

## Intro

This is a simple docker image to expose file listing to the web

## Compatibility

* X64
* ARM64

## Usage

```sh
docker run -d -p 80:80 -v /path/to/directory:/usr/share/nginx/html ghcr.io/johndoe6345789/nginx-directory-lister:latest
```