---
title: Static web apps
---

--sep--
---
title: Objectives & Prerequisites
---
## Objectives & Prerequisites

### Objectives

In this workshop, you will learn how to create a full application with a `frontend`, a `serverless backend`, `user authentication` and a `database` to store your data.

Don't worry if you are not familiar with Microsoft Azure. This workshop will walk you through some of the most important services if you are a web developer. We will see how to use `Cosmos DB` with the `MongoDB` API, `Azure Static Web Apps` to host your client application and `Azure Functions` for your backend and `GitHub Actions` to automate your app deployment!

At the end of this workshop, you will have a full understanding on how to develop and deploy a web app on Azure.

### Prerequisites

To do this workshop, you will need:
* Basic JavaScript knowledge
* A Microsoft Azure account
* A GitHub account
* Visual Studio Code (VSCode)
* Node.js 12 or higher installed
* Docker (optional)
* Azure Functions Core Tools (V3)

--sep--
---
title: What is Azure Static Web Apps
---

## What is Azure Static Web Apps

Azure Static Web Apps is a service that enables developers to deploy their web applications on Azure in a seamless way. This means developers can focus on their code and spend less time administering servers!

So, with Azure Static Web Apps (aka SWA), developers can not only deploy frontend static apps and their serverless backends but they can also benefit from features like `Custom domains`, `pre-prod environments`, `authentication providers`, `custom routing` and more.
 
### Who is it for?
Azure Static Web Apps is for every developer who wants to spend more time in their code editor than they do managing resources in the cloud.

If you are a so-called "Full stack developer", then you probably want to deploy both your frontend and your backend to the cloud, ideally with limited administration and configuration management.

### Front end developers
Azure Static Web Apps supports many frameworks and static site generators out of the box. If you are using a framework like `Angular`, `React`, `Vue.js`, a site generator like `Gatsby`, `Hugo` or one of the many solutions Azure Static Web Apps supports, then you don't have to take care of the deployment. If you have a specific need to customise the build for your app, you can configure it yourself very easily!

### Backend developers
Azure Static Web Apps relies on `Azure Functions` for your application backend. So, if you are developing in `JavaScript`, `Java`, `Python` or `.NET`, SWA makes it very easy to deploy your backend as well!

<div class="box info">
<div>
You can find the official Static Web Apps documentation here: 
<a href="https://aka.ms/swadocs?ocid=OCID&wt.mc_id=WTMCID" target="_blank">https://aka.ms/swadocs</a>
</div>
</div>

Oh, and did I forget to mention there is a Free tier for Static Web Apps? You can start using it for free and only pay once your application gets popular!

--sep--
---
title: Start with a website
---

## Start with a website

Once upon a time, there was a website that needed a place to live, be visible to the world and have a backend to be more interactive.

There are two ways you can start using the project template for this workshop

### From a GitHub Template

Go to <a href="https://github.com/tagazok/swa-workshop" target="_blank">this GitHub repository</a> and click on `Use this template`. 

![Add a Dev Container](media/githubtemplate.png)

You will be redirected to the repository creation page. Just enter a name for your new repository and click on `Create repository from template`.

### From a zip file
#### Download the website template

Download the website from the resources tab in the sidebar or click <a href="https://github.com/tagazok/my-workshops/raw/master/static-web-apps/data/swa-workshop.zip" target="_blank">here</a>.

#### Deploy your website on GitHub

Azure Static Web Apps has been built to work with GitHub by default. So, the first thing you will do is create a new GitHub repository and push the source code you just downloaded.

<div class="box assignment">
<div>
Choose your path
<ul>
<li>Create the repository from the GitHub Template</li>
<li>Go to <a href="https://github.com/" target="_blank">Github.com</a>, create a new repository and push your code to it.</li>
</ul>
</div>
</div>

You now have your baseline project. Open the `swa-workshop` folder in VSCode.

--sep--
---
title: Set up your environment using a container
---

## Set up your environment using a dev container

**Note:** This step is optional. You can either use a container as described below, or install all the tools yourself as we walk through the workshop.

There is not much you need to start working with `Azure Static Web Apps`. If you already have all the requirements listed at the beginning of the workshop, you are good to go. We will see at each step what are the tools and the VSCode extensions you will need to install.

However, if you don't want to install everything, or don't want to remember what is needed to build and deploy a Static Web App, we've got you covered.

Open VSCode and search for the `Remote - Containers` extension in the extension panel on the left or go <a href="https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers&ocid=OCID&wt.mc_id=WTMCID" target="_blank">here</a> and click `Install`.

The `Remote - Containers` extension lets you use a Docker container as a fully-featured development environment. The best part is that the extension comes with a list of containers already setup for you... including one for Static Web Apps.

So, open the VSCode command panel using `Ctrl + Shift + p` and search for `Add Development Container Configuration Files...`. This will show you a list of pre-configured containers. Search for `Azure Static Web Apps` and hit Enter.

![Add a Dev Container](media/dev-container.png)

A few files will be added to your project with all the container configurations.

You now need to reopen your project in the container. To do so, open the VSCode command panel and search for `Reopen in container`. Wait a few seconds until the docker image is ready and you are good to go. You now have all the tools installed to work with Static Web Apps.

<div class="box info">
<div>
The Container Extension uses Docker. If you don't have Docker already installed on your computer, go to <a href="https://www.docker.com/get-started" target="_blank">https://www.docker.com/get-started</a> to download and install it.
</div>
</div>


--sep--
---
title: Create an Azure Static Web App
---

## Create an Azure Static Web App

Start by opening the <a href="https://portal.azure.com/#create/Microsoft.StaticApp?ocid=OCID&wt.mc_id=WTMCID" target="_blank">Create Static Web App form</a> in the Azure Portal. This link will take you directly to the Static Web App creation form. You may be prompted to log into your Azure Subscription. If you don't have one you can create a Free trial.  

Let's fill it out!

* Select your Subscription.
* Create a new Resource Group.

<div class="box info">
In Azure, a Resource Group is a logical structure that holds resources usually related to an application or a project. A Resource Group can contain virtual machines, storage accounts, web applications, databases and more.
</div>

* Give a Name to your Static Web App.
* Select the Free Plan (we won't need any feature in the Standard Plan for this workshop).
* Select `West Europe` for your backend.

<div class="box tip">
It is recommended to host your backend in a Region closest to your users.
</div>

* Select `GitHub` as a deployment source.

We are going to host our website source code on GitHub. Later in the workshop, we will see how Static Web Apps will automatically deploy our website every time we push new code to our repository.

* Sign in with your GitHub account and select the repository and the branch of your project.

As we mentioned at the beginning of the workshop, our app will have a backend and a frontend. In order for Static Web App to know what to deploy and where, we need to tell it where our apps are located in our repository.

Azure Static Web Apps can handle several well-known frontend frameworks and can "compile" your Angular, React or Hugo application before deploying them.

In our case, we have a very simple JavaScript application which does not require anything to run. So, let's choose `Custom`.
* In the `App location`, enter the `/www` folder as this is where our frontend is.
* In the `Api location`, enter the `/api` folder as this is where our backend is.
* In the `Output`, enter the `/www` folder as your frontend does not need any build system to run.

![Enter GitHub information when creating SWA](media/swa-github.png)

* Click on `Review + Create` and then on `Create`.

After a few minutes, your Static Web App will be created on Azure and your website deployed.

Once the resource is created, you should `pull` your repository in VSCode as a few files have been added to your GitHub repo by Azure.

## So, what just happened?

### On GitHub

When Azure created your Static Web App, it pushed a new YAML file to the `.github/workflow` folder of your repository.

The files in this folder describe GitHub Actions, which are event-based actions that can be triggered by events like a `push`, a `new pull request`, a `new issue`, a `new collaborator` and more. 

You can see the complete list of triggers <a href="https://docs.github.com/en/actions/reference/events-that-trigger-workflows" target="_blank">here</a>

<div class="box info">
<div>
If you are not familiar with GitHub Actions, you can read about them <a href="https://github.com/features/actions" target="_blank">here</a>.
</div>
</div>

Let's have a look at the YAML file Azure created for us:

```yaml
on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - main
```

Here, you can see that the GitHub Action is going to be triggered every time there is a `push` on the `main` branch or every time a Pull Request is `opened`, `synchronize`, `reopened` or `closed`.  

As we want our website to be redeployed automatically every time we push on our main branch, this is perfect!

Take a few minutes to read the YAML file and understand what exactly happens when the GitHub Action is triggered. You can see that most of the information you entered when you created your Static Web App on Azure is here.

<div class="box tip">
The YAML file is in your GitHub repository so you can edit it! Your frontend site folder name changed? No problem, just edit the file and push it to GitHub!
</div>

Now, go to your GitHub repository in a web browser and click on the `Actions` tab. Here, you will see the list of all the GitHub Actions that have been triggered so far. Click on the last one to see your application being deployed.

![Check your GitHub Actions](media/github-actions.png)

### On Azure

Once your Static Web App is created, go to the Resource page. You can find the list of all your Static Web Apps <a href="https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Web%2FStaticSites?ocid=OCID&wt.mc_id=WTMCID" target="_blank">here</a>

In the Overview panel of your Static Web App, look for the `URL` parameter. This is the url of your website. 

![Resource overview of your project](media/resource-overview.png)

Open the link and you can see that your TODO list app has been deployed and is accessible to the world!

Congratulations, you just deployed your first Static Web App on Azure! 🥳

--sep--
---
title: Let's add a backend
---

## Let's add a backend

Now that our TODO frontend is deployed, we want to make it interactive and need to add a backend!  

Azure Static Web Apps relies on Azure Functions for your application backend. Azure Functions is an Azure service which enables you to deploy simple code-based microservices triggered by events. In our case, events will be HTTP requests.

<div class="box info">
Ever heard of Serverless or FaaS (Function as a Service)? Well, you get it, this is what Azure Functions is ^^.
</div>

### Installation

You can create an Azure Function from the <a href="https://portal.azure.com/?ocid=OCID">Azure portal</a> but let's be honest, it's so much easier to stay in VSCode and use the Azure Functions extension.

So, start by installing the Azure Function extension from VSCode.

You can download the extension either directly from the `Extension panel (Ctrl + Shift + X)` in VSCode or by going <a href="https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions&ocid=OCID&wt.mc_id=WTMCID" target="_blank">here</a> and clicking on the `Install` button.

### Create your Function app

Azure Functions live in an Azure Functions App. When you create your Function App, a single Azure Function will be created by default. You can then add more Functions as required.

So, let's create our Functions App and a Function to retrieve our task list for our TODO frontend.

* In VSCode, open the Command panel and search for `Azure Functions: Create new project`. 
* Select the `api` folder. This is where our Function App will be created.
* Choose `JavaScript` as this is the language we are going to use to write our Function.

<div class="box info">
Azure Static Web Apps don't support all the languages you can develop Azure Functions with. Supported backends can be developed using  JavaScript, TypeScript, Python or C#.
</div>

* As we are creating a REST API that will be called by our website, the trigger we are looking for is the `HTTP trigger`. 
* Our first Function will be used to retrieve our task list. Let's call it `tasks-get`. 
* Select the `Anonymous` authorization level.

<div class="box info">
<div>
If you want to learn more about the different authorization levels for Functions and how to secure your API, check out the docs <a href="https://docs.microsoft.com/azure/azure-functions/security-concepts?ocid=OCID&wt.mc_id=WTMCID" target="_blank">here</a>.
</div>
</div>

A Function scaffold will be created for you so you don't start with a blank project. Let's modify the scaffold for our needs.

Right now, we don't have a database to store our users or our tasks so let's use an array as a "fake" database.

```json
const tasks = [
    {
        id: 1,
        label: "🍔 Eat",
        status: ""
    },
    {
        id: 2,
        label: "🛏 Sleep",
        status: ""
    },
    {
        id: 3,
        label: "</> Code",
        status: ""
    }
];
```

<div class="box assignment">
<div>
Modify the Azure Function so it returns the list of tasks.
</div>
</div>

Once deployed, you will be able to call your function like any REST API. 

### Configure your endpoints

By default, when an Azure Function is created using the VSCode extension, the function will support `GET` and `POST` requests and the URL will end with your function name. In our case, the `tasks-get` function can either be called using
* `GET https://your-website-url.com/api/tasks-get`
* `POST https://your-website-url.com/api/tasks-get`

This is not exactly what we need. Thankfully, there is a way to configure this. Open the `function.json` file in your Function folder.

```json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "type": "httpTrigger",
      "direction": "in",
      "name": "req",
      "methods": [
        "get",
        "post"
      ]
    },
    {
      "type": "http",
      "direction": "out",
      "name": "res"
    }
  ]
}
```
Here, you can find most of the information you selected when you created your Function. 

As we only need our Function to retrieve a list of tasks, let's remove the `POST` method in the methods array so our Function can only be called using `GET` requests.

The other thing you may want to change is the URL of your Function. Having a route called `/api/tasks-get` is not very standard. You can easily change your endpoint name in the `function.json` file by adding a `route` parameter.

```json
{
    ...,
    "methods": ["get"],
    "route": "tasks"
    ...
}
```

Now, your Function is only accessible using a `GET /api/tasks` request.

You've done it! You wrote your first Azure Function. Congratulations! 🥳

--sep--
---
Title: Test you project locally
---

## Test your project locally

There are two ways to test your project. You can either push your code on GitHub every time you need to test it (not recommended), or use the `Static Web Apps CLI`.

### The Static Web App CLI

The Static Web Apps Command Line Interface, also known as the `SWA CLI`, serves as a local development tool for Azure Static Web Apps. In our case, we will use the CLI to:

* Serve static app assets
* Serve API requests
* Emulate authentication and authorization
* Emulate Static Web Apps configuration, including routing

You can install the CLI via npm.

```bash
npm install -g @azure/static-web-apps-cli
```

We are only going to use a few features of the CLI so if you want to become a SWA CLI expert, you can find all the features the CLI provides <a href="https://github.com/Azure/static-web-apps-cli" target="_blank">here</a>

### Run your project locally

The CLI offers many options, but in our case we want it to serve both our API located in our `api` folder and our web application located in our `www` folder.

In your terminal, type the following command to start your project:

```bash
swa start ./www --api ./api
```

This CLI gives you two urls:

* <a href="http://localhost:4280" target="blank">http://localhost:4280</a> corresponding to your frontend.
* <a href="http://localhost:7071/api/tasks" tartet="_blank">http://localhost:7071/api/tasks</a> corresponding to your API.

<div class="box tip">
<div>
The CLI may take more time than usual to launch your Azure Function, especially the first time. The default timeout is 30 seconds but you can increase it by using the <code>--devserver-timeout=60000</code> parameter
</div>
</div>

Congratulations, you now have everything you need to test your app on your computer! 🥳

--sep--
---
title: Add authentication
---

## Add authentication

Azure Static Web Apps manages authentication out of the box. There are pre-configured providers and you can add your own custom providers if needed. Among the pre-configured ones are `Twitter` are `GitHub`

<div class="box info">
If you are using the CLI, you won't really be connecting to the selected provider. The CLI offers a proxy to simulate the connection to the provider and gives you a fake userId.
</div>

### Sign in & Sign out

When I said "out of the box", I really meant it. You don't need to do anything for most of the providers. Let's use the GitHub one for our application. The only thing you will have to do is add a button in your frontend that redirects to `/.auth/login/github`.

<div class="box assignment">
<div>
Add a button in the login.html so your users can sign in using GitHub. Then, navigate to <a href="http://localhost:4280/login.html" target="_blank">http://localhost:4280/login.html</a>.
</div>
</div>

By default, once logged in, your users are redirected to the same page. However, we would like our users to be redirected to our TODO page after successfully logging in. You can do that by using the `post_login_redirect_uri` query param at the end of the url.  
Eg. `?post_login_redirect_uri=/index.html` 

<div class="box tip">
<div>
If you are building a React app, go <a href="https://docs.microsoft.com/learn/modules/publish-static-web-app-authentication/?ocid=OCID&wt.mc_id=WTMCID" target="_blank">check the Microsoft Learn module</a> that will show you how to do it.
</div>
</div>

### Getting user information

Once your user is authenticated, you can retrieve the user's information by fetching the url `/.auth/me`. This will return some JSON containing a clientPrincipal object. If the object is null, the user is not authenticated. Otherwise, the object contains data like the provider, the roles and the username.

```json
{
  "identityProvider": "github",
  "userId": "d75b260a64504067bfc5b2905e3b8182",
  "userDetails": "tagazok",
  "userRoles": ["anonymous", "authenticated"]
}
```
The `userId` is unique and can be used to identify the user. We will use it later in our database.

<div class="box assignment">
<div>
Complete the <code>getUser()</code> method to retrieve the logged-in user information and display the username in the <code>&lt;div id=&quot;username&quot;&gt;&lt;/div&gt;</code> element located at the top left of your web page.
</div>
</div>

![Your TODO app is running](media/todo.png)

Congratulations, you can now log into your app! 🥳

--sep--
---
Title: Routes & Roles
---

## Routes & Roles

In many cases, your routes will be managed by your frontend, especially if you are using a framework such as React or Angular. 

You may also be used to managing authorization on your backend for your API calls.

Azure Static Web Apps offers you the possibility to handle HTTP requests in a single file. Start by creating a file called `staticwebapp.config.json` in your `www` folder.

<div class="box info">
<div>
You need to restart the CLI each time you make a change in the <code>staticwebapp.config.json</code> file.
</div>
</div>

### Secure our website and APIs

There are many properties available to configure your Static Web App but let's concentrate only on the few we need in our app.

The `routes` parameter is an array of all the rules for your routes. For example, in our case, we would like to prevent unauthenticated users from calling our API. We can do that very easily.

```json
{
   "routes": [
      {
          "route": "/api/tasks/*",
          "allowedRoles": [
              "authenticated"
          ]
      }
    ]
}
```

What if we want to restrict a part of our frontend to authenticated users? We can do exactly the same with any frontend route.

```json
{
   "routes": [
      {
          "route": "/",
          "allowedRoles": [
              "authenticated"
          ]
      }
    ]
}
```

Now you have made this change your website root will only be accessible to logged in (authenticated) users.

### Manage HTTP error codes

 You will notice that your unauthenticated users are redirected to a default 401 (HTTP Unauthorized) web page. We can customise that using another property in the config file. The `responseOverrides` property enables you to redirect a user to a specific page when an HTTP code is returned. Let's redirect all non-authenticated users to the `login.html` page.

```json
{
   "responseOverrides": {
        "401": {
            "rewrite": "/login.html"
        }
    },
}
```

Here, we simply tell our Static Web App to redirect every 401 response to the `login.html` page.

<div class="box assignment">
<div>
Create a <code>custom-404.html</code> page in your www folder and add a rule to redirect users to this page when they enter a URL which does not exist (HTTP error code 404).
</div>
</div>

Now, try to go to a non-existent page on your website like `/hello.html`. You should be redirected to the `custom-404.html` page you just created.

<div class="box tip">
<div>
This is also very useful if you are doing a Single Page Application (SPA) where the routing is managed on the client. You may then need to redirect all your URLs to <code>index.html</code>. Check the <code>navigationFallback</code> property in the documentation <a href="https://docs.microsoft.com/azure/static-web-apps/configuration?ocid=OCID&wt.mc_id=WTMCID" target="_blank">here</a>.
</div>
</div>

Congratulations, your website and your APIs are now secured and you have a seamless workflow for your users. 🥳

--sep--
---
title: Store your data in a database
---

## Store your data in a database

There are several databases available on Azure. One of the most powerful ones is `Cosmos DB`. Azure Cosmos DB is a fully managed NoSQL database which supports several APIs. When you create your Cosmos DB Database, you can choose which API you want to use. Among the most popular ones are `MongoDB`, `SQL` and `Cassandra`.

### Set up your dev environment

Let's go back to our Azure Function in VSCode. We will be using the Cosmos DB MongoDB API, so we need a library to connect to our database. In the `/api` folder, open the `package.json` file and add `"mongodb": "^4.0.1"` to the `dependencies` property as shown below.

```json
...
  "dependencies": {
    "mongodb": "^4.0.1"
  },
...
```

In a terminal, type `npm install` and hit enter. This will download the dependencies for you to the `node_modules` folder of your Azure Functions App.

While you are in VSCode, let's install the `Azure Database` extension. This will allow you to explore your database and make queries from VSCode without having to go to the Azure Portal.

In the extension menu of VSCode, search for `Azure Database` or <a href="https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb&ocid=OCID&wt.mc_id=WTMCID" target="_blank">here</a> and click on `Install`.

### Create your database

Start by opening the <a href="https://portal.azure.com/#create/Microsoft.DocumentDB?ocid=OCID&wt.mc_id=WTMCID" target="_blank">Create Azure Cosmos DB form</a> in the Azure Portal. For our application, we are going to use the `MongoDB` API so select `Azure Cosmos DB API for MongoDB`

* Select your Subscription.
* Select the same Resource Group you used earlier in this workshop.
* Enter a name to identify your Cosmos DB Account. This name must be unique.
* Select the Location where your Account is going to be hosted. We recommend using the same location as your Static Web Apps. 
* Select `Provisioned throughput` there and ensure you select the Free Tier Discounts.
* Select `Apply` when asked if you want to Apply the free tier discount
* Click on `Review + Create` and then on `Create`.

Creating the Cosmos DB Accounts may take some time so grab a cup of hot chocolate and be ready to deal with Cosmos DB!

☕

OK, let's go back to VSCode. In the Azure Extension, you now have the `Database` tab where you should see the Cosmos DB Account you just created. If you don't see it, just click the refresh button.

Once you see your Account, right click on it, select `Create Database` and enter a name. Once your Database is created, right click on it, select `Create Collection` and name it `tasks` as it will be used to store our tasks.

![Create a Cosmos DB database](media/create-db.png)

### Add some data

Let's focus on our existing Azure Function. We will see later how to create a Function to add new tasks in our database.  

Right now, we just want to get our tasks from the database instead of the static JSON array we created earlier in our Function.

In VSCode, right click on your `tasks` collection and select `Create Document`. Copy and paste a task of the following json and make sure to replace the userId by the one of your logged in user. To find the userId, just log into your web application and navigate to `/.auth/me`

```json
{
  "_id": {
    "$oid": "AUTO-GENERATED"
  },
  "userId": "YOUT-USER-ID",
  "label": "Buy tomatoes",
  "status": "checked"
}
```

Do it again for the two following tasks

```json
{
  "_id": {
    "$oid": "AUTO-GENERATED"
  },
  "userId": "YOUT-USER-ID",
  "label": "Learn Azure",
  "status": ""
}
```

```json
{
  "_id": {
    "$oid": "AUTO-GENERATED"
  },
  "userId": "YOUT-USER-ID",
  "label": "Go to space",
  "status": ""
}
```
### Let's code

Now that we have our database setup and have added some data to it, let's make sure our user interface displays it!

In your `tasks-get` Azure Function, start by importing the `mongoClient` from the MongoDB library we installed earlier.

```javascript
const mongoClient = require("mongodb").MongoClient;
```

When your Static Web App calls the API, the user information is sent to the Function in the `x-ms-client-principal` HTTP header. 

You can use the code below to retrieve the same user JSON you get in the `clientPrincipal` property when you go to `/.auth/me`.

```javascript
const header = req.headers['x-ms-client-principal'];
const encoded = Buffer.from(header, 'base64');
const decoded = encoded.toString('ascii');
const user = JSON.parse(decoded);
```

Let's see how the MongoDB API works:

* First, your need to connect to your server (in our case our Cosmos DB Accounts)

In order to connect your application to your database, you will need a connection string.  

You can find your server connection string in the Azure Portal. But, as always, you can stay in your VSCode. In the Azure Database extension, right click on your database server and select `Copy Connection String`.

![Retrive your Cosmos DB connection string](media/connection-string.png)

Now, let's connect!  

You have two ways to connect, a clean and secure way and the quick and dirty way...

#### The clean and secure way

It's not safe to store your private key or connection strings in your code. Azure Static Web Apps provides a way to store environment variables that you can then use in your app.


To check how to add your MongoDB connection string in the environment variables of your Static Web App, check this quick video.

<a href="https://www.youtube.com/watch?v=R9qhGra9FHs&list=PLlrxD0HtieHgMPeBaDQFx9yNuFxx6S1VG&t=112s" target="_blank">
  <img src="media/swa-tips-video-environment.png">
</a>

#### The quick and dirty way

```javascript
const client = await mongoClient.connect("YOUR-SERVER-CONNECTION-STRING");
```

### Request your data

Once you are connected to your Cosmos DB server using the MongoDB API, you can use this connection to select a database.

```javascript
const database = client.db("YOUR-DB-NAME");
```

Replace `YOUR-DB-NAME` by the name you entered when you created your database.

Then, query the document where the userId property is the same as the userId sent in the headers when your Function is called.

```javascript
const response = await database.collection("tasks").find({
    userId: user.userId
});

const tasks = await response.toArray();
```

<div class="box assignment">
  Update your Azure Function so it returns the tasks in the database associated with your logged in user.
</div>

Test your website locally and push your changes to GitHub. The GitHub Action will be triggered and your website deployed. Go check the public URL, you should see the tasks of your database.

![Your TODO app up and running](media/finish.png)


--sep--
---
Title: Bonus
---

## Bonus

### Finish your application

You now know how to create and publish an app with a frontend, a backend, a database and some user authentication.

However, in order to make your TODO app fully functional, you need to add a few more features. The good news? You have everything you need to do it!

#### Add a new task

We have already added the source code to call the API in the frontend so all you need to do is to create the Azure Function and connect it to the database.  

<div class="box assignment">
Create one Azure Function to add a new task to the database. You don't need to create a new project, just create a new Function in your existing Function App project in VSCode.
</div>


#### Update a task

You may have noticed that there is a <code>status</code> attribute in every task in your database. The value can be either <code>""</code> or <code>"checked"</code>. Right now, there is no way to change this status.   

<div class="box assignment">
Write an Azure Function and the JavaScript code in your frontend to update this status.
</div>

### Monitor your app

You now know how to create ressources on Azure and how connection strings work. 

You may have noticed that, once deployed, we don't have any logs for our app which means we have no way to know what happens if there are any issues.

<div class="box assignment">
<div>
Create an <a href="https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview?ocid=OCID&wt.mc_id=WTMCID" target="_blank">Application Insights</a> resource in your Resource Group and connect it to your Static Web App.
</div>
</div>

--sep--
---
Title: Conclusion
---

## Conclusion

Congratulations, you've reached the end of this workshop!

## Solution

You can download the completed app code with the features to add and update a task <a href="https://github.com/tagazok/my-workshops/raw/master/static-web-apps/data/swa-workshop-final.zip" target="_blank">here</a>
