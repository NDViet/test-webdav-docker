Repository is used to build [Docker image](https://hub.docker.com/r/ndviet/webdav) and [Helm chart](https://www.ndviet.org/charts) of the WebDAV server for internal umbrella project.

The image is built on top of the underlying Python Alpine with main application [WsgiDAV](../../../../mar10/wsgidav) - a generic and extendable WebDAV server written in Python and based on WSGI.

The Helm chart is used to simplify the deployment of WebDAV server to Kubernetes.

## Install the chart

```shell
# Add ndviet helm repository
helm repo add ndviet https://www.ndviet.org/charts

# Update charts from ndviet repo
helm repo update

# List all versions present in the ndviet repo
helm search repo ndviet/webdav --versions

# Install full components as default with latest version
helm upgrade -i test ndviet/webdav

# Download the chart latest version to local
helm fetch ndviet/webdav --untar
```

## Build the umbrella chart

```shell
mvn clean install
```
Built chart is located under target/helm/repo/webdav-x.x.x.tgz

## System requires

1. Maven (Tested version 3.8.6)
2. Helm v3 (Tested version v3.11.3)
3. Kubernetes (Tested version v1.25.5 - Runtime: Docker v20.10.24 - Provisioned by Minikube v1.26.1)

## Change Log

### :heavy_check_mark: 4.3.0
**Added**
- Build Docker image and Helm chart for WebDAV server based on [WsgiDAV v4.3.0](../../../../mar10/wsgidav/releases/tag/v4.3.0) 