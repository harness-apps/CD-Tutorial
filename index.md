---
layout: page
title: Continuous deployment with Harness CD
---

![A lovely image of our beloved Captain Canary](/assets/images/canary.png)
Hi!, I’m Captain Canary.

## Getting started

Hey! Welcome back. Captain Canary here. I take it you’ve completed the [CI getting started guide](https://harness-apps.github.io/CI-Tutorial/)? Good, I’m really excited. To complete this guide, you’ll need a lot of the same prerequisites. Remember, these guides are for our MERN stack example app. This means the prerequisites are specific to this app. Things like a Mongo Atlas account are necessary for this app. Your application may not need them. Before we continue, please gather the following:


## 🛫 Pre-flight checklist

- A Version Control System account 👩🏾‍💻. In this guide we’re going to use GitHub. Our example app’s source is on GitHub and you’ll need to fork those repos, so make sure you have a 🆓 GitHub account. Alternatively, if you’re comfortable following your inner-shoulder-angel’s guide to converting GitHub instructions you can use your own VCS. This, however, is an exercise for the reader. 
- A 🆓 Docker Hub account. Harness helps you publish container images virtually anywhere. For this guide we’ll use Docker Hub.
- Kubernetes cluster. You k8s cluster can run anywhere, so long as it has access to the internet. Later on you’ll create a ‘`demo`’ namespace. (yeah, naming things is hard 🙇‍♀️) Make sure that namespace is available. (Or you can JIT Translate in your head) 
  > Note, you need to be able to execute `kubectl` commands on your cluster, so make sure you’ve authenticated.
- MongoDB Atlas instance. Our MERN stack app uses Mongodb Atlas, as its datastore. You’ll need to [sign up 🆓 and get the connection URL from the Mongo Atlas interface.](https://www.mongodb.com/atlas/database) Helps to copy paste that to a notes file.
* A lovely beverage. I like coffee, but I’m not judging. 
* A sense of contentment from having worked through the CI getting started guide. You can find that guide here.

<a class="btn btn-primary" href="Delegate/delegateIntro">👏 Ok, I've got those things, let's get started</a>