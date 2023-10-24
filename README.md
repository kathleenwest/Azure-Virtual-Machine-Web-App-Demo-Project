# Azure Virtual Machine Web App Demo Project
 
 This tutorial azure cloud project demonstrates how to install a basic web app on a virtual machine. We will use our azure account to creature a resource group and virtual machine. Then we will install and configure the virtual machine to run nginx web server and python. Our web app is a flask template and python web application that is uploaded to our virtual machine and then configured to run with nginx.
 
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

1. Login to the Azure portal. 
2. On the homepage, click "Create a resource"
3. Select "Compute" from the category menu
4. Select the "Virtual Machine" product and select Create to start the wizard process
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
   - Inbound Port Rules: "Allow Select Ports" and make sure from the drop-down menu, 22 and 80 are selected
   - Monitoring: Disable boot diagnostics
6. Click Review + Create and carefully review your virtual machine settings 
7. Create your virtual machine (VM). This process may take awhile but a notification will inform you that your resource is created when it is ready.
8. Take a look at your newly created and running resource.
9. Stop the machine if you are done using it or continue to the next section.   

Note: We chose not to reserve a Public IP address. The one shown in the VM overview is temporary for only when the VM is running and will change the next time you start the VM.

[![Watch the tutorial video](/images/CreateVirtualMachinePoster.jpg)](https://www.youtube.com/watch?v=m4oAQGtG5SA "Video Tutorial - How to Create a Virtual Machine")

## Access Virtual Machine and Transfer Web App

1. In Visual Studio Code (VSC) create a terminal window in the directory of your project. 
2. Login to azure through the terminal window.
3. Login to Azure portal and find your virtual machine. Start your VM.
4. Find and record your Public IP address from the azure portal VM Overview or type `az vm list-ip-addresses -g web-app-vm-project -n linux-vm-project` in your VSC terminal window to obtain your IP address
5. Next, we're going to copy our web-app from our local machine to the VM home user directory using the secure copy utility command `scp -r ./web-app projectadmin@IPADDRESS:/home/projectadmin`
6. Login with your credentials to the virtual machine to complete the secure copy.
   - Username: (username you chosen) `projectadmin`
   - Password: (password you chosen) `projectadmin|2021`

NOTE: The first time you try connecting to the VM, you'll see a similar message to the one below and should answer 'yes' to permanently add the IP address to the list of known hosts.
```
The authenticity of host '52.191.135.139 (52.191.135.139)' can't be established.
ECDSA key fingerprint is SHA256:7bBVTsYNImhXxAn+xscCHm/OkcodHZS615VSKO3GP8c.
Are you sure you want to continue connecting (yes/no)?
```
7. Once the files have been copied to the VM, we can connect to the VM using secure shell `ssh projectadmin@IPADDRESS` and login with the same credentials
8. Navigate to the web-app directory and `ls` contents to see that our files have transferred.
9. Stop the virtual machine if you are done or continue to the next section. 

[![Watch the tutorial video](/images/CopyFilesToVirtualMachinePoster.jpg)](https://www.youtube.com/watch?v=KhKMpnzXEG8 "Video Tutorial - How to Copy Files to a Virtual Machine")

## Configure and Deploy Web Server

1. Start your virtual machine (VM) and record your public IP address
2. In Visual Studio Code (VSC) open a terminal window and login to azure.
3. SSH login to your VM in the terminal window `ssh projectadmin@IPADDRESS`
   - Username: (username you chosen) `projectadmin`
   - Password: (password you chosen) `projectadmin|2021`
4. Update the VM package repository information `sudo apt-get -y update`
5. Install the web server nginx and python which will run our web app on the server `sudo apt-get -y install nginx python3-venv`
6. Setup the reverse proxy for our nginx web server
   - Open a new terminal window and navigate to `/etc/nginx/sites-available`
   - Unlink the existing default reverse proxy file `sudo unlink /etc/nginx/sites-enabled/default`
   - Open up a new terminal window and secure copy our reverse-proxy.conf file to our home directory `scp -r reverse-proxy.conf projectadmin@IPADDRESS:/home/projectadmin`
   - Switch back to our ssh terminal window (connected to the VM) and verify the file has been copied to the projectadmin home directory
   - Move the reverse-proxy.conf `sudo mv reverse-proxy.conf /etc/nginx/sites-available`
   - Navigate to the sites-available directory `cd /etc/nginx/sites-available`
   - Verify the reverse-proxy.conf file is in the directory
   - Link our proxy file to the sites-enabled `sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf`
7. Restart the nginx service `sudo service nginx restart`
8. Navigate to the web-app directory 
9. Setup the python virtual environment `python3 -m venv ven`
10. Activate the python environment `source venv/bin/activate`
11. Upgrade pip in the virtual environment `pip install --upgrade pip`
12. Install dependencies for our web-app project `pip install -r requirements.txt`
13. Run the python web app `python application.py`
14. Open a web browser and navigate to the public IP address of your virtual machine

Voila! You have successfully created a Flask web application running on an azure virtual machine. 

Congratulations!

[![Watch the tutorial video](/images/ConfigureandDeployWebServerPoster.jpg)](https://youtu.be/xZwO4P_xj9E "Video Tutorial - How to Configure and Deploy a Web Server")

## Cleanup

Don't forget to stop your virtual machine after you are done playing with your project and to delete your resource group. 
