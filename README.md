# Introduction to Google Cloud Platform (GCP)
This document contains instructions on how to complete the introductory GCP lab. 

## Table of Contents
1. [Background and Requirements](#background-and-requirements)
2. [Create Two Compute Instances to Serve as Your Target Pool](#compute-instances)
3. [Add a Firewall Rule](#firewall-rule)
4. [Create the Load Balancer](#load-balancer)
5. [Send Traffic to Your Compute Instances](#send-traffic)
6. [Delete the GCP Services](#delete-resources)

## 1. Background and Requirements <a name="background-and-requirements"></a>

Welcome! This lab will introduce you to the basics of GCP with a focus on navigating and creating services through the GCP Console. To successfully complete this lab, you will need to create your own personal GCP account. 

Creating a GCP account is simple. Just click on this [link](https://cloud.google.com/free?utm_source=google&utm_medium=cpc&utm_campaign=na-US-all-en-dr-bkws-all-all-trial-e-dr-1707554&utm_content=text-ad-none-any-DEV_c-CRE_665665924741-ADGP_Hybrid+%7C+BKWS+-+MIX+%7C+Txt_Google+Cloud+Free-KWID_43700078974895982-aud-2201603469980:kwd-886545049102&utm_term=KW_gcp+free+account-ST_gcp+free+account&gad_source=1&gclid=CjwKCAiA8NKtBhBtEiwAq5aX2LjLxVpWNJxm1DV34_Fz6LOdgQyXfP4Qs-sKk1JPU_1lLVKAbcSHzRoC378QAvD_BwE&gclsrc=aw.ds&authuser=1) and select **Get started for free**

<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/5d03bc81-dfe3-4f7d-9d01-a475e7eeda1a" width="400" height="200">

You will be prompted to create a google account to use, and you will need to create a google account if you do not already have one. Once complete, you will be taken to the GCP home page: 

<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/d2f78299-2791-44fc-9d19-f9e0c22f6cc9" width="600" height="300">

### Important Points to Note About Your Free GCP Account

•  Each resource you create in your account will incur costs. 

•  GCP gives you a $300 dollar credit and UCLA will provide an additional $50 credit to allow you to experiment with different cloud services.

•  All GCP resources are created in a project. Your account comes with a default project called **My Project** that you can use.

•  To search for different services, such the **Compute Instance** service, just the search bar located at the top of the GCP console. You will be taken to that services hompage. Once there, you will need to enable the service:

<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/fef5dbde-517f-4f35-86ab-0715a31e3a88" width="400" height="200">

•   After clicking on enable, you will need to activate your billing account:

<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/edab95bf-1126-4ca0-bb02-5c2ccc6de550" width="400" height="200">

•   Once complete, you will see the Compute Engine homepage:

<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/0ac9d549-7023-4157-9b4e-d92f320f9c11" width="700" height="300">

## 2. Create Two Compute Instances to Serve as Your Target Pool <a name="compute-instances"></a>

#### Instance 1 
1. Go to Compute Engine to create instance. Keep all the default settings selected and only change the following:
   * **Name:** my-ucla-instance-1
   * **Region:** us-central1 
   * **Zone:** us-central1-b 
   * **OS image:** Debian GNU/Linux 
   * Under **Advanced Options**, **Networking**, add a networking tag of **my_ucla_name_tag** under the Network tags section
   * Under **Advanced Options**, **Management**, paste this startup script under the **Automation** section: 

  ```bash
   #! /bin/bash
   sudo apt-get update
   sudo apt-get install apache2 -y
   sudo service apache2 restart
   sudo chmod 777 /var/www/html -R
   echo '<!doctypehtml><html><body><h1>go-bruins! this is instance number 1</h1></body></html>' | tee /var/www/html/index.html
  ```

#### Instance 2

2. Go to Compute Engine to create instance. Keep all the default settings selected and only change the following:
   * **Name:** my-ucla-instance-2 
   * **Region:** us-central1 
   * **Zone:** us-central1-b 
   * **OS image:** Debian GNU/Linux 
   * Under **Advanced Options**, **Networking**, add a networking tag of **my_ucla_name_tag** under the Network tags section
   * Under **Advanced Options**, **Management**, paste this startup script under the **Automation** section: 

  ```bash
   #! /bin/bash
   sudo apt-get update
   sudo apt-get install apache2 -y
   sudo service apache2 restart
   sudo chmod 777 /var/www/html -R
   echo '<!doctypehtml><html><body><h1>go-bruins! this is instance number 2</h1></body></html>' | tee /var/www/html/index.html
   ```


## 3. Add a Firewall Rule <a name="firewall-rule"></a>

Navigate to the Firewall page by typying 'Firewall' in the search bar: 


<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/fbd4a788-1183-4d6e-bd13-dc5e213691be" width="600" height="300">


3. Create firewall rule: 
   * **Name:** my_UCLA_team_name
   * **-firewall Targets:** Specified target tags Target tags: **my_ucla_name_tag**
   * **Source filter:** IPv4 ranges 
   * Set the **Source IPv4 ranges** to 0.0.0.0/0, which allows traffic from any source. 
   * For specified protocols and ports, select **TCP** and enter **80**. 
   * NOTE: It may take a few minutes for the Console to display the new firewall rule or refresh to see the rule.
  
   * NOTE: Your compute instances are launched with a **default-allow-ssh** rule. As a security best practice, this should be deleted. Go to **Firewall > Policies > Delete default-allow-ssh**


## 4. Create the Load Balancer <a name="load-balancer"></a>

* Click the Navigation menu, located in the top left-hand side.
* Select Network services > Load balancing.
* Click Create Network Load Balancer.
* Click Start Configuration for the Network Load Balancer (TCP/SSL)
* Select From Internet to my VMs.
* Select Single region only.
* Select Target Instance.
* Click Continue.
* Enter the following information: Name: my-ucla-lb Region: us-central1 (Iowa)
* Select Backend configuration. Selected Network Service Tier = Standard
* Click Select Existing Instances.
* For VM instances, select my-ucla-instance-1(us-central1-b) and my-ucla-instance-2(us-central1-b). Click OK.
* Select Frontend configuration.
* For Name, enter my-UCLA-team-name-fe.
* For IP address, select Create IP Address.
* In the Reserve a new static IP address dialog, enter my-UCLA-team-name-ip for the Name.
* Click Reserve.
* For Port, enter 80.
* Click Done.
* Click Review and finalize (optional).
* Click Create.
* Click the my-ucla-lb then choose EDIT.
* Under the Backend configuration in the Health check section, choose CREATE A HEALTH CHECK.
* Enter the following information: Name: health Protocol: HTTP Port: 80.
* Keep the given defaults for Health criteria.
* Click Save.
* Click UPDATE.
* Click UPDATE LOAD BALANCER 

## 5. Send Traffic to Your Compute Instances <a name="send-traffic"></a>

a. Copy the IP address and place it in the URL, you will then see either **"go-bruins! this is instance number 1"** or **"go-bruins! this is instance number 22 displayed"**. This will confirm your traffic is being served the instance webpages. 

b. Open Cloud Shell and execute command while true; do curl -m1 IP_ADDRESS; done. This will show that both of your servers are serving the application traffic to your end users. 

## 6. Delete the GCP Services (After Lab is Complete)<a name="delete-resources"></a>

Once the lab assignment is complete, you will want to delete the resources you just created to avoid incurring costs. In this lab, we created 2 GCP Compute Intances, 1 GCP Firewall Rule and 1 GCP Load Balancer. Navigate to each of those services and select the option to delete each one. 
