# KuraLabs

Deployment 1
Build test and deploy a flask application on Jenkins and deploy using AWS Elastic Beanstalk

## Table of contents

1. Create a pipeline build on Jenkins
2. Jenkins CI/CD Pipeline
3. Deploy application to Elastic Beanstalk
4. System Design

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

## Jenkins CI/CD Pipeline

Once the credentials are complete Jenkins will start the pipeline

* Pull repository from github
  * Clone the repository onto the EC2 instance
  * Look for a Jenkinfile inside the repository
  * This is the Jenkinsfile for this project

    ```
        pipeline {
      agent any
      stages {
        stage ('Build') {
          steps {
            sh '''#!/bin/bash
            python3 -m venv test3
            source test3/bin/activate
            pip install pip --upgrade
            pip install -r requirements.txt
            export FLASK_APP=application
            '''
        }
      }
        stage ('test') {
          steps {
            sh '''#!/bin/bash
            source test3/bin/activate
            py.test --verbose --junit-xml test-reports/results.xml
            ''' 
          }
        
          post{
            always {
              junit 'test-reports/results.xml'
            }
          
          }
        }
      
      }
    }
    ```

  * Stages declared in the pipeline
    * Build
      * Install all the dependencies of the Flask application
      * Create a virtual environment
    * Test
      * Run pytest to test functionality of the application
  * Successful execution of all stages can be seen in the Jenkins GUI
  
![jenkins-stages](https://github.com/Antoniorios17/deployment_elastic_beanstalk/blob/main/images/Jenkins-stages.png)

## Deploy application to Elastic Beanstalk


# Elastic Beanstalk Flask App Deployment

1. Open AWS Console: [Elastic Beanstalk](us-east-1.console.aws.amazon.com/elasticbeanstalk).

2. Click "Create application".

3. Enter "url-shortener" as the app name.

4. Choose "Python" platform.

5. Select "Python 3.9 running on 64bit Amazon Linux 2023".

6. Upload your zipped app code.

7. Set version label to "v1".

8. Select "ElasticEC2" instance profile.

9. Choose your default VPC and an Availability Zone.

10. Configure storage: 10 GB size, "General Purpose (SSD)".

11. For instance types, select "T.2 MICRO".

12. Click "Submit".

13. Once environment health is "OK", note your Domain Name.

![elastic-beanstalk](https://github.com/Antoniorios17/deployment_elastic_beanstalk/blob/main/images/elastic-beanstalk-ok.png)

14. Once environment health is "OK", note your Domain Name.

## System Design

Your Flask app is now deployed on Elastic Beanstalk. Access it using the provided Domain Name.

![url-shortenet-webpage](https://github.com/Antoniorios17/deployment_elastic_beanstalk/blob/main/images/url-shortener-webpage.png)

![system-design](http)