---
title: Static web apps
---

--sep--
---
title: Objectives & Prerequesites
---
## Objectives & Prerequesites

### Objectives

In this woskhop, you will learn how to create a full application with a `frontend`, a `serverless backend`, `user authentication` and a `database` to store your data.

Don't worry if you are not familiar with Microsoft Azure. This workshop will walk you through some of the most important services if you are a web developer. We will see how to use `Cosmos DB` with the `MongoDB` API, `Azure Static Web Apps` to host your client application and your `Azure Functions` and `GitHub Actions` to automate your app deployment!

At the end of this workshop, you will have a full understanding on how to develop and deploy a web app on Azure.

### Prerequisites

To do this workshop, you will need:
* Basic JavaScript knowledge
* A Microsoft Azure account
* A GitHub account
* VSCode
* Node.js 12 or higher installed

--sep--
---
title: What is Azure Static Web Apps
---

## What is Azure Static Web Apps

Azure Static Web Apps is a service that enables developers to deploy their web applications on Azure in a seemingless way. Therefore, developers can focus on their code and spend less time adminstrating servers!

So, with Static Web Apps (aka SWA), developers can not only deploy frontend static apps and their serverless backends but they can also benefit from some nice features like `Custom domains`, `pre-prod environment`, `authentication providers`, `custom routing` and more.
 

### For who ?
Azure Static Web Apps is for every developer who wants to spend more time in their code editor than managing resources in the cloud.
If you are a so-called "Full stack developer", then you probably want to deploy both your frontend and your backend in the cloud, hopefully with limited administration and configuration.

### Front end developers
Azure Static Web Apps supports many frameworks and static site generators out of the box. If you are using a framework like `Angular`, `React`, `Vue.js`, a site generator like `Gatsby`, `Hugo` or one of the many solutions Azure Static Web Apps supports, then you don't have to take care of the deployment. And, if you have a specific need to build your app, you can configure it yourself very easily!

### Backend developers
Azure Static Web Apps relies on `Azure Functions` for your application backend. So, if your are developing in `JavaScript`, `Java`, `Python` or `.Net`, SWA makes it very easy to deploy your backend!

<div class="box info">
<div>
You can find the official Static Web Apps documentation here: 
<a href="
aka.ms/swadocs" target="_blank">https://aka.ms/swadocs</a>
</div>
</div>

Oh, and did I forget to mention there is a Free tier for Static Web Apps? You can start using it for free and only pay once your application gets popular!


--sep--
---
title: Start with a website
---

## Start with a website

Once upon a time, there was a website that needed a place to live, be visible to the world and a backend to be more interactive.

There are two ways you can start using the project template

### From a GitHub Template

Go to <a href="https://github.com/tagazok/swa-workshop" target="_blank">this GitHub repository</a> and click on `Use this template`. 

![Add a Dev Container](media/githubtemplate.png)

You will be redirected to the repository creation page. Just enter a name for your new repository and click on `Create repository from template`.

### From a zip file
#### Download the website template

Download the website from the resources tab in the sidebar or click <a href="https://github.com/tagazok/my-workshops/raw/master/static-web-apps/data/swa-workshop.zip" target="_blank">here</a>.

#### Deploy your website on GitHub

Azure Static Web Apps has been built from the begining to work with GitHub. So, the first thing you will do is create a new GitHub repository and push the source code you just downloaded.


<div class="box assignment">
<div>
Choose your path
<ul>
<li>Create the repository from the GitHub Template</li>
<li>Go to <a href="https://github.com/" target="_blank">Github.com</a>, create a new repository and push your code to it.</li>
</ul>
</div>
</div>


You now have your projet. Open the `swa-workshop` in VSCode.


--sep--
---
title: Setup your environment using a container
---

## Setup your environment using a dev container

**Note:** This step is optional. You can either use a container like described below, or install all the tools yourself as we walk through the workshop.


There is not much you need to start working with `Azure Static Web Apps`. If you already have all the requirements listed at the begining of the workshop, you are good to go. We will see at each step what are the tools and the VSCode extensions you will need to install.

However, if you don't want to install everything or don't want to remember what is needed to build and deploy a Static Web App, we've got you covered.

Open VSCode and search for the `Remote - Containers` extension in the extension panel on the left or go <a href="https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers" target="_blank">here</a> and click `Install`.

The `Remote - Containers` extension lets you use a Docker container as a full-featured development environment. The best part is that the extension comes with a list of containers already setup for you... including one for Static Web Apps.

So, open the VSCode command panel usting `Ctrl + Shift + p` and search for `Add Development Container Configuration Files...`. This will show you a list of pre-configured containers. Search for `Azure Static Web Apps` and hit Enter.

![Add a Dev Container](media/dev-container.png)

A a few files will be aded to your project with all the container configurations.

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

In the <a href="https://portal.azure.com/" target="_blank">Azure Portal</a>, look for `Static Web Apps` in the search bar. Once you are on the product page, click on the `Create` button at the top left. Or, you can simply click <a href="https://portal.azure.com/#create/Microsoft.StaticApp" target="_blank">here</a> ^^. This link will take you directly to the Static Web App creation form.  

Let's fill it out!

* Select your subscription.
* Create a new resource group.

<div class="box info">
In Azure, a resource group is a logical container that holds resources usually related to an application or a project. A resource group can therefore contain virtual machines, storage accounts, web applications, databases and more.
</div>

* Give a name to your Static Web App.
* Select the free plan (we won't need any feature in the standard plan for this workshop).
* Select `West Europe` for your backend.

<div class="box tip">
It is recommended to host your backend in the region closests to your users.
</div>

* Select `GitHub` as a deployment source.

We are going to host our website on GitHub. Later in the workshop, we will see how Static Web Apps will automaticaly deploy our website every time we push new code to our repository.

* Sign in with your GitHub account and select the repository and the branch of your project.

As we mentioned at the begining of the workshop, our app will have a backend and a frontend. In order for Static Web App to know what to deploy and where, we need to tell it where our apps are located in our repository.

Azure Static Web Apps can handle several well-known frontend frameworks and therefore, "compile" your Angular, React or Hugo application before deploying it.

In our case, we have a very simple Vanilla JavaScript appliation which does not require anything to run. So, let's choose `Custom`.
* In the `App location`, enter the `www/` folder as this is where our frontend is.
* In the `Api location`, enter the `api/` folder as this is where our backend is.
* In the `Output`, enter the `www/` folder as your frontend does not need any build system to run.

![Enter GitHub information when creating SWA](media/swa-github.png)

* Click on `Review + Create` and then on `Create`.

After a few minutes, your static web app will be created on Azure and your website deployed.

Once the resource is created, `pull` your code as a few files have been added to your GitHub repo by Azure.

## So, what just happened?

    

### On GitHub

When Azure created your Static Web App, it pushed a new YAML file in the `.github/workflow` folder of your repository.

The files in this folder decribe the GitHub Actions, which are event-based actions that can be triggered by events like a `push`, a `new pull request`, a `new issue`, a `new collaborator` and many many more. 

You can see the complete list of triggers <a href="https://docs.github.com/en/actions/reference/events-that-trigger-workflows" target="_blank"/>here</a>

<div class="box info">
<div>
If you are not familiar with GitHub Actions, go have a look <a href="https://github.com/features/actions" target="_blank">here</a>.
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
Here, you can see that the GitHub Action is going to be triggered every time there is a `push` on the `main branch` or every time a pull request is `opened`, `synchronize`, `reopened` or `closed`.  
As we want our website to be redeployed automaticaly every time we push on our main branch, this is perfect!

Take a few minutes to read the YAML file and understand what exactly happens when the GitHub Action is triggered. You can see that most of the information you entered when you created your Static Web App on Azure is here.

<div class="box tip">
The YAML file is in your GitHub repository so you can edit it! Your frontend site folder name changed? No problem, just edit the file and push it on GitHub.
</div>

So, go back to your GitHub reposiroty and click on the `Actions` tab. Here, you will see the list of all the GitHub actions that have been triggered so far. Click on the last one to see your application being deployed.

![Check your GitHub Actions](media/github-actions.png)
### On Azure

Once your Static Web App is created, go to the Resource page. You can find the list of all your Static Web Apps <a href="https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Web%2FStaticSites" target="_blank">here</a>

In the overview panel of your resource, look for the `URL` parameter. This is the url of your website. 

![Resource overview of your project](media/resource-overview.png)


Go have a look, your TODO list app has been deployed and is accessible to the world!

Congratulations, you just deployed your first Static Web App on Azure ! 🥳


--sep--
---
title: Let's add a backend
---

## Let's add a backend

Now that our TODO app is deployed, we want to make it interactive. Therefore, we want it to interact with a backend!  

Azure Static Web Apps relies on Azure Functions for your application backend. Azure Functions is an Azure service which enables you to deploy simple functions triggered by events. In our case, events will be HTTP requests.

<div class="box info">
Ever heard of Serverless or FaaS (Function as a Service)? Well, you get it, this is what Azure Functions is ^^.
</div>


### Installation

You can create an Azure Function from the <a href="https://portal.azure.com">Azure portal</a> but let's be honest, it's so much easier to stay in VSCode and use the Azure Functions extension.

So, start by installing the Azure Function extension from VSCode.
You can download the extension either directly from the `Extension panel (Ctrl + Shift + X)` in VSCode or by going <a href="https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions" target="_blank">here</a> and clicking on the `Install` button.

### Create your Function app

Azure functions live in an Azure Functions App. When you create your app, a function will be created. You can then add several functions it. 
So, let's create our Functions App and a Function to retrieve our task list.

* In VSCode, open the Command panel and search for `Azure Functions: Create new project`. 
* Select the `api` folder. This is where our Function App will be created.
* Choose `JavaScript` as this is the langage we are going to use to write our Function.

<div class="box info">
Not all the Azure Functions languages are supported. You can write your Azure Static Web App backend in JavaScript, TypeScript, Python or C#.
</div>

* As we are creating a REST API that will be called by our website, the trigger we are looking for is the `HTTP trigger`. 
* Our first function will be used to retrieve our task list. Let's call it `tasks-get`. 
* Select the `Anonymous` authorization level.

<div class="box info">
<div>
If you want to learn more about the different authorization levels and how to secure your API, go check <a href="https://docs.microsoft.com/en-us/azure/azure-functions/security-concepts" target="_blank">this link</a>.
</div>
</div>

A function template will be created for you so you don't start with a blank file. Let's modify it for our needs.

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

By default, when an Azure Function is created using the VSCode extension, the function will manage `GET` and `POST` requests and the url will end with your function name. In our case, the `tasks-get` function can either be called using
* `GET https://your-website-url.com/api/tasks-get`
* `POST https://your-website-url.com/api/tasks-get`

This is not exactly what we need. Hopefuly, there is a way to configure this. Open the `function.json` file in your function folder.

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
Here, you can find most of the information you selected when you created your function.  
As we only need our function to retrieve a list of tasks, let's remove the `post` method in the methods array so our function can only be called using `GET` requests.

The other thing you may want to change is the url of your function. Having a route called `/api/tasks-get` is not very standard. You can easily change your enpoint name in the `function.json` file by adding a `route` parameter.

```json
{
    ...,
    "methods": ["get"],
    "route": "tasks"
    ...
}
```

Now, your function is only accessible using a `GET /api/tasks` request.

You've done it. You wrote your first Azure Function. Congratulations ! 🥳


--sep--
---
Title: Test you project locally
---

## Test your project locally

There are two ways to test your project. You can either push your code on GitHub every time you need to test it (not recommended), or use the `Static Web Apps CLI`

### The Static Web App CLI

The Static Web Apps Command Line Interface, also known as the `SWA CLI` , serves as a local development tool for Azure Static Web Apps. In our case, we will use the CLI to:
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

The CLI offers many options but in our case, we want it to serve both our API located in our `api` folder and our web application located in our `www` folder.

In your terminal, type the following command to start your project:

```bash
swa start ./www --api ./api
```

This CLI gives you two urls:
* <a href="http://localhost:4280" target="blank">http://localhost:4280</a> corresponding to your frontend.
* <a href="http://localhost:7071/api/tasks" tartet="_blank">http://localhost:7071/api/tasks</a> corresonding to you api.

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

Azure Static Web Apps manages authentication out of the box. There are pre-configured providers but you can add you own custom providers if needed. Among the pre-configured ones are `Twitter`, `Google`, `Microsoft`, `GitHub` and others.

<div class="box info">
If you are using the CLI, you won't really be connecting to the selected provider. The CLI offers a proxy to simulare the connection to the provider and gives you a fake userId.
</div>

### Sign in & Sign out

When I said "out of the box", I really meant it. You don't need to do anything for most of the providers. Let's use the GitHub one for our application. The only thing you will have to do is a button that redirects to `/.auth/login/github`.

<div class="box assignment">
<div>
Add a button in the login.html so your users can sign in using GitHub. Then, navitage to <a href="http://localhost:4280/login.html" target="_blank">http://localhost:4280/login.html</a>.
</div>
</div>

By default, once logged in, your users are redirected to the same page. However, we would like our users to be redirected to our TODO page after successfully logging in. You can do that by using the `post_login_redirect_uri` query param at the end of the url.  
Eg. `?post_login_redirect_uri=/index.html` 

<div class="box tip">
<div>
If you are building a React app, go <a href="https://docs.microsoft.com/en-us/learn/modules/publish-static-web-app-authentication/?WT.mc_id=javascript-17844-cxa" target="_blank">check the MSLearn module that will show you how to do it.</a>
</div>
</div>

### Getting user information

Once your user is authenticated, you can retrieve the associated information by fetching the url `/.auth/me`. This will return a json containing a clientPrincipal object. If the object is null, the user is not authenticated. Otherwize, the object contains data like the provider, the roles and the username.

```json
{
  "identityProvider": "github",
  "userId": "d75b260a64504067bfc5b2905e3b8182",
  "userDetails": "tagazok",
  "userRoles": ["anonymous", "authenticated"]
}
```
The `userId` is unique and can be used to identify the user. We will use it later in the database.

<div class="box assignment">
<div>
Complete the <code>getUser()</code> methor to retrieve the logged-in user information and display the username in the <code>&lt;div id=&quot;username&quot;&gt;&lt;/div&gt;</code> element located at the top left of your webpage.
</div>
</div>

![Yout TODO app is running](media/todo.png)

Congratulations, you can now login into your app! 🥳

--sep--
---
Title: Routes & Roles
---

## Routes & Roles

In many cases, your routes will be managed by your frontend, especially if you are using a framework such as React or Angular.   
You may also be used to managing authorization on your backend for your API calls.

Azure Static Web Apps offers you the possibility to handle http requests in a single file. Start by creating a file called `staticwebapp.config.json` in your `www` folder.

<div class="box info">
<div>
Yout need to restart the CLI each time your make a change in the <code>staticwebapp.config.json</code> file
</div>
</div>

### Secure our website and APIs

There are many properties available to configure your Static Web App but let's concentrate only on the few we need in our app.

The `routes` parameter is an array of all the rules for your routes. For example, in our case, we would like to prevent non-authorized users from calling our API. We can do that very easily.

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

Here, your website root will only be accessible to logged in users.

### Manage HTTP error codes

 Now, if you try that, you will notice that your users are redirected to a default 401 web page. We can customise that using another property in the config file. The `responseOverrides` property enables you to redirect a user to a specific page when an HTTP code is returned. Let's redirect all non-authenticated users to the `login.html` page.

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
Create a <code>custom-404.html</code> page in your www folder and add a rule to redirect users to this page when they enter a url which does not exist.
</div>
</div>

Now, try to go to a non-existing page on your website like `/hello.html`. You should be redirected to the `custom-404.html` page you just created.

<div class="box tip">
<div>
This is also very useful if you are doing a SPA (Single Page Application) where the routing is managed on the client side. You may then need to redirect all your urls to <code>index.html</code>. Check the <code>navigationFallback</code> property in the documentation <a href="https://docs.microsoft.com/en-us/azure/static-web-apps/configuration" target="_blank">here</a>
</div>
</div>

Congratulations, your website and your APIs are now secured and you have a seamless workflow for your users. 🥳

--sep--
---
title: Store your data in a database
---

## Store your data in a database

There are several databases available on Azure. One of the most powerful one is `Cosmos DB`. Azure Cosmos DB is a fully managed NoSQL database which supports several query langages. When you create your Database, you can choose which API you want to use. Among the most popular ones are `MongoDB`, `SQL` or `Cassandra`.

### Setup your environment

Let's go back to our Azure Function in VSCode. As we are using the Cosmos DB API, we will need a library to connect to our database. In the `/api` folder, open the `package.json` file and add `"mongodb": "^4.0.1"` to the `dependencies` property.

```json
...
  "dependencies": {
    "mongodb": "^4.0.1"
  },
...
```

In a terminal, type `npm install` and hit enter. This will download the dependencies for you in the `node_modules` folder of your Azure Functions App.

While you are in VSCode, let's install the `Azure Database` extension. This will allow you to explore your database and make queries from VSCode without having to go in the portal.  
In the extension menu of VSCode, search for `Azure Database` or <a href="https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb" target="_blank">here</a> and click on `Install`.


### Create your database

Go in the Azure portal and search for `Azure Cosmos DB`. Once on the product page, click on `Create` at the top left. For our application, we are going to use the `MongoDB` API so select `Azure Cosmos DB API for MongoDB`

* Select your subscription.
* Select the same resource group you created for your project.
* Enter a name to identify your Cosmos DB account. (This name should be unique).
* Select the location where your database is going to be hosted. We recommand using the closest location to your users. 
* Select `Provisioned throughput` as there is a free tier to it.
* Select `Apply` when asked if you want to Apply the free tier discount
* Click on `Review + Create` and then on `Create`.

Creating the resource may take some time so grab a cup of hot chocolate and be ready to deal with Cosmos DB!

Let's go back to VSCode. In the Azure Extension, you now have the `Database` tab where you should see the CosmosDB server you just created. If you don't see it, just click the refresh button.  
Once you see your server, right click on it, select `Create Database` and give it a name. Once your database is created, right click on it, select `Create Collection` and name it `tasks` as it will be used to store our tasks.

![Create a Cosmos DB database](media/create-db.png)

### Add some data

Let's focus on our existing Azure Functions. We will see later how to create a function to add new tasks in our database.  
Right now, we just want to get our tasks from the database instead of the json array we created earlier in our function.

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

In your `tasks-get` Azure function, start by importing the  mongoClient from the mongodb library we installed earlier

```javascript
const mongoClient = require("mongodb").MongoClient;
```

When your Static Web App calls the API, the user information is sent to the function in the `x-ms-client-principal` HTTP header. 
You can use the code below to retrieve the same user json you get in the `clientPrincipal` property when you go to `/.auth/me`.

```javascript

const header = req.headers['x-ms-client-principal'];
const encoded = Buffer.from(header, 'base64');
const decoded = encoded.toString('ascii');
const user = JSON.parse(decoded);
```

Let's see how the mongoDB API works:
* First, your need to connect to your server

In order to connect your application to your database, you will need a connection string.  
You can find your server connection string in the Azure portal. But, as always, you can stay in your VSCode. In the Azure Database extension, right click on your database server and select `Copy Connection String`.

![Retrive your Cosmos DB connection string](media/connection-string.png)

Now, let's connect!  
You have two ways to connect, a clean and secure way and the quick and dirty way

#### The clean and secure way

It's not safe to store your private key or connection strings in your code. Azure Static Web Apps porovides a way to store environment variables that you can then use in your app.

// TODO


To check how to add your Mongo DB connection string in the environment variavles of your Static Web App, check this quick video.

<a href="https://www.youtube.com/watch?v=R9qhGra9FHs&list=PLlrxD0HtieHgMPeBaDQFx9yNuFxx6S1VG&t=112s" target="_blank">
  <img src="media/swa-tips-video-environment.png">
</a>

#### The quick and dirty way

```javascript
const client = await mongoClient.connect("YOUR-SERVER-CONNECTION-STRING");
```

### Request your data

Once your are connected to your Cosmos DB server using the mongoDB API, you can use this connection to select a database
```javascript
const database = client.db("YOUR-DB-NAME");
```
Replace `YOUR-DB-NAME` by the name you entered when you created your database.

Then, just query the document where the userId property is the same as the userId sent in the headers when your function is called

```javascript
const response = await database.collection("tasks").find({
    userId: user.userId
});

const tasks = await response.toArray();
```

<div class="box assignment">
  Update your Azure function so it returns the tasks in the database associated to your logged in user.
</div>

Test your website locally and push your changes to GitHub. The GitHub Action will be triggered and your website deployed. Go check the url, you should see the tasks of your database.

![Your TODO app up and running](media/finish.png)


--sep--
---
Title: Bonus
---

## Bonus

### Finish your application

You now know how to create and publish an app with a frontend, a backend, a database and some user authentication.
However, in order to make your TODO app fully functional, you need to add a few more features. The good news? You have everything your need to do it!

#### Add a new task

We have already added the source code to call the API in the frontend so all you need to do is to create the Azure Function and connect it to the database.  

<div class="box assignment">
Create one Azure Function to add a new Task. You don't need to create a new project, just create new function from VSCode.
</div>


#### Update a task

You may have noticed that there is a <code>status</code> attribute in every task in your database. The value can be either <code>""</code> or <code>"checked"</code>. Right now, there is no way to change this status.   


<div class="box assignment">
Write an Azure Function and the javascript code in your frontend to update this status.
</div>


### Monitor your app

You now know how to create ressources on Azure and how connection string work. 

You may have noticed that, once deployed, we don't have any log for our app. Therefore, we have no way to know what happens.

<div class="box assignment">
<div>
Create an <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview" target="_blank">App Insights</a> resource in your ressource group and connect it to your Static Web App.
</div>
</div>

--sep--
---
Title: Conclusion
---

## Conclusion

Congratulations, you've reach the end of this workshop!

## Solution

You can download the complete code with the features to add and update a task <a href="https://github.com/tagazok/my-workshops/raw/master/static-web-apps/data/swa-workshop-final.zip" target="_blank">here</a>

## Credits

This workshop was created by <a href="" target="_blank">Olivier Leplus</a>

Thanks to <a href="https://twitter.com/maudstweetse" target="_blank">Maud Levy</a>, <a href="https://twitter.com/simonwaight" target="_blank">Simon Waight</a>, Christophe Harrison, Sylvain Pontoreau for their feedback