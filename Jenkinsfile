pipeline {
    agent {
        docker {
            image 'maroofshaikh09/agent:latest'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
    SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage('git checkout') {
            steps {
                git 'https://github.com/maroof16/argo.git'
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
                    withCredentials([string(credentialsId: 'sonar-token', variable: 'sonar')]) {
                        // sh 'mvn sonar:sonar -Dsonar.login=$sonar -Dsonar.host= sonarqube'
                    // withSonarQubeEnv('sonarqube') {
                        sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Argo \
                           -Dsonar.java.binaries=. \
                           -Dsonar.projectKey=Argo '''
                    }
                }
            }
        }
    }
}
