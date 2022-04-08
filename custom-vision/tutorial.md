---
title: Machine Learning with Custom Vision
---

--sep--
---
title: Objectives & Prerequesites
---
## Objectives & Prerequesites

### Objectives

In this workshop, you will learn how to build a model to detect dog breeds. You'll start by installing and configuring the necessary tools, then creating the custom model by uploading and tagging images, and finally use the model using the Custom Vision REST API and the Software Development Kit (SDK).

![Add a Dev Container](images/result.png)

### Prerequisites

To do this workshop, you will need:
* Basic JavaScript or Python knowledge
* A Microsoft Azure account
* [A GitHub account](http://github.com/)
* [Visual Studio Code](https://code.visualstudio.com/) (VSCode)
* [Node.js 14 installed](https://nodejs.org/)
* [Python 3.8 or greater with pip installed]()
* [Azure Functions Core Tools](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=v3%2Clinux%2Ccsharp%2Cportal%2Cbash%2Ckeda#v2&ocid=OCID&wt.mc_id=WTMCID) (V3)

--sep--
---
title: Setup your Custom Vision Resource
---

## Create your Azure resources

As with any project, a few tools are going to be needed. In particular you'll need a coe editor, an Azure subscription, and a couple of keys for Custom Vision

Start by opening the <a href="https://ms.portal.azure.com/#blade/Microsoft_Azure_ProjectOxford/CognitiveServicesHub/CustomVision?ocid=OCID&wt.mc_id=WTMCID" target="_blank">Custom Vision dashboard</a> in the Azure Portal. Then, click on the `Create`button. This link will take you to the Custom Vision creation form. You may be prompted to log into your Azure Subscription. If you don't have one you can create a Free trial.  

Let's fill it out!

* Select `Both` for `Create options` as we are going to use our resource to both train our model and make predictions.
* Select your Subscription.
* Create a new Resource Group.

<div class="box info">
In Azure, a Resource Group is a logical structure that holds resources usually related to an application or a project. A Resource Group can contain virtual machines, storage accounts, web applications, databases and more.
</div>

* Select `West Europe` as Region if you are in Europe. Or chose the closed region you are in.
* Give a Name to your Project.
* Select the Free F0 Plan for the training and prediction pricing tiers.

<div class="box tip">
It is recommended to host your resource in a Region closest to your users.
</div>

* Click on `Review + Create` and then on `Create`.

After a few minutes, your Custom Vision resource will be created on Azure.

You now have all the necesary tools for creating your custom vision model.

--sep--
---
title: Train your model
---

## Train your model

### Create your Custom Vision Project

Custom Vision lives in another platform than the Azure Portal. Now that you have created your resource, let's use the Custom Vision Portal to train your model.

First, navigate to <a href="https://www.customvision.ai/?ocid=OCID&wt.mc_id=WTMCID" target="_blank">Custom Vision</a> and sign-in with your account.

* Select `New Project`
* Enter `Dog Classification` for the project name 
* Select the resource you created in the previous step of the workshop
* Select `Classification` as `Project Types`

<div class="box info">
Image classification tags whole images where Object Detection finds the location of content within an image.
</div>

* Select `Multiclass`for  `Classification Types` as our dogs will only have one breed.
* Select `General [A2] for `Domain` as our dogs are not related to any other domain.

<div class="box info">
You can find more information about the differences between Domains in the <a href="https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/select-domain" target="_blank">Custom Vision documentation</a>.
</div>

### Upload your images

Once the project is created, it's time to upload images. These images will be used to train your model.

<div class="box tip">
As a general rule, the more images you can use to train a model the better. You want to include as much variety in the images as possible, including different lighting, angles, and settings.
</div>

We will provide you with a few images of dogs to train your model. Download the `Training images set` in the `Resources` menu of this workshop.

In the Custom Vision portal:
* Select `Add images`
* Navigate to the `training-images` folder you just downloaded
* Select all the images marked as `american-staffordshire-terrier` in the folder, and select `Open`.
* Enter `american-staffordshire-terrier`for the tag and select `Upload 8 files`
* Ckick `Done`
* Repeat the above steps for the other breeds.
  * `australian-shepherd`
  * `buggle`
  * `german-wirehaired-pointer`
  * `shorkie`


### Train your model

Now that you have uploaded and tagged your images, it's time to train your model.

* Ckick `Train` to open the training dialog.
* Leave `Quick Training`selected and click `Train` to begin the training process.

It will take a few minutes to train your model.

--sep--
---
title: Test & Publish your model
---

## Test & Publish

With the model trained it's time to turn our attention to using it. We'll start by testing it in the Custom Vision website. Then we'll explore how we can call the model from code by using the REST API or the SDK.

### Test your model in the Custom Vision portal

Let's see how well our model works. <b>It's important to use images which weren't used to train the model</b>. After all, if the model has already seen the image it's going to know the answer. Start by downloading the `Testing images set` in the `Resources` menu of this workshop.

Then, in the Custom Vision portal
* Click on the `Quick Test` button
* Select `Browse local files`
* Navigate to the `testing-images` folder you just downloaded	and select one of the dog images
* Click `Open`

Notice the `tag`and `probability`scores. The `tag` is the breed of the dog, and the `probability` is the confidence that the model has in the breed. Try with another images :)

### Publish your model

Playing with your model in the Custom Vision portal is funny. But, the goal of creating a model in Custom Vision is to use it in different applications. To access it from outside of the Custom Vision website it needs to be published.

* Go to the `Performance`tag and click `Publish`
* Enter `dogs` as `Model name`
* xxxx
* Click `Publish`

--sep--
---
title: Azure Static Web App
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

![Add a Dev Container](images/githubtemplate.png)

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

We are going to host our website source code on GitHub. Later in the workshop, we will see how Static Web Apps will automaticaly deploy our website every time we push new code to our repository.

* Sign in with your GitHub account and select the repository and the branch of your project.

As we mentioned at the begining of the workshop, our app will have a backend and a frontend. In order for Static Web App to know what to deploy and where, we need to tell it where our apps are located in our repository.

Azure Static Web Apps can handle several well-known frontend frameworks and can "compile" your Angular, React or Hugo application before deploying them.

In our case, we have a very simple JavaScript appliation which does not require anything to run. So, let's choose `Custom`.
* In the `App location`, enter the `/www` folder as this is where our frontend is.
* In the `Api location`, enter the `/api` folder as this is where our backend is.
* In the `Output`, enter the `/www` folder as your frontend does not need any build system to run.

![Enter GitHub information when creating SWA](images/swa-github.png)

* Click on `Review + Create` and then on `Create`.

After a few minutes, your Static Web App will be created on Azure and your website deployed.

Once the resource is created, you should `pull` your repository in VSCode as a few files have been added to your GitHub repo by Azure.

## So, what just happened?

### On GitHub

When Azure created your Static Web App, it pushed a new YAML file to the `.github/workflow` folder of your repository.

The files in this folder decribe GitHub Actions, which are event-based actions that can be triggered by events like a `push`, a `new pull request`, a `new issue`, a `new collaborator` and more. 

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

As we want our website to be redeployed automaticaly every time we push on our main branch, this is perfect!

Take a few minutes to read the YAML file and understand what exactly happens when the GitHub Action is triggered. You can see that most of the information you entered when you created your Static Web App on Azure is here.

<div class="box tip">
The YAML file is in your GitHub repository so you can edit it! Your frontend site folder name changed? No problem, just edit the file and push it to GitHub!
</div>

Now, go to your GitHub repository in a web browser and click on the `Actions` tab. Here, you will see the list of all the GitHub Actions that have been triggered so far. Click on the last one to see your application being deployed.

![Check your GitHub Actions](images/github-actions.png)

### On Azure

Once your Static Web App is created, go to the Resource page. You can find the list of all your Static Web Apps <a href="https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Web%2FStaticSites?ocid=OCID&wt.mc_id=WTMCID" target="_blank">here</a>

In the Overview panel of your Static Web App, look for the `URL` parameter. This is the url of your website. 

![Resource overview of your project](images/resource-overview.png)

Open the link and you can see that your TODO list app has been deployed and is accessible to the world!

Congratulations, you just deployed your first Static Web App on Azure! 🥳


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
swa start ./www --api-location ./api
```

This CLI gives you two urls:

* <a href="http://localhost:4280" target="blank">http://localhost:4280</a> corresponding to your frontend.
* <a href="http://localhost:7071/api/tasks" tartet="_blank">http://localhost:7071/api/tasks</a> corresonding to you API.

<div class="box tip">
<div>
<div>
The CLI may take more time than usual to launch your Azure Function, especially the first time. The default timeout is 30 seconds but you can increase it by using the <code>--devserver-timeout=60000</code> parameter
</div>
<div>
If you have an error like:
<code>
'func' is not recognized as an internal or external command
 </code>
Don't hesitate to restart your IDE, Terminal or computer and verify by taping func in another terminal to see if you have correctly install <a href="https://docs.microsoft.com/fr-fr/azure/azure-functions/functions-run-local?tabs=windows%2Ccsharp%2Cportal%2Cbash%2Ckeda">Azure functions core tools</a>
</div>
</div>
</div>

Congratulations, you now have everything you need to test your app on your computer! 🥳

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

* In VSCode, open the Command panel using `Ctrl + Shift + p` and search for `Azure Functions: Create new project`. 
* Select the `api` folder. This is where our Function App will be created.
* Choose `JavaScript` as this is the langage we are going to use to write our Function.

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


--sep--
---
title: Call your model
---

--sep--
---
Title: Bonus
---

## Bonus


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

Congratulations, you've reach the end of this workshop!

This workshop is based of <a href="https://github.com/jlooper/workshop-library/tree/main/full/ml-model-custom-vision" target="_blank">this workshop</a>.


