pipeline {
    agent {
        docker{
            image 'maroofshaikh09/docker-agent:latest'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        sonarqube_url = "http://13.233.69.215:9000"
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
        stage ("static code analysis") {
            steps {
                withSonarQubeEnv(credentialsId: 'sonar-token') {
                sh'mvn sonar:sonar -Dsonarlogin=$sonar-token -Dsonar.host.url=${sonarqube_url}'
                }
            }
        }
    }
}
