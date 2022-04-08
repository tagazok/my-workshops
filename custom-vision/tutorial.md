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
title: Use your model
---

## Use your model

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


