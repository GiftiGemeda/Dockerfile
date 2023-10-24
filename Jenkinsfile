pipeline {
    agent any

    tools {
        dockerTool 'Default'
    }

   environment {
        DOCKER_REGISTRY_CREDENTIALS = credentials('doc')
    }

    stages {
        stage("Clone Repository") {
            steps {
                script {
                    // Clone the GitHub repository
                    checkout scm
                }
            }
        }
        stage("build docker image"){
            steps {
                script {
                    withCredentials([string(credentialsId: 'doc', variable: 'DOCKER_REGISTRY_CREDENTIALS')]) {
                        def customImage = docker.build('gifti/example:myfirsttag', '-f Dockerfile .').withRegistry("", 'DOCKER_HUB_ACCESS_TOKEN')
                    }
                    
                }
            }
        }
        stage ("push docker image"){
            steps {
                script {
                    customImage.push()
                }
            }
        }
    

 
    }
}
