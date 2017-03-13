# Jupyterhub Docker-based Informatics Learning Environment

This repository is based on the reference deployment found [here](https://github.com/jupyterhub/jupyterhub-deploy-docker).

This deployment:

* Runs the [JupyterHub components](https://jupyterhub.readthedocs.org/en/latest/getting-started.html#overview) in a Docker container on the host
* Uses [DockerSpawner](https://github.com/jupyter/dockerspawner) to spawn a single-user Jupyter Notebook server based on docker-stacks [data science notebook](https://github.com/jupyter/docker-stacks/tree/master/datascience-notebook) in separate Docker containers on the same host for each user
* Persists JupyterHub data in a Docker volume on the host
* Persists user notebook directories in Docker volumes on the host
* Uses [OAuthenticator](https://github.com/jupyter/oauthenticator) and [GitHub OAuth](https://developer.github.com/v3/oauth/) to authenticate users
* Uses [Lightning Visualization Server]()
* Uses LetsEncrypt SSL certificates generated from the docker-compose application from [here](https://github.com/fatk/docker-letsencrypt-nginx-proxy-companion-examples)
* Uses Geonode, Geoserver and PostGIS
  * PostgreSQL
  * PostGIS
  * Geonode
  * Geoserver

## Disclaimer

This deployment is **NOT** intended for a production environment.  

## Prerequisites

* This deployment tries to [Docker Engine](https://docs.docker.com/engine) and [Docker Compose](https://docs.docker.com/compose/overview/) for almost everything.See the [installation instructions](https://docs.docker.com/engine/installation/) for your environment.
* This example configures JupyterHub for HTTPS connections (the default).
   As such, you must provide TLS certificate chain and key files to the JupyterHub server.
   If you do not have your own certificate chain and key, you can either
   [create self-signed versions](https://jupyter-notebook.readthedocs.org/en/latest/public_server.html#using-ssl-for-encrypted-communication),
   or obtain real ones from [Let's Encrypt](https://letsencrypt.org)
   (see the [letsencrypt example](examples/letsencrypt/README.md) for instructions).

## Setup Procedure

* Set up an account on GitHub to use for OAuth authentication. Review instructions from here. You would need the following to add to an ".env" file. Use "env-template" as a template. The ".env" file is read by Docker Compose to load environment variables into the build and launch processes. Keep the contents of ".env" hidden and do not commit this to GitHub.
 * GITHUB_CLIENT_ID="your GitHub client ID"
 * GITHUB_CLIENT_SECRET="your GitHub client secret"
 * OAUTH_CALLBACK_URL="your call back url"
* Clone this repository:  https://github.com/PHI-Toolkit/jupyterhub-informatics.git
```
$ git clone https://github.com/PHI-Toolkit/jupyterhub-informatics.git
```
* Use the Makefile to create the JupyterHub image and the Lightning server image. This also pulls the Mongo, PostgreSQL containers.
```
$ make build
```
* Create the Jupyter Notebook single-user Docker image (uses Dockerfile-singleuser).
```
$ make notebook_image
```
* Launches all containers with "docker-compose". Adding "-d" (detached mode) runs all containers in the background. Launch first without "-d" to check for any launch errors.
```
$ docker-compose up
```
* Check that all containers are running in the background. Open another terminal and do a "docker ps".
```
$ docker ps
```
* Open your browser to "https://notebook.domain.tld".
