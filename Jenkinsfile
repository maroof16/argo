pipeline {
    agent {
        docker{
            image 'maroofshaikh09/docker-agent:latest'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Clean Workspace') {
            steps {
                sh 'rm -rf argo' // Clean the directory if it exists
            }
        }
        stage('git checkout') {
            steps {
                sh "echo passwd"
                sh "git clone https://github.com/maroof16/argo.git"
            }
        }
        stage("Build and test") {
            steps{
                sh 'mvn clean package'
            }
        }
    }
}
