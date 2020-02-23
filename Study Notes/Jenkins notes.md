Windows-based systems should use the bat step for executing batch commands.

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


---

Timeouts and retries, clean-ups, etc.

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

---


