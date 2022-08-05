---
layout: page
title: Continuous deployment with Harness CD
---

Open Harness Cd and click New Pipeline.

![alt_text](../images/image19.png "image_tooltip")

Enter "Deploy MERN Client" in the *name* field, then click *Start*.

![alt_text](../images/image33.png "image_tooltip")

Click **Add Stage**, then select **Deploy**.

![alt_text](../images/image43.png "image_tooltip")

Enter “MERN Client” in the **Stage Name** field.

Ensure you selected **Service** is selected under **What would you like to deploy?**. Then click **Set Up Stage**.

![alt_text](../images/image14.png "image_tooltip")

#### Client Manifest

Select **MERN Client** from the **Specify Service** drop-down menu.

Select **Kubernetes** for the **Deployment Type**, then click **Add Manifest**.

![alt_text](../images/image31.png "image_tooltip")

Select **K8s Manifest**, then click **Continue.**

![alt_text](../images/image4.png "image_tooltip")

Select **GitHub**, then click **Select GitHub Connector**.

![alt_text](../images/image22.png "image_tooltip")

Select **MERN Stack Example GitOps**, then click **Apply Selected**.

![alt_text](../images/image11.png "image_tooltip")

Check the **GitHub Connector **field. Make sure that you selected the **MERN Stack Example GitOps**.

![alt_text](../images/image1.png "image_tooltip")

Enter “client” in the **Manifest Identifier** field.

Select **Latest from Branch** in the **Git Fetch Type** field.

Enter “main” in the **Branch** field.

Enter “client-manifest.yaml” in the **File/Folder Path** field, then click **Submit**.

![alt_text](../images/image2.png "image_tooltip")

#### Client Manifest Values

Verify that the **client** entry appears in the manifest list, then click **Add Manifest**.

![alt_text](../images/image24.png "image_tooltip")

Select **Values YAML**, then click **Continue**.

![alt_text](../images/image42.png "image_tooltip")

Select **GitHub**, then click **Select GitHub Connector**.

![alt_text](../images/image20.png "image_tooltip")

Select **MERN Stack Example GitOps**, then click **Apply Selected**.

![alt_text](../images/image11.png "image_tooltip")

Verify that **MERN Stack Example GitOps** appears in the **GitHub Connector** field. Then click **Continue**.

![alt_text](../images/image1.png "image_tooltip")

Enter “clientValues” in the **Manifest Identifier** field.

Select **Latest from Branch** in the **Git Fetch Type** field.

Enter “main” in the **Branch** field.

Enter “client-manifest-values.yaml” in the **File/Folder Path** field, then click **Submit**.

![alt_text](../images/image2.png "image_tooltip")

#### Client Artifact

Verify that **clientValues** appears in the manifest list, then click **Add Primary Artifact**.

![alt_text](../images/image39.png "image_tooltip")

Click **Docker Registry**, then click **Continue**.

![alt_text](../images/image47.png "image_tooltip")

Click **Select Docker Registry Connector**.

![alt_text](../images/image36.png "image_tooltip")

Select **Docker Hub**, then click **Apply Selected**.

![alt_text](../images/image27.png "image_tooltip")

Verify that **Docker Hub** appears in the **Docker Registry Connector** field. Then click **Continue**.

![alt_text](../images/image17.png "image_tooltip")

Enter “dockerusername/mern-client” in the **Image Path** field. Where “dockerusername” is your Docker Hub username. Then click **Submit**.

![alt_text](../images/image15.png "image_tooltip")

Verify that **mern-client** appears in the artifact list, then click **Continue**.

![alt_text](../images/image6.png "image_tooltip")

Select **demo** from the drop-down menu in the **Specify Environment** field.

Select **Kubernetes** for **Infrastructure Definition**. Then click **Select Connector**.

![alt_text](../images/image25.png "image_tooltip")

Select **My Cluster**, then click **Apply Selected**.

![alt_text](../images/image10.png "image_tooltip")

Verify that **My Cluster** appears in the **Connector** field.

Enter “demo” in the **Namespace** field, then click **Continue**.

![alt_text](../images/image8.png "image_tooltip")

Select the **Rolling**, then click **Use Strategy**.

![alt_text](../images/image29.png "image_tooltip")

### Run Pipeline

Click **Save**.

![alt_text](../images/image32.png "image_tooltip")

Click **Run**.

![alt_text](../images/image35.png "image_tooltip")

Captain Canary again. This next bit of instruction is going to require your help. You see, to complete this step the Client CI process must have successfully run. You’ll need to know the build number for the last successful client CI pipeline. If you followed along with our CI getting started guide, (and if my minions haven’t broken the client codebase), this should almost always be 1. I like to push buttons because they're there. So I may have re-run that CI pipeline a few times. If you’ve run that pipeline multiple times for grins and giggles pick a good client CI pipeline execution tag. That said, Select the appropriate tag from the drop-down menu in the **Tag** field, then click **Run Pipeline**.

![alt_text](../images/image5.png "image_tooltip")

Wait for the deployment to complete successfully.

![alt_text](../images/image49.png "image_tooltip")

Run `kubectl` to retrieve the external IP of the MERN Client. In this example, the external IP is `34.148.210.10`, **_<span style="text-decoration:underline;">yours will be different.</span>_**

```
$ kubectl --namespace demo get service/client
NAME     TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE
client   LoadBalancer   10.108.0.164   34.148.210.10   80:32552/TCP   10m
```

Hey, Captain Canary again. Check out that external-IP. Copy and paste it into your browser window, and boom! Bob's your uncle. Welcome to our MERN Stack Example. This is exciting. I’m all a flutter. You’ve built a Continuous Deployment pipeline! You've used it to deploy this fantastic app to your own Kubernetes Cluster. I mean this is like having your cake and eating it too.

While we’re here, let me walk you through this **_life changing_** application. 

You should see something like this: 

![alt_text](../images/image45.png "image_tooltip")

Up there in the top right is the magic button. Clicking it takes you to a page where you can click _yet another button_ to create a new record. Yeah, the _Redundant committee on redundancy brought you that UI._

When you click that second button, it will simply record the current Date/Time and log your IP address. 

Like I said, **_Life Changing_**. 

But that’s not all you can do with this example. You can also interact with the Kubernetes pod that was deployed by Harness CD. This gives you access to logs, for instance. Here’s how:

In your terminal, execute:

```
kubectl get pods -n demo
```

Which should give you something like this:

```
NAME                                 READY   STATUS             RESTARTS   AGE
restaurant-server-7975fc6fd9-k2kkf   0/1     CrashLoopBackOff   3554       13d
```

Yep, my pod is struggling. Sigh. Minions. 

Anyway, what’s important to note here is the _name_ of your pod. You’re gonna need that. With that name in your copy/paste buffer, execute this:

```
kubectl logs -n demo <<PASTE YOUR POD NAME HERE>>
```

I'm going to assume you've visited the application in your browser. You did do that, right? If so, you should see some logs like this:

```
{"level":30,"time":1656447497424,"pid":1,"hostname":"restaurant-server-7975fc6fd9-k2kkf","msg":"Server listening at http://0.0.0.0:5001"}
```

You may see *more* logs, but you should at least see that much!               As    

If  don’t know about you, but  I think this is simply stellar. I want to thank you for working through this with me. We’ve now completed this CD getting started guide and I have two parting things to leave you: 

1. Remember, tweet @Capt_Canary with any questions, comments and snide remarks. 
2. You’re awesome. Keep that up.