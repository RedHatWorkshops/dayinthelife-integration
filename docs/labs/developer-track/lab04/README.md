# Lab 4

## Swagger to REST

### Contract-first API development with a DB interface, implemented using Eclipse Che.

* Duration: 20 mins
* Audience: Developers and Architects

## Overview

Once you have APIs in your organization and have applications being written, you also want to be sure in many cases that thee various types of users of the APIs are correctly authenticated. In this lab you will discover how to set up the widely used OpenID connect pattern for Authentication. 

### Why Red Hat?

The Red Hat SSO product provides important functionality for managing identities at scale. In this lab you can see how it fits together with 3scale and OpenShift.

### Skipping The Lab

We know sometime we don't have enough time to go over the labs step by step. So here is a [short video](https://youtu.be/-3QGAD3Tt48) where you can see how to implement a Contract-first API.

If you are planning to follow to the next lab or are having trouble with this lab, you can reference the working project [here](https://github.com/RedHatWorkshops/dayinthelife-integration/tree/master/projects/location-service)

### Environment

**URLs:**

Check with your instruction the *GUID* number of your current workshop environment. Replace the actual number on all the URLs where you find **GUID**. 

Example in case of *GUID* = **1234**: 

```bash
https://master.GUID.openshiftworkshop.com
```

becomes =>

```bash
https://master.1234.openshiftworkshop.com
```

**Credentials:**

Your username is your asigned user number. For example, if you are assigned user number **1**, your username is: 

```bash
user1
```

The password to login is always the same:

```bash
openshift
```

## Lab Instructions

### Step 1: Create an Eclipse Che environment for your personal use

1. Open a browser window and navigate to:

    ```bash
    http://che-rh-che-0879.apps.GUID.openshift.opentlc.com/dashboard/#/
    ```

    *Remember to replace the GUID with your [environment](#environment) value and your user number.*

1. Click on **Create Workspace**.

    ![00-create-workspace.png](images/00-create-workspace.png "Create Workspace")

1. Enter a unique name for your workspace e.g. simon-dev-workspace.  Select "day in the life workshop" stack, increase the RAM to 4MB and then click **Create**.

    ![00-new-workspace.png](images/00-new-workspace.png "New Workspace")

1. Click on **Open** to generate and open the workspace.

    ![00-open-workspace.png](images/00-open-workspace.png "Open Workspace")

### Step 2: Import the skeleton projects from Git an convert them to Maven projects.

1. Click on the **Import Project** link.  A pop-up will appear.

    ![00-import-project.png](images/00-import-project.png "Import Project")

1. Enter `https://github.com/weimeilin79/dayinthelife-import` as the git URL, select "Import Recursively" and then click "Import".

1. When the "Save" pop-up appears, click the "X" to close the pop-up.

    ![00-close-save.png](images/00-close-save.png "Close Save")

1. Write click on the **location-soap2rest** project and select **Convert to Project**

    ![00-convert-project.png](images/00-convert-project.png "Convert Project")

1. Select **Maven** then click **Save**.

    ![00-select-maven.png](images/00-select-maven.png "Select Maven")

1. Convert the remaining projects to Maven, by repeating steps 4 - 6 for the **location-service** and **location-gateway** projects.


### Step 3: Configure 3scale Integration

1. Open a browser window and navigate to:

    ```bash
    https://userX-admin.apps.GUID.openshiftworkshop.com/
    ```

    *Remember to replace the GUID with your [environment](#environment) value and your user number.*

1. Accept the self-signed certificate if you haven't.

    ![selfsigned-cert](images/00-selfsigned-cert.png "Self-Signed Cert")

1. Log into 3scale using your designated [user and password](#environment). Click on **Sign In**.

    ![01-login.png](images/01-login.png)

1. The first page you will land is the *API Management Dashboard*. Click on the **API** menu link.

    ![01a-dashboard.png](images/01a-dashboard.png)

1. This is the *API Overview* page. Here you can take an overview of all your services. Click on the **Integration** link.

    ![02-api-integration.png](images/02-api-integration.png)

1. Click on the **edit integration settings** to edit the API settings for the gateway.

    ![03-edit-settings.png](images/03-edit-settings.png)

1. Scrolll down the page, under the *Authentication* deployment options, select **OpenID Connect**. 

    ![04-authentication.png](images/04-authentication.png)

1. Click on the **Update Service** button.

1. Dismiss the warning about changing the Authentication mode by clicking **OK**.

    ![04b-authentication-warning.png](images/04b-authentication-warning.png)
    
1. Back in the service integration page, click on the **edit APIcast configuration**.

    ![05-edit-apicast.png](images/05-edit-apicast.png)

1. Scroll down the page and expand the authentication options by clicking the **Authentication Settings** link.

    ![05-authentication-settings.png](images/05-authentication-settings.png)

1. In the **OpenID Connect Issuer** field, type in your previously noted client credentials with the URL of your Red Hat Single Sing On instance:

    ```bash
    http://3scale-admin:CLIENT_SECRET@sso-rh-sso.apps.GUID.openshiftworkshop.com/auth/realms/userX
    ```

    *Remember to replace the GUID with your [environment](#environment) value, your user number and the CLIENT_SECRET you get in the [Step 1](#step-1-get-red-hat-single-sign-on-service-account-credentials)*.

    ![06-openid-issuer.png](images/06-openid-issuer.png "OpenID Connect Issuer")

1. Scroll down the page and click on the **Update Staging Environment** button.

    ![08-back-integration.png](images/08-back-integration.png "Back Integration")

1. After the reload, scroll down again and click the **Back to Integration &amp; Configuration** link.

    ![07-update-environment.png](images/07-update-environment.png "Update Environment")

1. Promote to Production by clicking the **Promote to Production** button.

    ![08a-promote-production.png](images/08a-promote-production.png "Update Environment")

### Step 4: Create a Test App

1. Go to the *Developers* tab and click on **Developer**.

    ![09-developers.png](images/09-developers.png "Developers")

1. Click on the **Applications** link.

    ![10-applications.png](images/10-applications.png "Applications")

1. Click on **Create Application** link.

    ![11-create-application.png](images/11-create-application.png "Create Application")

1. Select **Basic** plan from the combo box. Type the following information:

    * Name: **Secure App**
    * Description: **OpenID Connect Secured Application**

    ![12-application-details.png](images/12-application-details.png "Application Details")

1. Finally, scroll down the page and click on the **Create Application** button.

    ![13-create-app.png](images/13-create-app.png "Create App")

1. Note the *API Credentials*. Write them down as you will need the **Client ID** and the **Client Secret** to test your integration.

    ![14-app-credentials.png](images/14-app-credentials.png "App Credentials")

*Congratulations!* You have now an application to test your OpenId Connect integration.

## Steps Beyond

So, you want more? Login to the Red Hat Single Sign On admin console for your realm if you are not there already. Click on the Clients menu. Now you can check that 3scale zync component creates a new Client in SSO. This new Client has the same ID as the Client ID and Secret from the 3scale admin portal.

### Test the integration

You can try to use Postman or OpenID Connet playground to test your integration. Remember to update the *Redirect URL*.

## Summary

Now that you can secure your API using three-leg authentication with Red Hat Single Sign-On, you can leverage the current assets of your organization like current LDAP identities or even federate the authentication using other IdP services.

For more information about Single Sign-On, you can check its [page](https://access.redhat.com/products/red-hat-single-sign-on).

You can now proceed to [Lab 5](../lab05/#lab-5)

## Notes and Further Reading

* [Red Hat 3scale API Management](http://microcks.github.io/)
* [Red Hat Single Sign On](https://access.redhat.com/products/red-hat-single-sign-on)
* [Setup OIDC with 3scale](https://developers.redhat.com/blog/2017/11/21/setup-3scale-openid-connect-oidc-integration-rh-sso/)