# Examples for deploying EFSS

In this repository, you can find examples of how to build images for your local EFSS deployment in Docker or in the Kubernetes environment. The examples describe the build including the sciencemesh patches and necessary integration application.

Currently, we have prepared the examples for **ownCloud deployment for CESNET QA environment** based on the official ownCloud Helm chart and custom-built ownCloud/server Docker image.
If you want to use this you have to change the `values.yaml` according to your site environment.

## Source Code

- <https://github.com/owncloud-docker/helm-charts>
- <https://github.com/owncloud-docker/server>
- <https://github.com/owncloud/core>

## Requirements

Kubernetes: `~1.21.0-0 || ~1.22.0-0 || ~1.23.0-0 || ~1.24.0-0 || ~1.25.0-0`
Helm

## Usage

```shell
helm repo add owncloud <https://owncloud-docker.github.io/helm-charts>
helm repo update
```

### Building & publishing Docker image

```shell
cd ./cesnet-owncloud-qa
docker build .  --tag your-registry.org/owncloud-qa:10.10 --compress
docker push your-registry.org/owncloud-qa:10.10
```

### Installing the Chart

To install the chart, with your customized values, with the release name `my-owncloud-qa-instance`:

```shell
helm install my-owncloud-qa-instance -f values.yaml owncloud/owncloud
```
