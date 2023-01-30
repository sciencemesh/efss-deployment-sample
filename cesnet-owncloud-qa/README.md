# CESNET QA environment examples for Sciencemesh instance

## Dockerfile

The file for Docker build `Dockerfile` is intended to build ownCloud 10.10 image with Sciencemesh support. That includes the Sciencemesh integration app for ownCloud 10.10 and all necessary changes relating to [REVA](https://reva.link/) connection. To run the build demonstrated in the Dockerfile you need to apply the patched Makefile, see below.

## Makefile diff
The file `Makefile.diff` is intended to integrate the changes in the OC's [Science mesh app Makefile](https://github.com/pondersource/oc-sciencemesh/blob/main/Makefile) necessary for the docker build described above.

## Values for Helm 
The file `values.yaml` specifies the [values](https://github.com/owncloud-docker/helm-charts/blob/main/charts/owncloud/README.md) for ownCloud Helm chart.
