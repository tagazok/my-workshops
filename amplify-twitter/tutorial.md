---
title: Static web apps
---

--sep--
---
title: Objectives & Prerequesites
---

Let's make our social media a little bit more appealing by giving the ability for users to attach images to their posts.

To do that, we will need to do two things:
 - Modify our data model to add an image to our Post
 - Find a way to store our image


### Modify our model

Go back to your model in the Data menu of `Amplify Studio` and modify your post to add an `image` field of type `String`. This time, we don't need to make it mandatory and we don't expect users to always have an immage to attach to their Post.

![Storage creation screen in Amplify Studio](/static/storage_postmodel_image.png)

Don't forget to:
 1. `Save and Deploy` your new model
 2. Run `amplify pull` on your local computer

### Add storage capability

Nothing is more simple than adding storage capability to your project.
As for the API, we can either add the storage to our project from the CLI or from the AWS Studio

:::::tabs
::::tab{id="studio" label="Using Amplify Studio"}

Go to the `Storage` menu in the Amplify Studio. Here, we can either an existing Amazon S3 bucket to your project, or create a new one.

:::alert{type="info" header="Tip"}
To learn more about Amazon S3 (Amazon Simple Storage Service), go [here](https://aws.amazon.com/s3/)
:::

In our case, we are going to create an Amazon S3 bucket dedicated to our project.  
You can change the name of the bucket but we advise that, for this workshop, you keep the one created by default.  

As we want our images to be only accessible to signed-in users, check the `Upload`, `View` and `Delete` options for `Signed-in userd` and keep all the options of `Guest users` unchecked.

:::alert{type="info" header="Tip"}
Bucket names must be unique across all AWS accounts in all the AWS Regions within a partition. A partition is a grouping of Regions. AWS currently has three partitions: `aws` (Standard Regions), `aws-cn` (China Regions), and `aws-us-gov` (AWS GovCloud (US)).
:::


![Storage creation screen in Amplify Studio](/static/create-bucket_studio.png)

Click next.

This step will take a few minutes to provision the ressources on AWS. Once it is done, just run `amplify pull` on your local machine to synchronise your version and the one in the Amplify Studio.

::::
::::tab{id="cli" label="Using Amplify CLI"}

Start by adding the storage capability to your Amplify project the same way you add any feature using `aplify add`.

```
amplify add storage
```

We are going to save files, specifacly images for our project. Select `Content`.

```
? Select from one of the below mentioned services: (Use arrow keys)
❯ Content (Images, audio, video, etc.) 
  NoSQL Database 
```

We only want logged in users to be able to access pictures. Select `Auth users only`

```
? Who should have access: …  (Use arrow keys or type to filter)
❯ Auth users only
  Auth and guest users
```

We want authenticated users to be able to create, read and delete images. Select all three options.

```
? What kind of access do you want for Authenticated users? …  (Use arrow keys or type to filter)
 ✔ create/update
 ✔ read
 ✔ delete
```

:::::

---
::::alert{type="success" header="Exercice"}
Choose your prefered method (CLI or Studio) and add a storage to your Amplify project.
::::

TODO: Add way to display image using S3Component`