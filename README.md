# Introduction

This is a simple demo showcasing some of RH-SSO features/concepts such as: Realm, Client, Roles, Social Login, Themes, etc..

For additional details, please refer to [Additional References](#demo-additional-references) section;

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
4. [Create RHSSO Roles](#demo-step-4)
5. [Create RHSSO User](#demo-step-5)
6. [Enable SignUp](#demo-step-6)
7. [Change Themes](#demo-step-7)
8. [User Required Actions](#demo-step-8)
9. [Social Login](#demo-step-9)
10. [Two Factor with OTP](#demo-step-10)
11. [End User Account Management](#demo-step-11)

### Starting RHSSO and slide-demo-app <a name="demo-step-1"></a>

* Open a terminal and start RHSSO:

  * *we're going to use "-P" to generate a random Port number for RHSSO. If you prefer, you can bind it to an alternative port of your choice*

```
docker run -it -P viniciusmartinez/rhsso:1.0
```

* Open a second terminal and start slide-demo-application:

  * *we're going to use "-P" to generate a random Port number for RHSSO. If you prefer, you can bind it to an alternative port of your choice*

```
docker run -it -P viniciusmartinez/slide-demo-app:1.0
```

* Open a third terminal and execute *docker ps* in order to fetch *RHSSO* and *slide-demo-app* port numbers. Example:

  * *take note of all ports used by RHSSO (32789, 32788) and slide-demo-app(32786,32785)*

```
docker ps
CONTAINER ID        IMAGE                                 COMMAND                  CREATED             STATUS              PORTS                                                                       NAMES
16f6cd0d3e11        viniciusmartinez/rhsso:1.0            "/opt/eap/bin/opensh…"   25 seconds ago      Up 24 seconds       0.0.0.0:32789->8080/tcp, 0.0.0.0:32788->8443/tcp, 0.0.0.0:32787->8778/tcp   upbeat_hermann
fe93676933d3        viniciusmartinez/slide-demo-app:1.0   "container-entrypoin…"   51 seconds ago      Up 50 seconds       0.0.0.0:32786->8080/tcp, 0.0.0.0:32785->8443/tcp
```

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

### Create RHSSO Roles <a name="demo-step-4"></a>

* Click on **Roles** right bellow the **Client Templates** at the left menu;
* Click on **Add Role** button;
* Inform a **Role Name** (e.g: realm-role) and afterward **Save** button;
* Click on **Clients** right bellow the **Realm Settings** at the left menu;
* Select **myclient** and **Roles afterward**;
* Click on **Add Role** button;
* Inform a **Role Name** (e.g: client-role) and afterward **Save** button;
* Click on **Roles** again;
* Select **Default Roles**
* Select **realm-role** and click on **Add Selected**
* Select **myclient** and repeat the same procedure, adding **client-role**

### Create RHSSO User <a name="demo-step-5"></a>

* Click on **Users** right bellow the **Groups** at the left menu;
* Click on **Add User** button;
* Inform a **Username** and click on **Save** button;
* Got to **Credentials** tab and inform a new password;
* Finally click on **Reset Password**;

  * *now you can try to login on slide-demo-app*

### Enable SignUp <a name="demo-step-6"></a>

* Click **Realm Settings** and select **Login** tab;
* Enable **User Registration**
* Click on **Save**

### Change Themes <a name="demo-step-7"></a>

* Click **Realm Settings** and select **Themes** tab;
* Select a different theme from **Login Theme** dropdown list;
* Click on **Save**

### User Required Actions <a name="demo-step-8"></a>

* Click on **Users** right bellow the **Groups** at the left menu;
* Select an user;
* Select a few actions on **Required User Actions** menu;
* Click on **Save**

### Social Login <a name="demo-step-9"></a>

* Click on **Identity Providers** right bellow the **Roles** at the left menu;
* Select **Github** user;
* Open a new tab and access your *Github* account. Select **Settings** -> **Developer Settings** and finally click on: **New Oauth App**
* Inform an *Application name* and a *Homepage URL* and finally copy the **Redirect URI** from RHSSO and paste it on **CallBack URL**
* Click on **Register Application**
* Copy both **Client ID** and **Client Secret** from *Github* and paste them on *RHSSO*
* Click on **Save**

### Two Factor with OTP <a name="demo-step-10"></a>

* Click on **Authentication** right bellow the **User Federation** at the left menu;
* Change the default *OTP FORM* from **OPTIONAL** to **REQUIRED**;
* Logout from *slide-demo-app* and try to log back;

### End User Account Management <a name="demo-step-11"></a>

* Open a new browser tab with the following url: *http://localhost:32792/auth/realms/myrealm/account*
* Navigate through the options and update your profile if desired;

## Additional References <a name="demo-additional-references">

[Docker Port](https://docs.docker.com/engine/reference/commandline/port/)

[Realm](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html-single/server_administration_guide/#the_master_realm)

[Managing Clients](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html-single/server_administration_guide/#clients)
[Roles](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html-single/server_administration_guide/#roles)

[Login Page Settings](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html-single/server_administration_guide/#login_page_settings)

[Themes](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html-single/server_administration_guide/#themes)

[Authentication Flow](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html-single/server_administration_guide/#authentication-flows)

[User Required Actions](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html-single/server_administration_guide/#required_actions)

[Social Identity Providers](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html-single/server_administration_guide/#social_identity_providers)

[OTP](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html-single/server_administration_guide/#otp_policies)
