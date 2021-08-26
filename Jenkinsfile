pipeline {
    agent any
    stages {
        stage('echotest') {
            steps {
                sh 'echo "test!"'
            }
        }
        
        stage('Build') {
            agent {
                docker {
                    //This image parameter (of the agent section’s docker parameter) downloads the python:2-alpine
                    //Docker image and runs this image as a separate container. The Python container becomes
                    //the agent that Jenkins uses to run the Build stage of your Pipeline project.
                    image 'python:3.8-alpine'
                }
            }
            steps {
                //This sh step runs the Python command to compile your application and
                //its calc library into byte code files, which are placed into the sources workspace directory
                sh 'python -m hello.py'
                //This stash step saves the Python source code and compiled byte code files from the sources
                //workspace directory for use in later stages.
                //stash(name: 'compiled-results', includes: 'sources/*.py*')
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
