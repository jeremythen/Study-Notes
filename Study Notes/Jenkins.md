Windows-based systems should use the bat step for executing batch commands.

```
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

```
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
                timeout(time: 2, unit: 'MINUTES) {
                    
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


