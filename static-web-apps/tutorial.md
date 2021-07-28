---
title: Static web apps
---

--sep--
---
title:
---
# Introduction to Static Web Apps

## what is Azure Static Web Apps

Static web front end + backend powered by Azure Functions + neat additional features  

Custom domains + pre-prod environment + authentification providers, custom routing, etc  

Based on GitHub  

Free plan ?  

aka.ms/swadocs

## For who ?

### Front end
Angular, React,  Vue, Svelt, Gatsby, Hugo & more

### Backend
JavaScript, Java, Python, .Net

## Tools
GitHub Account + Azure Accounts (add links)

Any code editor but VSCode has some great extensions !
- VSCode (list extensions : SWA + Functions)
- CLIs (Functions Core Tools & SWA CLI)

```bash
npm install -g @azure/static-web-app-cli
```
Requieres nodejs (link to video)  

--sep--
---
title: Setup your environment using dev container
---

Don't know what a dev container is ? see video

// TODO: Check if need docker ?

Click on the remote development extension icon and select `Add Development Container Configuration Files...` and search for `Azure Static Web Apps`

A few files will be added to your project with all the container configurations

Click again on the remote development extension icon to reopen your project in a container.

So what just happened? A docker image is mounted with all the tools you need to work on your Progressive Web App


--sep--
---
title: Start with a website
---

Once upon a time, there was a website that needed a place to live, be visible to the world and a backend to be more interactive.

### Download the website template

Download from resources on the left or <a href="" target="_blank">here</a>

### Deploy your website on GitHub

Azure Static Web Apps has been built from the start to work with GitHub so, the first thing you will do is to create a new GitHub repo and push the source code you just downloaded.

Go on <a href="https://github.com" target="_blank">Github.com</a>, create a new repository and push you code to it.

--sep--
---
title: Create a Azure Static Web App
---

## Create a Azure Static Web App

In the <a href="https://portal.azure.com/" target="_blank">Azure Portal</a>, look for `Static Web App` in the search bar. Once you are on the product page, click on the `Create` button at the top left. Or, you can directly click <a href="https://portal.azure.com/#create/Microsoft.StaticApp" target="_blank">here ^^</a>. This link will  take you directly to the Static Web App creation form.  

Let's fill it!

* Select your subscription.
* Create a new resource group.

<div class="box info">
In Azure, a resource group is a logical container that holds resources usually related to an application or a project. A resource group can therefore contain virtual machines, storage accounts, web applications, databases and more.
</div>

* Give a name to your Static Web App.
* Select the free plan (we won't need any feature in the standard plan for this workshop).
* Select `West Europe` for your backend.

<div class="box tip">
It is recommended to host your backend in the closest region of your users.
</div>

* Select `GitHub` as a deployment source.

We are going to host our website on GitHub. Later in the workshop, we will see how Static Web Apps will automaticaly deploy our website every time we push new code to our repository.

* Log in with your GitHub account and select the repository and the branch of your project.

As we mentioned at the begining of the workshop, our app will have a backend and a frontend. In order for Static Web App to know what to deploy and where, we need to tell it where our apps are located in our repository.

Azure Static Web Apps can handle several well-known frontend frameworks and therefore, "compile" your Angular, React or Hugo application before deploying it.

In our case, we have a very simple Vanilla JavaScript appliation which does not require anything to run. So, let's choose `Custom`.
* In the `App location`, enter the `www/` folder as this is where our frontend is.
* In the `Api location`, enter the `api/` folder as this is where our backend is.

* Click on `Review + Create` and then on `Create`.

After a few minutes, your static web app will be created on Azure and your website deployed.

## So, what happened?

    
### On GitHub

When Azure created your Static Web App, it pushed a new YAML file in in the `.github/workflow` folder of your repository.

<div class="box info">
The files in this folder decribe the GitHub Actions, which are event-based actions that can be triggered by events like a `push`, a `new pull request`, a `new issue`, a `new collaborator` and many many more.  

You can see the complete list of triggers <a href="https://docs.github.com/en/actions/reference/events-that-trigger-workflows" target="_blank">here</a>

If you are not familiar with GitHub Actions, go have a look <a href="https://github.com/features/actions" target="_blank">here</a>.
</div>

Let's have a look at the YAML file Azure created for us:
```
on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - main
```
Here, you see that the GitHub Action is going to be triggered every time there is a push on the `main branch` or everytime a pull request is `opened`, `synchronize`, `reopened` or `closed`.  
As we want our website to be redeployed automaticaly every time we push on our main branch, this is perfect!

Take a few minutes to read the YAML file and understand what exactly happens when the GitHub action is triggered. You can see that most of the information you entered when you created your Static Web App on Azure is here.

<div class="box tip">
The YAML file is in your GitHub repo so you can edit it! Your frontend site folder name changed? No problem, just edit the file and push it on GitHub.
</div>

So, go back to your GitHub repo and click on the `Actions` tab. Here, you will see the list of all the GitHub actions that have been triggered so far. Click on the last one to see your application being deployed

![Configuration des variables d'environnement dans Azure Function](media/github-actions.png)
### On Azure

Once your Static Web App is created, go to the Resource page. You can find the list of all your Static Web Apps <a href="https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Web%2FStaticSites" target="_blank">here</a>

In the overview panel of your resource, look for the `URL` parameter. This is the url of your website. 

![Configuration des variables d'environnement dans Azure Function](media/resource-overview.png)


Go have a look, your TODO list app has been deployed and is accessible to the world!

Congratulations, you just deployed your first Static Web App on Azure !


--sep--
---
title: Let's add a backend
---

Now that our TODO app is deployed, we want to make it interactive, we want to interact with a backend!  

Azure Static Web Apps relies on Azure Functions for your application backend. Azure Functions is an Azure Service which allows you to deploy simple functions triggered by events. In our case, events will be HTTP calls.

<div class="box info">
Ever heard of Serverless or FaaS (Function as a Service)? Well, this is what Azure Functions is ^^.
</div>


## Installation

You can create an Azure Function from the portal but let's be honnest, it's so much easier to stay in VSCode and use the Azure Functions extension.

So, start by installing the Azure Function extension from VSCode.
You can download the extension either from the `Extension panel` (Ctrl+Shift+X) directly in VSCode or <a href="https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions" target="_blank">here</a>

## Create your Function app

In VSCode, open the Command panel and search for `Azure Functions: Create Function App in Azure`. As we are creating an API that will be called by our website, the trigger we are looking for is the `HTTP trigger`.  

A function template will be created for you. Let's modify it for our needs.

--sep--
---
Title: Test you project locally
---

## Test your project

There are two way to test your project now. You can either push your code on GitHub (not recommended), or use the Static Web Apps CLI

### The Static Web App CLI

The Static Web Apps CLI, also known as SWA CLI, serves as a local development tool for Azure Static Web Apps. In our case, we will use the API to:
* Serve static app assets
* Serve API requests
* Emulate authentication and authorization
* Emulate Static Web Apps configuration, including routing


You can install the CLI using npm.
```bash
npm install -g @azure/static-web-apps-cli
```

Fin all the features the CLI provides <a href="https://github.com/Azure/static-web-apps-cli" target="_blank">here</a>

### Run your project locally

The CLI offers many options but in our case, we want it to serve both our API located in our `api` folder and our web application located in our `www` folder.

In your terminal, type the following command to start your project.

```bash
swa start ./www --api ./api --devserver-timeout=60000
```

This CLI gives you several urls:
* http://0.0.0.0:4280 corresponding to your frontend
* http://localhost:7071/api/tasks corresonding to you api

<div class="info">
The CLI may take time to launch your Azure Function. The default timeout is 30 seconds but you can increase it using the `--devserver-timeout=60000` parameter
</div>

--sep--
---
title: Add authentication
---

SWA manages authentication out of the box. There are pre-configured providers but you can add you own custom providers. Among the pre-configured ones are Twitter, Google, Microsoft, GitHub and others.

## The different urls

When we said "out of the box", we really meant it. You don't need to do anything for most of the provider. Let's use the GitHub one for our application. The only thing you will have to do is a button that redirect to `/.auth/login/github`.

Go add a button in the `login.html` page.

By default, once logged in, your user is redirected to the same page. However, we would like our user to be redirected to our TODO page after successfully logging in. You can do that by using the `post_login_redirect_uri` query param at the end of the url. Eg. `?post_login_redirect_uri=/index.html` 

## Getting user informations

Once your user is authenticated, you can retrieve the associated information by fetching the url `/.auth/me`. This will return a json containing a clientPrincipal object. If the object is null, the user is not authenticated. Otherwize, the object contains several data

```javascript
{
  "identityProvider": "github",
  "userId": "d75b260a64504067bfc5b2905e3b8182",
  "userDetails": "tagazok",
  "userRoles": ["anonymous", "authenticated"]
}
```
The userId is unique and can be used to identify the user. We will use it to refer to the user in the database.


If you are building a React app, go <a href="https://docs.microsoft.com/en-us/learn/modules/publish-static-web-app-authentication/?WT.mc_id=javascript-17844-cxa" target="_blank">check the MSLearn module that will show you how to do</a> 



--sep--
---
Title: MISC
---




`staticwebapp.config.json`

So what do we want? We want the our JavaScript framework to handle the routes so we simply ask Staticweb app to redirect all urls to index.html

However, we don't want our router to mess with our assets so let's exclude all the other resources like stylesheets or images.

```javascript
{
    "navigationFallback": {
        "rewrite": "/index.html",
        "exclude": ["*.{css,scss,js,png,gif,ico,jpg,svg}"]
    }
}
```
However, you can still overide all the urls you want here. Let's say you have a new url for your products list as `products` makes more sense than `catelog`. You can easily do that in the `routes` object.

```javascript
{
    ...,
    "routes": [
        {
            "route": "/catalog",
            "redirect": "/products"
        }
    ]
}
```

--sep--
---
title: Authorization
---

Now that our user can auehtnticate, what about adding a layer of authorization as we only want our authenticated users to access our product list.


--sep--
---
title: 
---


Topics:
CI/CD preview branches (GitHub Actions) Video 4/16
Edit app, api and output location in the github action (video 4/16)