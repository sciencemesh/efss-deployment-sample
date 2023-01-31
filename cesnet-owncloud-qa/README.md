# CESNET QA environment examples for Sciencemesh instance

## Dockerfile

The file for Docker build `Dockerfile` is intended to build ownCloud 10.10 image with Sciencemesh support. That includes the Sciencemesh integration app for ownCloud 10.10 and all necessary changes relating to [REVA](https://reva.link/) connection. To run the build demonstrated in the Dockerfile you need to apply the patched Makefile, see below.

### Be aware of blessed version of the oc-sciencemesh-app - QA Environment
[Blessed versions](https://developer.sciencemesh.io/docs/technical-documentation/iop/iop-nextcloud-owncloud10-integrations/) specify the compatibility of oc-sciencemesh-app. The **Dockerfile** is prepared for the **latest** version of the app. It is for the sake of testing. For operational deployment is the preffereed way to install the oc-sciencemesh-app from the OC Marketplace. In case of QA environment build you can omit the [lines](https://github.com/sciencemesh/efss-deployment-sample/blob/13ded0c61620c58779d522a0228364a94d435258/cesnet-owncloud-qa/Dockerfile#L1-L14) relating to oc-sciencemesh-app installation and the [line](https://github.com/sciencemesh/efss-deployment-sample/blob/13ded0c61620c58779d522a0228364a94d435258/cesnet-owncloud-qa/Dockerfile#L23) enabling the app itself. Then you do not need to use **Makefile.diff**. All you need is to add to the file [values.yaml](https://github.com/sciencemesh/efss-deployment-sample/blob/main/cesnet-owncloud-qa/values.yaml#L12) option `sciencemesh`, which will install the application from the OC Marketplace.

## Makefile diff
The file `Makefile.diff` is intended to integrate the changes in the OC's [Science mesh app Makefile](https://github.com/pondersource/oc-sciencemesh/blob/main/Makefile) necessary for the docker build described above.

## Values for Helm 
The file `values.yaml` specifies the [values](https://github.com/owncloud-docker/helm-charts/blob/main/charts/owncloud/README.md) for ownCloud Helm chart.
