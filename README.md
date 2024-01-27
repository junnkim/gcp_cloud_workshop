# Introduction to Google Cloud Platform (GCP)
This document contains instructions on how to complete an introductory GCP lab. 

# Table of Contents
1. [Background and Requirements](#background-and-requirements)
2. [Create Two Compute Instances to Server as Your Target Pool](#compute-instances)
3. [Add a Firewall Rule](#firewall-rule)
4. [Create the Load Balancer](#load-balancer)
   
## Background and Requirements <a name="background-and-requirements"></a>

Welcome! This lab will introduce you to the basics of GCP with a focus on navigating and creating services through the GCP Console. To successfully complete this lab, you will need to create your own personal GCP account. 

Creating a GCP account is simple. Just click on this [link](https://cloud.google.com/free?utm_source=google&utm_medium=cpc&utm_campaign=na-US-all-en-dr-bkws-all-all-trial-e-dr-1707554&utm_content=text-ad-none-any-DEV_c-CRE_665665924741-ADGP_Hybrid+%7C+BKWS+-+MIX+%7C+Txt_Google+Cloud+Free-KWID_43700078974895982-aud-2201603469980:kwd-886545049102&utm_term=KW_gcp+free+account-ST_gcp+free+account&gad_source=1&gclid=CjwKCAiA8NKtBhBtEiwAq5aX2LjLxVpWNJxm1DV34_Fz6LOdgQyXfP4Qs-sKk1JPU_1lLVKAbcSHzRoC378QAvD_BwE&gclsrc=aw.ds&authuser=1) and select **Get started for free**

<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/5d03bc81-dfe3-4f7d-9d01-a475e7eeda1a" width="400" height="200">

You will be promoted to a google account to use and you will need to create a google account if you do not already have one. Once complete, you will be taken to the GCP home page: 

<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/d2f78299-2791-44fc-9d19-f9e0c22f6cc9" width="600" height="300">

### Important Points to Note About Your Free GCP Account

•  Each resource you create in your account will incur costs. 

•  GCP gives you a $300 dollar credit and UCLA will provide an additional $50 credit to allow you to experiment with different cloud services

•  All GCP resources are created in a project. Your account comes with a default project called **My Project** that you can use

•  To search for different services, such the **Compute Instance** service, just the search bar located at the top of the GCP console. You will be taken to that services hompage. Once there, you will need to enable the service:

<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/fef5dbde-517f-4f35-86ab-0715a31e3a88" width="400" height="200">

•   After clicking on enable, you will need to activate your billing account:

<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/edab95bf-1126-4ca0-bb02-5c2ccc6de550" width="400" height="200">

•   Once complete, you will see the Compute Engine homepage:

<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/0ac9d549-7023-4157-9b4e-d92f320f9c11" width="700" height="300">

## Create Two Compute Instances to Server as Your Target Pool <a name="compute-instances"></a>

#### Instance 1 
1. Go to Compute Engine to create instance:
   * **Name:** my-UCLA-team-name-1 
   * **Region:** us-central1 
   * **Zone:** us-central1-b 
   * **OS image:** Debian GNU/Linux 
   * Add a networking tag of **my_UCLA_team_name-tag.** 
   * Paste this startup script: 

  ```bash
  #! /bin/bash 
  sudo apt-get update 
  sudo apt-get install apache2 -y 
  sudo service apache2 restart 
  echo '<!doctypehtml><html><body><h1>my-UCLA-team-name-1</h1></body></html>' | tee var/www/html/index.html
  ```

#### Instance 2

2. Go to Compute Engine to create instance:
   * **Name:** my-UCLA-team-name-2 
   * **Region:** us-central1 
   * **Zone:** us-central1-b 
   * **OS image:** Debian GNU/Linux 
   * Add a networking tag of **my_UCLA_team_name-tag.** 
   * Paste this startup script: 

  ```bash
  #! /bin/bash 
  sudo apt-get update 
  sudo apt-get install apache2 -y 
  sudo service apache2 restart 
  echo '<!doctypehtml><html><body><h1> my-UCLA-team-name-2</h1></body></html>' | tee /var/www/html/index.html 
   ```


## Add a Firewall Rule <a name="firewall-rule"></a>

Navigate to the Firewall page by typying 'Firewall' in the search bar: 

<img src="https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/5b667f74-8ece-4faf-ace0-95b7b9b4d93d" width="700" height="300">

3. Create firewall rule: 
   * **Name:** my_UCLA_team_name
   * **-firewall Targets:** Specified target tags Target tags: my-UCLA-team-name-tag
   * **Source filter:** IPv4 ranges 
   * Set the **Source IPv4 ranges** to 0.0.0.0/0, which allows traffic from any source. 
   * For specified protocols and ports, select **TCP** and enter **80**. 
   * NOTE: It may take a few minutes for the Console to display the new firewall rule or refresh to see the rule. 


## Create the Load Balancer <a name="load-balancer"></a>

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

