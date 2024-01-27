# Introduction to Google Cloud Platform (GCP)
This document contains instructions on how to complete the GCP lab assignment. 

## Background

This lab will introduce you to the basics of Google Cloud Platform (GCP). 

### Create Two Compute Instances to Server as Your Target Pool
1. Go to Compute Engine to create instance:
   * Name: my-UCLA-team-name-1 
   * Region: us-central1 
   * Zone: us-central1-b 
   * OS image Debian GNU/Linux 
   * Add a networking tag of my_UCLA_team_name-tag. 
   * Paste this startup script: 

  ```bash
  #! /bin/bash 
  sudo apt-get update 
  sudo apt-get install apache2 -y 
  sudo service apache2 restart 
  echo '<!doctypehtml><html><body><h1>my-UCLA-team-name-1</h1></body></html>' | tee var/www/html/index.html 
  ```

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

