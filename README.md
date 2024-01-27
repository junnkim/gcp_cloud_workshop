# Introduction to Google Cloud Platform (GCP)
This document contains instructions on how to complete the GCP lab assignment. 

## Background and Requirements

Welcome! This lab will introduce you to the basics of GCP with a focus on navigating and creating services through the GCP Console. To successfully complete this lab, you will need to create your own personal GCP account. 

Creating a GCP account is simple. Just click on this [link](https://cloud.google.com/free?utm_source=google&utm_medium=cpc&utm_campaign=na-US-all-en-dr-bkws-all-all-trial-e-dr-1707554&utm_content=text-ad-none-any-DEV_c-CRE_665665924741-ADGP_Hybrid+%7C+BKWS+-+MIX+%7C+Txt_Google+Cloud+Free-KWID_43700078974895982-aud-2201603469980:kwd-886545049102&utm_term=KW_gcp+free+account-ST_gcp+free+account&gad_source=1&gclid=CjwKCAiA8NKtBhBtEiwAq5aX2LjLxVpWNJxm1DV34_Fz6LOdgQyXfP4Qs-sKk1JPU_1lLVKAbcSHzRoC378QAvD_BwE&gclsrc=aw.ds&authuser=1) and select **Get started for free**

![gcp free trial](https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/5d03bc81-dfe3-4f7d-9d01-a475e7eeda1a)

You will be promoted to a google account to use and you will need to create a google account if you do not already have one. Once complete, you will be taken to the GCP home page: 
![gcp page](https://github.com/junnkim/gcp_cloud_workshop/assets/104690669/d2f78299-2791-44fc-9d19-f9e0c22f6cc9)


## Create Two Compute Instances to Server as Your Target Pool

### Instance 1 
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

### Instance 2








#### Deployment steps
1.	Navigate to the cloned repo directory, or run `sam init` then choose ‘Custom Template Location’ and paste the repo URL.
2.	Build the AWS SAM application, replace <templateName> with Python or DotNet template:
    
    `sam build -t <templateName>`

3.	Deploy the AWS SAM application:
    
    `sam deploy –guided`


## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
