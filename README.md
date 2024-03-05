# Meraki Portal Auth with Azure Active Directory 

This Node.js app was created to facilitate the authorization of users registered on an Azure Active Directory with Meraki wireless infrastructures. Instead of using a RADIUS server for the authentication, you can spin up a web server that will be serving as your Captive Portal, which will then authenticate the user using MSAL

## References
This application and the step by step below were created / cloned based on the code provided by Microsoft, hosted [here](https://github.com/Azure-Samples/ms-identity-node/tree/main). Additionally, the information available at Meraki's [documentation](https://create.meraki.io/build/captive-portal-with-client-side-javascript/) about building your own JavaScript captive portal.

## Quick Start
In order to work with Meraki's captive portal, your server will need to run on a publicly available IP, i.e., you will need to host it out in the Internet. There are several alternatives to address this. For development purposes, I recommend using ngrok, which will create introspectable tunnels to your localhost. For production environments, I'd use Heroku, which is a PAAS that has a free tier of service.

* Getting Started on Heroku with Node.js - [Getting started guide](https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction)
* ngrok - [How it works](https://ngrok.com/product)

If you're using ngrok, run this command:

```
$ ngrok http 3000
```

Once you have the public URL where the server will run, take note of that. I'll refer to it as `http://public-url.example.com` on this document.

## Meraki Dashboard Setup

The steps below were copied from Meraki's official documentation [Configuring a Custom-Hosted Splash Page
](https://documentation.meraki.com/MR/Splash_Page/Configuring_a_Custom-Hosted_Splash_Page)

### Configure Access Control
* In Dashboard, navigate to Configure > Access control.
* Select the SSID you want to configure from the SSID drop-down. 
* Under Network access > Association requirements, choose "Open", "WPA2," or "WEP." 
* Under Network access > Network sign-on method, choose "Click-through splash page" or "Sign-on splash page." 
* Enable walled garden (located under Network access > Walled garden) and enter the public IP address or domain name of your web server.
* Click "Save Changes." 


### Enabling a Custom-Hosted Splash page on the Meraki Cloud
* Navigate to Configure > Splash page
* Select the SSID you want to configure from the SSID drop-down.
* Under Custom splash URL select the radio button Or provide a URL where users will be redirected:
* Type the URL of your custom splash page:
	`http://public-url.example.com/login`
* Click Save Changes.

## Azure Setup
As seen on [https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS)

### Step 1: Register an Azure AD Tenant
To use this sample you will need a Windows Azure Active Directory Tenant. If you're not sure what a tenant is or how you would get one, read [What is an Azure AD tenant](http://technet.microsoft.com/library/jj573650.aspx)? or [Sign up for Azure as an organization](http://azure.microsoft.com/en-us/documentation/articles/sign-up-organization/). These docs should get you started on your way to using Windows Azure AD.

### Step 2: Download node.js for your platform
To successfully use this sample, you need a working installation of Node.js.

### Step 3: Download the Sample application and modules

Next, clone the sample repo and install the NPM.

From your shell or command line:

* `$ clone this git https://github.com/dcoladmin/meraki-azure-ad`
* `$ npm install`

### Step 4: Configure your server

* Provide the parameters in .env.dev


### Step 5: Run the application

* Run the app. Use the following command in terminal.

```
$ node app.js
```

### You're done!
You will have a server successfully running on `http://localhost:3000`.

## User Experience
When the user selects the configured wireless SSID, a splash page will be shown prompting for their Azure AD Credentials.

### Written by 
Brayton Stafford
2023
