pipeline {
    agent any
    // agent {
    //     docker{
    //         image 'maroofshaikh09/agent:latest'
    //         args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
    //     }
    // }
      environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage('Clean Workspace') {
            steps {
                sh 'sudo rm -rf *' // Clean the directory if it exists
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
                script {
                    withSonarQubeEnv('sonarqube') {
                        sh "${SCANNER_HOME}/bin/sonar-scanner "
                        sh 'sonar-scanner -Dsonar.projectKey=my-project-key'
                    }
                }
            }
        }
    }
}
