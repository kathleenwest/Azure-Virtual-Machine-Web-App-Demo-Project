# Azure Virtual Machine Web App Demo Project
 
 This is a tutorial azure cloud project that demonstrates how to install a basic web app on a virtual machine. We will use our azure account to creature a resource group and virtual machine. Then we will install and configure the virtual machine to run nginx and python web applications. Our web app is a flask template web application that is uploaded to our virtual machine and then configured to run with nginx.
 
 Watch the video tutorials and follow step-by-step instructions to learn how to create your own starter web app running on an azure cloud virtual machine.

## Running the Web App Locally

First clone this repo to your project directory. 

Let's test and run our web app locally first. In this tutorial we are using Visual Studio Code (VSC) as our IDE. Navigate to the web-app directory in your VSC terminal window and run the python application. 

`...\web-app>python application.py`

Open a web browser and navigate to https://localhost:3000 to view the template Flask application running. 

Press Ctrl + C to quit or close your VSC terminal window.

[![Watch the tutorial video](/images/RunFlaskPythonLocallyPoster.jpg)](https://youtu.be/vriPs8FYYSU "Video Tutorial - How to run Flask Python web app locally")

## Create Azure Resource Group

Login into your Azure account and create a resource group for this project. In this tutorial we will be using the resource group name `web-app-vm-project` .

Record the resource group name since we will be using it later.

[![Watch the tutorial video](/images/CreateResourceGroupPoster.jpg)](https://youtu.be/7cv4tIqOJAo "Video Tutorial - How to Create a Resource Group")

## Create a Virtual Machine

1. Loging to the Azure portal. 
2. On the homepage, click "Create a resource"
3. Click on "Compute" in the left menu
4. Click on "Virtual Machine"
5. Create a Linux VM with the following details:
 - Subscription: This will vary for you. Should default to your main subscription.
 - Resource Group: `web-app-vm-project`
 - VM Name: `linux-vm-project`
 - Region: East US or a region closest to you that is available
 - Availability Options: Default option of "No infrastructure redundancy required" is fine here.
 - Image: Ubuntu Server (any version) but I'm going to use the latest version 18.04 LTS
 - Azure Spot instance: No
 - Size: Click on "Select Size" and select "Standard B1ls"
 - Authentication type: Password
 - Username: (any username you choose) `projectadmin`
 - Password: (any password you choose) `projectadmin|2021`
 - Inbound Port Rules: "Allow Select Ports" and make sure from the drop-down menu, 22 and 80 are selected.

[![Watch the tutorial video](/images/CreateVirtualMachinePoster.jpg)](https://youtu.be/oKk8BR2s7Ho "Video Tutorial - How to Create a Virtual Machine")

## Access Virtual Machine and Transfer Web App

Description

[![Watch the tutorial video](/images/CopyFilesToVirtualMachinePoster.jpg)](https://youtu.be/6_ZMbPsve20 "Video Tutorial - How to Copy Files to a Virtual Machine")

## Configure and Deploy Web Server

Description

[![Watch the tutorial video](/images/ConfigureandDeployWebServerPoster.jpg)](https://youtu.be/xZwO4P_xj9E "Video Tutorial - How to Configure and Deploy a Web Server")
