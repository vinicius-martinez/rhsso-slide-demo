# Introduction

This is a simple demo showcasing some of RH-SSO features/concepts such as: Realm, Client, Social Login, Themes, etc..

For additional details, please refer to "Additional References section"

## Environment

- [Docker 18.06.1-ce](https://docs.docker.com/install/)
- [Red Hat Single Sign On 7.2](https://access.redhat.com/containers/?tab=security#/registry.access.redhat.com/redhat-sso-7/sso72-openshift/images/1.2-8.1539812404)
*based on redhat-sso-7/sso72-openshift:1.2-8.1539812404 image*

## Deploy from DockerHub

- docker pull viniciusmartinez/slide-demo-app:1.0
- docker pull viniciusmartinez/rhsso:1.0

## Building from "Source"

- Clone the application:
```
git clone https://github.com/vinicius-martinez/rhsso-slide-demo.git
```
- Build *(docker build)* RHSSO:
```
cd rhsso
docker build -t viniciusmartinez/rhsso:1.0 .
```
- Build *(docker build)* slide-demo-app:
```
cd slides-app
docker build -t viniciusmartinez/slide-demo-app:1.0 .
```

## Additional References

[CDK/Minishift Download](https://developers.redhat.com/products/cdk/download/)

[CDK/Minishift Documentation](https://developers.redhat.com/products/cdk/docs-and-apis/)

[CDK/Minishift NodePort](https://access.redhat.com/documentation/en-us/red_hat_container_development_kit/3.6/html-single/getting_started_guide/#nodeport-services)

[Openshift NodePort](https://docs.openshift.com/container-platform/3.10/dev_guide/expose_service/expose_internal_ip_nodeport.html)
