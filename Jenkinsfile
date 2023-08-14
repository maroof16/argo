pipeline {
    agent {
        docker {
            image 'maroofshaikh09/agent:latest'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('git checkout') {
            steps {
                 git branch: 'main', url:'https://github.com/sahill20/java-maven-sonar-argocd-helm-k8s.git'
            }
        }
        stage("Build and test") {
            steps {
                sh 'mvn -X clean package'
            }
        }
        stage ("static code analysis") {
            environment {
        SONAR_URL = "http://13.235.246.22:9000"
        }
            steps {
                withCredentials([string(credentialsId: 'sonar-token', variable: 'sonar')]) {
                    sh 'mvn sonar:sonar -Dsonar.login=$sonar -Dsonar.host.url=${SONAR_URL}'
                }
            }
        }
        stage ('Build And Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-id-pass') {
                    sh """ docker build -t image .
                    docker tag  image maroofshaikh09/argocd-demo:$BUILD
                    docker push   maroofshaikh09/argocd-demo:$BUILD
                    """
                    }
                }
            }
        }
    }
}
 