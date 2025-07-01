---
title: Edge Impulse AWS IoTCore/Greengrass Integration Workshop
---

The next step is to create our Edge Impulse environment. Edge Impulse provides a simple solution to creating and building a ML model for specific edge devices focused on specific tasks.  Lets get started. 

## Create Edge Impulse Account

Please create a user account in Edge Impulse

## Clone Project Into Your Account

Next, we are going to clone an existing project into our own space:

## Build your Project

Let's have a look at some of the features in Edge Impulse studio:

Our model has already been trained and tested.  What we want to do now is to deploy our model to a specific edge device type.  Depending on the specific hardware you are using in this workshop, you can choose from the following deployment edge device choices:


Please select the appropriate choice and press "Build"

NOTE:  For these edge device choices, please select the "int8" option prior to pressing "Build":


## Create your Project API Key

Lastly, lets create our API key for our project. We'll use this key to connect our Greengrass component's environment to our Edge Impulse project:


OK!  We are making good progress!  Next up, we are going to install AWS IoT Greengrass into our edge device. Lets go!