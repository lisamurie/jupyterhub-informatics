# Jupyterhub Docker-based Informatics Learning Environment

This repository provides is based on the reference deployment found [here](https://github.com/jupyterhub/jupyterhub-deploy-docker).

This deployment:

* Runs the [JupyterHub components](https://jupyterhub.readthedocs.org/en/latest/getting-started.html#overview) in a Docker container on the host
* Uses [DockerSpawner](https://github.com/jupyter/dockerspawner) to spawn a single-user Jupyter Notebook server based on docker-stacks [data science notebook](https://github.com/jupyter/docker-stacks/tree/master/datascience-notebook) in separate Docker containers on the same host for each user
* Persists JupyterHub data in a Docker volume on the host
* Persists user notebook directories in Docker volumes on the host
* Uses [OAuthenticator](https://github.com/jupyter/oauthenticator) and [GitHub OAuth](https://developer.github.com/v3/oauth/) to authenticate users
* Uses [Lightning Visualization Server]()
* Uses LetsEncrypt SSL certificates generated from the docker-compose application from [here](https://github.com/fatk/docker-letsencrypt-nginx-proxy-companion-examples)

## Disclaimer

This deployment is **NOT** intended for a production environment.  

## Prerequisites

* This deployment uses Docker for all the things, via  [Docker Compose](https://docs.docker.com/compose/overview/).
  It requires [Docker Engine](https://docs.docker.com/engine) 1.12.0 or higher.
  See the [installation instructions](https://docs.docker.com/engine/installation/) for your environment.
* This example configures JupyterHub for HTTPS connections (the default).
   As such, you must provide TLS certificate chain and key files to the JupyterHub server.
   If you do not have your own certificate chain and key, you can either
   [create self-signed versions](https://jupyter-notebook.readthedocs.org/en/latest/public_server.html#using-ssl-for-encrypted-communication),
   or obtain real ones from [Let's Encrypt](https://letsencrypt.org)
   (see the [letsencrypt example](examples/letsencrypt/README.md) for instructions).

## Setup Procedure
