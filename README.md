# KuraLabs

Deployment 1
Build test and deploy a flask application on Jenkins and deploy using AWS Elastic Beanstalk

## Table of contents

1. Create a pipeline build on Jenkins
2. Deploy application to Elastic Beanstalk
3. 

## Create a pipeline build on Jenkins

* Create a new item
  * Select multibranch pipeline
* Add source: Github
* Create a new personal access token on github
  * Log in to github
  * Access the setting
  * Select developer settings
  * Select Token (Classic)
  * Generate new token
  * Check the boxes for repo, admin:org and admin:repo_hook
* Add github credentials
  * Add github username
  * Add repository link
  * Add personal access token as password
  * Validate connection to the repository
  * Apply and save configuration


