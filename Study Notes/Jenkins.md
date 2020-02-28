Windows-based systems should use the bat step for executing batch commands.

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'set'
            }
        }
    }
}
```

---

Timeouts and retries, clean-ups, etc.

```groovy
pipeline {
    agent any
    stages {
        stage('Test') { // 'Deploy', 'Build'
            steps {
                timeout(time: 3, unit: 'MINUTES') {
                    retry(5) {
                        sh './flakey-deploy.sh'
                    }
                }
                retry(3) {
                    bat 'executethisfile.sh'
                }
                timeout(time: 2, unit: 'MINUTES') {
                    
                }
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
```
---


# CI/CD

* Continuous Integration
  * Is merging all the code from branches to a central branch, build it and test it.
* Continuous Delivery
  * Is getting the code to a production-like environment, test it, keep it on a stable state ready to be deployed.
* Continuous Deployment
  * Is automatically deploying the changes to production, where the user can test it directly.


# Terms

* Job or Project
* Parameterizing job
* Steps
* Stages


# Parameterizing

* Its a way to describe parameters for the pipelines to be able to pass parameters dynamically.


```groovy

pipeline {
    agent any
    parameters { // Declare parameters
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
    }
    stages {
        stage('Example') {
            steps {
                echo "${params.Greeting} World!" // Use parameters
            }
        }
    }
}

```

You can also specify the parameter while creating an item selection the following option:

**This project is parameterized**

## With timeout

```groovy
pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    sh '/var/jenkins_home/scripts/fibonacci.sh 5'
                }
                timeout(time: 1, unit: 'MINUTES') {
                    sh '/var/jenkins_home/scripts/fibonacci.sh 32'
                }
            }
        }
    }
}

```
# Jenkins features:

* Run tasks perioriacally with Schedule, with cron.

# Connect Jenkins to Github

* In Github, go to user Settings > Developer Settings > Personal access token > Generate new token and select the scopes.
* In Jenkins, go to Manage Jenkins > Configure System > GitHub Server > Add GitHub Server. Test the connection


# Webhooks

* In GitHub, this can be used to push committed changes to Jenkins.
* In Jenkins, create a new item > Multibranch Pipeline > Save > Branch Source > GitHub > Credentials > Jenkins > Username (your user name) > Password (the token) > Id (unique id) > Add > Credential (new credential created) > Repository HTTPS URL (the GitHub repository you want to inform Jenkins) > Save.


> jenkins-webhook : d2993596542a7b1e6e3c7714029caeb40f3f27ad


---

# SSH build agent

## To add slaves worker machines where other instances of Jenkins may be running and make them communicate via SSH:

* Use a provider like Google Cloud or Amazon, create your credential keys and share it with jenkins so jenkins can use those resources to create nodes in Google or Amazon and use them as slave/workers.

# Pending

* Use docker with Jenkins
* Target specific machines
* Free style project
* Why would you use docker with Jenkins
* Shared libraries
* Jenkins notification
* Build state badges for SCM (to show the status of the build on the SCM)
    * With something like: [![Build Status](http://jenkins.kumulus.co:8080/buildStatus/icon?job=libraries)] in the README file.
* Code coverage

---

## Jenkins is very extensible. Extend it by using plug-ings



