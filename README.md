# Introduction

This is a simple demo showcasing some of RH-SSO features/concepts such as: Realm, Client, Social Login, Themes, etc..

For additional details, please refer to "Additional References section"

## Environment

- [Docker 18.06.1-ce](https://docs.docker.com/install/)
- [Red Hat Single Sign On 7.2](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/)
- [Red Hat Single Sign On 7.2 1.2-8 container image](https://access.redhat.com/containers/?tab=security#/registry.access.redhat.com/redhat-sso-7/sso72-openshift/images/1.2-8.1539812404)

## Deploy from DockerHub
```
docker pull viniciusmartinez/slide-demo-app:1.0
docker pull viniciusmartinez/rhsso:1.0
```
## Building from "Source"

- Clone the application:
```
git clone https://github.com/vinicius-martinez/rhsso-slide-demo.git
```
- Build *(docker build)* RHSSO. Example:
```
cd rhsso
docker build -t rhsso:1.0 .
```
- Build *(docker build)* slide-demo-app. Example:
```
cd slides-app
docker build -t slide-demo-app:1.0 .
```

## Demo Script:

1. [Starting RHSSO and slide-demo-app](#demo-step-1)
2. [Create RHSSO Realm](#demo-step-2)
3. [Create RHSSO Client APP](#demo-step-3)
4. [Create RHSSO Client Roles](#demo-step-4)
5. [Create RHSSO User](#demo-step-5)
6. [Enable SignUp](#demo-step-6)
7. [Change Themes](#demo-step-7)
8. [Authentication Flow](#demo-step-8)
9. [Two Factor with OTP](#demo-step-9)

### Starting RHSSO and slide-demo-app <a name="demo-step-1"></a>

* Open a terminal and start RHSSO:
```
docker run -it -P viniciusmartinez/rhsso:1.0
```
* *we're going to use "-P" to generate a random Port number for RHSSO. If you prefer, you can bind it to an alternative port of your choice*

* Open a second terminal and start slide-demo-application:
```
docker run -it -P viniciusmartinez/slide-demo-app:1.0
```
*we're going to use "-P" to generate a random Port number for RHSSO. If you prefer, you can bind it to an alternative port of your choice*

* Open a third terminal and execute *docker ps* in order to fetch *RHSSO* and *slide-demo-app* port numbers. Example:
```
docker ps
CONTAINER ID        IMAGE                                 COMMAND                  CREATED             STATUS              PORTS                                                                       NAMES
16f6cd0d3e11        viniciusmartinez/rhsso:1.0            "/opt/eap/bin/opensh…"   25 seconds ago      Up 24 seconds       0.0.0.0:32789->8080/tcp, 0.0.0.0:32788->8443/tcp, 0.0.0.0:32787->8778/tcp   upbeat_hermann
fe93676933d3        viniciusmartinez/slide-demo-app:1.0   "container-entrypoin…"   51 seconds ago      Up 50 seconds       0.0.0.0:32786->8080/tcp, 0.0.0.0:32785->8443/tcp
```
*take note of all ports used by RHSSO (32789, 32788) and slide-demo-app(32786,32785)*

* Open a browser of choice and try to access *RHSSO* on the following address with admin/admin credentials:
http://localhost:32789/auth

* Open a new tab and try to access *slide-demo-app* on the following address:
http://localhost:32786/demo.html

### Create RHSSO Realm <a name="demo-step-2"></a>

* Return to the *RHSSO* browser tab and place the mouser on the left top corner, right above the **MASTER**. Click on the arrow button and select **Add Realm**;

* Inform a **NAME** (e.g myrealm) and click on **Create** button;

### Create RHSSO Client APP <a name="demo-step-3"></a>

* Click on **Clients** right bellow the **Realm Settings** at the left menu;
* Click on **Create** button on the right corner;
* Inform a **Name** (e.g: myclient);
* Inform the **Root URL** (e.g: http://localhost:32794);
* Click on **Save** button;
* Switch back to the *slide-demo-app* tab and click on **Config** button;
* Inform **SSO Server URL** (e.g: http://localhost:32792/auth)
* Inform **SSO Realm** (e.g: myrealm)
* Inform **App Client ID** (e.g: myclient)
* Click on **Save** and afterward **Close** button;
* If everything is successfully configured, a *green* **Configurado!** button will be displayed

### Create RHSSO Client Roles <a name="demo-step-4"></a>
### Create RHSSO Client Roles <a name="demo-step-4"></a>
### Enable SignUp <a name="demo-step-5"></a>
### Change Themes <a name="demo-step-6"></a>
### Authentication Flow <a name="demo-step-7"></a>
### Two Factor with OTP <a name="demo-step-8"></a>

## Additional References

[CDK/Minishift Download](https://developers.redhat.com/products/cdk/download/)

[CDK/Minishift Documentation](https://developers.redhat.com/products/cdk/docs-and-apis/)

[CDK/Minishift NodePort](https://access.redhat.com/documentation/en-us/red_hat_container_development_kit/3.6/html-single/getting_started_guide/#nodeport-services)

[Openshift NodePort](https://docs.openshift.com/container-platform/3.10/dev_guide/expose_service/expose_internal_ip_nodeport.html)
